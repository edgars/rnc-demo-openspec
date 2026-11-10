# Gestão de Clientes

## Why

O sistema legado mantém Clientes na tela "Clientes" sobre a tabela `clientes` (8 campo(s)). A aplicação
moderna precisa preservar esse cadastro — listar, criar, editar e excluir — com as regras de
negócio que o legado aplica, citadas pela chave `RK-…`.

## What Changes

- Rotas `/clientes`, `/clientes/new`, `/clientes/[id]/edit` e API `/api/clientes`.
- 11 requirement(s) de negócio do legado.
- 0 lookup(s) para outras entidades.

## Capabilities

### New Capabilities

- `clientes`: cadastro de Clientes: lista, formulários, exclusão e regras de negócio

### Modified Capabilities

_none_

## Impact

- Tabela `clientes` (migração própria).
- API `/api/clientes` e páginas de lista/formulário.
- Depende da change de fundação.

## Fora de escopo — comportamentos legados a confirmar

Rotinas do legado ligadas a esta entidade (impressões, conexões, diálogos). Não são
requirements: confirme com o produto antes de portar.

- `RK-a5e15f15e584` Geracao de valor: clienteid = ProximoId("clientes")
