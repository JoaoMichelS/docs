---
title: "Login e Autenticação"
description: "Como acessar o Alpex Digital Hub com segurança"
icon: "lock"
---

# Login e Autenticação

## Acessando a Plataforma

Para acessar o Alpex Digital Hub, abra seu navegador e acesse a URL fornecida pela sua empresa.

### Tela de Login

A tela de login apresenta dois campos:

| Campo | Descrição |
|-------|-----------|
| **Usuário** | Seu código de usuário (matrícula) cadastrado no sistema |
| **Senha** | Sua senha pessoal de acesso |

<Steps>
  <Step title="Abrir a plataforma">
    Acesse a URL do Alpex Digital Hub no seu navegador.
  </Step>
  <Step title="Informar credenciais">
    Digite seu **usuário** e **senha** nos campos correspondentes.
  </Step>
  <Step title="Clicar em Entrar">
    Clique no botão **Entrar** para acessar a plataforma.
  </Step>
  <Step title="Autenticação 2FA (se habilitada)">
    Se a autenticação de dois fatores estiver ativada, insira o código gerado pelo seu aplicativo autenticador.
  </Step>
</Steps>

## Autenticação de Dois Fatores (2FA)

O Alpex Digital Hub suporta autenticação de dois fatores para aumentar a segurança do seu acesso.

Quando o 2FA está habilitado, após inserir usuário e senha, você precisará fornecer um código de verificação gerado por um aplicativo autenticador (como Google Authenticator ou Authy).

<Warning>
  O limite de tentativas para o código 2FA é de **5 tentativas por minuto**. Após exceder esse limite, aguarde 1 minuto antes de tentar novamente.
</Warning>

## Limite de Tentativas de Login

Para proteger sua conta, o sistema impõe um limite de **5 tentativas de login por minuto** (por combinação de email + IP). Após exceder esse limite, aguarde 1 minuto para tentar novamente.

## Registro de Acessos

Todas as tentativas de login são registradas automaticamente no sistema, incluindo:

- **Matrícula** do usuário
- **Data e hora** do acesso
- **Endereço IP** de origem
- **Status** (sucesso ou falha)

Esses registros são utilizados para auditoria e segurança.

## Esqueceu sua Senha?

Caso tenha esquecido sua senha, entre em contato com o administrador do sistema para solicitar a redefinição.

<Note>
  O acesso ao Alpex Digital Hub requer uma permissão específica (rotina 500001). Se você não conseguir acessar mesmo com credenciais corretas, entre em contato com o administrador para verificar suas permissões.
</Note>
