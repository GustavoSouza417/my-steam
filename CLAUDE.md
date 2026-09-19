# CLAUDE.md

## Contexto e objetivo

Este repositório é um projeto pessoal de aprendizado: uma cópia da Steam para
a web (loja, biblioteca, perfis, comunidade etc.), construída de forma
incremental. A Steam é a especificação.

O objetivo é duplo:

1. Construir o produto aos poucos, funcionalidade por funcionalidade.
2. Aprender desenvolvimento assistido por IA e a prática de *vibe coding* —
   conversar, decidir e evoluir o código junto com o agente.

O escopo e as decisões de produto já tomadas estão em
[`docs/product/`](docs/product/) — incluindo os jogos em C compilados para
WebAssembly. A stack da plataforma (linguagem, framework, banco, modelo de
dados) **ainda não foi decidida**: não a presuma. Essas decisões serão tomadas
explicitamente, uma de cada vez, junto com o usuário, e registradas em
[`docs/adr/`](docs/adr/).

## Princípios gerais de desenvolvimento

- **Incremental**: uma funcionalidade pequena e funcionando de cada vez.
- **Funcionando antes de bonito**: primeiro o caminho feliz, depois refino.
- **Decisão explícita**: escolhas relevantes são discutidas antes de virar código.
- **Reversível**: prefira caminhos fáceis de desfazer ou trocar depois.
- **Entendível**: o usuário está aprendendo; código óbvio vale mais que código esperto.
- **Escopo fechado**: entregue o que foi pedido, nem mais nem menos.

## Comportamento esperado do agente

- Não tome decisões técnicas estruturais sozinho. Quando houver uma escolha
  relevante (stack, banco, estrutura de pastas, padrão de projeto), **proponha
  uma recomendação com alternativas e justificativa curta**, e espere a decisão.
- Decisões pequenas e óbvias podem ser tomadas direto — apenas avise o que fez.
- Explique o "porquê" das sugestões. O aprendizado é parte da entrega.
- Não invente requisitos. Se algo não foi dito, pergunte ou declare a suposição.
- Não crie arquivos, configurações ou dependências que não foram pedidos.
- Seja honesto sobre limitações, riscos e o que não foi testado.

## Fluxo de trabalho para mudanças

1. **Entender**: confirmar o que será feito e o critério de "pronto".
2. **Propor**: descrever a mudança em poucas linhas antes de codar, se ela
   envolver decisões novas.
3. **Implementar**: a menor mudança que resolve o pedido.
4. **Verificar**: rodar/testar o que for possível e relatar o resultado real.
5. **Relatar**: o que mudou, o que ficou de fora e o que exige decisão futura.

Mudanças grandes devem ser quebradas em etapas menores, cada uma revisável.

### Commits

Conventional Commits, em inglês, título apenas, pequenos e frequentes.
Regras completas em [`docs/devsecops/001-commits.md`](docs/devsecops/001-commits.md).

## Documentação

A documentação vive em [`docs/`](docs/): `product/` (o que construímos),
`devsecops/` (como trabalhamos) e `adr/` (decisões de arquitetura, ainda
vazia). Todos os documentos são numerados. Ver [`docs/README.md`](docs/README.md),
que explica os critérios e onde cada assunto deve ser registrado.

- Documentar o que **não** dá para deduzir lendo o código: decisões, motivos
  e alternativas descartadas.
- Não duplicar em documento o que o código já diz.
- **Ampliar antes de criar**: o padrão é acrescentar a um documento existente.
  Arquivo novo só quando o assunto não couber em nenhum. Muitos documentos
  geram duplicidade e inflam a carga cognitiva de quem acompanha o projeto.
- Ser objetivo: texto curto, sem repetir o que já está dito em outro lugar.
- Manter este arquivo atualizado conforme decisões forem sendo tomadas: quando
  uma escolha tecnológica ou arquitetural for definida, registre-a.
- Documentação curta e no lugar certo é melhor que documentação extensa.

## Evitar complexidade e abstrações prematuras

- Resolva o caso concreto de hoje, não o hipotético de amanhã.
- Nada de camadas, interfaces ou generalizações sem pelo menos dois casos reais.
- Nada de bibliotecas ou ferramentas novas sem necessidade demonstrada.
- Duplicação pontual é aceitável enquanto o padrão ainda não está claro.
- Se uma solução começar a ficar complicada, pare e discuta antes de continuar.
