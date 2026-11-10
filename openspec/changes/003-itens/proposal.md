# Gestão de Itens

## Why

O sistema legado mantém Itens na tela "Itens" sobre a tabela `itens` (7 campo(s)). A aplicação
moderna precisa preservar esse cadastro — listar, criar, editar e excluir — com as regras de
negócio que o legado aplica, citadas pela chave `RK-…`.

## What Changes

- Rotas `/itens`, `/itens/new`, `/itens/[id]/edit` e API `/api/itens`.
- 3 requirement(s) de negócio do legado.
- 0 lookup(s) para outras entidades.

## Capabilities

### New Capabilities

- `itens`: cadastro de Itens: lista, formulários, exclusão e regras de negócio

### Modified Capabilities

_none_

## Impact

- Tabela `itens` (migração própria).
- API `/api/itens` e páginas de lista/formulário.
- Depende da change de fundação.
