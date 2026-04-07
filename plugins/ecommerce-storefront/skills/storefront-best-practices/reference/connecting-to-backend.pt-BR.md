# Connecting to Backend

## Visão Geral

O storefront deve se integrar ao backend de forma previsível, segura e orientada ao estado do negócio. Isso inclui descoberta da tecnologia, configuração de ambiente, autenticação, estado do carrinho e tratamento de erro.

## Descobrindo o Backend

- Verifique se o projeto usa Medusa, API REST própria, GraphQL ou outro stack.
- Confirme endpoints reais antes de escrever integração.
- Nunca assuma nomes de métodos do SDK sem validar na documentação.

## Configuração de Ambiente

- Centralize URL base da API em variáveis de ambiente.
- Separe ambientes local, staging e produção.
- Não espalhe URLs literais pelo frontend.

## Autenticação

- Respeite headers, cookies e tokens exigidos pelo backend.
- Reutilize cliente HTTP ou SDK centralizado.
- Mantenha sessão e refresh token coerentes com a estratégia do produto.

## Estado do Carrinho

- Carrinho deve refletir o backend, não apenas estado local.
- Recarregue e invalide cache após mutações relevantes.
- Preserve consistência entre popup, carrinho e checkout.

## Tratamento de Erros

- Diferencie falha de rede, falha de validação e falha de negócio.
- Exiba mensagens úteis e acionáveis.
- Faça retry apenas quando fizer sentido.

## Casos de Uso Yello Solar Hub

- Catálogo B2B integrado a backend Medusa para kits, componentes e propostas.
- Regras comerciais distintas por canal, região ou distribuidor.
- Sincronização de carrinho com itens técnicos e complementares de projeto solar.

## Erros Comuns

- Assumir método do SDK sem validação.
- Hardcode de endpoints.
- Estado local divergente do carrinho real.
