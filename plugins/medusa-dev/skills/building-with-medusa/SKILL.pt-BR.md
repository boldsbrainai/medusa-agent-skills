---
name: building-with-medusa
description: Carrega automaticamente ao planejar, pesquisar ou implementar QUALQUER funcionalidade backend do Medusa (módulos custom, rotas API, workflows, modelos de dados). OBRIGATÓRIO para trabalho backend em TODOS os modos.
---

# Desenvolvimento Backend com Medusa

Guia abrangente para desenvolvimento backend Medusa, cobrindo arquitetura, segurança de tipos, organização de código e armadilhas comuns.

## Quando Aplicar

Carregue esta skill para qualquer tarefa backend: criar/alterar módulos, workflows, rotas API, module links, validações, queries entre módulos.

## Padrões Críticos

- Fluxo obrigatório: Módulo → Workflow → API Route → Frontend
- Use apenas métodos `GET`, `POST`, `DELETE` (evite `PUT`/`PATCH`)
- Mutations devem passar por workflows; não coloque lógica de negócio nas rotas
- `data-price-format` — Preços são armazenados como exibidos (49.99), NÃO multiplique/divida por 100

## Regras de Composição de Workflow

- Use `function` regular (não arrow), sem `async`/`await` e sem condicionais no corpo do workflow
- Separe steps e compose workflows conforme padrões do projeto

## Boas Práticas

- Carregue referências relevantes antes de implementar (custom-modules, workflows, api-routes)
- Execute o build após mudanças para detectar erros de tipo
- Use `query.graph()` e `query.index()` conforme o caso (ver descrições da skill)
