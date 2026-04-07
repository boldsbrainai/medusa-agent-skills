# Medusa Backend Integration

## Visão Geral

Quando o backend é Medusa, a integração do storefront deve priorizar o SDK oficial, estado consistente de região e carrinho, e respeito às regras de preço do projeto.

## Setup

- Instale e configure o Medusa JS SDK conforme a stack do frontend.
- Centralize a instância do SDK em um único módulo.
- Use variáveis de ambiente para `baseUrl`, publishable key e outras opções necessárias.

## Regras Críticas

- Use métodos prontos do SDK para endpoints nativos.
- Use `sdk.client.fetch()` para rotas customizadas.
- Não use `JSON.stringify()` no `body` do SDK.
- Não use `fetch` cru quando o SDK cobrir o caso.
- Em YSH Store, preços são tratados como valor final; não multiplique nem divida por 100.

## Tipos e Organização

- Separe tipos de domínio, respostas e parâmetros quando o frontend crescer.
- Mantenha hooks de React Query próximos do cliente do SDK ou em camada própria.
- Nomeie query keys de forma hierárquica.

## Região e Estado Comercial

- Região afeta preço, métodos de entrega e disponibilidade.
- Reaja a mudanças de região invalidando caches relevantes.

## Casos de Uso Yello Solar Hub

- Listagem técnica de produtos solares com pricing coerente por canal.
- Checkout B2B apoiado por regras comerciais e distribuidores.
- Consulta de kits e itens relacionados a projetos empresariais.

## Erros Comuns

- Duplicar serialização do body.
- Ignorar invalidation após mutação.
- Tratar preço como centavos.
