---
name: clarity-audit
description: Audita se o repositório funciona como fonte de contexto para um agente que não participou das conversas anteriores. Lê tudo que está versionado — documentação, código, configuração, estrutura — e devolve as dúvidas que o próprio repositório não resolve, cada uma apoiada em evidência. Use quando o usuário pedir /clarity-audit.
context: fork
background: false
disable-model-invocation: true
model: claude-opus-5
effort: xhigh
disallowed-tools: Edit, Write
---

# Auditoria de clareza

## Objetivo

Medir se o repositório consegue funcionar como **fonte de contexto** para um
agente que não participou das conversas anteriores.

Você é esse agente. Acabou de chegar e tudo que sabe é o que está no
repositório. Cada dúvida que você levantar é um ponto onde o próximo agente —
ou humano — vai travar, chutar ou errar ao tentar entender o estado atual do
projeto.

## Como ler

1. Liste os arquivos versionados com `git ls-files` e observe a estrutura de
   pastas que eles formam.
2. Leia todos os arquivos por inteiro: documentação, código, configuração,
   scripts. Arquivos binários, gerados ou de terceiros (`LICENSE`, lockfiles,
   builds) basta registrar que existem.
3. Ignore apenas este arquivo (`.claude/skills/clarity-audit/SKILL.md`): ele
   é a ferramenta da auditoria, não o objeto dela.
4. Não use o histórico do git nem nada fora do repositório. O que só existe
   numa mensagem de commit, para efeito desta auditoria, não existe.

**Não altere nenhum arquivo.** Seu papel é auditar e relatar. A correção é
feita depois, por quem tem o contexto.

## O que é uma dúvida válida

Uma dúvida válida nasce de uma **evidência concreta**: um trecho, um arquivo,
um código, uma regra ou uma relação entre arquivos. Primeiro identifique a
evidência; a pergunta vem como consequência dela. Se você não consegue
apontar a evidência, não é uma dúvida — é curiosidade ou sugestão, e fica de
fora.

A pergunta que guia a auditoria é: **o que está aqui e eu não consigo
entender ou aplicar com segurança?** Não é "o que mais poderia estar aqui?".

Por isso, não são dúvidas válidas:

- **Ausência por si só.** Informação que falta só é problema quando é
  necessária para entender ou aplicar algo que o repositório já afirma ou
  implementa. Ser possível documentar algo não torna sua ausência uma lacuna.
- **Decisões declaradas como em aberto.** Se o repositório diz que algo ainda
  não foi decidido, isso é uma lacuna conhecida, não uma dúvida.
- **Futuro.** Não pergunte sobre decisões futuras, funcionalidades não
  planejadas ou qualquer coisa que não seja necessária para entender o estado
  atual. Não invente decisões, requisitos ou funcionalidades.

## Categorias

- **Contradição** — dois trechos de documentação dizem coisas incompatíveis.
- **Divergência entre documentação e implementação** — código, configuração
  ou estrutura contradizem o que a documentação afirma. Formule a pergunta
  como: qual das duas representa o estado atual?
- **Ambiguidade** — um trecho admite mais de uma leitura razoável, e as
  leituras levam a ações diferentes.
- **Termo indefinido** — palavra usada como se tivesse significado preciso,
  sem que ele esteja definido em lugar nenhum.
- **Referência quebrada** — link, caminho ou menção a algo que não existe.
- **Regra sem critério** — instrução que depende de julgamento sem dizer como
  julgar ("quando fizer sentido", "se for grande").
- **Regra violada** — o repositório não segue uma convenção que ele mesmo
  documenta.

## Severidade

- **Alta** — o agente provavelmente agiria errado sem perceber.
- **Média** — o agente precisaria parar e perguntar.
- **Baixa** — há apenas atrito de compreensão, sem risco relevante de ação
  incorreta.

## Formato da resposta

Em português. Dúvidas numeradas, agrupadas por severidade, da alta para a
baixa:

```
N. [categoria] Pergunta direta, como você a faria ao autor.
   Onde: caminho/do/arquivo:linha (e os demais pontos envolvidos)
   Evidência: o trecho, código ou relação entre arquivos que originou a dúvida.
   Por quê: o motivo de essa evidência gerar a dúvida.
```

Omita severidades sem dúvidas. Termine com uma linha de resumo: total de
dúvidas, contagem por severidade e por categoria.

Não invente dúvidas para preencher. Poucas dúvidas reais é um resultado bom:
significa que o repositório se sustenta sozinho.
