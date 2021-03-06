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

Até o momento, quando o player é adicionando no mundo, ele cai. Isso é conseguido por meio da configuração de gravidade do sprite usando `player.body.gravity.y`.  O código atribui o valor 300. Quanto maior o valor, maior é o efeito da gravidade sobre o objeto, fazendo com que ele caia mais rápido. O player não vai sair da tela porque a colisão com os limites da área de visualização do mundo está sendo tratada por meio de `player.body.collideWorldBounds = true`.

Quando o player colide com um dos limites do mundo ou com um corpo físico \(próxima seção\), há uma leve "quicada" na vertical, o que é conseguido por meio de `player.body.bounce.y = 0.2`. O atributo `player.body.bounce.y` é um valor numérico entre 0 \(nenhum quique\) e 1 \(um quique completo\).

## Tratando colisão

Colisões entre objetos representam grande parte do funcionamento de um mecanismo de física em um framework de jogos. Com o código até o momento, o player é adicionado em uma posição do mundo e cai, mas não para sobre o sprite que representa o chão \(ground\). Para fazer isso é necessário tratar colisão em um estado do jogo chamado `update`. A seguir o trecho de código apresenta a função `update()`:

```
function update() {
    game.physics.arcade.collide(player, platforms);
}
```

A função `update()` é chamada a cada frame do jogo. Por essa razão ela é executada no "loop de jogo". A função collide\(\) testa a colisão entre dois objetos. Neste caso, está testando se existe uma colisão entre `player` e `platforms`. Como o segundo é um grupo, então a função testa a colisão entre o `player` e todos os componentes do grupo \(todas as plataformas\).

A partir de então, o player cai ao ser adicionado no mundo, mas fica parado sobre o chão \(ground\).

## Controlando o player com o teclado

O Phaser possui um gerenciador de entrada do usuário a partir do teclado, que pode ser obtido acrescentando a linha de código a seguir ao final da função `create()`:

```
cursors = game.input.keyboard.createCursorKeys();
```

O objeto `cursors` é uma variável declarada fora da função `create()` para poder ser utilizada no restante do código. O tratamento de qual tecla foi pressionada é realizado na função `update()`, cujo código é apresentado a seguir:

```
function update() {
    game.physics.arcade.collide(player, platforms);

    player.body.velocity.x = 0;
    if (cursors.left.isDown)
    {
        player.body.velocity.x = -150;
        player.animations.play('left');
    }
    else if (cursors.right.isDown)
    {
        player.body.velocity.x = 150;
        player.animations.play('right');
    }
    else
    {
        player.animations.stop();
        player.frame = 4;
    }

    if (cursors.up.isDown && player.body.touching.down)
    {
        player.body.velocity.y = -350;
    }            
}
```

Quando a tecla "seta para esquerda" for pressionada o atributo `cursors.left.isDown` será `true` e o código executará a animação "left", usando `player.animations.play()`. Além disso, o atributo `player.body.velocity` é modificado, fazendo com que seja negativo no eixo x \(ou seja, move o player para a esquerda\).

Quando a tecla "seta para direita" for pressionada o atributo `cursors.right.isDown` será `true` e o código executará a animação "right". O player será movido para a direta, atribuindo valor positivo para o atributo `player.body.velocity.x`.

Se nenhuma dessas teclas estiver pressionada, a animação para e o player recebe a textura que está no frame 4.

A última parte do código adiciona a habilidade de pular. O código checa se a tecla "seta para cima" foi pressionada e se o player está tocando o chão \(atributo `player.body.touching.down`\). Se o condicional for verdadeiro, o código aplica uma velocidade vertical negativa de 350 pixels por segundo. O player vai cair novamente de volta para o chão por causa da gravidade aplicada anteriormente.

## Adicionando propósito ao jogo

Até agora o jogo mais parece um "aplicativo interativo". Faltam elementos principais que procurem despertar no jogador um sentimento de desafio e de saber o quanto ele está desempenhando bem ou mal essa tarefa. Para isso, a partir daqui vamos trabalhar para adicionar propósito ao jogo. A estratégia para isso será adicionar estrelas brilhantes que devem ser coletadas pelo jogador. Assim, a principal modificação será na função `create()`:

