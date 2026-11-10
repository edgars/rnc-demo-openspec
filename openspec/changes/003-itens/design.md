# Design

## Context

Campos da tela legada, na ordem em que devem ser renderizados. A coluna *Componente* usa os nomes
genéricos mapeados para shadcn/ui no design da fundação.

| Campo | Rótulo | Componente | Máscara | Comportamento | Obrigatório | Coluna da lista |
|---|---|---|---|---|---|---|
| clienteid | Clienteid | input | — | — | não | sim |
| produtoid | Produtoid | input | — | — | não | sim |
| data | Data | date | — | — | não | sim |
| qtde | Qtde | input | — | — | não | sim |
| precounit | Precounit | input | — | — | não | sim |
| subtotal | Subtotal | input | — | — | não | não |
| status | Status | select | — | — | não | não |

## Goals / Non-Goals

**Goals:**
- Reproduzir o cadastro do legado sem inventar campo, tela ou regra.
- Cada `RK-…` aplicada em um ponto único e comentado do código.

**Non-Goals:**
- Migrar dados do legado.
- Funcionalidades que o legado não tinha.

## Decisions

- **Onde cada regra vale** — `RK-97d3c0193d59`: a definir — ler a regra antes de escolher a camada
- **Onde cada regra vale** — `RK-e5a3716dfd5f`: a definir — ler a regra antes de escolher a camada
- **Onde cada regra vale** — `RK-1a7c75fecf85`: a definir — ler a regra antes de escolher a camada

## Risks / Trade-offs

- [Regra ambígua implementada errado] → cada NEEDS REVIEW leva `// TODO(review): RK-…`; QA confere pelo MCP.
- [Coluna inventada para campo a confirmar] → sem origem confirmada, o campo não vira coluna.
