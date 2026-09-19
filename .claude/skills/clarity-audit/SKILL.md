---
name: clarity-audit
description: Audita o quanto a documentação do repositório se explica sozinha para um agente sem contexto de conversa. Lê tudo que está versionado e devolve as dúvidas que o texto não resolve — contradições, ambiguidades, termos indefinidos, referências quebradas. Use quando o usuário pedir /clarity-audit ou quiser testar se um agente novo entenderia o projeto.
context: fork
disable-model-invocation: true
---

# Auditoria de clareza

Você é um agente que acabou de chegar a este repositório. Não participou de
nenhuma conversa sobre ele. Tudo que você sabe é o que está escrito nos
arquivos.

Sua tarefa é levantar as dúvidas que surgem **só pelo que está escrito**. O
resultado mede o quanto a documentação se sustenta sozinha: cada dúvida é um
ponto onde o próximo agente — ou humano — vai travar, chutar ou errar.

## Como ler

1. Liste os arquivos versionados com `git ls-files`.
2. Leia **todos por inteiro**, exceto `LICENSE` e o conteúdo de `.claude/`
   (esta skill não faz parte do que está sendo auditado).
3. Não use o histórico do git nem nada fora do repositório. Se uma informação
   só existe numa mensagem de commit, para efeito desta auditoria ela não
   existe.

Não edite nenhum arquivo. Seu papel é apontar, não corrigir — a correção é
feita depois, por quem tem o contexto.

## O que conta como dúvida

- **Contradição**: dois trechos que dizem coisas incompatíveis.
- **Ambiguidade**: um trecho que admite mais de uma leitura razoável, e as
  leituras levam a ações diferentes.
- **Termo indefinido**: palavra usada como se tivesse significado preciso, sem
  que ele esteja definido em lugar nenhum.
- **Referência quebrada**: link, caminho ou menção a algo que não existe.
- **Regra sem critério**: instrução que depende de julgamento sem dizer como
  julgar ("quando fizer sentido", "se for grande").
- **Regra violada**: o próprio repositório contradiz uma convenção que ele
  documenta.

## O que não conta

Coisas que a documentação **declara** como ainda não decididas não são
dúvidas — são lacunas conhecidas. "Qual framework vamos usar?" não é uma
dúvida válida se o texto diz que a stack não foi escolhida.

Questione o que está escrito, não o que ainda não foi planejado. A pergunta
certa não é "o que falta aqui?", e sim "o que está aqui e não consigo
entender ou aplicar com segurança?".

## Severidade

- **Alta** — um agente provavelmente agiria errado sem perceber.
- **Média** — um agente teria que parar e perguntar.
- **Baixa** — atrito de leitura, sem risco de ação errada.

## Formato da resposta

Em português. Dúvidas numeradas, agrupadas por severidade (alta primeiro).
Cada uma com:

```
N. [categoria] Pergunta direta, como você a faria ao autor.
   Onde: caminho/do/arquivo.md:linha (e outros trechos envolvidos)
   Por quê: o que no texto gerou a dúvida, citando o trecho.
```

Termine com uma linha de resumo: total de dúvidas, contagem por severidade e
por categoria.

Se não encontrar nenhuma dúvida numa severidade, omita o grupo. Não invente
dúvidas para preencher — uma auditoria com poucas dúvidas reais é um resultado
bom, não um resultado fraco.
