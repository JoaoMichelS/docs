---
title: "Cotação Avulsa"
description: "Como criar cotações avulsas por cliente no Alpex Digital Hub"
icon: "file-circle-plus"
---

# Cotação Avulsa

A cotação avulsa é utilizada para registrar cotações de frete que não estão vinculadas a pedidos do ERP. É ideal para fretes extraordinários ou operações que não seguem o fluxo padrão de pedidos.

## Criar Cotação Avulsa

<Steps>
  <Step title="Acessar a tela">
    No menu lateral, navegue até **100 - Gestão de Fretes > Gestão de Cotação > 102 - Cotação Avulsa**.
  </Step>
  <Step title="Buscar pedidos">
    Utilize os filtros para localizar os pedidos do cliente que deseja cotar. Você pode buscar por número do pedido, cliente, CNPJ ou outros critérios.
  </Step>
  <Step title="Selecionar o pedido">
    Clique no pedido desejado na lista para abri-lo.
  </Step>
  <Step title="Preencher as cotações">
    Informe até **3 opções de transportadora** com seus respectivos valores:
    - **Transportadora 1** — nome e valor do frete
    - **Transportadora 2** — nome e valor do frete
    - **Transportadora 3** — nome e valor do frete
  </Step>
  <Step title="Salvar">
    Clique em **Salvar** para registrar a cotação. Ela aparecerá automaticamente na tela de aprovação.
  </Step>
</Steps>

## Tabela de Cotações Avulsas

A tabela lista os pedidos com as seguintes colunas:

| Coluna | Descrição |
|--------|-----------|
| **Data** | Data de lançamento do pedido |
| **N. Pedido** | Número do pedido (inicia com 300 para avulsos) |
| **Filial** | Filial de origem |
| **Valor** | Valor total do pedido |
| **Cod. Cliente** | Código do cliente |
| **Cliente** | Nome do cliente |
| **Documento** | CNPJ/CPF do cliente |
| **Peso (Kg)** | Peso total |
| **Praça** | Praça de destino |
| **Município** | Município de destino |
| **Estado** | Estado de destino |
| **Ação** | Botão para abrir a cotação |

## Filtros Disponíveis

| Filtro | Descrição |
|--------|-----------|
| **Data (de/até)** | Período de lançamento |
| **Número do Pedido** | Busca direta por número |
| **Cliente** | Nome do cliente |
| **CNPJ** | Documento do cliente |
| **Estado** | Estado de destino |
| **Município** | Município de destino |
| **Peso (de/até)** | Faixa de peso |
| **Valor (de/até)** | Faixa de valor |

## Funcionalidades

- **Ordenação** — clique no cabeçalho de qualquer coluna para ordenar
- **Personalização de colunas** — reordene e oculte colunas
- **Exportação para Excel** — exporte os dados filtrados
- **Paginação** — navegação por páginas (15 itens por página)

<Note>
  Pedidos avulsos são identificados por números que iniciam com **300**. Eles são diferenciados dos pedidos normais do ERP na tela de aprovação.
</Note>
