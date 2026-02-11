---
title: "Conferência CTE"
description: "Como conferir CTEs contra cotações aprovadas"
icon: "magnifying-glass-dollar"
---

# Conferência CTE

A conferência de CTE é o processo de comparação entre os valores cobrados no CTE (documento fiscal da transportadora) e os valores das cotações aprovadas no sistema. O objetivo é identificar divergências e garantir que os valores cobrados estão corretos.

## Objetivo

- Comparar o **valor do CTE** com o **valor da cotação aprovada**
- Identificar **diferenças** que precisam de atenção
- Gerar **relatórios** de conferência para auditoria

## Conferir CTEs

<Steps>
  <Step title="Acessar a tela">
    No menu lateral, navegue até **100 - Gestão de Fretes > Auditoria de Cotação > 108 - Conferência**.
  </Step>
  <Step title="Filtrar os CTEs">
    Utilize os filtros disponíveis para localizar os CTEs que deseja conferir (por período, transportadora, filial, etc.).
  </Step>
  <Step title="Analisar as colunas">
    A tabela exibe lado a lado:
    - **Valor CTE** — valor cobrado pela transportadora no documento fiscal
    - **Valor Aprovado** — valor da cotação aprovada no sistema
    - **Diferença** — diferença entre os dois valores
  </Step>
  <Step title="Identificar divergências">
    Linhas com diferença significativa são destacadas visualmente para facilitar a identificação.
  </Step>
  <Step title="Tomar ação">
    Para CTEs com divergência, entre em contato com a transportadora ou registre a ocorrência no sistema.
  </Step>
</Steps>

## Colunas Principais

| Coluna | Descrição |
|--------|-----------|
| **Número CTE** | Número do documento fiscal |
| **Transportadora** | Nome da transportadora |
| **N. Pedido** | Número do pedido vinculado |
| **Valor CTE** | Valor cobrado no CTE |
| **Valor Aprovado** | Valor da cotação aprovada |
| **Diferença** | Diferença entre CTE e cotação (CTE - Aprovado) |
| **Status** | Status da conferência |

## Interpretando a Diferença

| Situação | Significado |
|----------|-------------|
| **Diferença = R$ 0,00** | Valor cobrado está igual ao aprovado |
| **Diferença positiva** | Transportadora cobrou **mais** que o aprovado |
| **Diferença negativa** | Transportadora cobrou **menos** que o aprovado |
| **Diferença > R$ 0,50** | Gera notificação automática para o gestor |

## Exportar Relatório

Clique no botão **Exportar Excel** para gerar um relatório completo de conferência, incluindo todas as colunas e a diferença calculada para cada CTE.

<Note>
  A conferência de CTE é uma ferramenta essencial de auditoria. Recomendamos conferir os CTEs semanalmente para identificar cobranças indevidas e manter o controle financeiro do frete.
</Note>
