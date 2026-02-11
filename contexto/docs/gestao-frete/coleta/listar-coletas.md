---
title: "Listar e Gerenciar Coletas"
description: "Como visualizar, editar e gerenciar coletas de frete"
icon: "list-check"
---

# Listar e Gerenciar Coletas

A tela de lista de coletas permite visualizar, editar e gerenciar todas as coletas registradas no sistema.

## Acessar a Lista

No menu lateral, navegue até **100 - Gestão de Fretes > Coletas > 111 - Lista de Coletas**.

## Tabela de Coletas

A tabela exibe todas as coletas com informações resumidas:

| Coluna | Descrição |
|--------|-----------|
| **Status** | Situação da coleta (Pendente, Confirmada) |
| **Transportadora** | Nome da transportadora |
| **N. Carregamento** | Número do carregamento |
| **Data de Chegada** | Data prevista de chegada |
| **Motorista** | Nome do motorista |
| **Veículo** | Tipo e placa do veículo |
| **Ações** | Botões de editar, visualizar PDF e histórico |

## Filtros Disponíveis

| Filtro | Descrição |
|--------|-----------|
| **Status** | Filtrar por status (Pendente, Confirmada) |
| **Transportadora** | Filtrar por transportadora |
| **N. Carregamento** | Filtrar por número de carregamento |
| **Data (de/até)** | Filtrar por período |

## Editar uma Coleta

<Steps>
  <Step title="Localizar a coleta">
    Use os filtros para encontrar a coleta desejada.
  </Step>
  <Step title="Clicar em Editar">
    Clique no botão **Editar** (ícone de lápis) na coluna de ações.
  </Step>
  <Step title="Informar justificativa">
    Ao editar uma coleta, é **obrigatório** informar uma justificativa para a alteração.
  </Step>
  <Step title="Alterar os campos">
    Modifique os campos necessários (motorista, veículo, data, etc.).
  </Step>
  <Step title="Salvar">
    Clique em **Salvar** para confirmar as alterações.
  </Step>
</Steps>

<Warning>
  Toda edição de coleta exige uma **justificativa obrigatória**. Essa informação é registrada no histórico de alterações para fins de auditoria.
</Warning>

## Histórico de Alterações

Cada coleta mantém um registro completo de todas as alterações realizadas, incluindo:

- **Data e hora** da alteração
- **Usuário** que realizou a alteração
- **Campo alterado** — qual campo foi modificado
- **Valor anterior** — o que estava antes
- **Valor novo** — o que foi alterado
- **Justificativa** — motivo da alteração

Para visualizar o histórico, clique no botão **Histórico** na coluna de ações.

## Exportar para Excel

Clique no botão **Exportar Excel** para baixar uma planilha com todas as coletas (respeitando os filtros aplicados).

## Download do PDF

Para baixar o PDF de uma coleta específica, clique no botão **PDF** na coluna de ações. O documento contém todos os dados da coleta, incluindo o QR Code de acesso.
