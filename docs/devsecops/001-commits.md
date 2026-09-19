# Commits

## Formato

[Conventional Commits](https://www.conventionalcommits.org/), sempre em
**inglês**. A conversa do projeto é em português; o histórico, não.

```
<tipo>(<plataforma ou módulo>): <descrição>
```

O escopo é **sempre obrigatório**: `my-steam` quando a mudança afeta a
plataforma toda, o nome do módulo quando é específica. A mesma regra vale para
o nome das branches — ver [`003-branches.md`](003-branches.md).

Sem espaço antes do parêntese — `feat(store):`, não `feat (store):`. É o que a
especificação exige e o que ferramentas como commitlint esperam.

Tipos: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `poc`.

`poc` marca trabalho experimental e descartável, feito em [`../../pocs/`](../../pocs/).

Descrição no imperativo e em minúscula, sem ponto final:
`feat(my-steam): add game page`.

## Escopo

Os módulos serão nomeados quando o código existir e a divisão ficar clara.
Enquanto não houver módulos, todo commit é da plataforma — `feat(my-steam):`.

## Só título

Commits têm **apenas o título**. Corpo de mensagem só quando for realmente
necessário — tipicamente para registrar o *porquê* de uma decisão que o código
não revela.

Se um commit precisa de parágrafos para ser explicado, em geral ele está
grande demais: o caminho é dividi-lo, não descrevê-lo melhor.

## Coautoria

Commits gerados com o agente levam o trailer de coautoria:

```
Co-Authored-By: <modelo que participou> <noreply@anthropic.com>
```

O nome é o do modelo que de fato escreveu o commit — por exemplo,
`Claude Opus 5`. Não copie o nome de commits anteriores.

É a única exceção à regra de só título: trailer não é descrição, e o histórico
deve deixar claro o que foi escrito em parceria com a IA — o projeto é sobre
desenvolvimento assistido por IA, então isso é informação, não ruído.

## Tamanho e frequência

Commits **pequenos e frequentes**. Um commit, uma mudança coesa.

O motivo é rastreabilidade e auditoria: commit pequeno é fácil de revisar, de
entender meses depois, de localizar num `bisect` e de reverter sem arrastar
junto o que não tem relação.

Na prática:

- Terminou algo que funciona e faz sentido sozinho? Commite.
- Mudanças sem relação entre si vão em commits separados, mesmo que tenham
  sido feitas na mesma sessão.
- Refatoração e mudança de comportamento não andam no mesmo commit.
