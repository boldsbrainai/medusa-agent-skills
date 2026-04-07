# Data Loading Principles and Patterns

## Conteúdo

- [Regras Fundamentais](#regras-fundamentais)
- [Checklist: Pense Antes de Codar](#checklist-pense-antes-de-codar)
- [Erro Comum vs Padrão Correto](#erro-comum-vs-padrão-correto)
- [Trabalhando com TanStack Query](#trabalhando-com-tanstack-query)
- [Buscando Dados com useQuery](#buscando-dados-com-usequery)
- [Atualizando Dados com useMutation](#atualizando-dados-com-usemutation)
- [Guia de Invalidação de Cache](#guia-de-invalidação-de-cache)
- [Notas Importantes sobre Metadata](#notas-importantes-sobre-metadata)
- [Padrões Comuns](#padrões-comuns)
- [Problemas Frequentes e Soluções](#problemas-frequentes-e-soluções)
- [Casos de Uso Yello Solar Hub](#casos-de-uso-yello-solar-hub)

## Regras Fundamentais

1. Use SEMPRE o Medusa JS SDK. Não use `fetch()` cru para APIs Medusa.
2. Dados exibidos no widget devem carregar no mount.
3. Separe query de exibição da query de modal/form.
4. Se armazenar IDs em metadata, busque entidades completas para renderizar.
5. Sempre exiba loading state antes de concluir que não há dados.
6. Invalide as queries que abastecem a UI principal após mutação.

## Checklist: Pense Antes de Codar

- [ ] Estou usando SDK da Medusa em todas as chamadas?
- [ ] Para endpoint nativo, estou usando método nativo do SDK?
- [ ] Quais dados precisam aparecer imediatamente?
- [ ] Onde esses dados estão persistidos?
- [ ] Eu preciso resolver referências (IDs -> entidades completas)?
- [ ] A query de display está separada da query de seleção?
- [ ] Tenho loading, erro e estado vazio corretos?
- [ ] Minha invalidação atualiza exatamente o que o usuário enxerga?

## Erro Comum vs Padrão Correto

### Errado: query única dependente de modal

```tsx
const { data } = useQuery({
  queryFn: () => sdk.admin.product.list(),
  enabled: modalOpen,
})

const selected = data?.products?.filter((p) => ids.includes(p.id))
```

Problema: no refresh, modal fechado, query não roda, UI aparece vazia.

### Correto: duas queries com responsabilidade distinta

```tsx
const { data: displayData } = useQuery({
  queryFn: () => fetchSelectedProducts(ids),
  queryKey: ["related-products-display", ids],
  enabled: ids.length > 0,
})

const { data: modalData } = useQuery({
  queryFn: () => sdk.admin.product.list({ limit, offset, q: search || undefined }),
  queryKey: ["products-selection", limit, offset, search],
  enabled: modalOpen,
  keepPreviousData: true,
})
```

## Trabalhando com TanStack Query

Observação para `pnpm`: instale versões exatas compatíveis com o dashboard.

```bash
pnpm list @tanstack/react-query --depth=10 | grep @medusajs/dashboard
pnpm add @tanstack/react-query@[exact-version]
```

## Buscando Dados com useQuery

### Query básica

```tsx
const { data, isLoading, isError } = useQuery({
  queryFn: () => sdk.admin.product.retrieve(productId, { fields: "+metadata,+variants.*" }),
  queryKey: ["product", productId],
})
```

### Query paginada

```tsx
const limit = pagination.pageSize
const offset = pagination.pageIndex * limit

const { data } = useQuery({
  queryFn: () => sdk.admin.product.list({ limit, offset, q: search || undefined }),
  queryKey: ["products", limit, offset, search],
  keepPreviousData: true,
})
```

### Query com dependência

```tsx
const { data } = useQuery({
  queryFn: () => sdk.admin.product.retrieve(productId),
  queryKey: ["product", productId],
  enabled: !!productId,
})
```

## Atualizando Dados com useMutation

```tsx
const updateProduct = useMutation({
  mutationFn: (payload) => sdk.admin.product.update(productId, payload),
  onSuccess: () => {
    queryClient.invalidateQueries({ queryKey: ["product", productId] })
    queryClient.invalidateQueries({ queryKey: ["related-products-display", productId] })
    toast.success("Atualizado com sucesso")
  },
  onError: (error) => toast.error(error.message || "Falha ao atualizar"),
})
```

## Guia de Invalidação de Cache

- Invalide query da entidade principal.
- Invalide query de display do widget.
- Normalmente não precisa invalidar query de seleção de modal.
- Use query keys específicas com IDs.

## Notas Importantes sobre Metadata

- Metadata aninhada deve ser enviada completa (não há merge profundo automático).
- Para remover chave de metadata, normalize com valor vazio conforme regra do projeto.

```tsx
sdk.admin.product.update(productId, {
  metadata: {
    ...product.metadata,
    related_product_ids: JSON.stringify(ids),
  },
})
```

## Padrões Comuns

### Busca com debounce

```tsx
const [search, setSearch] = useState("")
const [debouncedSearch] = useDebouncedValue(search, 300)
```

### Loading state explícito

```tsx
{isLoading ? <Spinner /> : <ProductsList data={data?.products || []} />}
```

## Problemas Frequentes e Soluções

1. `401/403` em chamadas admin: provável uso de `fetch` cru.
2. Tela vazia após refresh: query de display condicionada por estado de modal.
3. Dado não atualiza após salvar: faltou invalidar query da UI principal.
4. Metadata perdida: update sem spread da metadata existente.

## Casos de Uso Yello Solar Hub

- Widget de fabricantes relacionados ao produto solar.
- Seleção de distribuidores em massa com DataTable e paginação.
- Exibição de ofertas técnicas associadas por IDs em metadata.
- Atualização de status comercial com feedback e refresh imediato da UI.
