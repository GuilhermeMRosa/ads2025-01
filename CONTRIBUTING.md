# Como contribuir

## Commits — Conventional Commits

Formato: `tipo(escopo): descrição`

Tipos:
- `feat` — nova funcionalidade
- `fix` — correção de bug
- `chore` — tarefa de manutenção (config, dependências, etc.)
- `docs` — documentação
- `refactor` — mudança de código sem alterar comportamento
- `test` — adição ou ajuste de testes
- `style` — formatação, sem mudança de lógica

O escopo é opcional. A descrição fica em português.

Exemplos:
```
feat(vagas): adiciona cadastro de vaga
fix(auth): corrige validação de token de reset
docs: atualiza README
```

## Branches — GitHub Flow

- `main` é sempre estável e protegida — ninguém dá push direto nela.
- Toda mudança nasce numa branch própria: `feat/nome-da-feature`, `fix/nome-do-bug`, `chore/...`.
- Toda mudança entra via **Pull Request**, mesmo pequena.
- **Ninguém aprova o próprio PR** — precisa de pelo menos uma revisão de outra pessoa antes do merge (mesmo princípio da moderação cruzada usada no conteúdo do site).
- Cada PR gera um preview deploy automático na Vercel — usa isso pra conferir a mudança rodando antes de aprovar.
