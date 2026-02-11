---
title: "Criar Coleta"
description: "Como criar uma coleta de frete no Alpex Digital Hub"
icon: "truck-loading"
---

# Criar Coleta

A coleta é o agendamento da retirada de mercadorias pela transportadora. Após a aprovação da cotação, o operador cria a coleta informando os detalhes do veículo, motorista e horário.

## Preencher Formulário de Coleta

<Steps>
  <Step title="Acessar a tela">
    No menu lateral, navegue até **100 - Gestão de Fretes > Coletas > 109 - Inserir Coleta**.
  </Step>
  <Step title="Informar dados de agendamento">
    Preencha os campos de agendamento:
    - **Data de chegada** — data prevista de chegada do veículo
    - **Transportadora** — selecione a transportadora aprovada
    - **Número de carregamento** — informe o número do carregamento
  </Step>
  <Step title="Informar dados do motorista">
    Preencha os dados do motorista:
    - **Nome do motorista** — nome completo
    - **CPF** — documento do motorista
    - **CNH** — número da carteira de habilitação
    - **Telefone** — contato do motorista
  </Step>
  <Step title="Informar ajudante (opcional)">
    Se houver ajudante, preencha:
    - **Nome do ajudante**
    - **CPF do ajudante**
  </Step>
  <Step title="Informar dados do veículo">
    Preencha os dados do veículo:
    - **Tipo de veículo** — selecione o tipo
    - **Placa** — placa do veículo
    - **Refrigerado** — marque se o veículo é refrigerado
  </Step>
  <Step title="Adicionar observações">
    No campo **Observações**, inclua qualquer informação adicional relevante para a coleta.
  </Step>
  <Step title="Salvar a coleta">
    Clique em **Salvar** para registrar a coleta.
  </Step>
</Steps>

## O que Acontece Após Salvar

Ao salvar a coleta, o sistema executa automaticamente:

1. **Geração de chave de acesso** — uma chave única é criada para identificar a coleta
2. **Geração de QR Code** — um QR Code é gerado para facilitar a validação na portaria
3. **Envio de email** — um email automático é enviado para a transportadora com todos os detalhes da coleta
4. **Geração de PDF** — um PDF da coleta é gerado e pode ser baixado a qualquer momento

## Campos do Formulário

| Campo | Obrigatório | Descrição |
|-------|:-----------:|-----------|
| Data de chegada | Sim | Data prevista de chegada do veículo |
| Transportadora | Sim | Transportadora responsável |
| N. Carregamento | Sim | Número do carregamento |
| Nome do motorista | Sim | Nome completo do motorista |
| CPF do motorista | Sim | Documento do motorista |
| CNH | Sim | Carteira de habilitação |
| Telefone | Não | Contato do motorista |
| Nome do ajudante | Não | Nome do ajudante |
| CPF do ajudante | Não | Documento do ajudante |
| Tipo de veículo | Sim | Categoria do veículo |
| Placa | Sim | Placa do veículo |
| Refrigerado | Não | Se o veículo é refrigerado |
| Observações | Não | Informações adicionais |

<Note>
  O PDF da coleta pode ser impresso e entregue na portaria para controle de acesso do veículo.
</Note>
