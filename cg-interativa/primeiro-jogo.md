# Primeiro jogo

O capítulo anterior demonstrou como iniciar com phaser para criar um jogo, mas tratou apenas das funcionalidades mais básicas: carregar uma imagem, criar um sprite, usar a imagem como textura e posicionar o sprite no mundo. Este capítulo apresenta a criação do jogo "jumper0", que demonstra como funcionam outros recursos do framework.

O código do "jumper0" utiliza o "hello world" como base. O código do arquivo `index.html` muda muito pouco, então trataremos mais diretamente com o conteúdo do elemento `script` responsável pelo código do jogo.

## Carregando recursos

Os recursos \(chamados de _assets_, em inglês\) representam as mídias usadas no jogo, como imagens, _sprite sheets_, áudios e vídeos. Dentre eles, as _sprites sheets_ são muito utilizadas em desenvolvimento de jogos. A figura a seguir ilustra o arquivo `dude.png`, utilizado no código apresentado mais para frente.

![](/assets/sprite-sheet-dude.png)

Um artista do jogo cria uma série de imagens que são usadas para representar as diversas posições de um personagem \(Dude\). Perceba que há transparência \(formato PNG\). Outra coisa importante é que cada "pedaço", por assim dizer, está igualmente distribuído na imagem, na dimensão 32 x 48 pixels. Isso é realmente importante porque tem que se manter padrão para que o carregamento utilizado a seguir funcione.

O trecho de código a seguir mostra a função `preload()`:

```
function preload () {
    game.load.image('sky', '../images/sky.png');
    game.load.image('ground', '../images/platform.png');
    game.load.image('star', '../images/star.png');
    game.load.spritesheet('dude', '../images/dude.png', 32, 48);
}
```

Como já visto, o objeto `game.load` fornece métodos para indicar ao Phaser que ele deve carregar recursos. O método `image()` carrega imagens. De forma semelhante, o método `spritesheet()` carrega um sprite sheet a partir de um arquivo de imagem, mas possui outros dois parâmetros, que representam, respectivamente, a largura e a altura dos sprites.

## Apresentando sprites

O "hello world" utilizou o recurso de posicionar o sprite no centro do mundo. De uma forma mais arbitrária, também é possível posicionar um sprite no mundo diretamente em um par de coordenadas \(x,y\). O trecho a seguir mostra a função create\(\):

```
function create () {
    game.add.sprite(0, 0, 'star');
}
```

O objeto `game.add`, do tipo `GameObjectFactory`, fornece o método `sprite()`, que mostra o sprite chamado "star" na posição definida pelo par de coordenadas `(0, 0)`. O resultado do jogo até então é ilustrado pela figura a seguir.

![](/assets/jumper0-1.png)

Perceba que o sprite está posicionado no canto superior esquerdo ou na posição \(0, 0\).



