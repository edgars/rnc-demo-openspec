# Spec Delta

## Purpose

Cadastro de Itens: a aplicação SHALL manter os registros de `itens` como o sistema legado mantinha — listar, criar, editar e excluir — aplicando as regras de negócio extraídas do legado.

## ADDED Requirements

### Requirement: Listar Itens
O sistema SHALL exibir em `/itens` uma lista paginada de Itens com busca e as colunas: `clienteid`, `produtoid`, `data`, `qtde`, `precounit`.

#### Scenario: Abrir a lista
- **WHEN** o operador abre `/itens`
- **THEN** vê a tabela com as colunas `clienteid`, `produtoid`, `data`, `qtde`, `precounit`, paginada
- **AND** pode filtrar pela busca

### Requirement: Criar Itens
O sistema SHALL permitir criar um registro de Itens em `/itens/new` com os campos, nesta ordem: `clienteid`, `produtoid`, `data`, `qtde`, `precounit`, `subtotal`, `status`.

#### Scenario: Salvar um registro válido
- **WHEN** o operador preenche o formulário e salva
- **THEN** o registro é gravado em `itens` e a lista o exibe

### Requirement: Editar Itens
O sistema SHALL permitir editar um registro existente de Itens em `/itens/[id]/edit`, com o formulário pré-preenchido.

#### Scenario: Alterar um registro
- **WHEN** o operador abre um registro da lista, altera um campo e salva
- **THEN** o registro é atualizado e a lista reflete a alteração

### Requirement: Excluir Itens
O sistema SHALL permitir excluir um registro de Itens após confirmação explícita.

#### Scenario: Excluir com confirmação
- **GIVEN** um registro aberto para edição
- **WHEN** o operador aciona *Excluir* e confirma
- **THEN** o registro é removido de `itens` e a lista não o exibe
- **AND** cancelar a confirmação não altera nada

### Requirement: Campo calculado: itens.subtotal = itens.qtde * itens.precounit
O sistema SHALL aplicar a regra `RK-97d3c0193d59`: Campo calculado: itens.subtotal = itens.qtde * itens.precounit

#### Scenario: Regra aplicada
- **GIVEN** os campos `itens.subtotal`
- **WHEN** a condição `itens.subtotal = itens.qtde * itens.precounit` se verifica
- **THEN** Campo calculado: itens.subtotal = itens.qtde * itens.precounit

### Requirement: Atualizacao em itens: qtde = nQtde, precounit = produtos.preco, subtotal = nQtde…
O sistema SHALL aplicar a regra `RK-e5a3716dfd5f`: Atualizacao em itens: qtde = nQtde, precounit = produtos.preco, subtotal = nQtde * produtos.preco

#### Scenario: Regra aplicada
- **GIVEN** os campos `itens.qtde`, `itens.precounit`, `itens.subtotal`
- **WHEN** a condição `qtde = nQtde` se verifica
- **THEN** Atualizacao em itens: qtde = nQtde, precounit = produtos.preco, subtotal = nQtde * produtos.preco

### Requirement: Pedido sem itens nao pode ser fechado
O sistema SHALL aplicar a regra `RK-1a7c75fecf85`: Pedido sem itens nao pode ser fechado

#### Scenario: Regra aplicada
- **GIVEN** os campos `pedidos`, `itens`
- **WHEN** a condição `aIt = 0` se verifica
- **THEN** Pedido sem itens nao pode ser fechado

