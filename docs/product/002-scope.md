# Escopo

Os domínios do sistema e o vocabulário de cada um. Define **o que as coisas
são** e como as chamamos — a linguagem usada em conversas, documentos e código.

Cada termo traz entre parênteses o nome em inglês usado no código — em
identificadores, módulos e rotas. Ao nomear algo que representa um conceito
daqui, use esse termo, não uma tradução própria.

A lista de funcionalidades e o que já existe estão em
[`003-backlog.md`](003-backlog.md).

## Loja (`store`)

Onde o usuário descobre e adquire **jogos** (`game`). Um jogo tem página própria com
mídia, descrição, preço e avaliações. Pode ser colocado na **wishlist** (`wishlist`),
adicionado ao **carrinho** (`cart`) e comprado — com pagamento sempre simulado.
Preços variam por **promoção** (`discount`).

## Biblioteca (`library`)

Os jogos que o usuário já possui. Um jogo na biblioteca tem um **estado** (`state`)
(não instalado, instalado, em execução) e acumula **tempo jogado** (`playtime`).

## Conta e perfil (`account`)

O **usuário** (`user`): credenciais, **perfil** (`profile`) público (vitrine, nível, badges) e
**carteira** (`wallet`) com saldo simulado. Compras saem da carteira.

## Social (`social`)

Relações entre usuários: **amigos** (`friend`), **chat** (`chat`) e o **feed de atividades** (`activity feed`)
do que os amigos andaram fazendo.

## Comunidade (`community`)

Conteúdo produzido por usuários em torno dos jogos: **reviews** (`review`) (positiva ou
negativa, com votos de utilidade), **discussões** (`discussion`), **guias** (`guide`), **grupos** (`group`) e
**conquistas** (`achievement`).

## Economia de itens (`economy`)

Itens virtuais que os usuários possuem e negociam: **inventário** (`inventory`), **mercado** (`market`)
(compra e venda entre usuários) e **trocas** (`trade`). Tudo simulado.

## Publicação (`publishing`)

O lado de quem oferta: **desenvolvedores** (`developer`) que cadastram e gerenciam seus
jogos, e a **administração** (`admin`) da plataforma (moderação, curadoria).

## Distribuição e execução (`distribution`)

Como o jogo sai da loja e chega a rodar. Nada aqui é simulado na interface: o
**download** (`download`) traz arquivos de verdade, a **instalação** (`install`) grava esses arquivos
numa pasta real na máquina do usuário (como a Steam faz) e a **execução** (`launch`) roda
o jogo.

Isso é **requisito de produto**. A viabilidade técnica — como o navegador
alcança uma pasta real — será validada na
[PoC 001](../../pocs/README.md). Se ela mostrar que é inviável, o requisito
volta para discussão.

### O que é um "jogo"

Cada jogo é um "Hello World" em C compilado para **WebAssembly** (`wasm`), que imprime
o próprio nome ao rodar. O jogo é artefato de teste, não produto — o que está
sendo construído é a plataforma ao redor dele. Isso torna barato gerar dezenas
de títulos e permite rodar tudo no navegador, sem cliente nativo.

O catálogo é inventado: títulos, capas, descrições, gêneros, tags, preços,
datas, desenvolvedores e publishers fictícios. Nada de jogos reais.

### Save e telemetria

O **save** (`save`) pertence ao jogo e é um contador: quantas vezes o jogador já abriu
aquele título. O jogo exibe esse número junto do próprio nome ao rodar. Fica
na nuvem, não no disco — reinstalar ou trocar de máquina preserva a contagem.

A **telemetria** (`telemetry`) pertence à plataforma: tempo jogado, sessões, última vez
jogado, conquistas. São coisas distintas e não devem ser confundidas.

### Overlay (`overlay`)

Camada da plataforma sobre o jogo em execução (amigos, chat, conquistas,
capturas). Como o jogo roda no navegador, é uma camada sobre o canvas do jogo.

### Fluxo alvo

Compra → biblioteca como *não instalado* → instalar (download com progresso
real, arquivos gravados em disco) → *instalado* → jogar (o WebAssembly roda e
exibe o nome do jogo e o contador de aberturas) → tempo de sessão vira tempo
jogado.
