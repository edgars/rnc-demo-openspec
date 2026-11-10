# Gestão de Produtos

## Why

O sistema legado mantém Produtos na tela "Produtos" sobre a tabela `produtos` (6 campo(s)). A aplicação
moderna precisa preservar esse cadastro — listar, criar, editar e excluir — com as regras de
negócio que o legado aplica, citadas pela chave `RK-…`.

## What Changes

- Rotas `/produtos`, `/produtos/new`, `/produtos/[id]/edit` e API `/api/produtos`.
- 8 requirement(s) de negócio do legado.
- 0 lookup(s) para outras entidades.

## Capabilities

### New Capabilities

- `produtos`: cadastro de Produtos: lista, formulários, exclusão e regras de negócio

### Modified Capabilities

_none_

## Impact

- Tabela `produtos` (migração própria).
- API `/api/produtos` e páginas de lista/formulário.
- Depende da change de fundação.
