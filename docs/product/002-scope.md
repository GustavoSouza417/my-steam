# Escopo

Os domínios do sistema e o vocabulário de cada um. Define **o que as coisas
são** e como as chamamos — a linguagem usada em conversas, documentos e código.

A lista de funcionalidades e o que já existe estão em
[`003-backlog.md`](003-backlog.md).

## Loja

Onde o usuário descobre e adquire **jogos**. Um jogo tem página própria com
mídia, descrição, preço e avaliações. Pode ser colocado na **wishlist**,
adicionado ao **carrinho** e comprado — com pagamento sempre simulado.
Preços variam por **promoção**.

## Biblioteca

Os jogos que o usuário já possui. Um jogo na biblioteca tem um **estado**
(não instalado, instalado, em execução) e acumula **tempo jogado**.

## Conta e perfil

O **usuário**: credenciais, **perfil** público (vitrine, nível, badges) e
**carteira** com saldo simulado. Compras saem da carteira.

## Social

Relações entre usuários: **amigos**, **chat** e o **feed de atividades**
do que os amigos andaram fazendo.

## Comunidade

Conteúdo produzido por usuários em torno dos jogos: **reviews** (positiva ou
negativa, com votos de utilidade), **discussões**, **guias**, **grupos** e
**conquistas**.

## Economia de itens

Itens virtuais que os usuários possuem e negociam: **inventário**, **mercado**
(compra e venda entre usuários) e **trocas**. Tudo simulado.

## Publicação

O lado de quem oferta: **desenvolvedores** que cadastram e gerenciam seus
jogos, e a **administração** da plataforma (moderação, curadoria).

## Distribuição e execução

Como o jogo sai da loja e chega a rodar. Nada aqui é simulado na interface: o
**download** traz arquivos de verdade, a **instalação** grava esses arquivos
numa pasta real na máquina do usuário (como a Steam faz) e a **execução** roda
o jogo.

### O que é um "jogo"

Cada jogo é um "Hello World" em C compilado para **WebAssembly**, que imprime
o próprio nome ao rodar. O jogo é artefato de teste, não produto — o que está
sendo construído é a plataforma ao redor dele. Isso torna barato gerar dezenas
de títulos e permite rodar tudo no navegador, sem cliente nativo.

O catálogo é inventado: títulos, capas, descrições, gêneros, tags, preços,
datas, desenvolvedores e publishers fictícios. Nada de jogos reais.

### Save e telemetria

O **save** pertence ao jogo e é um contador: quantas vezes o jogador já abriu
aquele título. O jogo exibe esse número junto do próprio nome ao rodar. Fica
na nuvem, não no disco — reinstalar ou trocar de máquina preserva a contagem.

A **telemetria** pertence à plataforma: tempo jogado, sessões, última vez
jogado, conquistas. São coisas distintas e não devem ser confundidas.

### Overlay

Camada da plataforma sobre o jogo em execução (amigos, chat, conquistas,
capturas). Como o jogo roda no navegador, é uma camada sobre o canvas do jogo.

### Fluxo alvo

Compra → biblioteca como *não instalado* → instalar (download com progresso
real, arquivos gravados em disco) → *instalado* → jogar (o WebAssembly roda e
exibe o nome do jogo e o contador de aberturas) → tempo de sessão vira tempo
jogado.
