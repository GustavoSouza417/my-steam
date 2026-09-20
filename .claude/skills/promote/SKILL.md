---
name: promote
description: Integra as branches temporárias pendentes em `dev` e promove `dev` por toda a cadeia de ambientes até `main`, seguindo as regras de merge do projeto. Não publica nada no remoto. Use quando o usuário pedir /promote.
disable-model-invocation: true
allowed-tools: Bash(git status:*), Bash(git branch:*), Bash(git switch:*), Bash(git merge:*), Bash(git log:*), Bash(git rev-parse:*)
disallowed-tools: Edit, Write
---

# Promoção

## Objetivo

Levar o trabalho pronto de onde ele está até `main`, sem pular etapa e sem
inventar. O procedimento é mecânico: as regras estão em
[`docs/devsecops/git.md`](../../../docs/devsecops/git.md) e esta skill apenas
as executa na ordem certa.

**Nunca dê `push`.** Publicar é decisão do usuário, sempre. Terminar a
promoção não é terminar o trabalho pela metade: é o escopo desta skill.

## Antes de começar

1. A árvore precisa estar limpa (`git status --porcelain` vazio). Se houver
   mudança não commitada, **pare e pergunte** — decidir o que entra em qual
   commit não é trabalho desta skill.
2. Não crie branch, não edite arquivo, não resolva conflito.

## 1. Integrar as temporárias

Liste o que ainda não está em `dev`:

```bash
git branch --no-merged dev
```

Dessa lista, mescle apenas as **branches temporárias** — as que têm `/` no
nome, como `my-steam/feat/game-download`.

Se uma branch de ambiente (`qa`, `staging`, `homolog`, `main`) aparecer na
lista, **pare e avise**: significa que alguém commitou direto num ambiente, o
que este fluxo não permite, e a promoção com `--ff-only` vai falhar adiante.

Cada uma entra em `dev` com `--no-ff` e mensagem no padrão do projeto,
incluindo o trailer de coautoria:

```bash
git switch dev
git merge --no-ff <branch> -m "chore(<escopo>): merge <resumo curto> into dev

Co-Authored-By: <modelo que participou> <noreply@anthropic.com>"
```

Conflito: `git merge --abort`, pare e relate qual branch conflitou. Resolver
exige contexto que esta skill não tem.

Depois, confira que a lista ficou vazia.

## 2. Promover a cadeia

Na ordem, sem pular nenhum estágio:

```
dev → qa → staging → homolog → main
```

Cada passo é `--ff-only`:

```bash
git switch <ambiente> && git merge --ff-only dev
```

**Se um `--ff-only` falhar, pare ali mesmo** e relate. A falha significa que
aquele ambiente tem commit que `dev` não tem — o fluxo está quebrado, e forçar
o merge esconderia o problema em vez de resolvê-lo.

## 3. Terminar

Volte para `dev`. Não apague branch nenhuma: temporária mesclada vive pelo
menos duas semanas.

## Relatório

Como manda o [`CLAUDE.md`](../../../CLAUDE.md), diga em texto, uma linha cada:

- quais temporárias foram mescladas em `dev`, e os commits de merge criados;
- até onde a cadeia subiu e em qual commit os ambientes ficaram;
- quantos commits cada branch está à frente do remoto;
- em qual branch a conversa está agora.

Feche lembrando que o push é do usuário, com o comando pronto para ele copiar.
