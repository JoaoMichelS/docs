---
title: "Listagem de Contratos"
description: "Tela de listagem de contratos em vigência com filtros e busca"
icon: "list"
---

# Listagem de Contratos

A tela `/contratos/` exibe todos os contratos em vigência. É o ponto de partida para localizar, revisar e operar sobre qualquer contrato após a assinatura.

## Colunas exibidas

| Coluna | Descrição |
|--------|-----------|
| **Número** | `CTR-AAAA-NNN` |
| **Parceiro** | Razão social ou nome |
| **Tipo** | Categoria do contrato |
| **Valor** | Valor total |
| **Início** | Data de início de vigência |
| **Fim** | Data de fim de vigência |
| **Status** | Estado atual (ativo, suspenso, encerrado, etc.) |
| **Setor** | Setor demandante |
| **Tags** | Tags associadas |

<Tip>
  Use a [Personalização de Colunas](/funcionalidades-gerais/personalizacao-colunas) para ocultar, reordenar ou exibir colunas adicionais conforme sua necessidade.
</Tip>

## Filtros disponíveis

A barra de filtros permite combinar diversos critérios:

- **Status** (múltipla seleção)
- **Parceiro** (busca textual ou CNPJ)
- **Tipo de contrato**
- **Setor**
- **Tags**
- **Período de vigência** (início e/ou fim)
- **Busca livre** (nome, número, parceiro)

## Ordenação

Clique no cabeçalho de qualquer coluna para ordenar crescente ou decrescente. Por padrão, a listagem vem ordenada por **data de criação descendente** (mais recentes primeiro).

## Ações por linha

Para cada contrato listado, você pode:

- **Abrir** — vai para a [tela de gestão completa](/gestao-contratos/contratos/gestao-detalhe)
- **Baixar PDF assinado** — download do contrato com assinatura digital
- **Visualizar histórico** — timeline de eventos e transições
- **Atalhos rápidos** para abas (aditivos, contatos, documentos)

## Ações em lote

Selecionando várias linhas via checkbox, é possível:

- Exportar para Excel ([Exportação de Dados](/funcionalidades-gerais/exportacao-dados))
- Aplicar tag em massa
- Mudar setor responsável

## Indicadores visuais

A listagem destaca contratos que precisam de atenção:

| Marcador | Significado |
|----------|-------------|
| 🔴 Borda vermelha | Vence nos próximos 30 dias |
| 🟡 Borda amarela | Vence nos próximos 90 dias |
| ⏸️ Ícone de pausa | Contrato suspenso |
| ⚠️ Triângulo | Pendência (revisão jurídica não finalizada, contato faltando, etc.) |

## Salvamento de filtros

Combinações de filtros podem ser salvas como **preset** com nome próprio. Útil para visões frequentes como:

- "Contratos do meu setor"
- "Vencendo nos próximos 60 dias"
- "Aguardando revisão jurídica"

Os presets ficam disponíveis no menu suspenso ao lado da barra de filtros.

## Próximo passo

Para entender o detalhe de um contrato, veja [Gestão (Detalhe)](/gestao-contratos/contratos/gestao-detalhe).
