# Design Guidelines

## Visão Geral

Este guia existe para preservar consistência visual e semântica ao criar componentes de storefront. O princípio central é simples: descubra os tokens e padrões já existentes antes de introduzir novas cores, fontes ou comportamentos.

## Descoberta da Identidade Existente

Antes de implementar qualquer componente:

- verifique o `tailwind.config` ou configuração equivalente;
- localize variáveis CSS de cor e tipografia;
- inspecione componentes já existentes para entender espaçamento, sombras, raios e estados interativos;
- confirme a versão do Tailwind antes de aplicar utilitários novos.

## Regras Críticas de Consistência

- Nunca introduza cores arbitrárias sem necessidade real.
- Nunca introduza novas fontes sem aprovação explícita.
- Use tokens semânticos em vez de hex codes soltos.
- Replique padrões já consolidados para botões, cards e formulários.
- Não use emojis em UI de storefront.

## Quando Pedir Aprovação ao Usuário

Peça aprovação antes de:

- adicionar nova cor ao sistema;
- introduzir nova família tipográfica;
- alterar uma definição central já existente;
- criar um novo padrão visual que ainda não existe no projeto.

## Setup de Novo Projeto

Se não houver identidade existente, defina:

- paleta primária e secundária;
- tipografia principal e de apoio;
- estilo desejado: minimalista, institucional, moderno, técnico, premium;
- referências visuais ou websites de comparação.

## Casos de Uso Yello Solar Hub

- Visual técnico, confiável e B2B para catálogos de energia solar.
- Ênfase em clareza de preço, disponibilidade e prova comercial.
- Componentes que comuniquem engenharia, financiamento e distribuição sem parecer marketplace genérico.

## Erros Comuns

- Misturar estilos entre páginas.
- Inserir cores de campanha fora do sistema visual.
- Criar UI chamativa demais para contexto técnico B2B.
