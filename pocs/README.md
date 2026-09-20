# PoCs

Experimentos para responder perguntas técnicas antes de decidir arquitetura.

Na raiz de `pocs/` ficam apenas este índice e o [`template.md`](template.md).
As PoCs em si vivem em `experiments/`, cada uma na sua subpasta, numerada por
**ordem de criação** — a sequência é histórica, como a dos [ADRs](../docs/adr/):

```
pocs/experiments/001-experiment-name/
```

## O que é código de PoC

Código **descartável**. Existe para responder uma pergunta e não precisa ser
bonito, testado, organizado nem reaproveitado. As convenções do projeto
valem para nomes de arquivos e pastas; o resto é liberdade.

PoC não vira produção. Quando a funcionalidade real for construída, ela é
escrita do zero, com o aprendizado da PoC — não copiando o código dela.

## O que cada PoC entrega

Um `README.md` na própria pasta, copiado de [`template.md`](template.md).

Ele nasce com título, metadados, pergunta e hipótese — antes de qualquer
código. "Como rodar", "Ambiente" e "O que foi feito" crescem durante o
experimento; "Resultados", "Veredito" e "O que ficou de fora" só no fim.

O **timebox** é combinado antes de começar e é um limite, não uma estimativa:
estourou, o experimento para e o veredito é escrito com o que houver — mesmo
que seja `inconclusiva`. PoC que não termina deixa de ser barata, e é o custo
baixo que a torna descartável.

Se a resposta levar a uma decisão de arquitetura, ela vira um ADR em
[`docs/adr/`](../docs/adr/). O ADR é o resultado que sobrevive; o código fica
como evidência de que a decisão foi testada, não imaginada.

## Índice

Registro novo entra **no topo** — os mais recentes primeiro.

Status: `planejada` · `em desenvolvimento` · `concluída` · `abandonada`

A data é a de criação do registro. A pasta da PoC só é criada quando ela entra
`em desenvolvimento` — até lá, o índice mostra o nome sem link. O andamento e
as conclusões ficam no `README.md` da própria PoC.

| PoC | Pergunta | Autor | Status | Data |
|---|---|---|---|---|
| 001-wasm-game-pipeline | Dá para baixar, instalar numa pasta real da máquina e executar um jogo WebAssembly pelo navegador? | GustavoSouza417 | planejada | 2026-09-19 |
