---
title: "Visão Geral - Cotações"
description: "Tipos de cotação disponíveis e quando usar cada um"
icon: "file-invoice-dollar"
---

# Visão Geral — Cotações

O Alpex Digital Hub oferece diferentes tipos de cotação para atender cenários distintos no processo logístico. Entender quando usar cada tipo é fundamental para otimizar o fluxo de trabalho.

## Tipos de Cotação

| Tipo | Código | Descrição | Melhor para |
|------|--------|-----------|-------------|
| **Inserir Cotação** | 101 | Cotação direta vinculada a pedidos do ERP | Pedidos já existentes no sistema |
| **Cotação Avulsa** | 102 | Cotação individual por cliente, não vinculada a pedido ERP | Fretes avulsos ou extraordinários |
| **Cotação Padrão** | 103 | Tabela fixa de valores por tipo de veículo | Rotas e veículos com preço tabelado |
| **Cotação por Carregamento** | 104 | Agrupa pedidos por carregamento | Múltiplos pedidos no mesmo veículo |
| **Pré-Cotação** | 106 | Preparação de dados para cotação futura | Envio prévio para transportadoras |

## Fluxograma de Decisão

```mermaid
flowchart TD
    START["Preciso cotar um frete"] --> Q1{"O pedido já existe\nno ERP?"}

    Q1 -->|"Sim"| Q2{"Preciso agrupar vários\npedidos no mesmo veículo?"}
    Q1 -->|"Não"| AVULSA["Cotação Avulsa\n(102)"]

    Q2 -->|"Sim"| CARREGAMENTO["Cotação por\nCarregamento (104)"]
    Q2 -->|"Não"| Q3{"Existe tabela de preço\nfixo para essa rota?"}

    Q3 -->|"Sim"| PADRAO["Cotação Padrão\n(103)"]
    Q3 -->|"Não"| Q4{"Preciso enviar dados\npara transportadoras\nantes de cotar?"}

    Q4 -->|"Sim"| PRECOT["Pré-Cotação (106)\n→ depois Inserir Cotação"]
    Q4 -->|"Não"| INSERIR["Inserir Cotação\n(101)"]

    style AVULSA fill:#E3F2FD,stroke:#1976D2
    style CARREGAMENTO fill:#E3F2FD,stroke:#1976D2
    style PADRAO fill:#E3F2FD,stroke:#1976D2
    style PRECOT fill:#E3F2FD,stroke:#1976D2
    style INSERIR fill:#E3F2FD,stroke:#1976D2
```

## Funcionalidades Comuns a Todas as Cotações

- **Filtros avançados** — cada tela possui filtros específicos para localizar cotações
- **Personalização de colunas** — reordenar e ocultar colunas conforme sua preferência
- **Exportação para Excel** — exportar dados filtrados para planilha
- **Ordenação** — clicar no cabeçalho da coluna para ordenar crescente/decrescente
- **Paginação** — navegação por páginas para grandes volumes de dados

## Fluxo Após a Cotação

Após criar uma cotação (em qualquer modalidade), o próximo passo é a **aprovação pelo gestor** na tela de [Aprovar Cotação](/gestao-frete/aprovacao-cotacao).

<Note>
  Cada tipo de cotação gera registros que aparecem automaticamente na tela de aprovação. O gestor não precisa saber em qual tela a cotação foi criada — todas convergem para o mesmo fluxo de aprovação.
</Note>
