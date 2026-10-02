# V1 — Escopo reduzido

## Por que reduzir

O desenho original (contas com papéis N:N, fila de solicitação genérica, moderação cruzada, auditoria, reset de senha por token) é o sistema completo, pensado pra quando o site for colaborativo de verdade. Mas nada disso é necessário pra site existir e já ser útil — a turma consegue se virar sem colaboração aberta no primeiro momento. Faz mais sentido reduzir a carga inicial, publicar algo funcional rápido, e só depois evoluir pra V2 com contas, papéis e moderação.

## O que entra no V1

Todas as seções de conteúdo planejadas continuam em V1 — a redução de escopo é só no **sistema de acesso**, não no conteúdo:

- Painel do dia (Início)
- Horários (grade semanal)
- Matérias (semestre atual + grade histórica completa)
- Provas e Atividades
- Calendário da API/Estágio
- Vagas de emprego
- Mural de avisos
- Blog da turma
- Pedidos ao representante
- Página de calendário unificado

Tudo **público em leitura**, sem exigir conta pra visitante nenhum.

## O que fica mais simples no V1

- **Sem cadastro público.** Não existe tela de registro de usuário, nem papel "aluno", nem fila de solicitação de conta.
- **Um único login fixo de admin.** Só existe uma conta — a do administrador — usada pra cadastrar e editar o conteúdo de todas as seções diretamente, sem fluxo de aprovação.
- **Sem moderação cruzada, sem fila de solicitação, sem auditoria.** Como só existe um admin editando, não faz sentido nenhuma dessas peças ainda — elas só existem pra coordenar várias pessoas com papéis diferentes.
- **Sem reset de senha por token.** É uma conta só, de uso do próprio administrador; se precisar trocar a senha, troca direto na variável de ambiente.

## Credencial de admin (V1)

A senha do admin **não fica em texto puro em nenhum lugar do repositório** (o repositório é público). Ela é lida de uma variável de ambiente local (`.env.local`, já ignorado pelo Git) e convertida em hash (bcrypt) antes de qualquer gravação em banco — ninguém, nem o próprio admin olhando o banco depois, consegue recuperar a senha original a partir do hash. O mesmo princípio de hash irreversível já combinado para V2 continua valendo aqui, só que pra uma conta só.

## O que vira V2

- Cadastro público de conta (papel-base "aluno")
- Papéis intermediários (moderador de vagas, de atividades, de cadastro/admissão, representante, redator) e a relação N:N usuário↔papel
- Fila de solicitação genérica (sugestão de conteúdo, pedido de papel, edição estilo "pull request")
- Moderação cruzada (ninguém aprova o próprio conteúdo)
- Auditoria de aprovação/rejeição
- Reset de senha por token de uso único
- Notificações internas
- Virada de semestre / arquivamento histórico automatizado

## Referência visual

O esqueleto visual de Início, Horários, Matérias, Provas/Atividades e Calendário API foi gerado no Google Stitch a partir do prompt em [`docs/prompt-stitch.md`](./prompt-stitch.md) — usado como base de estilo e estrutura, não como regra fechada; as telas são ajustadas livremente no próprio Stitch ou no Figma conforme o projeto evolui.
