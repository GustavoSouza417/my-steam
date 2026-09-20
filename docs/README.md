# Documentação

A documentação só é numerada onde a **ordem importa por ser histórica**: em
[`adr/`](adr/) e em [`../pocs/`](../pocs/), onde cada registro só faz sentido
diante dos anteriores. Nas demais pastas os arquivos têm nome livre, sem
prefixo — a ordem de leitura fica descrita aqui.

## [`product/`](product/) — o que estamos construindo

Decisões de **produto**. Na ordem em que fazem sentido ser lidas:

1. [`overview.md`](product/overview.md) — o que é o projeto e por quê.
2. [`scope.md`](product/scope.md) — domínios do sistema e a linguagem que usamos.
3. [`backlog.md`](product/backlog.md) — funcionalidades macro e o que já foi construído.

Documento novo só quando não couber em nenhum existente; o normal é ampliar um
destes.

## [`devsecops/`](devsecops/) — como trabalhamos

Convenções de trabalho: commits, branches, CI/CD, segurança, deploy.

1. [`commits.md`](devsecops/commits.md) — formato, tamanho e frequência dos commits.
2. [`naming.md`](devsecops/naming.md) — nomes de arquivos, pastas e identificadores no código.
3. [`branches.md`](devsecops/branches.md) — modelo de branches, nomenclatura e hotfix.

## [`adr/`](adr/) — como estamos construindo

Decisões de **arquitetura**: como o navegador grava na pasta do usuário, como
os jogos são compilados, onde os arquivos ficam hospedados. Numerados por
**ordem de criação**: a sequência é o histórico das decisões.

Números nunca são reaproveitados nem reordenados. Uma decisão revista não apaga
a anterior: entra como um ADR novo que a substitui.

Ainda vazio — ver [`adr/README.md`](adr/README.md).

## Fora de `docs/`

- [`../pocs/`](../pocs/) — experimentos. Cada PoC tem sua pasta numerada e um
  `README.md` próprio. A PoC ou o conjunto de PoCs que levar a uma decisão de
  arquitetura gera um ADR aqui em [`adr/`](adr/).
- `../.claude/` — configuração do agente (skills, settings). É versionada, mas
  não é documentação do projeto: não entra nos índices acima e segue os nomes
  que a ferramenta espera, como `SKILL.md`.
