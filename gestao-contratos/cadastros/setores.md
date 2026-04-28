---
title: "Setores"
description: "Cadastro dos setores demandantes de contratos"
icon: "building"
---

# Setores

Os **setores** representam as áreas internas da empresa que demandam contratos. Cada solicitação e cada contrato em vigência é vinculado a um setor responsável — isso facilita roteamento, relatórios e responsabilização.

## Onde fica

Acesse em **Solicitações de Contrato → Setores**.

## Campos do cadastro

| Campo | Obrigatório | Descrição |
|-------|-------------|-----------|
| **Nome** | Sim | Nome do setor |
| **Sigla** | Recomendado | Sigla curta (TI, FIN, JUR, etc.) |
| **Responsável** | Recomendado | Pessoa-chave do setor |
| **Email** | Recomendado | Email do setor para notificações |
| **Status** | Sim | Ativo / Inativo |

## Como o setor é usado

| Onde | Função |
|------|--------|
| **Cadastro manual** | Você seleciona o setor demandante no formulário |
| **Intake por IA** | A IA tenta extrair o setor do email/PDF e cruzar com o cadastro |
| **Filtragem** | Listagens permitem filtrar por setor |
| **Notificações** | Email do setor recebe alertas sobre contratos vinculados |
| **Dashboard** | KPIs podem ser segmentados por setor |

## Status Ativo vs. Inativo

| Status | Comportamento |
|--------|---------------|
| **Ativo** | Disponível para seleção em novas solicitações e contratos |
| **Inativo** | Não aparece em novos cadastros; preservado em contratos existentes |

<Tip>
  Quando uma área é dissolvida ou fundida, **inative** o setor antigo em vez de excluir — mantém a integridade do histórico.
</Tip>

## Boas práticas

<CardGroup cols={2}>
  <Card title="Padronize a granularidade" icon="layer-group">
    Decida se o setor representa diretorias, gerências ou times — e mantenha consistência. Misturar níveis confunde os relatórios.
  </Card>
  <Card title="Use siglas reconhecíveis" icon="font">
    Siglas curtas e claras facilitam a leitura em listagens com muitas colunas.
  </Card>
  <Card title="Mantenha o responsável atualizado" icon="user">
    Quando muda o gestor da área, atualize o cadastro — quem chega assume o histórico do setor.
  </Card>
  <Card title="Cadastre antes de operar" icon="check">
    Tenha todos os setores cadastrados antes de habilitar o intake automático — facilita o match da IA com os campos extraídos.
  </Card>
</CardGroup>

## Edição e exclusão

- **Editar** — todos os campos podem ser alterados.
- **Inativar** — preferível à exclusão.
- **Excluir** — possível apenas se nenhum contrato (solicitação ou em vigência) estiver vinculado ao setor.
