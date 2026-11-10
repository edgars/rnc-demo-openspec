# Mundial — Plano de Construção (OpenSpec)

> **Este repositório não contém código de aplicação.** Ele é um **pacote de changes
> OpenSpec** — propostas, specs de comportamento, design e tarefas — produzido por
> engenharia reversa de um sistema legado. Qualquer desenvolvedor, com **qualquer agente de
> AI coding** que a OpenSpec suporte (Claude Code, Cursor, Codex, OpenCode, Kiro, Copilot…),
> constrói a aplicação moderna aplicando as changes em ordem.

---

## 1. De onde isto veio

| | |
|---|---|
| **Sistema legado** | Engenharia reversa: 3 tela(s), 4 entidade(s), 26 regra(s) de negócio extraída(s) |
| **Gerado por** | Plataforma **RNC**: código legado → UIR (representação intermediária) → changes OpenSpec |
| **Stack alvo** | Frontend **nextjs + shadcn/ui** · Backend **nextjs + prisma** · Banco **sqlite** · **docker-compose** |
| **SSO** | desligado |
| **Locale e formatos** | pt-BR · datas `DD/MM/YYYY` · moeda `R$`· máscaras: CPF, telefone |
| **Formato** | [OpenSpec](https://github.com/Fission-AI/OpenSpec) schema spec-driven v1 — schema `spec-driven`. Testado com a CLI `@fission-ai/openspec` 1.16. |

Na OpenSpec, `openspec/specs/` descreve **como o sistema funciona hoje** e cada pasta em
`openspec/changes/` propõe **o que vai mudar** — proposta, specs delta (`ADDED Requirements`),
design e tarefas. Como o app novo ainda não existe, `specs/` nasce vazio: **cada change
arquivada constrói a verdade do sistema novo**. As changes aqui já estão escritas — derivadas
do código legado, não à mão. Seu agente executa o build (`apply`), você verifica e arquiva.

---

## 2. Mapa do repositório — leia nesta ordem

```
README.md                         ← você está aqui (o "como usar")
AGENTS.md                         ← instruções para qualquer agente de coding (loop apply → verify → archive)
CLAUDE.md, .mcp.json, .claude/    ← Claude Code (Rota B)
openspec/
├── config.yaml                   ← ordens permanentes: idioma, stack, precedência, regras por artefato
├── specs/                        ← vazio de propósito; cresce a cada `openspec archive`
└── changes/                      ← o plano, em ordem numérica
    ├── 001-project-foundation/   ← PRIMEIRA: scaffold, stack, convenções, tabelas de referência
    ├── 002-clientes/ …           ← uma change por entidade gerenciada
    ├── 005-deployment/           ← ÚLTIMA: Dockerfiles, compose/manifests
    │   └── proposal.md · design.md · tasks.md · specs/<capability>/spec.md · .openspec.yaml
    └── archive/                  ← changes concluídas (`openspec archive` move para cá)
```

**Quando documentos parecerem divergir**, a hierarquia é:
**1.** diretivas do autor (*"follow VERBATIM"* em `openspec/config.yaml`) → **2.** configuração
explícita do canvas → **3.** decisões derivadas → **4.** defaults. Nunca "conserte" uma diretiva:
ela carrega intenção do arquiteto.

---

## 3. O domínio em um minuto

| Entidade | Colunas | Papel | Change |
|---|---|---|---|
| `clientes` | 7 | Gerenciada — CRUD completo em `/clientes` | `002-clientes` |
| `itens` | 8 | Gerenciada — CRUD completo em `/itens` | `003-itens` |
| `produtos` | 5 | Gerenciada — CRUD completo em `/produtos` | `004-produtos` |
| `pedidos` | 5 | Referência — somente leitura, sem tela própria | (API read-only na change de fundação) |

Cada regra de negócio tem uma **chave estável** `RK-…`(ex.: `RK-734dab5f870e`). Ela aparece no texto do
requirement da spec e na tarefa que o implementa, e identifica a regra para sempre — dá para
rastreá-la até o código-fonte original pelo MCP da RNC.

---

## 4. Passo a passo

**Pré-requisitos:** Node.js ≥ 22.12, git, Docker + Docker Compose, e um agente de AI coding suportado pela
OpenSpec (Claude Code, Cursor, Codex, OpenCode, Kiro, GitHub Copilot, Gemini CLI…).

### 4.1 — Instale a CLI da OpenSpec

```bash
npm install -g @fission-ai/openspec@latest
openspec --version
```

Uma vez por máquina. Também existe `brew install openspec`.

### 4.2 — Conecte sua ferramenta ao projeto

```bash
openspec init --tools claude
```

Na raiz deste repositório. O `openspec/config.yaml` **já existe e é preservado**; o `init`
só gera os skills e comandos `/opsx:*` da ferramenta escolhida (`--tools all` para todas,
`openspec init --help` lista os ids). Para trocar de ferramenta depois: `openspec update`.

Ferramentas já previstas neste pacote (Rota B): **Claude Code**.

### 4.3 — Valide o pacote

```bash
openspec validate --all --strict
openspec list --changes
```

Tudo precisa passar **antes** de abrir o agente. `--strict` trata avisos como erro — é o
nível que este pacote foi escrito para atingir. Se algo falhar, veja a seção 7.

### 4.4 — Aplique as changes, uma por vez, em ordem

Abra sua ferramenta na raiz do repositório e, para **cada** change em ordem numérica:

1. **Aplicar** — `/opsx:apply` com o id da change. O agente lê `proposal.md`, `design.md` e as specs,
   implementa `tasks.md` e marca cada tarefa `- [x]` ao concluir.
2. **Verificar** — leia o diff. Cada tarefa `Enforce RK-…` precisa de um comentário
   `// RK-…` no ponto do código onde a regra vale. Com o perfil expandido da OpenSpec
   (`openspec config profile`), `/opsx:verify` faz essa conferência contra as specs.
3. **Arquivar** — `/opsx:archive` com o id da change. As specs delta entram em `openspec/specs/`,
   que passa a descrever o sistema novo. Só então comece a próxima change.

```
/opsx:apply 001-project-foundation
/opsx:archive 001-project-foundation
/opsx:apply 002-clientes
…
/opsx:archive 005-deployment
```

A grafia muda por ferramenta: Claude Code e OpenCode usam `/opsx:apply`, Cursor e Copilot
`/opsx-apply`, Codex `$openspec-apply`. Sem skills, o prompt equivalente é:

> Leia `openspec/config.yaml` por inteiro e trate o bloco `context` como instruções
> permanentes desta sessão. Depois leia `AGENTS.md`. Aplique a change
> `openspec/changes/001-project-foundation`: leia `proposal.md`, `design.md` e `specs/`, implemente cada item
> de `tasks.md` na ordem e marque `- [x]` ao concluir. Não invente stack, entidade ou campo
> que não esteja nos documentos. Ao terminar, rode `openspec validate --strict` e pare.

### 4.5 — (Recomendado) Conecte o MCP da RNC

Com o MCP conectado o agente confere cada `RK-…` contra a regra do legado (`getRule`) e lê o
código original das regras marcadas **NEEDS REVIEW** (`getSourceFile`) em vez de adivinhar.
Nenhuma credencial vai no repositório: exporte a URL da API da RNC e o token gerado em
Settings → MCP antes de abrir a ferramenta:

```bash
export RNC_MCP_URL=https://<host-da-api-rnc>
export RNC_MCP_TOKEN=<token>
```

Renovou o token? Atualize `RNC_MCP_TOKEN` e reabra a ferramenta — nada no repositório muda.

- **Claude Code** — abra com `claude`; o `.mcp.json` já aponta para o servidor `rnc`.

### 4.6 — Ao final

```bash
cp .env.example .env
docker compose up --build
```

App no ar: frontend nextjs, API nextjs, sqlite com volume persistente.

### 4.7 — Depois do build: evoluir pela OpenSpec

O repositório fica no fluxo normal da OpenSpec. Para qualquer mudança nova: `/opsx:explore`
para investigar, `/opsx:propose` para criar a change (proposta + specs delta + design +
tarefas), `/opsx:apply` e `/opsx:archive`. Para alterar um requirement já arquivado, a change
usa `## MODIFIED Requirements` copiando o bloco inteiro. As specs continuam sendo a verdade.

---

## 5. O protocolo de build

1. **Uma change por vez, na ordem numérica. Arquive antes de começar a próxima.**
2. **As specs são a fonte de verdade de comportamento.** `proposal.md` explica o porquê,
   `design.md` o como; a spec diz o quê.
3. **`NEEDS REVIEW`** = regra ambígua no fonte: implemente a interpretação mais provável e
   deixe `// TODO(review): RK-… <dúvida>`.
4. **Tabelas de referência não ganham CRUD** — só API read-only + dropdown, como no legado.
5. **"Comportamentos legados a confirmar"** (impressões, conexões, diálogos) listados nas
   propostas **não são requirements** — portar ou aposentar é decisão de produto.
6. **Campos "a confirmar"** no `design.md` (coluna de origem não rastreada): não derive a
   coluna pelo nome do campo; confirme a origem antes do schema.
7. **Relações prováveis** no design da fundação são sugestões — confirme antes de criar FK.
8. **Nunca edite uma spec para o código passar.** Se a spec estiver errada, registre em
   `design.md` § Open Questions e pare a change.

---

## 6. Decisões pendentes deste projeto

- **Comportamentos legados** — 1 rotina(s) do legado (impressões, conexões, diálogos)
  listada(s) nas propostas; portar ou aposentar é decisão de produto.

---

## 7. Problemas comuns

| Sintoma | Ação |
|---|---|
| `openspec validate` reclama de heading ou de `SHALL` | Os cabeçalhos `## Purpose`, `## Requirements`, `### Requirement:`, `#### Scenario:`, `## ADDED Requirements` e as palavras `SHALL`/`WHEN`/`THEN` ficam em inglês; o resto é livre |
| `Duplicate requirement` ao arquivar | Dois requirements com o mesmo nome na mesma capability — renomeie um deles na change |
| Agente resumiu e pulou regras | Uma change por vez; peça para recitar as `RK-…` de `tasks.md` antes de codar |
| Agente inventou tela/campo | Aponte a seção 5 e o `context` do `openspec/config.yaml`; peça diff contra a spec |
| Agente criou coluna para campo *a confirmar* | `design.md` § Open Questions: confirme a origem antes do schema |
| Quer mudar um requirement já arquivado | Nova change com `## MODIFIED Requirements` (bloco inteiro), nunca editar `openspec/specs/` à mão |
| Dúvida sobre uma regra | Procure a `RK-…` na spec (condição + campos) ou `getRule` pelo MCP |

---

*Gerado pela plataforma RNC. Formato: OpenSpec (https://github.com/Fission-AI/OpenSpec).
Para regenerar, use o workspace de origem na RNC — este pacote sobrescreve `openspec/changes/`
e nunca `openspec/specs/` nem o código já construído.*
