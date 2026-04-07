---
name: building-admin-dashboard-customizations
description: Carregue automaticamente ao planejar, pesquisar ou implementar UI do Admin Medusa (widgets, páginas customizadas, formulários, tabelas, carregamento de dados e navegação). OBRIGATÓRIO para todo trabalho de Admin UI em todos os modos.
---

# Customizações do Admin Dashboard Medusa

Construa extensões de UI para o Admin do Medusa com Admin SDK, Medusa UI, SDK JS e padrões de carregamento robustos.

Observação: UI Routes são páginas customizadas do admin e não substituem rotas backend.

## Quando Aplicar

Carregue esta skill para:

- widgets em páginas de produto, pedido e cliente;
- páginas customizadas do admin;
- formulários, modais, drawers e validação;
- exibição de dados em listas e tabelas;
- navegação e roteamento interno no dashboard.

Também combine com:

- `building-with-medusa` para backend das APIs chamadas pelo admin;
- `building-storefronts` quando o trabalho for storefront.

## CRÍTICO: Carregar Referências Certas

A referência rápida não basta para implementação. Antes de codar, carregue arquivos de referência apropriados:

- Widget com leitura e atualização: `references/data-loading.md`
- Formulários e modais: `references/forms.md`
- Listas e tabelas: `references/display-patterns.md`
- Seleção em datasets grandes: `references/table-selection.md`
- Links e rotas: `references/navigation.md`
- Tipografia e hierarquia visual: `references/typography.md`

Mínimo: 1-2 referências relevantes por tarefa.

## Skill vs MedusaDocs MCP

Use esta skill como fonte primária para:

- estruturação de feature de Admin UI;
- padrões de implementação e anti-padrões;
- regras de loading, invalidação, tipografia e UX operacional.

Use MedusaDocs como fonte secundária para:

- assinaturas específicas de componentes;
- detalhes de métodos do SDK;
- opções de configuração e referência oficial.

## Regras Críticas de Setup

### Configuração do SDK

```tsx
import Medusa from "@medusajs/js-sdk"

export const sdk = new Medusa({
  baseUrl: import.meta.env.VITE_BACKEND_URL || "/",
  debug: import.meta.env.DEV,
  auth: { type: "session" },
})
```

### Usuários pnpm

Instale dependências pares antes de codar:

```bash
pnpm list @tanstack/react-query --depth=10 | grep @medusajs/dashboard
pnpm add @tanstack/react-query@[exact-version]

pnpm list react-router-dom --depth=10 | grep @medusajs/dashboard
pnpm add react-router-dom@[exact-version]
```

`npm` e `yarn`: normalmente já vem via dashboard.

## Categorias de Regra (Prioridade)

1. Data Loading (CRÍTICO)
2. Design System (CRÍTICO)
3. Data Display (ALTO)
4. Typography (ALTO)
5. Forms & Modals (MÉDIO)
6. Selection Patterns (MÉDIO)

## Referência Rápida

### Data Loading

- use sempre SDK da Medusa;
- query de display no mount;
- query de modal separada;
- invalidação da query certa após mutação;
- loading state explícito.

### Design System

- classes semânticas, sem hardcode;
- espaçamento consistente (`px-6 py-4`, `gap-2`, `gap-3`);
- botões de widget em `size="small"`;
- usar componentes Medusa UI, não HTML cru.

### Data Display

- preço Medusa no YSH é valor final; não dividir por 100.

### Typography

- usar `Text` para labels e descrição;
- evitar Heading em microseções.

### Forms & Modals

- criação: FocusModal;
- edição: Drawer;
- botão desabilitado e loading durante mutação.

### Selection

- 2-10 opções: Select;
- dataset grande: DataTable + FocusModal;
- configure `search` no `useDataTable`.

## Padrão Crítico de Data Loading

Nunca carregue dados de display condicionalmente por estado de modal. Use duas queries:

- Query A: display data (mount)
- Query B: seleção modal (on demand)

Depois da mutação, invalide query da entidade e query de display.

## Checklist de Erros Comuns

- usar `fetch` cru;
- query única para display + modal;
- não invalidar query de display;
- hardcode de cor e spacing;
- tipografia inconsistente;
- seleção sem search configurado;
- preço tratado como centavos.

## Integração com Backend

No admin:

- endpoint nativo: método nativo do SDK;
- endpoint custom: `sdk.client.fetch()`;
- nunca `fetch` cru para rotas Medusa.

## Widget vs UI Route

Widget:

- estende página existente;
- bom para contexto local.

UI Route:

- página completa customizada;
- bom para gestão e operações maiores.

## Problemas Frequentes

- `Cannot find module` com pnpm: instalar versões exatas.
- `No QueryClient set`: dependência de React Query ausente/incompatível.
- `DataTable.Search not enabled`: faltou config de search.
- widget não atualiza: invalidação incompleta.
- tela vazia após refresh: query de display condicionada por modal.

## Casos de Uso Yello Solar Hub

- widget de fabricante no detalhe do produto solar;
- tela de distribuidores com busca, paginação e seleção em lote;
- fluxo de aprovação comercial com modais e feedback;
- gestão de cotações B2B com UI route dedicada.

## Próximos Passos de Teste

1. subir ambiente local;
2. abrir admin em `http://localhost:9000/app`;
3. validar widget ou UI route no caminho configurado;
4. testar loading, erro, busca, paginação e mutações;
5. conferir atualização visual após invalidação de cache.
