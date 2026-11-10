# Fundação do projeto — Mundial

## Why

O sistema legado será reconstruído em uma stack moderna. Antes de qualquer entidade, o
repositório precisa do scaffold, das convenções de API e UI que todas as changes seguintes
assumem e das tabelas de referência que as telas usam como dropdown. Esta change existe para
que as changes de entidade sejam só domínio.

## What Changes

- Scaffold do frontend (nextjs + shadcn/ui) e do backend (nextjs) com prisma, na estrutura de `design.md`.
- Banco sqlite: migrações versionadas, uma por change.
- Convenções: REST em `/api/<entidade>`, paginação, contrato de erro de validação.
- Navegação principal listando cada entidade gerenciada.
- Tabelas de referência (`pedidos`) com API somente leitura — sem tela de edição.
- Variáveis de ambiente documentadas em `.env.example`.
- Locale pt-BR: datas `DD/MM/YYYY`, símbolo de moeda `R$`; máscaras de entrada e serviços de endereço conforme `design.md` § Máscaras de campo e serviços.

## Capabilities

### New Capabilities

- `app-shell`: navegação, convenções de API, configuração e dados de referência
- `locale-and-formats`: locale, formatos de data e moeda, máscaras de entrada e os serviços de endereço que os formulários usam

### Modified Capabilities

_none_

## Impact

- Novo repositório; nenhum código existe antes desta change.
- Toda change seguinte depende das convenções fixadas aqui.

## Fora de escopo — regras sem entidade neste build

Regras extraídas do legado cujos campos e tabelas não existem em nenhuma entidade deste
build. Ficam registradas para decisão de produto; nenhuma change as implementa.

- `RK-7a8b2a9034ab` Data do pedido nao pode ser futura
- `RK-1e07591d8905` Quantidade deve ser maior que zero
- `RK-9a6d70889993` Transicao de estado: status = "F" (STATE_TRANSITION)
- `RK-afb9d538c5aa` Persistencia transacional via TABLEUPDATE
