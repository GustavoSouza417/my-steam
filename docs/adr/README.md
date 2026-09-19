# ADRs — Architecture Decision Records

Esta pasta está **intencionalmente vazia**.

Ainda não há decisões de arquitetura tomadas neste projeto. Criar ADRs agora
produziria vários registros pequenos, especulativos e provavelmente
contraditórios entre si.

## Quando criar o primeiro ADR

Quando houver material suficiente para uma decisão real: um problema concreto,
alternativas avaliadas e uma escolha com consequências. Exemplos de gatilhos
plausíveis: escolha de stack, modelo de persistência, forma de autenticação,
separação (ou não) entre front e back.

## Regra

Um ADR registra uma decisão **relevante e já tomada**, não uma intenção.
Se não dá pra escrever "consequências" com honestidade, ainda não é um ADR.

## Numeração

Prefixo `001-`, `002-`, ... em **ordem de criação**. A sequência é o histórico
das decisões do projeto, então números nunca são reaproveitados nem
reordenados. Uma decisão revista entra como um ADR novo que substitui o
anterior — o antigo permanece, marcado como substituído.

O formato interno do documento será definido no primeiro registro.
