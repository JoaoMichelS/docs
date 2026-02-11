---
title: "Upload de CTE"
description: "Como importar XMLs de Conhecimento de Transporte Eletrônico"
icon: "file-import"
---

# Upload de CTE

O CTE (Conhecimento de Transporte Eletrônico) é o documento fiscal que comprova a prestação de serviço de transporte. Nesta tela, você importa os XMLs dos CTEs emitidos pelas transportadoras para que o sistema possa cruzar automaticamente com as cotações aprovadas.

## O que é o CTE

O CTE é um documento fiscal eletrônico (XML) emitido pela transportadora que contém informações como:

- Dados da transportadora (emitente)
- Dados do remetente e destinatário
- Valor do frete cobrado
- Peso da mercadoria
- Chave de acesso (44 dígitos)
- Data de emissão

## Upload de XMLs

<Steps>
  <Step title="Acessar a tela">
    No menu lateral, navegue até **100 - Gestão de Fretes > Auditoria de Cotação > 107 - Importar CTE**.
  </Step>
  <Step title="Selecionar arquivos">
    Clique no botão **Selecionar Arquivos** ou arraste os XMLs para a área de upload.
  </Step>
  <Step title="Verificar limites">
    Confirme que os arquivos estão dentro dos limites:
    - **Máximo de 25 arquivos** por upload
    - **Máximo de 2 MB** por arquivo
    - Formato aceito: **XML** (.xml)
  </Step>
  <Step title="Enviar">
    Clique em **Enviar** para iniciar o processamento dos XMLs.
  </Step>
  <Step title="Verificar resultado">
    O sistema exibirá o resultado do processamento:
    - Arquivos importados com sucesso
    - Arquivos duplicados (já importados anteriormente)
    - Arquivos com erro de formato
  </Step>
</Steps>

## Dados Extraídos Automaticamente

O sistema extrai automaticamente os seguintes dados de cada XML:

| Dado | Descrição |
|------|-----------|
| **Chave CTE** | Chave de acesso de 44 dígitos |
| **Número CTE** | Número do documento |
| **Série** | Série do CTE |
| **Data emissão** | Data de emissão do CTE |
| **Transportadora** | Nome e CNPJ do emitente |
| **Remetente** | Dados do remetente |
| **Destinatário** | Dados do destinatário |
| **Valor frete** | Valor total do frete cobrado |
| **Peso** | Peso da mercadoria |

## Validações Automáticas

O sistema realiza validações automáticas após a importação:

- **Duplicidade** — verifica se o CTE já foi importado anteriormente (pela chave de acesso)
- **Diferença de valor** — compara o valor do CTE com a cotação aprovada. Se a diferença for superior a **R$ 0,50**, uma notificação é gerada automaticamente

<Warning>
  CTEs com diferença superior a R$ 0,50 em relação à cotação aprovada geram uma notificação automática para o gestor. Verifique esses casos na tela de conferência.
</Warning>

## Tabela de CTEs Importados

A tela exibe todos os CTEs importados com diversas colunas de informação.

## Filtros Disponíveis

A tela possui **18 filtros** para localização precisa:

| Filtro | Descrição |
|--------|-----------|
| **Data emissão (de/até)** | Período de emissão |
| **Número CTE** | Busca por número |
| **Chave CTE** | Busca por chave de acesso |
| **Transportadora** | Filtrar por transportadora |
| **CNPJ transportadora** | Documento da transportadora |
| **Remetente** | Nome do remetente |
| **Destinatário** | Nome do destinatário |
| **Valor (de/até)** | Faixa de valor |
| **Peso (de/até)** | Faixa de peso |
| **Número pedido** | Número do pedido vinculado |
| **Filial** | Filial de origem |
| **Status** | Status do CTE |
| **Série** | Série do CTE |
| **Estado origem** | UF de origem |
| **Estado destino** | UF de destino |
| **Município origem** | Cidade de origem |
| **Município destino** | Cidade de destino |
| **Data importação** | Data em que o XML foi importado |

## Exportar para Excel

Clique no botão **Exportar Excel** para baixar uma planilha com todos os CTEs importados (respeitando os filtros aplicados).

<Note>
  Recomendamos importar os CTEs diariamente para manter a conferência atualizada e identificar divergências rapidamente.
</Note>
