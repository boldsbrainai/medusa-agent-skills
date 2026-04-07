# Displaying Entities - Patterns and Components

## Conteúdo

- [Quando Usar Cada Padrão](#quando-usar-cada-padrão)
- [Padrão com DataTable](#padrão-com-datatable)
- [Padrões de Lista Simples](#padrões-de-lista-simples)
- [Elementos de Design](#elementos-de-design)
- [Estado Vazio](#estado-vazio)
- [Estado de Loading](#estado-de-loading)
- [Renderização Condicional por Quantidade](#renderização-condicional-por-quantidade)
- [Padrões de Classe](#padrões-de-classe)
- [Casos de Uso Yello Solar Hub](#casos-de-uso-yello-solar-hub)

## Quando Usar Cada Padrão

Use DataTable quando:

- houver volume maior de itens;
- usuário precisar de busca, filtro ou paginação;
- existir seleção múltipla e ações em lote.

Use lista simples quando:

- houver poucos itens;
- contexto for widget lateral ou resumo;
- o foco for leitura rápida.

## Padrão com DataTable

```tsx
const table = useDataTable({
  data: data?.products || [],
  columns,
  getRowId: (row) => row.id,
  rowCount: data?.count || 0,
  isLoading,
  search: { state: search, onSearchChange: setSearch },
  pagination: { state: pagination, onPaginationChange: setPagination },
})
```

```tsx
<DataTable instance={table}>
  <DataTable.Toolbar>
    <DataTable.Search placeholder="Buscar produtos..." />
  </DataTable.Toolbar>
  <DataTable.Table />
  <DataTable.Pagination />
</DataTable>
```

### Troubleshooting rápido

- `DataTable.Search not enabled`: faltou bloco `search` no `useDataTable`.
- erro em paginação: inicializar `pageIndex` e `pageSize`.

## Padrões de Lista Simples

### Item com thumbnail

```tsx
<div className="shadow-elevation-card-rest bg-ui-bg-component rounded-md px-4 py-2">
  <div className="flex items-center gap-3">
    <Thumbnail src={item.thumbnail} />
    <div className="flex flex-1 flex-col">
      <Text size="small" leading="compact" weight="plus">{item.title}</Text>
      <Text size="small" leading="compact" className="text-ui-fg-subtle">{item.subtitle}</Text>
    </div>
  </div>
</div>
```

### Lista textual compacta

```tsx
<div className="flex flex-col gap-y-2">
  {items.map((item) => (
    <div key={item.id} className="flex items-center justify-between">
      <Text size="small" leading="compact" weight="plus">{item.title}</Text>
      <Text size="small" leading="compact" className="text-ui-fg-subtle">{item.meta}</Text>
    </div>
  ))}
</div>
```

## Elementos de Design

- títulos com `weight="plus"`;
- descrição com `text-ui-fg-subtle`;
- espaçamentos consistentes (`gap-2`, `gap-3`);
- cards com `shadow-elevation-card-rest`;
- hover e foco acessíveis para itens clicáveis.

## Estado Vazio

```tsx
{items.length === 0 ? (
  <Text size="small" leading="compact" className="text-ui-fg-subtle">Nenhum item para exibir</Text>
) : (
  <ItemsList items={items} />
)}
```

## Estado de Loading

```tsx
{isLoading ? (
  <div className="flex items-center justify-center p-8"><Spinner /></div>
) : (
  <ItemsList items={items} />
)}
```

## Renderização Condicional por Quantidade

```tsx
if (items.length > 10) return <ItemsTable items={items} />
if (items.length > 0) return <SimpleList items={items} />
return <EmptyState />
```

## Padrões de Classe

- seção: `px-6 py-4`
- lista vertical: `flex flex-col gap-2`
- item: `rounded-md transition-colors`
- ação inline: `flex items-center gap-2`

## Casos de Uso Yello Solar Hub

- Tabela de distribuidores homologados com busca por UF e status.
- Lista compacta de fabricantes vinculados em widget de produto.
- Grid de kits solares selecionáveis por categoria técnica.
- Renderização condicional entre DataTable e lista em dashboards operacionais.
