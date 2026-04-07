# Navigation and Routing

## Conteúdo

- [Pré-requisitos para pnpm](#pré-requisitos-para-pnpm)
- [Navegação Básica com Link](#navegação-básica-com-link)
- [Navegação Programática](#navegação-programática)
- [Parâmetros de Rota](#parâmetros-de-rota)
- [Links para Páginas Nativas do Admin](#links-para-páginas-nativas-do-admin)
- [Navegação a partir de Widgets](#navegação-a-partir-de-widgets)
- [Padrões Comuns](#padrões-comuns)
- [Casos de Uso Yello Solar Hub](#casos-de-uso-yello-solar-hub)

## Pré-requisitos para pnpm

```bash
pnpm list react-router-dom --depth=10 | grep @medusajs/dashboard
pnpm add react-router-dom@[exact-version]
```

## Navegação Básica com Link

```tsx
<Link to="/custom/distributors" className="rounded-md outline-none">
  <Text size="small" leading="compact" weight="plus">Ver distribuidores</Text>
</Link>
```

### Link dinâmico

```tsx
<Link to={`/products/${product.id}`}>{product.title}</Link>
```

### Link com aparência de botão

```tsx
<Button asChild size="small" variant="secondary">
  <Link to="/custom/manufacturers">Abrir painel</Link>
</Button>
```

## Navegação Programática

```tsx
const navigate = useNavigate()

const createMutation = useMutation({
  mutationFn: (data) => sdk.admin.product.create(data),
  onSuccess: (result) => navigate(`/products/${result.product.id}`),
})
```

## Parâmetros de Rota

```tsx
const { id } = useParams()
const [searchParams, setSearchParams] = useSearchParams()
const status = searchParams.get("status")
```

## Links para Páginas Nativas do Admin

- `/products`
- `/orders`
- `/customers`
- `/categories`
- `/settings`

## Navegação a partir de Widgets

Padrão útil: botão `View All` em widget apontando para UI Route customizada.

```tsx
<Button asChild size="small" variant="transparent">
  <Link to={`/custom/products/${product.id}/related`}>View All</Link>
</Button>
```

## Padrões Comuns

- voltar para lista após salvar;
- breadcrumbs em páginas de detalhe;
- manter query params para filtros persistirem.

## Casos de Uso Yello Solar Hub

- widget de produto navegando para rota customizada de fabricante;
- tela de pedidos com link para fluxo de cotação B2B;
- atalhos de navegação para distribuidores e aprovações comerciais.
