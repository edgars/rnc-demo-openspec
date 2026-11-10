# Design

## Context

Campos da tela legada, na ordem em que devem ser renderizados. A coluna *Componente* usa os nomes
genéricos mapeados para shadcn/ui no design da fundação.

| Campo | Rótulo | Componente | Máscara | Comportamento | Obrigatório | Coluna da lista |
|---|---|---|---|---|---|---|
| nome | Nome | input | — | — | sim | sim |
| cpfcnpj | Cpfcnpj | input | `###.###.###-##` | input mascarado | não | sim |
| email | Email | input | — | — | não | sim |
| telefone | Telefone | input | `(##) ####-####` | input mascarado | não | sim |
| limite | Limite | input | — | — | não | sim |
| ativo | Ativo | toggle | — | — | não | não |
| clienteid | Clienteid | read-only | — | — | não | não |
| obs | Obs | textarea | — | — | não | não |

## Goals / Non-Goals

**Goals:**
- Reproduzir o cadastro do legado sem inventar campo, tela ou regra.
- Cada `RK-…` aplicada em um ponto único e comentado do código.

**Non-Goals:**
- Migrar dados do legado.
- Funcionalidades que o legado não tinha.

## Decisions

- **Onde cada regra vale** — `RK-734dab5f870e`: a definir — ler a regra antes de escolher a camada
- **Onde cada regra vale** — `RK-08f0a245805c`: a definir — ler a regra antes de escolher a camada
- **Onde cada regra vale** — `RK-f4720b305355`: a definir — ler a regra antes de escolher a camada
- **Onde cada regra vale** — `RK-327c2b860142`: a definir — ler a regra antes de escolher a camada
- **Onde cada regra vale** — `RK-8919c708d165`: a definir — ler a regra antes de escolher a camada
- **Onde cada regra vale** — `RK-c45f79719b8d`: a definir — ler a regra antes de escolher a camada
- **Onde cada regra vale** — `RK-d90174e54a35`: a definir — ler a regra antes de escolher a camada
- **Onde cada regra vale** — `RK-e3f1424d5010`: a definir — ler a regra antes de escolher a camada
- **Onde cada regra vale** — `RK-80fd7c0ac69e`: a definir — ler a regra antes de escolher a camada
- **Onde cada regra vale** — `RK-2a0c862a6b7a`: a definir — ler a regra antes de escolher a camada
- **Onde cada regra vale** — `RK-d4fb739728ef`: a definir — ler a regra antes de escolher a camada
- **Validação dupla** — campos obrigatórios validados no formulário e na API; a API é a última palavra.

## Risks / Trade-offs

- [Regra ambígua implementada errado] → cada NEEDS REVIEW leva `// TODO(review): RK-…`; QA confere pelo MCP.
- [Coluna inventada para campo a confirmar] → sem origem confirmada, o campo não vira coluna.
