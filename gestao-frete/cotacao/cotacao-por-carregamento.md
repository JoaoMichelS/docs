---
title: "Cotação por Carregamento"
description: "Como criar cotações agrupadas por número de carregamento"
icon: "boxes-stacked"
---

# Cotação por Carregamento

A cotação por carregamento permite agrupar vários pedidos que serão transportados no mesmo veículo, criando uma cotação única para o grupo. Isso é ideal quando múltiplos pedidos compartilham a mesma rota e transportadora.

## Criar Cotação por Carregamento

<Steps>
  <Step title="Acessar a tela">
    No menu lateral, navegue até **100 - Gestão de Fretes > Gestão de Cotação > 104 - Inserir Cotação por Carregamento**.
  </Step>
  <Step title="Filtrar pedidos">
    Utilize os filtros de **filial** e **número de carregamento** para localizar os pedidos que deseja agrupar.
  </Step>
  <Step title="Selecionar pedidos">
    Na coluna **Selecionar**, marque os pedidos que farão parte do mesmo carregamento.
  </Step>
  <Step title="Preencher cotações">
    Informe até **3 opções de transportadora** com seus respectivos valores para o grupo de pedidos selecionado.
  </Step>
  <Step title="Salvar">
    Clique em **Salvar** para registrar a cotação agrupada. Todos os pedidos selecionados serão vinculados ao mesmo grupo.
  </Step>
</Steps>

## Tabela de Pedidos

A tabela exibe os pedidos disponíveis com as seguintes colunas:

| Coluna | Descrição |
|--------|-----------|
| **Selecionar** | Checkbox para selecionar pedidos para agrupamento |
| **Data** | Data do pedido |
| **Tipo** | Tipo do pedido |
| **N. Pedido** | Número do pedido |
| **Filial** | Filial de origem |
| **Agrupamento** | Grupo de carregamento (se já agrupado) |
| **Valor** | Valor total do pedido |
| **Cod. Cliente** | Código do cliente |
| **Cliente** | Nome do cliente |
| **Documento** | CNPJ/CPF do cliente |
| **Peso (Kg)** | Peso total |
| **N. Carregamento** | Número do carregamento |
| **Data Entrega** | Data prevista de entrega |
| **Tipo Frete Redespacho** | CIF ou FOB (redespacho) |
| **Tipo Frete Padrão** | CIF, FOB, Gratuito, Próprio CIF, Próprio FOB, Terceiro |
| **Praça** | Praça de destino |
| **Município** | Município de destino |
| **Estado** | Estado de destino |
| **Ação** | Botão para inserir cotação individual |

## Filtros Disponíveis

| Filtro | Descrição |
|--------|-----------|
| **Filial** | Filtrar por filial de origem |
| **N. Carregamento** | Filtrar por número de carregamento |
| **Data (de/até)** | Período dos pedidos |
| **Cliente** | Nome do cliente |
| **Estado** | Estado de destino |

## Cotações Agrupadas

Quando pedidos são agrupados, o sistema registra o vínculo na tabela de carregamentos agrupados. Na tela de aprovação, o gestor visualiza o grupo completo e pode aprovar todos os pedidos do carregamento de uma vez.

<Note>
  O agrupamento por carregamento é especialmente útil para otimizar custos de frete, pois permite negociar um valor único para múltiplas entregas na mesma rota.
</Note>
