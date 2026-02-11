---
title: "Navegação"
description: "Como navegar pela plataforma usando menu lateral, breadcrumbs e barra superior"
icon: "compass"
---

# Navegação

O Alpex Digital Hub possui uma interface intuitiva com três elementos principais de navegação: **menu lateral (sidebar)**, **barra superior (top menu)** e **breadcrumbs**.

## Menu Lateral (Sidebar)

O menu lateral é o principal meio de navegação entre os módulos da plataforma.

### Estrutura do Menu

```
├── Parametrização
├── 100 - Gestão de Fretes
│   ├── Gestão de Cotação
│   │   ├── 101 - Inserir Cotação
│   │   ├── 102 - Cotação Avulsa
│   │   ├── 103 - Cadastro de Cotação Padrão
│   │   ├── 104 - Inserir Cotação por Carregamento
│   │   ├── 105 - Aprovar Cotação
│   │   └── 106 - Pré Cotação
│   ├── Auditoria de Cotação
│   │   ├── 107 - Importar CTE
│   │   └── 108 - Conferência
│   ├── Coletas
│   │   ├── 109 - Inserir Coleta
│   │   ├── 110 - Confirmar Coleta
│   │   └── 111 - Lista de Coletas
│   └── 112 - Dashboard
├── 200 - Contratos
├── 300 - Kanban
├── 400 - Calendário
├── 500 - Gráficos
├── 600 - Canhotos
└── 700 - Marketing
    ├── 701 - Posts
    └── 702 - Relatórios
```

### Modos do Menu

O menu lateral possui dois modos de operação que podem ser alternados via toggle na parte inferior:

| Modo | Comportamento |
|------|---------------|
| **Automático** | O menu fica recolhido (apenas ícones) e expande ao passar o mouse por cima |
| **Manual** | O menu permanece expandido ou recolhido conforme sua escolha |

### Busca no Menu

No topo do menu lateral há um campo de **busca** que permite filtrar os itens do menu em tempo real. Digite o nome ou o número do módulo para encontrar rapidamente a funcionalidade desejada.

### Comportamento Responsivo

| Dispositivo | Comportamento |
|-------------|---------------|
| **Desktop** (>= 768px) | Menu sempre visível, recolhido por padrão (64px), expande ao hover (320px) |
| **Mobile** (< 768px) | Menu oculto por padrão, abre como overlay ao clicar no ícone de menu |

## Barra Superior (Top Menu)

A barra superior contém:

- **Logo** da plataforma
- **Ícone de notificações** (sino) — mostra notificações não lidas
- **Perfil do usuário** — acesso às configurações de conta

## Breadcrumbs

Os breadcrumbs (trilha de navegação) aparecem no topo de cada página, indicando sua localização atual na hierarquia do sistema.

Exemplo: `Início > Gestão de Fretes > Cotação Avulsa`

## Permissões e Visibilidade do Menu

<Warning>
  Os itens do menu são exibidos de acordo com as permissões do seu usuário. Se um módulo ou funcionalidade não aparece no menu, significa que você não tem permissão para acessá-lo. Nesse caso, entre em contato com o administrador do sistema.
</Warning>

O sistema utiliza **códigos de rotina** para controlar o acesso. Cada item do menu está associado a um código e somente será exibido se o usuário tiver a permissão correspondente habilitada.

### Indicador de Página Ativa

A página em que você está atualmente é destacada no menu com um fundo azul claro, facilitando a identificação da sua localização na plataforma.
