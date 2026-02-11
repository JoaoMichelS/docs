---
title: "Pré-Cotação"
description: "Como criar e gerenciar pré-cotações no Alpex Digital Hub"
icon: "file-lines"
---

# Pré-Cotação

A pré-cotação é uma etapa preparatória que permite organizar os dados de frete e enviá-los para as transportadoras antes de formalizar a cotação. É útil para obter propostas de preço antecipadamente.

## Criar Pré-Cotação Manualmente

<Steps>
  <Step title="Acessar a tela de Pré-Cotação">
    No menu lateral, navegue até **100 - Gestão de Fretes > Gestão de Cotação > 106 - Pré Cotação**.
  </Step>
  <Step title="Clicar em Nova Pré-Cotação">
    Clique no botão **Nova Pré-Cotação** para abrir o formulário.
  </Step>
  <Step title="Selecionar a filial">
    Escolha a **filial** de origem no campo dropdown.
  </Step>
  <Step title="Selecionar o cliente">
    Busque e selecione o **cliente** destinatário.
  </Step>
  <Step title="Adicionar produtos">
    Adicione os **produtos** que serão transportados, informando quantidade e peso.
  </Step>
  <Step title="Verificar cálculo automático">
    O sistema calcula automaticamente o **peso total** com base nos produtos adicionados.
  </Step>
  <Step title="Salvar">
    Clique em **Salvar** para registrar a pré-cotação. Um email será enviado automaticamente para as transportadoras cadastradas.
  </Step>
</Steps>

## Importar via Excel

<Steps>
  <Step title="Baixar template">
    Na tela de Pré-Cotação, clique no botão **Download Template** para baixar a planilha modelo.
  </Step>
  <Step title="Preencher o template">
    Abra o arquivo Excel e preencha os dados seguindo o formato do template:
    - Código da filial
    - Código do cliente
    - Produtos e quantidades
    - Peso
  </Step>
  <Step title="Fazer upload">
    Clique no botão **Importar Excel** e selecione o arquivo preenchido.
  </Step>
  <Step title="Validação automática">
    O sistema valida os dados automaticamente. Caso haja erros, uma mensagem indicará quais linhas precisam de correção.
  </Step>
</Steps>

## Tabela de Pré-Cotações

A tela lista todas as pré-cotações com as seguintes colunas:

| Coluna | Descrição |
|--------|-----------|
| **Cód. Pedido** | Código identificador da pré-cotação |
| **Código da Filial** | Código da filial de origem |
| **Filial** | Nome da filial |
| **Cód. Cliente** | Código do cliente |
| **Cliente** | Nome do cliente |
| **Peso Total** | Peso total calculado |
| **Custo Total** | Valor total estimado |
| **Status** | Situação atual da pré-cotação |
| **Ações** | Botões de editar, visualizar e excluir |

## Filtros Disponíveis

- **Filial** — filtrar por filial de origem
- **Cliente** — filtrar por cliente
- **Produto** — filtrar por produto

## Funcionalidades Adicionais

- **Exportar para Excel** — exporte os dados filtrados em planilha
- **Personalizar colunas** — reordene e oculte colunas conforme sua necessidade
- **Notificação por email** — ao criar uma pré-cotação, o sistema envia automaticamente um email para as transportadoras com os dados necessários

<Note>
  A pré-cotação é uma etapa opcional. Você pode iniciar o processo diretamente pela cotação se já tiver os valores das transportadoras.
</Note>
