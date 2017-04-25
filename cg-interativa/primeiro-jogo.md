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

O objeto `game.add`, do tipo `GameObjectFactory`, fornece o método `sprite()`, que cria um sprite usando a imagem chamada "star" como textura, e o inclui no mundo, na posição definida pelo par de coordenadas `(0, 0)`. O resultado do jogo até então é ilustrado pela figura a seguir.

![](/assets/jumper0-1.png)

Perceba que o sprite está posicionado no canto superior esquerdo ou na posição \(0, 0\).

## Construindo um mundo

Uma das habilidades de um programador de jogos é construir mundos. Visualmente, já sabemos que o Phaser indica que a posição \(0, 0\) representa a origem do plano de coordenadas que representa o mundo. Isso significa que faz parte dessa habilidade desenvolver a prática de posicionar objetos. A figura a seguir ilustra uma etapa do jogo que foi crida usando posicionamento e outros recursos.

![](/assets/jumper0-2.png)

Embora o usuário veja uma cena que parece ter sido construída utilizando um software de edição de imagem, ela é, na verdade, uma composição de várias imagens carregadas anteriormente, em específico, as imagens chamadas "sky" \(o céu, ao fundo\) e "platform" \(plataforma, que está replicada em vários locais\).

O trecho de código a seguir apresenta a função `create()`:

```
var platforms;

function create() {
    game.physics.startSystem(Phaser.Physics.ARCADE);
    game.add.sprite(0, 0, 'sky');
    platforms = game.add.group();
    platforms.enableBody = true;
    var ground = platforms.create(0, game.world.height - 64, 'ground');
    ground.scale.setTo(2, 2);
    ground.body.immovable = true;
    var ledge = platforms.create(400, 400, 'ground');
    ledge.body.immovable = true;
    ledge = platforms.create(-150, 250, 'ground');
    ledge.body.immovable = true;   
}
```

Primeiro, o código chama o método `startSystem()` do objeto `game.physics`, do tipo `Phaser.Physics`, passando como parâmetro o valor `Phaser.Physics.ARCADE`. Isso faz com que um sistema de física chamado "Arcade Physics" seja utilizado.

Na sequência, sprites são adicionados no mundo, começando pelo sprite "sky", que é adicionado na posição \(0, 0\). A textura desse sky representa o fundo \(o céu\).

Um grupo de objetos do jogo é criado por meio do método `group()` do objeto `game.add`, do tipo `GameObjectFactory`. O tipo retornado por esse método é `Phaser.Group`. Inclusive é importante notar que a variável `platforms` é declarada fora da função `create()` para que seja utilizada, posteriormente, por outras funções. Como o jogo utiliza física, o objetivo é tornar as plataformas em áreas que interagem fisicamente com um objeto \(por exemplo, um personagem fica em cima de uma plataforma\). Assim, o atributo `enableBody` recebe o valor `true`.

A partir de então, o objeto `platforms` é utilizado para criar outros objetos \(fazendo com que os mesmos pertençam ao grupo em questão\). Nesse caso, ao invés de utilizar `game.add.sprite()` é usado o método `create()` do objeto `platforms`, que também retorna um objeto do tipo `Phaser.Sprite`. O primeiro sprite é o objeto `ground`, posicionado em 0, 600 \(600 é o valor do atributo `game.world.height`\) e que usa a textura da imagem chamada "ground". O objeto `ground.scale` tem o método `setTo()`, que permite mudar a escala do sprite. No caso, a escala do objeto é modificada para o dobro do tamanho tanto no eixo x quanto no eixo y. Por fim, o objeto ground.body, do tipo `Phaser.Physics.Arcade.Body` tem o atributo `immovable`. Definido com o valor `true`, faz com que o sprite não receba impactos de outros corpos físicos. Isso quer dizer que o valor `false` faria com que, ao colidir com outros objetos, ele se movesse, o que não é desejável.

Outros sprites são adicionados no grupo, em posições diferentes, para representar os níveis superiores da plataforma.

## Adicionando o player

O código a seguir é adicionado ao final da função `create()`:

```
player = game.add.sprite(32, game.world.height - 150, 'dude');
game.physics.arcade.enable(player);
player.body.bounce.y = 0.2;
player.body.gravity.y = 300;
player.body.collideWorldBounds = true;
player.animations.add('left', [0, 1, 2, 3], 10, true);
player.animations.add('right', [5, 6, 7, 8], 10, true);
```

O sprite representado pelo objeto `player` é adicionado no mundo, utilizando como textura a imagem chamada "dude". Importante relembrar que essa textura é um sprite sheet. A física é habilitada usando `game.physics.arcade.enable()`. Além disso, o sprite tem duas animações, criadas usando `player.animations.add()`:

* left: usa os frames 0 a 3 e executa a 10 frames por segundo
* right: usa os frames 5 a 8 e executa a 10 frames por segundo





