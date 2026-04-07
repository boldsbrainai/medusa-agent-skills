# Wishlist Feature

## Visão Geral

A wishlist ajuda o usuário a organizar intenção de compra, comparar alternativas e retornar ao catálogo depois. Em cenários B2B, também pode servir como pré-seleção para orçamento ou aprovação interna.

## Estrutura

- Botão de salvar e remover em cards e PDP.
- Página dedicada da wishlist.
- Feedback visual imediato ao salvar.
- Estado persistido para usuários autenticados.

## Usuário Logado x Visitante

- Para logados, persista no backend.
- Para visitantes, use armazenamento local com estratégia clara de migração após login.
- Não perca itens ao trocar sessão sem aviso.

## UX

- Evite esconder a wishlist em áreas secundárias.
- Permita mover item para o carrinho.
- Mostre preço atual e alterações relevantes desde o salvamento.

## Casos de Uso Yello Solar Hub

- Integradores salvando combinações de módulos e inversores para futura cotação.
- Compradores comparando kits solares por faixa de potência.
- Lista de interesse para análise financeira e aprovação interna.

## Erros Comuns

- Tratar wishlist como simples ícone sem página dedicada.
- Não sincronizar após login.
- Não informar quando um item ficou indisponível.
