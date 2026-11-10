# Tasks

## 1. Modelo de dados

- [ ] 1.1 Migração criando `produtos` com as colunas de `design.md` (tipos e nulidade); entidade/modelo no ORM.

## 2. API

- [ ] 2.1 `GET /api/produtos` paginado com buscapor `descricao`, `preco`, `estoque`, `unidade`, `ativo`; teste de paginação.
- [ ] 2.2 `POST /api/produtos` validando o corpo (obrigatórios: `descricao`); teste rejeitando corpo inválido com `400`.
- [ ] 2.3 `GET /api/produtos/:id`, `PUT /api/produtos/:id`, `DELETE /api/produtos/:id`; testes de cada verbo.

## 3. Telas

- [ ] 3.1 Página `/produtos`: tabela com as colunas de lista (`descricao`, `preco`, `estoque`, `unidade`, `ativo`), busca e paginação, botão *Novo*.
- [ ] 3.2 Formulário `/produtos/new` com os campos na ordem de `design.md`; obrigatórios com erro inline.
- [ ] 3.3 Formulário `/produtos/[id]/edit` pré-preenchido, com salvar e excluir (confirmação).

## 4. Regras de negócio

- [ ] 4.1 Enforce `RK-89b58328383c` — Produto inexistente ou inativo; comentário `// RK-89b58328383c` no ponto do código onde a regra vale.
- [ ] 4.2 Enforce `RK-cf3d19dd8e6d` — Estoque insuficiente. Disponivel:; comentário `// RK-cf3d19dd8e6d` no ponto do código onde a regra vale.
- [ ] 4.3 Enforce `RK-e5a3716dfd5f` — Atualizacao em itens: qtde = nQtde, precounit = produtos.preco, subtotal = nQtde * produtos.preco; comentário `// RK-e5a3716dfd5f` no ponto do código onde a regra vale.
- [ ] 4.4 Enforce `RK-bfca0ddf1d4e` — Atualizacao em produtos: estoque = estoque - nQtde; comentário `// RK-bfca0ddf1d4e` no ponto do código onde a regra vale.
- [ ] 4.5 Enforce `RK-dc47b88f5812` — Descricao obrigatoria; comentário `// RK-dc47b88f5812` no ponto do código onde a regra vale.
- [ ] 4.6 Enforce `RK-678c161373aa` — Preco deve ser maior que zero; comentário `// RK-678c161373aa` no ponto do código onde a regra vale.
- [ ] 4.7 Enforce `RK-54d7c0aa28ec` — Regra de validacao em spnEstoque.Valid; comentário `// RK-54d7c0aa28ec` no ponto do código onde a regra vale.
- [ ] 4.8 Enforce `RK-c685cf0351b0` — Persistencia transacional via TABLEUPDATE; comentário `// RK-c685cf0351b0` no ponto do código onde a regra vale.

## 5. Verificação

- [ ] 5.1 Um teste por `#### Scenario:` de `specs/produtos/spec.md`, todos verdes.
- [ ] 5.2 `openspec validate 004-produtos --strict` passa; com o MCP da RNC conectado, `getRule` conferido para cada `RK-…` acima.
