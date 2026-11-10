# Spec Delta

## Purpose

Cadastro de Produtos: a aplicação SHALL manter os registros de `produtos` como o sistema legado mantinha — listar, criar, editar e excluir — aplicando as regras de negócio extraídas do legado.

## ADDED Requirements

### Requirement: Listar Produtos
O sistema SHALL exibir em `/produtos` uma lista paginada de Produtos com busca e as colunas: `descricao`, `preco`, `estoque`, `unidade`, `ativo`.

#### Scenario: Abrir a lista
- **WHEN** o operador abre `/produtos`
- **THEN** vê a tabela com as colunas `descricao`, `preco`, `estoque`, `unidade`, `ativo`, paginada
- **AND** pode filtrar pela busca

### Requirement: Criar Produtos
O sistema SHALL permitir criar um registro de Produtos em `/produtos/new` com os campos, nesta ordem: `descricao`, `preco`, `estoque`, `unidade`, `ativo`, `produtoid`.

#### Scenario: Salvar um registro válido
- **WHEN** o operador preenche o formulário e salva
- **THEN** o registro é gravado em `produtos` e a lista o exibe

### Requirement: Editar Produtos
O sistema SHALL permitir editar um registro existente de Produtos em `/produtos/[id]/edit`, com o formulário pré-preenchido.

#### Scenario: Alterar um registro
- **WHEN** o operador abre um registro da lista, altera um campo e salva
- **THEN** o registro é atualizado e a lista reflete a alteração

### Requirement: Excluir Produtos
O sistema SHALL permitir excluir um registro de Produtos após confirmação explícita.

#### Scenario: Excluir com confirmação
- **GIVEN** um registro aberto para edição
- **WHEN** o operador aciona *Excluir* e confirma
- **THEN** o registro é removido de `produtos` e a lista não o exibe
- **AND** cancelar a confirmação não altera nada

### Requirement: Campos obrigatórios de Produtos
O sistema SHALL rejeitar a gravação de Produtos sem os campos obrigatórios: `descricao`.

#### Scenario: Salvar sem um campo obrigatório
- **WHEN** o operador salva com `descricao` vazio
- **THEN** o formulário mostra erro inline no campo e nada é gravado
- **AND** a API responde `400` com a mensagem do campo

### Requirement: Produto inexistente ou inativo
O sistema SHALL aplicar a regra `RK-89b58328383c`: Produto inexistente ou inativo

#### Scenario: Regra aplicada
- **GIVEN** os campos `produtos.ativo`, `pedidos`, `produtos`
- **WHEN** a condição `!FOUND() OR !produtos.ativo` se verifica
- **THEN** Produto inexistente ou inativo

### Requirement: Estoque insuficiente. Disponivel:
O sistema SHALL aplicar a regra `RK-cf3d19dd8e6d`: Estoque insuficiente. Disponivel:

#### Scenario: Regra aplicada
- **GIVEN** os campos `produtos.estoque`, `pedidos`, `produtos`
- **WHEN** a condição `nQtde > produtos.estoque` se verifica
- **THEN** Estoque insuficiente. Disponivel:

### Requirement: Atualizacao em itens: qtde = nQtde, precounit = produtos.preco, subtotal = nQtde…
O sistema SHALL aplicar a regra `RK-e5a3716dfd5f`: Atualizacao em itens: qtde = nQtde, precounit = produtos.preco, subtotal = nQtde * produtos.preco

#### Scenario: Regra aplicada
- **GIVEN** os campos `itens.qtde`, `itens.precounit`, `itens.subtotal`
- **WHEN** a condição `qtde = nQtde` se verifica
- **THEN** Atualizacao em itens: qtde = nQtde, precounit = produtos.preco, subtotal = nQtde * produtos.preco

### Requirement: Atualizacao em produtos: estoque = estoque - nQtde
O sistema SHALL aplicar a regra `RK-bfca0ddf1d4e`: Atualizacao em produtos: estoque = estoque - nQtde

#### Scenario: Regra aplicada
- **GIVEN** os campos `produtos.estoque`
- **WHEN** a condição `estoque = estoque - nQtde` se verifica
- **THEN** Atualizacao em produtos: estoque = estoque - nQtde

### Requirement: Descricao obrigatoria
O sistema SHALL aplicar a regra `RK-dc47b88f5812`: Descricao obrigatoria

#### Scenario: Regra aplicada
- **GIVEN** os campos `produtos.descricao`
- **WHEN** a condição `EMPTY(this.Value)` se verifica
- **THEN** Descricao obrigatoria

### Requirement: Preco deve ser maior que zero
O sistema SHALL aplicar a regra `RK-678c161373aa`: Preco deve ser maior que zero

#### Scenario: Regra aplicada
- **GIVEN** os campos `produtos.preco`
- **WHEN** a condição `this.Value <= 0` se verifica
- **THEN** Preco deve ser maior que zero

### Requirement: Regra de validacao em spnEstoque.Valid
O sistema SHALL aplicar a regra `RK-54d7c0aa28ec`: Regra de validacao em spnEstoque.Valid

#### Scenario: Regra aplicada
- **GIVEN** os campos `produtos.estoque`
- **WHEN** a condição `this.Value < 0` se verifica
- **THEN** Regra de validacao em spnEstoque.Valid

### Requirement: Persistencia transacional via TABLEUPDATE
O sistema SHALL aplicar a regra `RK-c685cf0351b0`: Persistencia transacional via TABLEUPDATE

#### Scenario: Regra aplicada
- **GIVEN** os campos `produtos`
- **WHEN** a condição `TABLEUPDATE(.T.)` se verifica
- **THEN** Persistencia transacional via TABLEUPDATE

