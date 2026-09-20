---
name: onboard
description: Carrega o contexto do projeto no começo de um chat novo. Lê a documentação por inteiro, mapeia a estrutura do repositório e devolve um resumo curto do estado atual, para o usuário conferir antes de o trabalho começar. Use quando o usuário pedir /onboard.
disable-model-invocation: true
---

# Onboarding no projeto

## Objetivo

Você acabou de chegar num chat novo e não sabe nada sobre este projeto além
do que o repositório conta. Esta skill existe para mudar isso **antes** de
qualquer trabalho começar.

O resumo do final não é o produto. O produto é o contexto que fica carregado
para o resto da conversa — o resumo serve só para o usuário conferir se esse
contexto saiu certo e corrigir o que ficou torto.

## O que ler

Nesta ordem:

1. `README.md` e `CLAUDE.md`, na raiz.
2. `docs/README.md` — o índice, que diz onde cada assunto mora e em que ordem
   ler o resto.
3. Tudo dentro de `docs/`, por inteiro, na ordem que o índice descreve.
4. `pocs/README.md` e o `README.md` de cada PoC. O código de uma PoC só se o
   README dela apontar algo que você precise confirmar.
5. As outras skills em `.claude/skills/`, só o frontmatter (`name` e
   `description`), para saber que ferramentas existem aqui. Não abra esta.

Do código da plataforma, **liste a estrutura** com `git ls-files` e entenda o
que existe e onde. Não leia arquivos de código por inteiro nesta etapa — isso
se faz depois, quando houver uma tarefa que peça.

Você pode olhar os últimos commits para saber o que foi mexido por último,
mas a fonte do estado atual é o que está versionado. Decisão que só existe
numa mensagem de commit não está registrada.

## O que não fazer

- **Não altere nada.** Nenhum arquivo, nenhum commit, nenhuma branch.
- **Não proponha trabalho.** Nada de próximo passo, melhoria, refatoração ou
  correção. Se o usuário quiser isso, ele pede depois.
- **Não invente.** O que o repositório não diz ou declara em aberto continua
  em aberto — não preencha com suposição.
- **Não audite.** Encontrar contradição ou referência quebrada é possível;
  sair procurando é trabalho de `/clarity-audit`, não desta skill.

## Formato da resposta

Em português e curto: o usuário conhece o projeto, o resumo é prova de
leitura, não aula. Poucas linhas em cada tópico.

- **O projeto** — uma ou duas frases.
- **Estado atual** — o que existe de fato no repositório e o que o backlog
  marca como construído.
- **Decidido** — as decisões que já valem e vão guiar seu trabalho: produto,
  convenções, fluxo de branches e commits.
- **Em aberto** — o que o repositório declara como ainda não decidido.
- **Dúvidas** — só se a leitura esbarrou em algo que travaria o trabalho.
  Sem nada a dizer, omita o tópico.

Termine perguntando o que vamos fazer. Nada além disso.
