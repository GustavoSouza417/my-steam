# Documentação

Toda documentação deste projeto é numerada com prefixo `001-`, `002-`, ...
O critério da numeração muda conforme a natureza da pasta.

## [`product/`](product/) — o que estamos construindo

Decisões de **produto**. Numerados por **ordem de leitura**: quem chega agora
lê do menor para o maior e entende o projeto inteiro, do geral ao específico.

1. [`001-overview.md`](product/001-overview.md) — o que é o projeto e por quê.
2. [`002-scope.md`](product/002-scope.md) — domínios do sistema e a linguagem que usamos.
3. [`003-backlog.md`](product/003-backlog.md) — funcionalidades macro e o que já foi construído.

Documento novo só quando não couber em nenhum existente; o normal é ampliar um
destes. Quando criar, entra na posição onde faz sentido lê-lo, renumerando os
seguintes. A ordem aqui é didática, não histórica.

## [`devsecops/`](devsecops/) — como trabalhamos

Convenções de trabalho: commits, branches, CI/CD, segurança, deploy. Numerados
por **ordem de leitura**, como `product/`.

1. [`001-commits.md`](devsecops/001-commits.md) — formato, tamanho e frequência dos commits.
2. [`002-naming.md`](devsecops/002-naming.md) — nomes de arquivos, pastas e identificadores no código.
3. [`003-branches.md`](devsecops/003-branches.md) — modelo de branches, nomenclatura e hotfix.

## [`adr/`](adr/) — como estamos construindo

Decisões de **arquitetura**: como o navegador grava na pasta do usuário, como
os jogos são compilados, onde os arquivos ficam hospedados. Numerados por
**ordem de criação**: a sequência é o histórico das decisões, e um ADR só faz
sentido diante dos anteriores.

Números nunca são reaproveitados nem reordenados. Uma decisão revista não apaga
a anterior: entra como um ADR novo que a substitui.

Ainda vazio — ver [`adr/README.md`](adr/README.md).
