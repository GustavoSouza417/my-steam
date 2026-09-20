# Branches

## Modelo

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

## Branches temporárias

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

## Nomenclatura

```
<plataforma ou módulo>/<tipo>/<nome>
```

Tudo minúsculo, em **inglês**, com as partes separadas por `/` e as palavras
de cada parte separadas por **hífen**.

| Parte | Regra |
|---|---|
| plataforma ou módulo | `my-steam` quando afeta a plataforma toda; o nome do módulo quando é específico |
| tipo | o mesmo do commit: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `poc` |
| nome | o que a branch faz, em poucas palavras |

```
my-steam/feat/game-download
my-steam/poc/wasm-game-pipeline
store/fix/cart-total
```

`store` é um módulo hipotético, só para ilustrar. Enquanto não houver
módulos, toda branch usa `my-steam`.

## Como mesclar

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

## Hotfix

Bug em produção não espera o fluxo inteiro. A branch sai da `main`, volta para
a `main` e a correção é **propagada para baixo** — `homolog`, `staging`, `qa`,
`dev` — para que nenhum ambiente fique sem ela.

```
main → my-steam/fix/login-crash → main → homolog → staging → qa → dev
```

É a única exceção ao sentido único de promoção.
