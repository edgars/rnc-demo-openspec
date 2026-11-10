# Tasks

## 1. Scaffold

- [ ] 1.1 Criar o frontend nextjs + shadcn/ui e o backend nextjs com prisma conforme `design.md`; o app sobe vazio com `docker compose up --build`.
- [ ] 1.2 Instalar e configurar a biblioteca de UI shadcn/ui: npx shadcn@latest init && npx shadcn@latest add button input textarea select command popover calendar switch table pagination alert-dialog sonner form sidebar breadcrumb dropdown-menu. Layout base com navegação.
- [ ] 1.3 Banco sqlite com migrações versionadas; migração inicial vazia aplicada no start.

## 2. Convenções

- [ ] 2.1 Contrato REST: `/api/<entidade>` com `GET` paginado (`page`, `size`, `q`), `POST`, `GET /:id`, `PUT /:id`, `DELETE /:id`; erro de validação `400` com mensagem por campo.
- [ ] 2.2 Navegação principal com um item por entidade gerenciada (Clientes, Itens, Produtos); teste que cada item abre a rota.
- [ ] 2.3 `.env.example` com toda variável lida pelo app; CORS só para a origem do frontend.

## 3. Dados de referência

- [ ] 3.1 Tabela `pedidos` (Pedidos) com migração e API `GET /api/pedidos` somente leitura; teste listando a tabela.

## 4. Locale, formatos e máscaras

- [ ] 4.1 Locale `pt-BR`: um formatador de data (`DD/MM/YYYY`) e um de moeda (`R$`) compartilhados por toda lista e formulário; testar uma data e um valor.
- [ ] 4.2 Input mascarado compartilhado (`#` dígito, `A` letra) para as máscaras de `design.md` (CPF `###.###.###-##`, telefone `(##) ####-####`); testar que um valor fora da máscara é rejeitado.

## 5. Verificação

- [ ] 5.1 `openspec validate 001-project-foundation --strict` passa; smoke test sobe o app e abre cada item da navegação.
