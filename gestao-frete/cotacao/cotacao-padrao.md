---
title: "Cotação Padrão"
description: "Como gerenciar a tabela de cotações padrão por tipo de veículo"
icon: "table-list"
---

# Cotação Padrão

A cotação padrão é uma tabela de referência que registra valores fixos de frete por combinação de tipo de veículo, transportadora e filial. É usada como base para cotações que seguem uma tabela de preços previamente negociada.

## Visualizar Cotações Padrão

Ao acessar a tela (**100 - Gestão de Fretes > Cotação por Carregamento > 103 - Cadastro de Cotação Padrão**), você verá a tabela com todas as cotações padrão cadastradas.

### Colunas da Tabela

| Coluna | Descrição |
|--------|-----------|
| **Tipo de Veículo** | Categoria do veículo (ex: Truck, Carreta, VUC) |
| **Cód. Transp.** | Código da transportadora |
| **Transportadora** | Nome da transportadora |
| **Cód. Filial** | Código da filial |
| **Filial** | Nome da filial |
| **Valor (R$)** | Valor fixo do frete |
| **Última Atualização** | Data da última modificação |
| **Ações** | Botões de editar e excluir |

## Criar Cotação Padrão

<Steps>
  <Step title="Clicar em Nova Cotação Padrão">
    Clique no botão **Nova Cotação Padrão** na tela principal.
  </Step>
  <Step title="Preencher os campos">
    Informe os dados da cotação:
    - **Tipo de veículo** — selecione o tipo (ex: Truck, Carreta, VUC)
    - **Transportadora** — busque e selecione a transportadora
    - **Filial** — selecione a filial de origem
    - **Valor** — informe o valor fixo do frete em R$
  </Step>
  <Step title="Salvar">
    Clique em **Salvar** para registrar a cotação padrão.
  </Step>
</Steps>

## Editar Cotação Padrão

<Steps>
  <Step title="Localizar a cotação">
    Na tabela, localize a cotação que deseja editar usando os filtros ou rolando a lista.
  </Step>
  <Step title="Clicar em Editar">
    Clique no botão **Editar** (ícone de lápis) na coluna de ações.
  </Step>
  <Step title="Alterar os dados">
    Modifique os campos desejados.
  </Step>
  <Step title="Salvar">
    Clique em **Salvar** para confirmar as alterações.
  </Step>
</Steps>

## Excluir Cotação Padrão

<Steps>
  <Step title="Localizar a cotação">
    Na tabela, localize a cotação que deseja excluir.
  </Step>
  <Step title="Clicar em Excluir">
    Clique no botão **Excluir** (ícone de lixeira) na coluna de ações.
  </Step>
  <Step title="Confirmar exclusão">
    Confirme a exclusão na janela de confirmação.
  </Step>
</Steps>

## Importar/Exportar via Excel

### Importar

<Steps>
  <Step title="Baixar template">
    Clique no botão **Download Template** para baixar a planilha modelo.
  </Step>
  <Step title="Preencher o template">
    Preencha o arquivo com os dados: tipo de veículo, código da transportadora, código da filial e valor.
  </Step>
  <Step title="Fazer upload">
    Clique em **Importar Excel** e selecione o arquivo preenchido. O sistema validará e importará os dados.
  </Step>
</Steps>

### Exportar

Clique no botão **Exportar Excel** para baixar uma planilha com todos os dados da tabela (respeitando os filtros aplicados).

## Filtros Disponíveis

| Filtro | Descrição |
|--------|-----------|
| **Tipo de Veículo** | Filtrar por tipo de veículo |
| **Transportadora** | Filtrar por transportadora |
| **Filial** | Filtrar por filial |

<Warning>
  Ao excluir uma cotação padrão, essa ação é irreversível. Certifique-se de que a cotação não está mais em uso antes de excluí-la.
</Warning>
