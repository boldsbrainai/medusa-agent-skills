# Forms and Modal Patterns

## Conteúdo

- [FocusModal vs Drawer](#focusmodal-vs-drawer)
- [Padrões de Botão Editar](#padrões-de-botão-editar)
- [Select para Datasets Pequenos](#select-para-datasets-pequenos)
- [Exemplo com FocusModal](#exemplo-com-focusmodal)
- [Exemplo com Drawer](#exemplo-com-drawer)
- [Formulário com Validação e Loading](#formulário-com-validação-e-loading)
- [Padrões-Chave](#padrões-chave)
- [Casos de Uso Yello Solar Hub](#casos-de-uso-yello-solar-hub)

## FocusModal vs Drawer

**FocusModal**: criação de novas entidades, fluxos mais longos e contexto focado.

**Drawer**: edição rápida de entidade existente sem tirar o usuário da tela.

Regra prática: criar -> FocusModal, editar -> Drawer.

## Padrões de Botão Editar

### Botão simples no cabeçalho

```tsx
<div className="flex items-center justify-between px-6 py-4">
  <Heading level="h2">Configurações</Heading>
  <Button size="small" variant="secondary" onClick={() => setOpen(true)}>
    <PencilSquare />
  </Button>
</div>
```

### Menu de ações

Use dropdown quando houver múltiplas ações: editar, criar, remover.

## Select para Datasets Pequenos

Use `Select` para 2-10 opções (status, tipo, flag).

Para datasets grandes, use DataTable + FocusModal (ver `table-selection.pt-BR.md`).

## Exemplo com FocusModal

```tsx
<FocusModal open={open} onOpenChange={setOpen}>
  <FocusModal.Content>
    <FocusModal.Header>
      <Button size="small" variant="secondary">Cancelar</Button>
      <Button size="small" onClick={handleSubmit}>Salvar</Button>
    </FocusModal.Header>
    <FocusModal.Body>
      <Input value={name} onChange={(e) => setName(e.target.value)} />
    </FocusModal.Body>
  </FocusModal.Content>
</FocusModal>
```

## Exemplo com Drawer

```tsx
<Drawer open={open} onOpenChange={setOpen}>
  <Drawer.Content>
    <Drawer.Header>
      <Drawer.Title>Editar</Drawer.Title>
    </Drawer.Header>
    <Drawer.Body>
      <Input value={name} onChange={(e) => setName(e.target.value)} />
    </Drawer.Body>
    <Drawer.Footer>
      <Button size="small" variant="secondary">Cancelar</Button>
      <Button size="small" onClick={handleSubmit}>Salvar</Button>
    </Drawer.Footer>
  </Drawer.Content>
</Drawer>
```

## Formulário com Validação e Loading

```tsx
const mutation = useMutation({
  mutationFn: (payload) => sdk.admin.product.update(id, payload),
  onSuccess: () => {
    queryClient.invalidateQueries({ queryKey: ["product", id] })
    toast.success("Salvo com sucesso")
  },
  onError: (e) => toast.error(e.message || "Falha ao salvar"),
})

<Button size="small" isLoading={mutation.isPending} onClick={onSubmit}>Salvar</Button>
```

## Padrões-Chave

- desabilite ações durante mutação;
- mostre loading no botão principal;
- valide antes de mutar;
- limpe erros por campo ao digitar;
- resete formulário após sucesso.

## Casos de Uso Yello Solar Hub

- cadastro de fabricante com validação de status e aliases;
- edição de distribuidor com Drawer;
- formulário de aprovação comercial com feedback imediato;
- criação de regra de oferta para kits solares com FocusModal.
