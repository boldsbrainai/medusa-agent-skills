# Data Loading Principles and Patterns

## Regras Fundamentais

- queries de display carregam no mount;
- queries de modal carregam sob demanda;
- mutações invalidam queries de display;
- loading state não é empty state.

## React Query

Use `useQuery` para leitura e `useMutation` para mutação. Estruture query keys com previsibilidade.

## Casos de Uso Yello Solar Hub

- lista de fabricantes no produto;
- tabela de distribuidores;
- visão administrativa de cotações.
