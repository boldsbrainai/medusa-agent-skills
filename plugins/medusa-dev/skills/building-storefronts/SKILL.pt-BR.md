---
name: building-storefronts
description: Carrega automaticamente ao planejar, pesquisar ou implementar funcionalidades de storefront Medusa (rotas API customizadas, integração com SDK, padrões do React Query, carregamento de dados). OBRIGATÓRIO para todo desenvolvimento de storefront em TODOS os modos. Contém padrões de uso do SDK, integração frontend e regras críticas que MCPs não fornecem.
---

# Desenvolvimento de Storefront com Medusa

Guia de integração frontend para construir storefronts com Medusa. Cobre uso do SDK, padrões do React Query e chamadas a rotas API customizadas.

## Quando Aplicar

Carregue esta skill para QUALQUER tarefa de storefront, incluindo:
- Chamar rotas API customizadas do Medusa
- Integrar o SDK Medusa em aplicações frontend
- Usar React Query para carregamento de dados
- Implementar mutações com updates otimistas
- Tratamento de erros e invalidação de cache

## REGRAS CRÍTICAS

- `sdk-always-use` — USE SEMPRE o Medusa JS SDK para TODAS as requisições de API; NÃO use `fetch()` direto
- `sdk-client-fetch` — Para rotas customizadas, use `sdk.client.fetch()`
- `sdk-no-json-stringify` — NUNCA use `JSON.stringify()` no corpo; o SDK faz a serialização
- `display-price-format` — PREÇO: Medusa armazena preços no formato de exibição (49.99 = 49.99). NÃO multiplique/divida por 100

## Padrões Rápidos

- Use `useQuery` para GETs e `useMutation` para POST/DELETE
- Invalide queries em `onSuccess` após mutações
- Estruture keys de queries hierarquicamente
- Trate estados `isLoading`, `isError`, `isPending`

## Referências

Antes de implementar, carregue o arquivo de referência adequado, por exemplo:

- `references/frontend-integration.md` — padrões de SDK e React Query

Seguir essas regras evita erros comuns como cabeçalhos faltando, serialização dupla e exibição incorreta de preços.
