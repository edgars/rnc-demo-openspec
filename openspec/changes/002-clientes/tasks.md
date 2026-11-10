# Tasks

## 1. Modelo de dados

- [ ] 1.1 Migração criando `clientes` com as colunas de `design.md` (tipos e nulidade); entidade/modelo no ORM.

## 2. API

- [ ] 2.1 `GET /api/clientes` paginado com buscapor `nome`, `cpfcnpj`, `email`, `telefone`, `limite`; teste de paginação.
- [ ] 2.2 `POST /api/clientes` validando o corpo (obrigatórios: `nome`); teste rejeitando corpo inválido com `400`.
- [ ] 2.3 `GET /api/clientes/:id`, `PUT /api/clientes/:id`, `DELETE /api/clientes/:id`; testes de cada verbo.

## 3. Telas

- [ ] 3.1 Página `/clientes`: tabela com as colunas de lista (`nome`, `cpfcnpj`, `email`, `telefone`, `limite`), busca e paginação, botão *Novo*.
- [ ] 3.2 Formulário `/clientes/new` com os campos na ordem de `design.md`; obrigatórios com erro inline.
- [ ] 3.3 Formulário `/clientes/[id]/edit` pré-preenchido, com salvar e excluir (confirmação).
- [ ] 3.4 Máscaras em `/clientes`: `cpfcnpj` `###.###.###-##`, `telefone` `(##) ####-####`; testar um valor fora de cada máscara.

## 4. Regras de negócio

- [ ] 4.1 Enforce `RK-734dab5f870e` — Nome e obrigatorio; comentário `// RK-734dab5f870e` no ponto do código onde a regra vale.
- [ ] 4.2 Enforce `RK-08f0a245805c` — CPF/CNPJ ja cadastrado; comentário `// RK-08f0a245805c` no ponto do código onde a regra vale.
- [ ] 4.3 Enforce `RK-f4720b305355` — Email invalido; comentário `// RK-f4720b305355` no ponto do código onde a regra vale.
- [ ] 4.4 Enforce `RK-327c2b860142` — Limite nao pode ser negativo; comentário `// RK-327c2b860142` no ponto do código onde a regra vale.
- [ ] 4.5 Enforce `RK-8919c708d165` — Preencha o nome antes de salvar; comentário `// RK-8919c708d165` no ponto do código onde a regra vale.
- [ ] 4.6 Enforce `RK-c45f79719b8d` — Persistencia transacional via TABLEUPDATE; comentário `// RK-c45f79719b8d` no ponto do código onde a regra vale.
- [ ] 4.7 Enforce `RK-d90174e54a35` — Cliente possui pedidos e nao pode ser excluido; comentário `// RK-d90174e54a35` no ponto do código onde a regra vale.
- [ ] 4.8 Enforce `RK-e3f1424d5010` — Confirma exclusao?; comentário `// RK-e3f1424d5010` no ponto do código onde a regra vale.
- [ ] 4.9 Enforce `RK-80fd7c0ac69e` — Persistencia transacional via TABLEUPDATE; comentário `// RK-80fd7c0ac69e` no ponto do código onde a regra vale.
- [ ] 4.10 Enforce `RK-2a0c862a6b7a` — Cliente inexistente ou inativo; comentário `// RK-2a0c862a6b7a` no ponto do código onde a regra vale.
- [ ] 4.11 Enforce `RK-d4fb739728ef` — Total excede o limite de credito do cliente; comentário `// RK-d4fb739728ef` no ponto do código onde a regra vale.

## 5. Verificação

- [ ] 5.1 Um teste por `#### Scenario:` de `specs/clientes/spec.md`, todos verdes.
- [ ] 5.2 `openspec validate 002-clientes --strict` passa; com o MCP da RNC conectado, `getRule` conferido para cada `RK-…` acima.