```
var stars;

function create() {
    // ...
    // criando estrelas
    stars = game.add.group();
    stars.enableBody = true;
    for (var i = 0; i < 12; i++) {
        var star = stars.create(i * 70, 0, 'star');
        star.body.gravity.y = 6;
        star.body.bounce.y = 0.7 + Math.random() * 0.2;
    }    
}
```

O processo é semelhante ao usado anteriormente para criar as plataformas: criar grupos de elementos usando `game.add.group()`. Ainda:

* as estrelas são posicionadas de forma igualmente espaçada \(veja `stars.create()`\)
* as estrelas caem por causa da gravidade \(`star.body.gravity.y = 6`\)
* as estrelas quicam quando caem sobre algum corpo físico

No último caso, a configuração da "quicada" é feita de forma aleatória, entre 0,7 e 0,9.

Agora, o jogo precisa tratar a colisão entre as estrelas e as plataformas. Isso é conseguido por uma alteração na função `update()`adicionando o seguinte:

```
game.physics.arcade.collide(stars, platforms);
```

Da mesma forma, o jogo precisa tratar a colisão entre o player e uma estrela. Dessa vez, não será usada a função `collide()`, mas a função `overlap()` \(ainda na função `update()`\):

```
game.physics.arcade.overlap(player, stars, collectStar, null, this);
```

A função `overlap()` recebe como parâmetros:

* os objetos \(`player` e `stars`\) para os quais deve-se verificar se há uma sobreposição \(outra forma de tratar colisão\)
* uma função callback chamada `collectStar`, para ser executada quando houver uma sobreposição

Importante considerar que a colisão não é tratada entre o player e cada estrela diretamente, mas entre o player e o grupo de estrelas. Quando isso acontece, o Phaser fica responsável por identificar que a colisão deve ser tratada entre o player e cada objeto \(estrela\) do grupo.

A função `collectStar()`recebe dois parâmetros: player e star e, nesse caso, executa a função kill\(\) indicando que a estrela deve ser excluída do jogo:

```
function collectStar(player, star) {
    star.kill();
}
```

Para concluir o jogo, falta indicar para o jogador o quão bom é o seu desempenho ao controlar o player para coletar estrelas. Há várias formas de apresentar informações ao jogador durante o jogo e isso é assunto longo, para outro momento. Vamos adotar uma forma mais simples: apresentar ao jogador, na tela, a sua pontuação, que é acrescentada em 10 pontos para cada estrela coletada. Para isso, são adicionadas duas variáveis ao código e acontece uma modificação na função `create()`:

```
var score = 0;
var scoreText;

function create() {
    // ...

    scoreText = game.add.text(16, 16, 'score: 0', { fontSize: '32px', fill: '#000' });
}
```

A função `game.add.text()` cria um objeto \(`scoreText`\) que representa texto. Os parâmetros indicam a posição do texto na tela, o texto que será apresentado \(começa com pontuação zero\) e algumas propriedades de estilo e apresentação \(tamanho da fonte e cor\).

O objeto scoreText é modificado na função `collectStar()`:

```
function collectStar(player, star) {
    star.kill();
    score += 10;
    scoreText.text = 'Score: ' + score;
}
```

Assim, o código remove do jogo a estrela que colidiu com o player, incrementa a pontuação \(variável `score`\) e atualiza o texto do objeto `scoreText` \(atributo `text`\) para refletir a nova pontuação.

A figura a seguir ilustra o último estágio desse primeiro jogo com Phaser.

![](/assets/phaser-primeiro-jogo-final.png)

Este capítulo apresentou as principais tarefas do desenvolvimento de jogos com Phaser. Para resumir, vimos aqui:

* utilizar sprites para construir um mundo
* utilizar recursos de física e tratar colisão
* controlar o player utilizando o teclado
* apresentar informações textuais na tela





