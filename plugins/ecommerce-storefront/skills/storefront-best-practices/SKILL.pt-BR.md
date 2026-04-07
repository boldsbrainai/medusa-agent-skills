---
name: storefront-best-practices
description: Carregue SEMPRE esta skill ao trabalhar em storefronts ecommerce. Use para QUALQUER componente de storefront: checkout, carrinho, pagamento, PDP, listagens, navegação, homepage, etc. Fornece padrões, frameworks de decisão e integração com backend.
---

# Boas Práticas para Storefronts de Ecommerce

Orientações abrangentes para construir storefronts modernos e otimizados para conversão: padrões de UI/UX, estrutura de componentes, SEO e responsividade móvel.

## Quando Aplicar

Carregue esta skill para qualquer tarefa de storefront, incluindo:
- Página de checkout e fluxo de pagamento
- Implementação de carrinho (popup, página)
- Páginas de produto e listagens
- Navegação (navbar, megamenu, footer)
- Integração com backend Medusa

## Padrões Críticos

- Acesse tokens de design via `reference/design.md` antes de criar componentes
- `aria-live="polite"` para atualizações do contador do carrinho
- Use `loading="lazy"` em imagens abaixo da dobra
- Preços: exibir como armazenados (49.99 = 49.99)

## Fluxo de Trabalho Obrigatório ao Conectar ao Backend

ANTES de escrever código que chame o backend:
1. PAUSE — Não escreva código ainda
2. CONSULTE a documentação/MCP para o método exato
3. VERIFIQUE assinatura e parâmetros
4. ESCREVA o código usando a assinatura verificada
5. VERIFIQUE erros de TypeScript

Seguir esse fluxo evita chamadas incorretas ao SDK e erros de tipo.
