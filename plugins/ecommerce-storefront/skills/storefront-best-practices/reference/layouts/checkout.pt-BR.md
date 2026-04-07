# Checkout Flow – Reference

## Visão Geral

Checkout deve reduzir atrito, manter consistência de preço e respeitar o modelo comercial do negócio.

## Estratégia

- Prefira 2 a 3 passos claros quando o fluxo for mais complexo.
- Em fluxos simples, single-page checkout pode funcionar melhor.
- Separe endereço, entrega, pagamento e revisão quando a complexidade exigir.

## Arquitetura

- Separe componentes server e client conforme a stack permitir.
- Centralize estado do checkout.
- Valide backend antes de avançar de etapa.

## Casos de Uso Yello Solar Hub

- Checkout B2B para kits solares com revisão comercial.
- Captura de dados de empresa, responsável e condições de pagamento.
- Fluxos com orçamento, aprovação e financiamento.
