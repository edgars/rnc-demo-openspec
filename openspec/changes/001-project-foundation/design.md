# Design

## Context

Stack decidida no Architecture Canvas da RNC. Modelo de dados completo abaixo; cada change de
entidade repete só a sua tabela.

## Goals / Non-Goals

**Goals:**
- Um esqueleto que roda vazio (`docker compose up --build`) antes da primeira entidade.
- Convenções únicas que as changes de entidade só reutilizam.

**Non-Goals:**
- Nenhuma tela de domínio: elas chegam pelas changes de entidade.
- Nenhuma migração de dados do legado.

## Decisions

- **Stack** — frontend nextjs, backend nextjs + prisma, banco sqlite. Escolhida no canvas da RNC como substituta suportada do legado.
- **Biblioteca de UI — shadcn/ui** (https://ui.shadcn.com). Toda tela usa seus componentes; nunca uma segunda biblioteca. Setup:
  - `npx shadcn@latest init`
  - `npx shadcn@latest add button input textarea select command popover calendar switch table pagination alert-dialog sonner form sidebar breadcrumb dropdown-menu`
  Tema: CSS variables on `:root` and `.dark` (`--background`, `--foreground`, `--primary`, `--destructive`, `--border`, `--ring`…); dark mode toggles the `.dark` class on `<html>`.
- **Locale e formatos** — locale pt-BR, datas `DD/MM/YYYY`, moeda `R$` (Configurações da Aplicação na RNC). Um formatador compartilhado por toda lista e formulário; nunca formatar inline.
- **Um módulo por entidade gerenciada** — rota, API, validação e páginas próprias; espelha a estrutura tela-por-entidade do legado.
- **Tabelas de referência são lookups, não telas** — API read-only; o FK guarda o id do registro relacionado. Reproduz o comportamento do legado sem inventar CRUD.
- **Configuração por ambiente** — tudo em `.env` com `.env.example` versionado; segredos nunca no código.

## Modelo de dados

### Clientes (`clientes`)

| Coluna | Tipo | Nulo |
|---|---|---|
| id | Int (PK, auto) | não |
| nome | String? | sim |
| cpfcnpj | String? | sim |
| email | String? | sim |
| telefone | String? | sim |
| limite | Decimal? | sim |
| ativo | Boolean? | sim |
| obs | String? | sim |

### Itens (`itens`)

| Coluna | Tipo | Nulo |
|---|---|---|
| id | Int (PK, auto) | não |
| pedidoid | Int? | sim |
| produtoid | Int? | sim |
| qtde | Decimal? | sim |
| precounit | Decimal? | sim |
| subtotal | Decimal? | sim |
| clienteid | String? | sim |
| data | DateTime? | sim |
| status | String? | sim |

### Produtos (`produtos`)

| Coluna | Tipo | Nulo |
|---|---|---|
| id | Int (PK, auto) | não |
| descricao | String? | sim |
| unidade | String? | sim |
| preco | Decimal? | sim |
| estoque | Int? | sim |
| ativo | Boolean? | sim |

### Pedidos (`pedidos`)  _— tabela de referência_

| Coluna | Tipo | Nulo |
|---|---|---|
| id | Int (PK, auto) | não |
| clienteid | Int? | sim |
| data | DateTime? | sim |
| status | String? | sim |
| total | Decimal? | sim |
| obs | String? | sim |

## Relações prováveis (derivadas — confirmar antes de impor)

O legado não declara chaves estrangeiras. Estas coincidências de nome sugerem joins; confirme
contra o código legado (ou pelo MCP da RNC) antes de criar constraints. O schema não as inclui.

- **Clientes** ↔ **Produtos** compartilham `ativo` — provavelmente unidas por isso no legado.
- **Itens** ↔ **Pedidos** compartilham `clienteid`, `status` — provavelmente unidas por isso no legado.

## Máscaras de campo e serviços

Do perfil de geração da RNC (locale pt-BR), resolvidas pelo nome do campo. Só os tipos que ocorrem neste build estão listados; cada change de entidade repete os próprios campos nas colunas Máscara e Comportamento. `#` = dígito, `A` = letra.

| Tipo | Máscara |
|---|---|
| CPF | `###.###.###-##` |
| telefone | `(##) ####-####` |


## Risks / Trade-offs

- [Stack diferente da escolhida] → `design.md` e `config.yaml` são a referência; o agente não troca stack.
- [Schema inventado para campo a confirmar] → cada change lista seus campos a confirmar; sem coluna confirmada, sem coluna.
