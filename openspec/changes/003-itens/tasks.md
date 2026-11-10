# Tasks

## 1. Modelo de dados

- [ ] 1.1 Migração criando `itens` com as colunas de `design.md` (tipos e nulidade); entidade/modelo no ORM.

## 2. API

- [ ] 2.1 `GET /api/itens` paginado com buscapor `clienteid`, `produtoid`, `data`, `qtde`, `precounit`; teste de paginação.
- [ ] 2.2 `POST /api/itens` validando o corpo (obrigatórios: nenhum); teste rejeitando corpo inválido com `400`.
- [ ] 2.3 `GET /api/itens/:id`, `PUT /api/itens/:id`, `DELETE /api/itens/:id`; testes de cada verbo.

## 3. Telas

- [ ] 3.1 Página `/itens`: tabela com as colunas de lista (`clienteid`, `produtoid`, `data`, `qtde`, `precounit`), busca e paginação, botão *Novo*.
- [ ] 3.2 Formulário `/itens/new` com os campos na ordem de `design.md`; obrigatórios com erro inline.
- [ ] 3.3 Formulário `/itens/[id]/edit` pré-preenchido, com salvar e excluir (confirmação).

## 4. Regras de negócio

- [ ] 4.1 Enforce `RK-97d3c0193d59` — Campo calculado: itens.subtotal = itens.qtde * itens.precounit; comentário `// RK-97d3c0193d59` no ponto do código onde a regra vale.
- [ ] 4.2 Enforce `RK-e5a3716dfd5f` — Atualizacao em itens: qtde = nQtde, precounit = produtos.preco, subtotal = nQtde * produtos.preco; comentário `// RK-e5a3716dfd5f` no ponto do código onde a regra vale.
- [ ] 4.3 Enforce `RK-1a7c75fecf85` — Pedido sem itens nao pode ser fechado; comentário `// RK-1a7c75fecf85` no ponto do código onde a regra vale.

## 5. Verificação

- [ ] 5.1 Um teste por `#### Scenario:` de `specs/itens/spec.md`, todos verdes.
- [ ] 5.2 `openspec validate 003-itens --strict` passa; com o MCP da RNC conectado, `getRule` conferido para cada `RK-…` acima.
