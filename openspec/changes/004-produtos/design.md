# Design

## Context

Campos da tela legada, na ordem em que devem ser renderizados. A coluna *Componente* usa os nomes
genéricos mapeados para shadcn/ui no design da fundação.

| Campo | Rótulo | Componente | Máscara | Comportamento | Obrigatório | Coluna da lista |
|---|---|---|---|---|---|---|
| descricao | Descrição | input | — | — | sim | sim |
| preco | Preço | input | — | — | não | sim |
| estoque | Estoque | input | — | — | não | sim |
| unidade | Unidade | select | — | — | não | sim |
| ativo | Ativo | toggle | — | — | não | sim |
| produtoid | Produtoid | read-only | — | — | não | não |

## Goals / Non-Goals

**Goals:**
- Reproduzir o cadastro do legado sem inventar campo, tela ou regra.
- Cada `RK-…` aplicada em um ponto único e comentado do código.

**Non-Goals:**
- Migrar dados do legado.
- Funcionalidades que o legado não tinha.

## Decisions

- **Onde cada regra vale** — `RK-89b58328383c`: a definir — ler a regra antes de escolher a camada
- **Onde cada regra vale** — `RK-cf3d19dd8e6d`: a definir — ler a regra antes de escolher a camada
- **Onde cada regra vale** — `RK-e5a3716dfd5f`: a definir — ler a regra antes de escolher a camada
- **Onde cada regra vale** — `RK-bfca0ddf1d4e`: a definir — ler a regra antes de escolher a camada
- **Onde cada regra vale** — `RK-dc47b88f5812`: a definir — ler a regra antes de escolher a camada
- **Onde cada regra vale** — `RK-678c161373aa`: a definir — ler a regra antes de escolher a camada
- **Onde cada regra vale** — `RK-54d7c0aa28ec`: a definir — ler a regra antes de escolher a camada
- **Onde cada regra vale** — `RK-c685cf0351b0`: a definir — ler a regra antes de escolher a camada
- **Validação dupla** — campos obrigatórios validados no formulário e na API; a API é a última palavra.

## Risks / Trade-offs

- [Regra ambígua implementada errado] → cada NEEDS REVIEW leva `// TODO(review): RK-…`; QA confere pelo MCP.
- [Coluna inventada para campo a confirmar] → sem origem confirmada, o campo não vira coluna.
