# Site da Sala — 4º ADS (Fatec SJC)

Site feito pela e para a turma do curso de Análise e Desenvolvimento de Sistemas da Fatec São José dos Campos, pra centralizar tudo que hoje está espalhado entre grupo de WhatsApp/Discord: horários de aula, matérias, professores, provas e atividades, calendário do estágio/API, vagas de emprego, avisos da sala e um canal pra blog/resenhas entre a turma.

A ideia não é só mostrar informação — é também deixar a sala **colaborar**: qualquer aluno cadastrado pode sugerir conteúdo novo (uma vaga, uma data de prova, um aviso), que passa por aprovação antes de ir pro ar.

## Índice

- [Motivação](#motivação)
- [O que o site oferece](#o-que-o-site-oferece)
- [Modelo de permissões](#modelo-de-permissões)
- [Fluxo de moderação](#fluxo-de-moderação)
- [Stack técnica](#stack-técnica)
- [Rodando localmente](#rodando-localmente)
- [Status do projeto](#status-do-projeto)
- [Como contribuir](#como-contribuir)

## Motivação

A sala já se vira com grupo de WhatsApp e Discord, mas informação importante (prova, vaga, data de entrega) se perde na rolagem. A proposta é um lugar único, visual e fácil de consultar — pensado **mobile-first**, já que o uso real é no celular, entre aulas.

## O que o site oferece

- **Horários** — grade semanal de aula, por dia e matéria.
- **Matérias e professores** — quem dá aula de quê, incluindo a **grade completa do curso** (matérias de todos os semestres, não só o atual).
- **Provas e atividades** — data de entrega, descrição, matéria e tipo (prova, trabalho, apresentação, entrega).
- **Calendário da API/Estágio** — dados de empresa, P2 e M2, atualizados a cada semestre.
- **Vagas de emprego** — cadastro flexível (título, link, fonte, local, requisitos), com status e expiração automática pra não acumular vaga morta.
- **Mural de avisos** — posts curtos e informais ("amanhã não tem aula de fulano").
- **Blog da sala** — posts longos, categorizados (tecnologia, livros, filmes, etc.), com visualizações e curtidas — espaço pra reviews e conteúdo mais elaborado entre a turma.
- **Pedidos ao representante** — canal pra pedir algo que só o representante de turma resolve por fora (ex: remarcar prova com o professor).
- **Página de calendário unificada** — cruza provas, calendário da API e avisos num só lugar.
- **Links úteis** e **materiais de aula** (redireciona pro Drive da sala, não hospedado no site).

## Modelo de permissões

Tudo é **público em leitura** — qualquer visitante, mesmo sem conta, vê horários, provas, vagas, mural e blog. Só **criar ou editar** conteúdo exige conta.

Os papéis não são excludentes: um usuário pode acumular mais de um ao mesmo tempo (ex: moderador de vagas **e** moderador de atividades).

| Papel | O que faz |
|---|---|
| **Visitante** | Navega e lê tudo, sem conta. |
| **Aluno** | Papel-base de quem tem conta. Pode sugerir conteúdo (entra na fila de aprovação) e abrir pedido ao representante. |
| **Moderador de vagas** | Modera solicitações de vaga de emprego. |
| **Moderador de atividades** | Modera solicitações de prova/atividade. |
| **Moderador de cadastro/admissão** | Aprova pedidos de conta — inclusive pedidos de outros papéis. |
| **Representante de turma** | Responsável pela fila de pedidos ao representante. |
| **Redator** | Escreve posts no blog da sala. |
| **Admin** | Acesso total. Único papel que não passa por fila de aprovação. Pode haver mais de um admin. |

Cadastro de conta nova (qualquer papel, inclusive "aluno") passa por aprovação — é assim que a sala garante que só entra gente da própria turma.

## Fluxo de moderação

- Só **admin** publica direto, sem revisão, em qualquer área.
- Todo o resto passa por uma fila de aprovação — inclusive o que um moderador posta na própria área.
- **Moderação cruzada:** ninguém aprova o próprio conteúdo. Sempre precisa de alguém "de fora" validando (admin serve de aprovador de última instância quando só existe um moderador daquele tipo).
- Toda aprovação/rejeição fica registrada (quem, quando, e motivo obrigatório em caso de rejeição) — auditável depois.
- Editar algo já publicado também não é direto: vira uma **solicitação de alteração** (no espírito de um pull request), que qualquer aluno pode abrir, e passa pela mesma aprovação.

Esse mesmo princípio — nada publicado sem revisão cruzada — é o que seguimos no próprio código deste repositório (veja [Como contribuir](#como-contribuir)).

## Stack técnica

- **[Next.js](https://nextjs.org)** (React + TypeScript, App Router) — frontend e backend no mesmo projeto.
- **PostgreSQL** via [Neon](https://neon.tech) (serverless, integra nativo com Vercel).
- **[Prisma](https://www.prisma.io)** como ORM.
- **Tailwind CSS**, mobile-first.
- Autenticação própria (bcrypt + sessão via cookie JWT assinado) — sem biblioteca de auth genérica, porque o fluxo de aprovação/papéis é específico demais.
- Upload de imagem de post convertido pra **WebP** (via `sharp`) e guardado no **Vercel Blob**.
- Documentos (PDF, provas antigas, listas de exercício) nunca sobem pro site — sempre link pro Google Drive da sala.
- Deploy na **[Vercel](https://vercel.com)**.

## Rodando localmente

```bash
npm install
npm run dev
```

Abre em `http://localhost:3000`. (Configuração de banco de dados/variáveis de ambiente será documentada aqui assim que o Prisma entrar no projeto.)

## Status do projeto

🚧 Em estruturação. O desenho de produto (entidades, papéis, fluxo de moderação, stack) está fechado; a modelagem do banco (Prisma) e as primeiras páginas ainda estão por vir.

## Como contribuir

Veja [CONTRIBUTING.md](./CONTRIBUTING.md) para o padrão de commits (Conventional Commits) e o fluxo de branches/PR (GitHub Flow, sem self-approve, sempre via Pull Request).
