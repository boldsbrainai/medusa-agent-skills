# Mobile Responsiveness for Ecommerce Storefronts

## Visão Geral

Boa parte do tráfego ecommerce vem de dispositivos móveis. A experiência mobile precisa ser priorizada desde a arquitetura de layout até interações de toque, performance e safe areas.

## Padrões Mobile

- Priorize leitura vertical e CTA visível.
- Garanta áreas de toque de pelo menos 44px.
- Evite hover-only interactions.
- Use drawers e accordions quando a densidade de informação for alta.

## Performance

- Comprima imagens.
- Adie assets abaixo da dobra.
- Reduza scripts e componentes pesados no primeiro carregamento.

## Safe Area

- Use `env(safe-area-inset-bottom)` em barras fixas e CTAs inferiores.
- Teste navegação com indicadores do iOS e Android.

## Casos de Uso Yello Solar Hub

- Compradores consultando catálogo técnico no canteiro ou em visita comercial.
- Integradores comparando kits pelo celular antes de fechar proposta.
- Navegação rápida por fabricantes, potência e faixa de preço.

## Erros Comuns

- Botões pequenos.
- Imagens de desktop servidas integralmente no mobile.
- CTA de compra escondido abaixo da dobra por excesso de conteúdo.
