# Documentação — Módulo de Contratos (EFX-HUB)

> Documento técnico-funcional do módulo de Contratos do EFX-HUB. Cobre as três versões coexistentes (V1 legado, V2 ativo, C3 novo), todos os fluxos (manual, email/IA, assinatura digital, aprovação pública), integrações, rotas, permissões, jobs, eventos e tabelas.

---

## Sumário

1. [Visão geral](#1-visão-geral)
2. [Arquitetura e bounded contexts](#2-arquitetura-e-bounded-contexts)
3. [Estrutura de pastas](#3-estrutura-de-pastas)
4. [Fluxos de negócio](#4-fluxos-de-negócio)
   - 4.1 [Fluxo manual (V2)](#41-fluxo-manual-v2)
   - 4.2 [Fluxo via email com IA (V2)](#42-fluxo-via-email-com-ia-v2)
   - 4.3 [Fluxo de revisão interna (V2)](#43-fluxo-de-revisão-interna-v2)
   - 4.4 [Fluxo de aprovação pública pelo diretor (V2)](#44-fluxo-de-aprovação-pública-pelo-diretor-v2)
   - 4.5 [Fluxo de assinatura digital — BoldSign (V2)](#45-fluxo-de-assinatura-digital--boldsign-v2)
   - 4.6 [Fluxo de rejeição (V2)](#46-fluxo-de-rejeição-v2)
   - 4.7 [Fluxo de criação automática do C3](#47-fluxo-de-criação-automática-do-c3)
   - 4.8 [Fluxo de gestão pós-vigência (C3)](#48-fluxo-de-gestão-pós-vigência-c3)
5. [Máquinas de estado](#5-máquinas-de-estado)
6. [Models / entidades](#6-models--entidades)
7. [Actions, Services e Jobs](#7-actions-services-e-jobs)
8. [Eventos e listeners](#8-eventos-e-listeners)
9. [Integrações externas](#9-integrações-externas)
10. [Rotas](#10-rotas)
11. [Permissões](#11-permissões)
12. [Webhooks e endpoints externos](#12-webhooks-e-endpoints-externos)
13. [Telas / componentes Livewire](#13-telas--componentes-livewire)
14. [Tabelas de banco](#14-tabelas-de-banco)
15. [Decisões de design relevantes](#15-decisões-de-design-relevantes)

---

## 1. Visão geral

O módulo de Contratos do EFX-HUB suporta o ciclo completo de vida de um contrato corporativo — desde a chegada do documento (por email ou cadastro manual), passando por análise de risco com IA, aprovação por diretores via link público, assinatura digital com certificação, até a gestão pós-vigência (aditivos, obrigações, reajustes, renovação e encerramento).

Existem **três versões** coexistindo no sistema, cada uma representando uma fase evolutiva:

| Versão | Status | Pasta DDD | Livewire | Rotas | Função |
|--------|--------|-----------|----------|-------|--------|
| **V1** | Deprecada (rotas bloqueadas por middleware) | `src/Contratos/` | `app/Livewire/Contratos/` | — | Sistema legado com workflow de aprovação por etapas |
| **V2** | **Ativo (intake + aprovação)** | `src/ContratosV2/` | `app/Livewire/ContratosV2/` | `routes/contratos-v2.php` | Recebe contratos por email, processa com IA, coleta aprovação e assinatura digital |
| **C3** | **Ativo (gestão pós-assinatura)** | `src/Contratos3/` | `app/Livewire/ContratosC3/` | `routes/contratos-c3.php` | Gestão do contrato em vigor (aditivos, contatos, documentos) |

> **Visão de pipeline:** o V2 é a "esteira de entrada" (intake → análise → aprovação → assinatura). Quando um contrato V2 é aprovado e assinado, um **listener cria automaticamente** um registro no C3 — que assume a gestão pós-vigência.

---

## 2. Arquitetura e bounded contexts

O módulo segue **DDD em camadas** dentro de `src/`, complementado por componentes Livewire em `app/Livewire/` para a camada de UI.

```
┌──────────────────────────────────────────────────────────────┐
│                     UI (Livewire 3 / Blade)                  │
│   app/Livewire/ContratosV2/  +  app/Livewire/ContratosC3/   │
└─────────────────┬────────────────────────────────────────────┘
                  │
┌─────────────────┴────────────────────────────────────────────┐
│                      Application Layer                       │
│        Actions  •  DTOs  •  Use Cases  •  Policies          │
└─────────────────┬────────────────────────────────────────────┘
                  │
┌─────────────────┴────────────────────────────────────────────┐
│                        Domain Layer                          │
│   Models  •  Enums  •  StateMachines  •  Events  •  Notifs  │
└─────────────────┬────────────────────────────────────────────┘
                  │
┌─────────────────┴────────────────────────────────────────────┐
│                   Infrastructure Layer                       │
│   BoldSign  •  Microsoft Graph  •  OpenAI  •  Storage       │
└──────────────────────────────────────────────────────────────┘
```

**Comunicação entre V2 e C3:** assíncrona, por **eventos de domínio**. O V2 emite `StatusV2Alterado`; o `CriarContratoC3Listener` (queued) reage e cria o registro C3.

---

## 3. Estrutura de pastas

### 3.1 Contratos V2 (`src/ContratosV2/`)

```
src/ContratosV2/
├── Domain/
│   ├── Models/
│   │   ├── ContratoV2.php             ← efx_hub_v2_contratos
│   │   ├── ContratoV2Log.php          ← auditoria
│   │   ├── AditivoV2.php
│   │   ├── ObrigacaoV2.php
│   │   ├── ComentarioContratoV2.php
│   │   ├── ReajusteContratoV2.php
│   │   ├── TagContratoV2.php
│   │   ├── DiretorV2.php
│   │   ├── EmailProcessado.php        ← idempotência intake
│   │   ├── TokenAprovacaoV2.php       ← tokens públicos (hash SHA256)
│   │   └── FiltroSalvoV2.php
│   ├── Enums/
│   │   ├── StatusContratoV2.php       ← 8 estados
│   │   ├── PeriodicidadeV2.php
│   │   ├── StatusObrigacaoV2.php
│   │   └── TipoReajusteV2.php
│   ├── Services/
│   │   └── ContratoV2StateMachine.php
│   ├── Events/
│   │   └── StatusV2Alterado.php
│   ├── Exceptions/
│   │   ├── TransicaoV2InvalidaException.php
│   │   ├── BoldSignException.php
│   │   ├── BoldSignApiException.php
│   │   └── BoldSignWebhookInvalidoException.php
│   └── Notifications/
│       ├── ContratoV2CriadoNotification.php
│       └── ContratoV2AssinadoNotification.php
├── Application/
│   ├── Actions/        ← 11 actions (ver §7)
│   └── DTOs/           ← CamposIAData, BoldSignEnvelopeData, BoldSignEventData
└── Infrastructure/
    └── BoldSign/
        ├── BoldSignClient.php
        ├── BoldSignService.php
        ├── BoldSignSignaturePageGenerator.php   ← FPDF
        └── BoldSignWebhookVerifier.php          ← HMAC SHA256
```

### 3.2 Contratos C3 (`src/Contratos3/`)

```
src/Contratos3/
├── Domain/
│   ├── Models/
│   │   ├── ContratoC3.php             ← efx_hub_c3_contratos (gera CTR-YYYY-NNN)
│   │   ├── AditivoC3.php
│   │   ├── ContatoParceiroC3.php
│   │   ├── DocumentoC3.php
│   │   └── ContratoC3Log.php
│   ├── Enums/
│   │   ├── StatusContratoC3.php       ← 7 estados
│   │   ├── PeriodicidadeC3.php
│   │   └── TipoReajusteC3.php
│   ├── Services/
│   │   └── ContratoC3StateMachine.php
│   ├── Events/
│   │   └── StatusC3Alterado.php
│   └── Exceptions/
│       └── TransicaoC3InvalidaException.php
└── Application/
    └── Actions/
        ├── CriarContratoC3.php
        └── TransicionarStatusC3.php
```

### 3.3 Contratos V1 — legado (`src/Contratos/`)

64 arquivos. Mantém modelos como `Contrato`, `TarefaAprovacao`, `InstanciaAprovacao`, `FluxoAprovacao`, `EtapaFluxo`, com workflow de aprovação multi-etapa orquestrado por `ApprovalEngine`. **Rotas bloqueadas por middleware** — referência apenas para histórico / migração.

---

## 4. Fluxos de negócio

### 4.1 Fluxo manual (V2)

Cadastro de contrato sem passar por email/IA. Útil para casos em que o documento é entregue fisicamente ou fora do canal padrão.

```
Usuário (CreateContratoV2)
  ├─ Preenche form: parceiro, tipo, valor, datas, setor, diretor
  ├─ Faz upload do PDF → storage/app/public/contratos/
  └─ Submete

CriarContratoV2 (Action)
  ├─ DB::transaction
  ├─ ContratoV2::create(status = aguardando_revisao)
  ├─ ContratoV2Log::create('Contrato criado manualmente')
  └─ Notification ContratoV2CriadoNotification (database + email)

→ Estado: aguardando_revisao  (sem chamada de IA — fluxo manual pula intake)
```

### 4.2 Fluxo via email com IA (V2)

**Pipeline assíncrono em duas filas** (`contratos-v2` para orquestração + `contratos-v2-ia` para chamadas a LLM).

```
┌─────────────────────────────────────────────────────────────┐
│ 1. POLLING (Microsoft Graph)                                │
│    EmailService::listUnreadMessages()                       │
│    GET /users/{inbox}/mailFolders/inbox/messages           │
│    Filtro: isRead=false, hasAttachments=true                │
│    → Dispatch ProcessarEmailIntakeJob                       │
└──────────────────────┬──────────────────────────────────────┘
                       ▼
┌─────────────────────────────────────────────────────────────┐
│ 2. INTAKE (ProcessarEmailIntakeJob — fila contratos-v2)     │
│    a) Idempotência: SELECT efx_hub_v2_emails_processados    │
│       WHERE internet_message_id = ?  → se existe, ignora    │
│    b) Validação: remetente, assunto, corpo, PDF anexo,      │
│       tamanho ≤ 20MB, MIME = application/pdf                │
│       → Falha: EnviarRespostaErroJob + marca processado     │
│    c) Salva PDF em storage/app/public/contratos/            │
│    d) CriarContratoV2 (status=aguardando_revisao,           │
│       canal_intake=email, campos_ia=null)                   │
│    e) INSERT efx_hub_v2_emails_processados                  │
│    f) Dispatch ProcessarIAJob (fila contratos-v2-ia)        │
│    g) Dispatch EnviarConfirmacaoIntakeJob (responde sender) │
└──────────────────────┬──────────────────────────────────────┘
                       ▼
┌─────────────────────────────────────────────────────────────┐
│ 3. PROCESSAMENTO IA (ProcessarIAJob — fila ...-ia)          │
│    a) ExtrairTextoPdfV2 (pdftotext)                         │
│       → Se vazio: pdf_ilegivel = true                       │
│    b) OpenAIService::extrairCamposEmail(corpo, textoPdf)    │
│       → Modelo Claude com response_format=json_object       │
│       → Retorna 8 campos: parceiro, tipo, valor, datas,    │
│         setor, diretor_nome, diretor_email                  │
│       → Cada campo recebe { valor, fonte, confianca }       │
│         confianca ∈ { auto, inferido, pendente }            │
│    c) AnalisarRiscoV2 (keyword scoring + IA semântica)      │
│       → Score final = (score_keyword + score_ia) / 2        │
│       → Classificação: baixo (<30) / médio (30-60) /       │
│         alto (>60)                                          │
│       → Persiste analise_risco (JSON) com pontos_atencao,  │
│         resumo_executivo, clausulas_identificadas           │
│    d) Resolução de diretor                                  │
│       → DiretorV2::ativos()->whereNomeOrEmail()             │
│       → Match: substitui campos_ia.diretor_* (auto)         │
│       → Sem match: mantém pendente (gestor escolhe)         │
│    e) Notification ContratoV2CriadoNotification             │
└──────────────────────┬──────────────────────────────────────┘
                       ▼
              Estado: aguardando_revisao
              (pronto para revisão humana)
```

### 4.3 Fluxo de revisão interna (V2)

Componente `RevisaoContratoV2` em `/solicitacoes-contrato/revisao/{contrato}`.

A tela exibe:
- Campos extraídos pela IA com **badge de confiança** (auto / inferido / pendente) e **fonte** (email / PDF / IA);
- **Análise de risco** com score numérico, classificação visual (verde/amarelo/vermelho), pontos de atenção e cláusulas identificadas;
- **PDF original** embutido (iframe ou viewer);
- Campos editáveis para correção/complemento manual.

**Três ações possíveis:**

| Ação | Efeito |
|------|--------|
| **Aprovar** | Valida campos obrigatórios → `TransicionarStatusV2` para `em_aprovacao` (com pessimistic lock) → dispatch `EnviarAprovacaoDiretorJob` (envia link público ao diretor) |
| **Rejeitar** | Solicita justificativa → transição para `reprovado` → `EnviarResultadoGestorJob` notifica remetente. Estado terminal (salvo reabertura administrativa) |
| **Solicitar dúvida** | Modal com texto → `EnviarDuvidaGestorJob` ao remetente original. Não transiciona — permanece em `aguardando_revisao` |

### 4.4 Fluxo de aprovação pública pelo diretor (V2)

Permite que diretores aprovem/rejeitem **sem login no sistema**, via link único.

```
Geração do token (GerarTokenAprovacao)
  ├─ raw_token = Str::random(64)
  ├─ hash = SHA256(raw_token)
  ├─ INSERT TokenAprovacaoV2 (token=hash, acao=null, usado_em=null)
  └─ Email ao diretor com link:
     https://hub.alpex.com.br/solicitacoes-contrato/aprovacao/{raw_token}

Diretor acessa link → AprovacaoDiretorController::show
  ├─ Resolver: hash = SHA256(raw_token) → SELECT WHERE token=hash
  ├─ Verificações:
  │   • Já usado?         → página "já decidido"
  │   • Expirado (>30d)?  → página "expirado"
  │   • Estado errado?    → página "inválido"
  └─ Renderiza approval-review-page.blade.php
     (detalhes + risco resumido + PDF + botões Aprovar/Rejeitar)

Caminho APROVAR  →  inicia BoldSign (§4.5)
Caminho REJEITAR →  marca token (acao=reprovado, usado_em=now)
                    transiciona para reprovado
                    EnviarResultadoGestorJob
```

**Segurança do token:** hash em DB (token bruto nunca é persistido); validação de expiração; uso único; verificação de estado do contrato; rate-limit no controller.

### 4.5 Fluxo de assinatura digital — BoldSign (V2)

Quando o diretor clica **"Aprovar"** na tela pública, o sistema cria o envelope BoldSign e exibe o assinador embutido.

```
SolicitarAssinaturaDiretor (Action)
  ├─ Valida contrato.status = em_aprovacao
  ├─ FORA da transação (evita orphans):
  │   BoldSignService::criarEnvelope()
  │     ├─ Lê PDF original
  │     ├─ Conta páginas
  │     ├─ Gera página de assinatura (FPDF, BoldSignSignaturePageGenerator)
  │     ├─ Monta payload (camelCase!): signers, formFields
  │     └─ POST /document/send → { documentId, status }
  ├─ DB::transaction
  │   ├─ TransicionarStatusV2 → aguardando_assinatura
  │   ├─ UPDATE assinatura_provider='boldsign',
  │       assinatura_document_id, assinatura_solicitada_em
  │   └─ Log 'envelope_criado'
  ├─ Marca token (acao=aprovado, usado_em=now)
  ├─ BoldSignClient::getSigningLink(documentId, signerEmail)
  │   → embedded URL para iframe
  └─ Renderiza approval-signing-page.blade.php
     (iframe BoldSign + polling AJAX a cada Ns)

Diretor assina no iframe BoldSign hospedado
  → BoldSign envia webhook: POST /webhooks/boldsign

BoldSignWebhookController (rota throttle:60,1)
  ├─ BoldSignWebhookVerifier::verify()
  │   ├─ Header X-BoldSign-Signature
  │   ├─ Timestamp: |now - ts| < 300s (anti-replay)
  │   ├─ HMAC = SHA256(timestamp + "." + rawBody, apiKey)
  │   └─ hash_equals (constant-time)
  ├─ ProcessarCallbackBoldSign::execute(payload)
  │   ├─ Normaliza eventType (Signed → Completed se todos assinaram)
  │   ├─ Filtra eventos acionáveis: Completed | Declined
  │   ├─ DB::transaction + pessimistic lock
  │   ├─ Idempotência: short-circuit se status já terminal
  │   ├─ Caso Completed:
  │   │   • BaixarDocumentoAssinado (pdf_assinado_path)
  │   │   • TransicionarStatusV2 → aprovado
  │   │   • UPDATE assinatura_concluida_em
  │   │   • ContratoV2AssinadoNotification
  │   │   • → DISPARA listener CriarContratoC3 (§4.7)
  │   └─ Caso Declined:
  │       • TransicionarStatusV2 → reprovado
  │       • UPDATE assinatura_declinada_em, decline_reason
  │       • EnviarResultadoGestorJob
  └─ Retorna 200 sempre (mesmo com erro downstream)

Polling AJAX (fallback dev/NAT)
  GET /solicitacoes-contrato/aprovacao/{token}/sign-link-status
  → BoldSignClient::getDocumentProperties (reconcilia se webhook não chegou)
  → JS redireciona para landing page (concluida / declinada)
```

**Job de reconciliação:** `ReconciliarAssinaturasPendentesJob` roda periodicamente para contratos parados em `aguardando_assinatura` — chama BoldSign API e sintetiza payload de webhook se o estado mudou remotamente.

### 4.6 Fluxo de rejeição (V2)

Pode ocorrer em três pontos:

| Origem | Estado origem | Ação |
|--------|---------------|------|
| Revisão interna | `aguardando_revisao` | Gestor rejeita por inadequação dos dados extraídos |
| Aprovação pública | `em_aprovacao` | Diretor rejeita explicitamente sem assinar |
| Webhook BoldSign | `aguardando_assinatura` | Diretor declina no assinador |

Em todos os casos: estado final = **`reprovado`** + `EnviarResultadoGestorJob` notifica o remetente original.

### 4.7 Fluxo de criação automática do C3

```
StatusV2Alterado (statusNovo = aprovado) → CriarContratoC3Listener (queued)
  ├─ DB::transaction
  ├─ ContratoC3::create([
  │     status = aguardando_revisao,
  │     solicitacao_v2_id = contrato_v2.id,
  │     numero_contrato = (auto: CTR-YYYY-NNN, gerado por boot model
  │                       com pessimistic lock em efx_hub_c3_numero_counter),
  │     parceiro, tipo, valor, datas, setor, responsavel, pdf_assinado_path
  │   ])
  └─ Log 'C3 pré-cadastro criado a partir de V2 #{id}'
```

> **Por que listener queued?** Mantém o webhook BoldSign rápido (resposta 200 imediata) e isola falhas: se a criação do C3 falhar, o V2 já está aprovado e o job pode ser reprocessado.

### 4.8 Fluxo de gestão pós-vigência (C3)

O C3 é o **registro de verdade** do contrato em vigor. Suas operações:

- **Revisão jurídica** (`aguardando_revisao` → `em_elaboracao`): time legal revisa cláusulas e detalhes financeiros;
- **Ativação** (`em_elaboracao` → `ativo`): contrato passa a vigorar;
- **Aditivos** (`AditivoC3Manager`): novas versões numeradas sequencialmente;
- **Contatos do parceiro** (`ContatoC3Manager`): cadastro de pessoas-chave;
- **Documentos anexos** (`DocumentoC3Manager`): documentação suplementar;
- **Suspensão / encerramento / cancelamento / expiração**: estados terminais ou pausa.

---

## 5. Máquinas de estado

### 5.1 V2 — `StatusContratoV2`

```
                  aguardando_revisao
                   │           │
            (aprovar)        (reprovar)
                   ▼           ▼
              em_aprovacao   reprovado ◄──┐
                   │           ▲          │
            (diretor aprova)   │ (decline)│
                   ▼           │          │
            aguardando_assinatura ────────┘
                   │
            (BoldSign Completed)
                   ▼
                aprovado ────────► (dispara C3)
                   │
              (entra em vigência)
                   ▼
                  ativo
                   │
                   ├─► encerrado
                   └─► cancelado
```

| Estado | Descrição |
|--------|-----------|
| `aguardando_revisao` | Contrato recebido (email ou manual), aguardando revisão do gestor |
| `em_aprovacao` | Gestor aprovou; aguardando decisão do diretor pelo link público |
| `aguardando_assinatura` | Diretor aprovou; envelope BoldSign criado, aguardando assinatura |
| `aprovado` | BoldSign completou; PDF assinado salvo; C3 criado por listener |
| `reprovado` | Rejeitado em qualquer etapa; estado terminal |
| `ativo` | Em vigência (gerido pelo C3 a partir daqui) |
| `encerrado` | Concluído normalmente |
| `cancelado` | Encerrado antecipadamente |

Validação de transição em `ContratoV2StateMachine` com **pessimistic lock** (`SELECT ... FOR UPDATE`) para prevenir race conditions.

### 5.2 C3 — `StatusContratoC3`

```
aguardando_revisao ─► em_elaboracao ─► ativo ─┬─► suspenso ─► ativo
                          │           │       ├─► encerrado
                          ▼           │       ├─► expirado
                      cancelado       │       └─► cancelado
                                      └─► cancelado
```

---

## 6. Models / entidades

### 6.1 V2

| Model | Tabela | Campos-chave |
|-------|--------|--------------|
| `ContratoV2` | `efx_hub_v2_contratos` | `status`, `canal_intake`, `email_*`, `internet_message_id`, `pdf_path`, `pdf_assinado_path`, `parceiro`, `tipo_contrato`, `valor`, `data_inicio`, `data_fim`, `setor`, `diretor_email`, `diretor_nome`, `campos_ia` (JSON), `analise_risco` (JSON), `score_risco`, `classificacao_risco`, `assinatura_provider`, `assinatura_document_id`, `assinatura_solicitada_em`, `assinatura_concluida_em`, `assinatura_declinada_em` |
| `ContratoV2Log` | `efx_hub_v2_logs` | `acao`, `usuario`, `dados_antes`, `dados_depois`, `justificativa` |
| `AditivoV2` | `efx_hub_v2_aditivos` | `versao`, `tipo_aditivo`, `descricao`, `data_vigencia` |
| `ObrigacaoV2` | `efx_hub_v2_obrigacoes` | `descricao`, `periodicidade`, `dias_para_cumprir` (pivot `obrigacoes_contratos` com `status`, `data_prevista`, `data_cumprimento`, `evidencia_path`) |
| `ComentarioContratoV2` | `efx_hub_v2_comentarios_contratos` | `conteudo`, `privado`, `usuario_id` |
| `ReajusteContratoV2` | `efx_hub_v2_reajustes_contratos` | `tipo_reajuste`, `indice`, `valor`, `percentual`, `data_base` |
| `TagContratoV2` | `efx_hub_v2_tags_contrato` | `nome`, `cor` |
| `DiretorV2` | `efx_hub_v2_diretores` | `nome`, `email`, `matricula`, `status` (scope `ativos()`) |
| `TokenAprovacaoV2` | `efx_hub_v2_tokens_aprovacao` | `token` (hash SHA256), `acao`, `usado_em` |
| `EmailProcessado` | `efx_hub_v2_emails_processados` | `internet_message_id` (unique) |
| `FiltroSalvoV2` | `efx_hub_v2_filtros_salvos` | `usuario_id`, `filtros` (JSON) |

### 6.2 C3

| Model | Tabela | Campos-chave |
|-------|--------|--------------|
| `ContratoC3` | `efx_hub_c3_contratos` | `status`, `solicitacao_v2_id`, **`numero_contrato`** (`CTR-YYYY-NNN` único, gerado em `boot()`), todos os campos herdados do V2, mais financeiro: `numero_parcelas`, `periodicidade_pagamento`, `forma_pagamento`, `multa_atraso`, `juros_mora`, `renovacao_automatica` |
| `AditivoC3` | `efx_hub_c3_aditivos` | `versao`, `tipo_aditivo`, `descricao` |
| `ContatoParceiroC3` | `efx_hub_c3_contatos_parceiro` | `nome`, `cargo`, `email`, `telefone` |
| `DocumentoC3` | `efx_hub_c3_documentos` | `tipo_documento`, `arquivo_path`, `arquivo_nome` |
| `ContratoC3Log` | `efx_hub_c3_logs` | auditoria |

---

## 7. Actions, Services e Jobs

### 7.1 Actions V2 (`src/ContratosV2/Application/Actions/`)

| Action | Função |
|--------|--------|
| `CriarContratoV2` | Persiste novo contrato (intake ou manual); `status=aguardando_revisao`; cria log |
| `ExtrairTextoPdfV2` | Extrai texto do PDF via `pdftotext`; marca `pdf_ilegivel` se falhar |
| `AnalisarRiscoV2` | Keyword scoring + análise IA semântica; gera `analise_risco` e `score_risco` |
| `TransicionarStatusV2` | Wrapper da `ContratoV2StateMachine` com auditoria + dispatch de evento |
| `SolicitarAssinaturaDiretor` | Cria envelope BoldSign **fora** da transação DB, transiciona para `aguardando_assinatura`, retorna sign link |
| `ProcessarCallbackBoldSign` | Processa webhook (Completed / Declined) com idempotência terminal |
| `BaixarDocumentoAssinado` | Baixa PDF assinado da BoldSign e armazena em `pdf_assinado_path` |
| `GerarTokenAprovacao` | Gera token bruto + hash SHA256; persiste hash em `TokenAprovacaoV2` |
| `AdicionarComentarioV2` | Adiciona comentário público/privado |
| `AplicarReajusteV2` | Cria registro de reajuste (índice / valor / %) |
| `RenovarContratoV2` | Clona contrato com novo período; `status=aguardando_revisao` |

### 7.2 Actions C3

| Action | Função |
|--------|--------|
| `CriarContratoC3` | Cria registro C3 (manual ou via listener); auto-gera `numero_contrato` |
| `TransicionarStatusC3` | Transição de estado com logging |

### 7.3 Services / State Machines

| Service | Função |
|---------|--------|
| `ContratoV2StateMachine` | `canTransition(from, to)`, `getAllowedTransitions(from)`, `transition(contrato, novo, justificativa)` com pessimistic lock |
| `ContratoC3StateMachine` | Equivalente para C3 |

### 7.4 Jobs

| Job | Fila | Tries | Backoff | Função |
|-----|------|-------|---------|--------|
| `ProcessarEmailIntakeJob` | `contratos-v2` | 3 | 120s | Valida email, salva PDF, cria contrato, dispara IA |
| `ProcessarIAJob` | `contratos-v2-ia` | 3 | 300s | Extrai texto, chama Claude para campos + risco |
| `EnviarAprovacaoDiretorJob` | `contratos-v2` | 3 | 120s | Gera token e envia link público ao diretor |
| `EnviarConfirmacaoIntakeJob` | `contratos-v2` | 3 | 120s | Confirma recebimento ao remetente |
| `EnviarDuvidaGestorJob` | `contratos-v2` | 3 | 120s | Encaminha dúvida ao remetente original |
| `EnviarResultadoGestorJob` | `contratos-v2` | 3 | 120s | Notifica resultado (aprovado / rejeitado) |
| `EnviarRespostaErroJob` | `contratos-v2` | 3 | 120s | Notifica falhas de validação do email |
| `ReconciliarAssinaturasPendentesJob` | `contratos-v2` | 3 | 300s | Recupera estado de assinaturas paradas |

---

## 8. Eventos e listeners

| Evento | Disparado por | Propriedades | Listener (queued) |
|--------|---------------|--------------|-------------------|
| `StatusV2Alterado` | `ContratoV2StateMachine::transition()` | `contrato`, `statusAnterior`, `statusNovo`, `justificativa` | `CriarContratoC3Listener` (apenas se `statusNovo = aprovado`) |
| `StatusC3Alterado` | `ContratoC3StateMachine::transition()` | idem | — (ponto de extensão) |

---

## 9. Integrações externas

| Sistema | Onde | Para quê |
|---------|------|----------|
| **Microsoft Graph** | `EmailService` | Polling de emails não lidos com anexo PDF |
| **OpenAI / Claude** | `OpenAIService` em `ProcessarIAJob` + `AnalisarRiscoV2` | Extração estruturada (`response_format=json_object`) e análise semântica de risco |
| **BoldSign** | `BoldSignClient`, `BoldSignService`, `BoldSignWebhookVerifier` | Assinatura digital embutida; HMAC SHA256 nos webhooks; reconciliação por API |
| **pdftotext** | `ExtrairTextoPdfV2` | Extração de texto offline |
| **FPDF** | `BoldSignSignaturePageGenerator` | Geração de página de assinatura anexa |
| **Storage `public`** | Diversos | PDFs (original e assinado), evidências de obrigações, documentos C3 |

---

## 10. Rotas

### 10.1 V2 — `routes/contratos-v2.php`

**Públicas (sem autenticação, apenas sessão `web`):**

| Método | URI | Controller | Função |
|--------|-----|-----------|--------|
| GET | `/solicitacoes-contrato/aprovacao/{token}` | `AprovacaoDiretorController@show` | Página de revisão pública |
| POST | `/solicitacoes-contrato/aprovacao/{token}/aprovar` | `@aprovar` | Aprova (cria envelope BoldSign) |
| POST | `/solicitacoes-contrato/aprovacao/{token}/reprovar` | `@reprovar` | Rejeita |
| GET | `/solicitacoes-contrato/aprovacao/{token}/assinatura-concluida` | `@assinaturaConcluida` | Landing pós-assinatura |
| GET | `/solicitacoes-contrato/aprovacao/{token}/assinatura-declinada` | `@assinaturaDeclinada` | Landing pós-recusa |
| GET | `/solicitacoes-contrato/aprovacao/{token}/sign-link-status` | `@signLinkStatus` | AJAX polling fallback |

**Webhook (público, throttle `60,1`):**

| POST | `/webhooks/boldsign` | `BoldSignWebhookController` |

**Autenticadas (`auth:sanctum` + `verified` + `VerifyUserPermission`):**

| Método | URI | Componente |
|--------|-----|-----------|
| GET | `/solicitacoes-contrato/` | `ContratoV2Index` |
| GET | `/solicitacoes-contrato/dashboard` | `DashboardV2` |
| GET | `/solicitacoes-contrato/revisao/{contrato}` | `RevisaoContratoV2` |
| GET | `/solicitacoes-contrato/gestao/{contrato}` | `GestaoContratoV2` |
| GET | `/solicitacoes-contrato/tags` | `TagsV2Index` |
| GET | `/solicitacoes-contrato/setores` | `SetoresV2Index` |

### 10.2 C3 — `routes/contratos-c3.php`

| Método | URI | Componente |
|--------|-----|-----------|
| GET | `/contratos/` | `ContratoC3Index` |
| GET | `/contratos/{contrato}` | `GestaoContratoC3` |

---

## 11. Permissões

Controle por `VerifyUserPermission` (códigos na faixa **500000**).

| Código | Escopo |
|--------|--------|
| `500006` | Acesso ao módulo V2 (todas as rotas autenticadas em `/solicitacoes-contrato/*`) |
| `500006` | Acesso ao módulo C3 (rotas em `/contratos/*`) |

> Permissões são **cacheadas indefinidamente** e invalidadas no logout via `PermissionCacheService`.

---

## 12. Webhooks e endpoints externos

### 12.1 Email inbound (Microsoft Graph)

- Não é webhook — é **polling** ativo via `EmailService::listUnreadMessages()`;
- Disparado por scheduler / chamada manual;
- Idempotência via `efx_hub_v2_emails_processados.internet_message_id` (UNIQUE).

### 12.2 BoldSign callback

- **Endpoint:** `POST /webhooks/boldsign`
- **Throttle:** `60` requisições por minuto
- **Autenticação:** HMAC SHA256 com janela de **300 s** anti-replay
- **Eventos relevantes:** `Completed`, `Declined` (demais são ignorados)
- **Idempotência:** short-circuit em estado terminal (Aprovado/Reprovado já registrado)
- **Resposta:** sempre 200 OK (mesmo em erro downstream — evita reentregas desnecessárias)

### 12.3 Reconciliação síncrona (fallback)

- **Endpoint:** `GET /solicitacoes-contrato/aprovacao/{token}/sign-link-status`
- **Uso:** polling pelo iframe quando webhook não chega (NAT, dev local sem túnel)
- **Lógica:** `BoldSignClient::getDocumentProperties` → se mudou, sintetiza payload e roda `ProcessarCallbackBoldSign`

---

## 13. Telas / componentes Livewire

### 13.1 V2 (`resources/views/livewire/contratos-v2/`)

| Componente | View | Funcionalidade |
|-----------|------|---------------|
| `ContratoV2Index` | `contrato-v2-index.blade.php` | Listagem com filtros (status, parceiro, tags, datas), busca global, ordenação, salvamento de filtros |
| `RevisaoContratoV2` | `revisao-contrato-v2.blade.php` | Revisão da extração IA, edição de campos, exibição de risco, ações aprovar/rejeitar/duvida |
| `GestaoContratoV2` | `gestao-contrato-v2.blade.php` | Detalhes do contrato em estado pós-aprovação; gestão de obrigações, aditivos, comentários, reajustes |
| `DashboardV2` | `dashboard-v2.blade.php` | KPIs, breakdown por status, tendências, top parceiros |
| `CreateContratoV2` | `create-contrato-v2.blade.php` | Formulário de criação manual |
| `TimelineContratoV2` | `timeline-contrato-v2.blade.php` | Linha do tempo de eventos e transições |
| `TagsV2Index` | `tags-v2-index.blade.php` | CRUD de tags |
| `SetoresV2Index` | `setores-v2-index.blade.php` | CRUD de setores |
| `CreateDiretorV2` | — | Cadastro rápido de diretor |
| `CreateTagV2` | — | Cadastro rápido de tag |
| `AditivoV2Manager` | — | Gestor de aditivos (CRUD) |
| `ObrigacaoV2Manager` | — | Gestor de obrigações + evidências |

### 13.2 C3 (`resources/views/livewire/contratos-c3/`)

| Componente | Funcionalidade |
|-----------|---------------|
| `ContratoC3Index` | Listagem com filtros |
| `GestaoContratoC3` | Detalhes, edição, abas (aditivos, contatos, documentos) |
| `CreateContratoC3` | Criação manual |
| `AditivoC3Manager` | Gestor de aditivos versionados |
| `ContatoC3Manager` | Gestor de contatos do parceiro |
| `DocumentoC3Manager` | Anexos suplementares |

### 13.3 Páginas públicas (Blade puro, sem Livewire)

| View | Função |
|------|--------|
| `contratos-v2/aprovacao/show.blade.php` | Revisão pelo diretor (token-gated) |
| `contratos-v2/aprovacao/assinatura-preparando.blade.php` | Wrapper do iframe BoldSign |
| `contratos-v2/aprovacao/assinatura-concluida.blade.php` | Confirmação de assinatura |
| `contratos-v2/aprovacao/assinatura-declinada.blade.php` | Confirmação de recusa |

---

## 14. Tabelas de banco

### 14.1 V2

| Tabela | Função |
|--------|--------|
| `efx_hub_v2_contratos` | Tabela principal (status, intake, IA, assinatura) |
| `efx_hub_v2_logs` | Auditoria (todas as transições e edições) |
| `efx_hub_v2_aditivos` | Aditivos contratuais |
| `efx_hub_v2_obrigacoes` | Catálogo de obrigações |
| `efx_hub_v2_obrigacoes_contratos` | Pivot obrigação ↔ contrato (status, prazo, evidência) |
| `efx_hub_v2_comentarios_contratos` | Comentários (públicos / privados) |
| `efx_hub_v2_reajustes_contratos` | Reajustes aplicados |
| `efx_hub_v2_tags_contrato` | Tags |
| `efx_hub_v2_tags_pivot` | Pivot tag ↔ contrato |
| `efx_hub_v2_diretores` | Cadastro de diretores aprovadores |
| `efx_hub_v2_tokens_aprovacao` | Tokens públicos (hash SHA256 + uso único) |
| `efx_hub_v2_emails_processados` | Idempotência de intake (`internet_message_id` UNIQUE) |
| `efx_hub_v2_filtros_salvos` | Presets de filtros por usuário |
| `efx_hub_v2_contratos_texto` | Full-text search |

### 14.2 C3

| Tabela | Função |
|--------|--------|
| `efx_hub_c3_contratos` | Contrato em vigência (com `numero_contrato CTR-YYYY-NNN`) |
| `efx_hub_c3_logs` | Auditoria |
| `efx_hub_c3_aditivos` | Aditivos versionados |
| `efx_hub_c3_contatos_parceiro` | Contatos do parceiro |
| `efx_hub_c3_documentos` | Anexos |
| `efx_hub_c3_numero_counter` | Sequencial anual (1 linha por ano) — pessimistic lock no `boot()` |
| `efx_hub_c3_tags_pivot` | Reaproveita `TagContratoV2` |

### 14.3 V1 (legado)

`efx_hub_contratos`, `efx_hub_tipos_contrato`, `efx_hub_aditivos`, `efx_hub_tags_contrato`, `efx_hub_obrigacoes_contratos`, `efx_hub_reajustes_contrato`, `efx_hub_fluxos_aprovacao`, `efx_hub_etapas_fluxo`, `efx_hub_instancias_aprovacao`, `efx_hub_eventos_aprovacao`, `efx_hub_tarefas_aprovacao`.

---

## 15. Decisões de design relevantes

1. **Pessimistic locking nas transições** — `SELECT ... FOR UPDATE` previne race conditions entre webhook BoldSign, polling de reconciliação e ações administrativas concorrentes (TOCTOU).
2. **Idempotência por short-circuit terminal** — webhooks de assinatura podem chegar duplicados; checar se o estado já é terminal evita reprocessamento.
3. **Envelope BoldSign criado FORA da transação** — se a chamada externa falhar após o commit, evitamos registros órfãos; se falhar antes, o estado interno permanece consistente.
4. **Token público com hash SHA256** — o token bruto **nunca** é persistido. Roubo do banco não compromete links já enviados.
5. **Filas separadas por finalidade** — `contratos-v2-ia` (IA, lenta, custosa) vs `contratos-v2` (orquestração) permite escalar workers e tunar timeouts independentemente.
6. **Polling AJAX como fallback do webhook** — em ambiente dev/NAT sem túnel, o iframe reconcilia o estado via API BoldSign.
7. **C3 criado por listener queued** — webhook BoldSign responde 200 imediato; falha na criação C3 não compromete a aprovação V2 e é reprocessável.
8. **Confiança da extração IA tipada** — campos com `confianca=pendente` forçam revisão humana; `inferido` exibe alerta visual; `auto` indica fonte de alta confiança.
9. **Numeração C3 sequencial atômica** — `efx_hub_c3_numero_counter` com pessimistic lock garante unicidade de `CTR-YYYY-NNN` mesmo sob alta concorrência.
10. **Webhooks BoldSign com HMAC + janela anti-replay** — verificação `hash_equals` (constant-time) e timestamp de 300 s impedem injeção e replay.

---

*Documento gerado em 2026-04-27 a partir da análise do código-fonte do EFX-HUB.*
