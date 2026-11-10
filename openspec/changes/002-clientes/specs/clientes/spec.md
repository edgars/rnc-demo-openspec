# Spec Delta

## Purpose

Cadastro de Clientes: a aplicação SHALL manter os registros de `clientes` como o sistema legado mantinha — listar, criar, editar e excluir — aplicando as regras de negócio extraídas do legado.

## ADDED Requirements

### Requirement: Listar Clientes
O sistema SHALL exibir em `/clientes` uma lista paginada de Clientes com busca e as colunas: `nome`, `cpfcnpj`, `email`, `telefone`, `limite`.

#### Scenario: Abrir a lista
- **WHEN** o operador abre `/clientes`
- **THEN** vê a tabela com as colunas `nome`, `cpfcnpj`, `email`, `telefone`, `limite`, paginada
- **AND** pode filtrar pela busca

### Requirement: Criar Clientes
O sistema SHALL permitir criar um registro de Clientes em `/clientes/new` com os campos, nesta ordem: `nome`, `cpfcnpj`, `email`, `telefone`, `limite`, `ativo`, `clienteid`, `obs`.

#### Scenario: Salvar um registro válido
- **WHEN** o operador preenche o formulário e salva
- **THEN** o registro é gravado em `clientes` e a lista o exibe

### Requirement: Editar Clientes
O sistema SHALL permitir editar um registro existente de Clientes em `/clientes/[id]/edit`, com o formulário pré-preenchido.

#### Scenario: Alterar um registro
- **WHEN** o operador abre um registro da lista, altera um campo e salva
- **THEN** o registro é atualizado e a lista reflete a alteração

### Requirement: Excluir Clientes
O sistema SHALL permitir excluir um registro de Clientes após confirmação explícita.

#### Scenario: Excluir com confirmação
- **GIVEN** um registro aberto para edição
- **WHEN** o operador aciona *Excluir* e confirma
- **THEN** o registro é removido de `clientes` e a lista não o exibe
- **AND** cancelar a confirmação não altera nada

### Requirement: Campos obrigatórios de Clientes
O sistema SHALL rejeitar a gravação de Clientes sem os campos obrigatórios: `nome`.

#### Scenario: Salvar sem um campo obrigatório
- **WHEN** o operador salva com `nome` vazio
- **THEN** o formulário mostra erro inline no campo e nada é gravado
- **AND** a API responde `400` com a mensagem do campo

### Requirement: Entrada formatada em Clientes
O formulário de Clientes SHALL aplicar as máscaras e os serviços de endereço da fundação (`locale-and-formats`) aos seus campos: `cpfcnpj` `###.###.###-##`, `telefone` `(##) ####-####`.

#### Scenario: `cpfcnpj` é digitado
- **WHEN** o usuário digita em `cpfcnpj`
- **THEN** o valor é formatado como `###.###.###-##`

#### Scenario: `telefone` é digitado
- **WHEN** o usuário digita em `telefone`
- **THEN** o valor é formatado como `(##) ####-####`

### Requirement: Nome e obrigatorio
O sistema SHALL aplicar a regra `RK-734dab5f870e`: Nome e obrigatorio

#### Scenario: Regra aplicada
- **GIVEN** os campos `clientes.nome`
- **WHEN** a condição `EMPTY(this.Value)` se verifica
- **THEN** Nome e obrigatorio

### Requirement: CPF/CNPJ ja cadastrado
O sistema SHALL aplicar a regra `RK-08f0a245805c`: CPF/CNPJ ja cadastrado

#### Scenario: Regra aplicada
- **GIVEN** os campos `clientes.cpfcnpj`, `clientes`
- **WHEN** a condição `aDup > 0` se verifica
- **THEN** CPF/CNPJ ja cadastrado

### Requirement: Email invalido
O sistema SHALL aplicar a regra `RK-f4720b305355`: Email invalido

#### Scenario: Regra aplicada
- **GIVEN** os campos `clientes.email`
- **WHEN** a condição `!EMPTY(this.Value) AND !("@" $ this.Value)` se verifica
- **THEN** Email invalido

### Requirement: Limite nao pode ser negativo
O sistema SHALL aplicar a regra `RK-327c2b860142`: Limite nao pode ser negativo

#### Scenario: Regra aplicada
- **GIVEN** os campos `clientes.limite`
- **WHEN** a condição `this.Value < 0` se verifica
- **THEN** Limite nao pode ser negativo

### Requirement: Preencha o nome antes de salvar
O sistema SHALL aplicar a regra `RK-8919c708d165`: Preencha o nome antes de salvar

#### Scenario: Regra aplicada
- **GIVEN** os campos `clientes.nome`
- **WHEN** a condição `EMPTY(clientes.nome)` se verifica
- **THEN** Preencha o nome antes de salvar

### Requirement: Persistencia transacional via TABLEUPDATE
O sistema SHALL aplicar a regra `RK-c45f79719b8d`: Persistencia transacional via TABLEUPDATE

#### Scenario: Regra aplicada
- **GIVEN** os campos `clientes`
- **WHEN** a condição `TABLEUPDATE(.T.)` se verifica
- **THEN** Persistencia transacional via TABLEUPDATE

### Requirement: Cliente possui pedidos e nao pode ser excluido
O sistema SHALL aplicar a regra `RK-d90174e54a35`: Cliente possui pedidos e nao pode ser excluido

#### Scenario: Regra aplicada
- **GIVEN** os campos `clientes`, `pedidos`
- **WHEN** a condição `aPed > 0` se verifica
- **THEN** Cliente possui pedidos e nao pode ser excluido

### Requirement: Confirma exclusao?
O sistema SHALL aplicar a regra `RK-e3f1424d5010`: Confirma exclusao?

#### Scenario: Regra aplicada
- **GIVEN** os campos `clientes`
- **WHEN** a condição `MESSAGEBOX("Confirma exclusao?",4+32,"Confirmacao") = 6` se verifica
- **THEN** Confirma exclusao?

### Requirement: Persistencia transacional via TABLEUPDATE (2)
O sistema SHALL aplicar a regra `RK-80fd7c0ac69e`: Persistencia transacional via TABLEUPDATE

#### Scenario: Regra aplicada
- **GIVEN** os campos `clientes`
- **WHEN** a condição `TABLEUPDATE(.T.)` se verifica
- **THEN** Persistencia transacional via TABLEUPDATE

### Requirement: Cliente inexistente ou inativo
O sistema SHALL aplicar a regra `RK-2a0c862a6b7a`: Cliente inexistente ou inativo

#### Scenario: Regra aplicada
- **GIVEN** os campos `clientes.ativo`, `pedidos`, `clientes`
- **WHEN** a condição `!FOUND() OR !clientes.ativo` se verifica
- **THEN** Cliente inexistente ou inativo

### Requirement: Total excede o limite de credito do cliente
O sistema SHALL aplicar a regra `RK-d4fb739728ef`: Total excede o limite de credito do cliente

#### Scenario: Regra aplicada
- **GIVEN** os campos `pedidos.total`, `clientes.limite`, `pedidos`, `clientes`
- **WHEN** a condição `pedidos.total > clientes.limite` se verifica
- **THEN** Total excede o limite de credito do cliente

