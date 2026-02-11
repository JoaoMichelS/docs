---
title: "Personalização de Colunas"
description: "Como personalizar a ordem e visibilidade das colunas nas tabelas"
icon: "table-columns"
---

# Personalização de Colunas

Todas as tabelas do módulo de Gestão de Frete permitem personalizar quais colunas são exibidas e em qual ordem. Essa configuração é salva por usuário — cada pessoa pode ter sua própria configuração sem afetar os demais.

## Personalizar Ordem e Visibilidade

<Steps>
  <Step title="Abrir configuração de colunas">
    Na tabela desejada, clique no botão **Personalizar Colunas** (ícone de engrenagem ou colunas) localizado acima da tabela.
  </Step>
  <Step title="Reordenar colunas">
    Arraste e solte as colunas na ordem desejada. A coluna no topo da lista será a primeira coluna da tabela (mais à esquerda).
  </Step>
  <Step title="Ocultar colunas">
    Desmarque as colunas que não deseja visualizar. Elas serão ocultadas da tabela, mas os dados continuam disponíveis.
  </Step>
  <Step title="Salvar">
    Clique em **Salvar** para aplicar as configurações. Sua preferência será mantida nos próximos acessos.
  </Step>
</Steps>

## Tabelas com Personalização Disponível

A personalização está disponível nas seguintes tabelas:

| Tela | Colunas Padrão |
|------|----------------|
| **Pré-Cotação** | Cód. Pedido, Código da Filial, Filial, Cód. Cliente, Cliente, Peso Total, Custo Total, Status, Ações |
| **Cotação Avulsa** | Data, N. Pedido, Filial, Valor, Cod. Cliente, Cliente, Documento, Peso, Praça, Município, Estado, Ação |
| **Cotação por Carregamento** | Selecionar, Data, Tipo, N. Pedido, Filial, Agrupamento, Valor, Cod. Cliente, Cliente, Documento, Peso, N. Carregamento, Data Entrega, Tipo Frete Redespacho, Tipo Frete Padrão, Praça, Município, Estado, Ação |
| **Cotação Padrão** | Tipo de Veículo, Cód. Transp., Transportadora, Cód. Filial, Filial, Valor (R$), Última Atualização, Ações |
| **Aprovar Cotação** | Ação, Data, Tipo, N. Pedido, Filial, Agrupamento, Valor, Cod. Cliente, Cliente, Documento, Peso, N. Carregamento, Data Entrega, Tipo Frete Redespacho, Tipo Frete Padrão, Praça, Município, Estado |
| **Upload CTE** | Colunas específicas de CTE |
| **Conferência CTE** | Colunas específicas de conferência |

## Resetar para Padrão

Se desejar restaurar a configuração original das colunas:

<Steps>
  <Step title="Abrir configuração de colunas">
    Clique no botão **Personalizar Colunas**.
  </Step>
  <Step title="Resetar">
    Clique no botão **Restaurar Padrão** para voltar à configuração original.
  </Step>
</Steps>

## Como Funciona Internamente

- As preferências são salvas **por usuário** (identificado pela matrícula)
- A configuração persiste entre sessões (é mantida em cache permanente)
- Se novas colunas forem adicionadas ao sistema, elas aparecerão automaticamente ao final da tabela, mesmo que você tenha uma ordem personalizada salva

<Note>
  A personalização de colunas não afeta as exportações para Excel. Ao exportar, todas as colunas serão incluídas independentemente da configuração de visibilidade.
</Note>
