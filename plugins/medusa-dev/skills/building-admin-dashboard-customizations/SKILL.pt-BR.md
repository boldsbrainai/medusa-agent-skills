---
name: building-admin-dashboard-customizations
description: Carrega automaticamente ao planejar, pesquisar ou implementar customizações da UI do Admin Medusa (widgets, páginas, formulários, tabelas, carregamento de dados, navegação). OBRIGATÓRIO para todo trabalho de UI admin em TODOS os modos.
---

# Customizações do Painel Admin do Medusa

Construa extensões de UI para o painel Admin do Medusa usando o Admin SDK e os componentes de UI fornecidos.

## Quando Aplicar

Carregue esta skill para QUALQUER tarefa de UI admin, incluindo:
- Criar widgets para páginas de produto/pedido/cliente
- Construir páginas customizadas do admin
- Implementar formulários e modais
- Exibir dados com tabelas ou listas
- Adicionar navegação entre páginas

## REGRAS CRÍTICAS

- Sempre carregar referências relevantes antes de codificar (por exemplo `references/forms.md` para formulários)
- `data-sdk-always` — USE SEMPRE o Medusa JS SDK para requisições (NUNCA use fetch() simples)
- `display-price-format` — PREÇO: Medusa armazena preços no formato de exibição (49.99 = 49.99). NÃO multiplique/divida por 100

## Padrões Rápidos

- Queries de exibição devem carregar na montagem do componente (no mount)
- Separe queries de display das queries de modal/form
- Invalide queries de display após mutações
- Use componentes Medusa UI (Container, Button, Text) em vez de tags HTML puras

## Dependências e pnpm

Se o projeto usa `pnpm`, instale peer dependencies (ex.: `@tanstack/react-query`) antes de codificar.

## Referências

Carregue arquivos de referência relevantes conforme a implementação (forms, display-patterns, table-selection, etc.).
