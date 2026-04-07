# Table Selection Pattern

## Conteúdo

- [Pré-requisitos para pnpm](#pré-requisitos-para-pnpm)
- [Exemplo Completo de Widget com Seleção](#exemplo-completo-de-widget-com-seleção)
- [Detalhes-Chave de Implementação](#detalhes-chave-de-implementação)
- [Variações do Padrão](#variações-do-padrão)
- [Notas Importantes](#notas-importantes)
- [Casos de Uso Yello Solar Hub](#casos-de-uso-yello-solar-hub)

## Pré-requisitos para pnpm

```bash
pnpm list @tanstack/react-query --depth=10 | grep @medusajs/dashboard
pnpm add @tanstack/react-query@[exact-version]

pnpm list react-router-dom --depth=10 | grep @medusajs/dashboard
pnpm add react-router-dom@[exact-version]
```

## Exemplo Completo de Widget com Seleção

Use `FocusModal + DataTable` para selecionar itens de datasets grandes com busca e paginação.

```tsx
const [open, setOpen] = useState(false)
const [rowSelection, setRowSelection] = useState<DataTableRowSelectionState>({})
const [searchValue, setSearchValue] = useState("")
const [pagination, setPagination] = useState<DataTablePaginationState>({ pageIndex: 0, pageSize: 10 })

const { data: displayProducts } = useQuery({
  queryFn: () => sdk.admin.product.list({ id: selectedIds, limit: selectedIds.length }),
  queryKey: ["related-products-display", selectedIds],
  enabled: selectedIds.length > 0,
})

const { data: modalProducts, isLoading } = useQuery({
  queryFn: () => sdk.admin.product.list({
    limit: pagination.pageSize,
    offset: pagination.pageIndex * pagination.pageSize,
    q: searchValue || undefined,
  }),
  queryKey: ["products-selection", pagination.pageIndex, pagination.pageSize, searchValue],
  enabled: open,
  keepPreviousData: true,
})
```

```tsx
const table = useDataTable({
  data: modalProducts?.products || [],
  columns,
  getRowId: (row) => row.id,
  rowCount: modalProducts?.count || 0,
  isLoading,
  rowSelection: { state: rowSelection, onRowSelectionChange: setRowSelection },
  search: { state: searchValue, onSearchChange: setSearchValue },
  pagination: { state: pagination, onPaginationChange: setPagination },
})
```

## Detalhes-Chave de Implementação

1. Separar query de display e query de modal.
2. Inicializar seleção com IDs persistidos (metadata ou vínculo equivalente).
3. Invalidar query da entidade e query de display após mutação.
4. Não depender de query de modal para renderizar UI principal.
5. Garantir `search` e `pagination` configurados no `useDataTable`.

## Variações do Padrão

- Seleção de categorias.
- Seleção de regiões.
- Seleção de entidades vindas de endpoint customizado com `sdk.client.fetch()`.

## Notas Importantes

- `keepPreviousData: true` evita flicker na paginação.
- Updates de metadata podem sobrescrever objeto inteiro se não houver spread.
- Mantenha query keys estáveis e específicas.

## Casos de Uso Yello Solar Hub

- Selecionar produtos relacionados por fabricante.
- Relacionar distribuidores a linhas de oferta.
- Seleção em massa para operações comerciais de kits solares.
- Escolha de entidades para aprovação e roteamento B2B.
