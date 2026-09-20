# Git

Commits e branches usam o **mesmo vocabulário** e acontecem no mesmo momento
do trabalho, por isso estão no mesmo documento.

## Tipo e escopo

Valem para o título do commit e para o nome da branch.

**Tipos**: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `poc`.

`poc` marca trabalho experimental e descartável, feito em [`../../pocs/`](../../pocs/).

**Escopo**: `my-steam` quando a mudança afeta a plataforma toda, o nome do
módulo quando é específica. É **sempre obrigatório**.

Os módulos serão nomeados quando o código existir e a divisão ficar clara.
Enquanto não houver módulos, tudo é da plataforma — `feat(my-steam):`.

## Commits

### Formato

[Conventional Commits](https://www.conventionalcommits.org/), sempre em
**inglês**. A conversa do projeto é em português; o histórico, não.

```
<tipo>(<escopo>): <descrição>
```

Sem espaço antes do parêntese — `feat(store):`, não `feat (store):`. É o que a
especificação exige e o que ferramentas como commitlint esperam.

Descrição no imperativo e em minúscula, sem ponto final:
`feat(my-steam): add game page`.

### Só título

Commits têm **apenas o título**. Corpo de mensagem só quando for realmente
necessário — tipicamente para registrar o *porquê* de uma decisão que o código
não revela.

Se um commit precisa de parágrafos para ser explicado, em geral ele está
grande demais: o caminho é dividi-lo, não descrevê-lo melhor.

### Coautoria

Todo commit gerado com o agente leva o trailer de coautoria, inclusive os
de merge:

```
Co-Authored-By: <modelo que participou> <noreply@anthropic.com>
```

O nome é o do modelo que de fato escreveu o commit — por exemplo,
`Claude Opus 5`. Não copie o nome de commits anteriores.

É a única exceção à regra de só título: trailer não é descrição, e o histórico
deve deixar claro o que foi escrito em parceria com a IA — o projeto é sobre
desenvolvimento assistido por IA, então isso é informação, não ruído.

### Tamanho e frequência

Commits **pequenos e frequentes**. Um commit, uma mudança coesa.

O motivo é rastreabilidade e auditoria: commit pequeno é fácil de revisar, de
entender meses depois, de localizar num `bisect` e de reverter sem arrastar
junto o que não tem relação.

Na prática:

- Terminou algo que funciona e faz sentido sozinho? Commite.
- Mudanças sem relação entre si vão em commits separados, mesmo que tenham
  sido feitas na mesma sessão.
- Refatoração e mudança de comportamento não andam no mesmo commit.

## Branches

### Modelo

Usamos **branches por ambiente** (*environment branches*): cada branch fixa
representa um estágio de promoção, e a mudança sobe de um para o outro.

> Não confundir com Git Flow, que é outro modelo — `main` + `develop` +
> `feature/*` + `release/*` + `hotfix/*`, sem branches de ambiente.

```
1+ branches temporárias → dev → qa → staging → homolog → main
```

| Branch | Papel | Sobe para a próxima quando |
|---|---|---|
| `dev` | Integração do trabalho em andamento | está integrado e funciona |
| `qa` | Testes | os testes passam |
| `staging` | Ambiente equivalente ao de produção | funciona num ambiente igual ao de produção |
| `homolog` | Homologação: validação oficial com o cliente | o cliente aprovou |
| `main` | Produção | — |

Branches de ambiente são permanentes. Nunca se apaga nenhuma delas.

Sendo um projeto pessoal, **o cliente é o autor do repositório**. O objetivo
é simular um ciclo de desenvolvimento completo, mesmo que nem todo estágio
tenha, por enquanto, um ambiente real por trás.

### Branches temporárias

É onde o trabalho acontece. Nascem de `dev` e sobem para `dev` quando prontas.

Depois do merge, a branch **continua viva por pelo menos duas semanas**. Só
então pode ser apagada. O prazo existe para que a branch ainda esteja lá se
for preciso revisar, comparar ou recuperar algo logo após a integração.

Mudança pequena resolve-se numa única branch temporária. Se for grande e a
divisão fizer sentido, pode-se fazer um **mini fluxo** entre branches
temporárias — várias alimentando uma branch temporária maior — antes de subir
para `dev`.

Quem decide se uma mudança é grande o bastante para isso é o **autor do
repositório**. O agente pode propor a divisão, mas não a adota por conta
própria.

### Nomenclatura

```
<escopo>/<tipo>/<nome>
```

Tudo minúsculo, em **inglês**, com as partes separadas por `/` e as palavras
de cada parte separadas por **hífen**. Escopo e tipo são os mesmos do commit;
o nome diz o que a branch faz, em poucas palavras.

```
my-steam/feat/game-download
my-steam/poc/wasm-game-pipeline
store/fix/cart-total
```

`store` é um módulo hipotético, só para ilustrar. Enquanto não houver
módulos, toda branch usa `my-steam`.

### Como mesclar

**Branch temporária → `dev`: sempre com `--no-ff`.**

```bash
git merge --no-ff my-steam/feat/game-download
```

O commit de merge preserva a fronteira do trabalho: dá para ver quais commits
vieram de qual branch. Sem ele, tudo se dissolve numa sequência única.

**Entre branches de ambiente: sempre com `--ff-only`.**

```bash
git switch qa && git merge --ff-only dev
```

A promoção não cria commit novo — o ambiente seguinte recebe exatamente o que
foi aprovado no anterior. Se um `--ff-only` falhar, é sinal de que alguém
commitou direto numa branch de ambiente, o que este fluxo não permite.

**Mensagem de merge**: segue o mesmo padrão dos commits — incluindo o trailer
de coautoria, porque um merge feito pelo agente também é um commit feito pelo
agente. O padrão do git (`Merge branch 'x'`) não serve.

```
chore(my-steam): merge clarity-audit fixes into dev

Co-Authored-By: <modelo que participou> <noreply@anthropic.com>
```

**Quem mescla**: o agente leva uma branch temporária até `dev` por conta
própria. De `dev` para cima, cada promoção acontece por ordem do usuário.

### Hotfix

Bug em produção não espera o fluxo inteiro. A branch sai da `main`, volta para
a `main` e a correção é **propagada para baixo** — `homolog`, `staging`, `qa`,
`dev` — para que nenhum ambiente fique sem ela.

```
main → my-steam/fix/login-crash → main → homolog → staging → qa → dev
```

É a única exceção ao sentido único de promoção.
