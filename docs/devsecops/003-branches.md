# Branches

## Modelo

Usamos **branches por ambiente** (*environment branches*): cada branch fixa
representa um estágio de promoção, e a mudança sobe de um para o outro.

> Não confundir com Git Flow, que é outro modelo — `main` + `develop` +
> `feature/*` + `release/*` + `hotfix/*`, sem branches de ambiente.

```
1+ branches temporárias → dev → qa → staging → homolog → main
```

| Branch | Papel |
|---|---|
| `dev` | Integração do trabalho em andamento |
| `qa` | Testes |
| `staging` | Ambiente equivalente ao de produção |
| `homolog` | Homologação: validação oficial com o cliente |
| `main` | Produção |

Branches de ambiente são permanentes. Nunca se apaga nenhuma delas.

## Branches temporárias

É onde o trabalho acontece. Nascem de `dev` e sobem para `dev` quando prontas.

Depois do merge, a branch **continua viva por pelo menos duas semanas**. Só
então pode ser apagada. O prazo existe para que a branch ainda esteja lá se
for preciso revisar, comparar ou recuperar algo logo após a integração.

Mudança pequena resolve-se numa única branch temporária. Se for grande e a
divisão fizer sentido, pode-se fazer um **mini fluxo** entre branches
temporárias — várias alimentando uma branch temporária maior — antes de subir
para `dev`.

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

## Hotfix

Bug em produção não espera o fluxo inteiro. A branch sai da `main`, volta para
a `main` e a correção é **propagada para baixo** — `homolog`, `staging`, `qa`,
`dev` — para que nenhum ambiente fique sem ela.

```
main → my-steam/fix/login-crash → main → homolog → staging → qa → dev
```

É a única exceção ao sentido único de promoção.
