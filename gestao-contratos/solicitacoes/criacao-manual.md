---
title: "Cadastro Manual de Contrato"
description: "Como cadastrar uma solicitação de contrato sem passar pelo email"
icon: "pen-to-square"
---

# Cadastro Manual de Contrato

O cadastro manual é usado quando o contrato chega **fora do canal de email padrão** — por exemplo, entregue fisicamente, enviado por outro meio, ou quando você precisa criar a solicitação por iniciativa interna.

<Note>
  Diferente do fluxo por email, o cadastro manual **não passa pela análise de IA**. Você preenche todos os campos diretamente.
</Note>

## Quando usar

- Contrato chegou impresso ou em outro canal
- Você quer iniciar a solicitação a partir de um modelo interno
- O contrato é uma renovação ou caso especial fora da esteira automática

## Como cadastrar

1. Acesse **Solicitações de Contrato** no menu lateral.
2. Clique em **Novo Contrato** no canto superior direito.
3. Preencha os campos obrigatórios:

| Campo | Obrigatório | Descrição |
|-------|-------------|-----------|
| **Parceiro** | Sim | Razão social ou CNPJ da contraparte |
| **Tipo de contrato** | Sim | Prestação de serviço, fornecimento, locação, etc. |
| **Valor** | Sim | Valor total do contrato |
| **Data de início** | Sim | Início da vigência |
| **Data de fim** | Sim | Fim da vigência |
| **Setor demandante** | Sim | Setor responsável dentro da empresa |
| **Diretor aprovador** | Sim | Quem aprovará via link público (selecione da lista) |
| **PDF do contrato** | Sim | Arquivo PDF do documento (até 20MB) |
| **Tags** | Não | Categorização livre |
| **Observações** | Não | Anotações internas |

4. Clique em **Salvar**.

## O que acontece depois

Ao salvar, o sistema:

- Cria a solicitação com status **Aguardando Revisão**
- Armazena o PDF
- Registra um log de auditoria com seu nome e data
- Envia notificação interna aos gestores responsáveis pelo setor

A solicitação aparece imediatamente na listagem e está pronta para a [Revisão Interna](/gestao-contratos/solicitacoes/revisao-interna).

<Warning>
  No cadastro manual, é sua responsabilidade preencher os campos corretamente — a IA não validará nem extrairá dados. Confira valores e datas antes de salvar.
</Warning>

## Diferenças entre cadastro manual e intake por email

| Aspecto | Manual | Email com IA |
|---------|--------|--------------|
| Origem dos dados | Preenchimento humano | Extração automática do PDF |
| Análise de risco | Não gerada automaticamente | Score automático baixo/médio/alto |
| Badges de confiança | Não exibidas | Auto / Inferido / Pendente |
| Notificação ao remetente | Não há remetente externo | Confirmação automática enviada |
| Tempo até estar pronto para revisão | Imediato | Alguns minutos (processamento da fila) |
