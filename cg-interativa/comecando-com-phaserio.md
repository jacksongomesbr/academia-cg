# Começando com phaser.io

[phaser.io](http://phaser.io/) é um framework HTML5 para desenvolvimento de jogos em plataforma desktop e mobile. Com a popularização do desenvolvimento front-end, baseado em HTML5, no aumento do desempenho e da popularidade dos browsers, tanto em desktop quanto mobile, a utilização de um framework dessa natureza é bastante razoável. Este capítulo apresenta um guia inícial para o desenvolvimento de jogos com phaser.io.

## Servidor Http

Software desenvolvido com phaser.io precisa ser fornecido para o usuário por meio do protocolo Http. Isso significa que abrir um arquivo html diretamente no browser \(o que irá usar o protocolo `file:///`\) não irá funcionar.

Para resolver essa questão é necessário utilizar um servidor Http para entregar os arquivos do software para o browser. Dentre as várias opções possíveis para isso, vamos utilizar o pacote `http-server` para o NodeJs. No prompt de comando, execute:

```
npm install --save-dev http-server
```

Isso fará com que o `http-server` esteja disponível no caminho `node_modules/.bin/http-server`_ ou _`node_modules/.bin/hs`.

## Download do phaser

O phaser.io está disponível na versão Community Edition \(CE\). Para o desenvolvimento há diversas opções, todas disponíveis na [página de download](http://phaser.io/download/stable):

* clonar o repositório do Github: [https://github.com/photonstorm/phaser-ce](https://github.com/photonstorm/phaser-ce)
* fazer download da versão compilada \(disponível em um arquivo não minimificado, `phaser.js`, e minimificado: `phaser.min.js`\)
* fazer download de um pacote compactado \(Zip ou Tar\), que contém código-fonte, a versão compilada e outros recursos, como documentação e projetos de exemplo
* utilizar npm e instalar o pacote `phaser-ce`

A sugestão é começar com a versão minimificada, por exemplo, fazendo download do arquivo `phaser.min.js` e armazenando-o na pasta `js`.

## Documentação da API

A documentação oficial do phaser.io está disponível em [https://photonstorm.github.io/phaser-ce/](https://photonstorm.github.io/phaser-ce/).

## Hello World e estrutura padrão do software

O código a seguir apresenta o conteúdo do arquivo `helloworld/index.html`:

```
<!doctype html>
<html lang="pt-br">
    <head>
        <meta charset="UTF-8" />
        <title>hello phaser!</title>
        <script src="../js/phaser.min.js"></script>
        <script type="text/javascript">
        var game = new Phaser.Game(800, 600, Phaser.AUTO, '', { preload: preload, create: create });

        function preload () {
            game.load.image('logo', '../images/phaser.png');
        }

        function create () {
            var logo = game.add.sprite(game.world.centerX, game.world.centerY, 'logo');
            logo.anchor.setTo(0.5, 0.5);
        }
        </script>
    </head>
    <body>
    </body>
</html>
```

A parte mais importante do código HTML possui dois elementos `script`. O primeiro representa a importação do framework phaser.io por meio do arquivo `phaser.min.js`. A partir de então, o segundo representa o código do software, em si e será explicado a seguir.

### Classe Game

A classe `Phaser.Game` representa o controlador principal do jogo. Ela é responsável por tratar o processo de boot, analisar arquivos de configuração, criar o renderer e configurar todos os sistemas do Phaser, como física, entrada e som.

A primeira linha do código cria uma instância dessa classe, informando alguns parâmetros:

```
var game = new Phaser.Game(800, 600, Phaser.AUTO, '', { preload: preload, create: create });
```

* primeiros dois parâmetros: representam a geometria \(resolução\) da área do jogo. No caso do exemplo, representa a criação de uma área com 800 x 600 pixels
* terceiro parâmetro: especifica o renderer, que trata das tarefas de desenho no browser. O padrão é `Phaser.AUTO`
* quarto parâmetro: especifica o parent, o componente no qual será criado um elemento `canvas`, usado pelo phaser para as tarefas de desenho. O padrão é `''`
* quinto parâmetro: especifica o objeto `State`, que representa o estado do jogo. No caso do exemplo, o estado do jogo possui duas fases: `preload` e `create`, cada um chamando uma função correspondente

Outra característica importante é que o código cria o objeto `game` e o disponibiliza globalmente para todo o código.

### Classe State

A classe `Phaser.State` representa o estado do jogo. No caso do exemplo são tratados dois estados:

* `preload`: tratado na função `preload()`
* `create`: tratado na função `create()`

#### Estado `preload`

O estado `preload` é o primeiro a ser chamado no ciclo de estados. Geralmente é usado para carregar recursos do jogo, como imagens e fontes. No caso do exemplo, a função `preload()` faz exatamente isso por meio do objeto `game.loader`, do tipo `Phaser.Loader`. Esse objeto, também chamado _loader_, fornece o método `image()`, que recebe os parâmetros:

* `key`: nome da imagem para o jogo \(no caso, chama-se `logo`\)
* `path`: o caminho da imagem \(no caso, `../images/phaser.png`\)

Assim, será possível fazer uma referência à imagem pelo seu nome.

A imagem não é carregada imediatamente logo após a chamada desse método. O arquivo é adicionado em uma fila do loader para ser carregado posteriormente.

#### Estado `create`

O estado `create` é chamado depois do estado `preload`.

No caso do exemplo, na função `create()` o código realizada duas tarefas. Primeiro, cria um _sprite_ e depois configura o seu posionamento na área do jogo.

```
var logo = game.add.sprite(game.world.centerX, game.world.centerY, 'logo');
```

O objeto `game.add`, do tipo `Phaser.GameObjectFactory`, fornece o método `sprite()`, que cria um objeto `Phaser.Sprite` e o posiciona. Aceita os parâmetros:

* `x`: posição na coordenada x
* `y`: posição na coordenada y
* `key`: nome da imagem \(usada como textura\)

No caso do código de exemplo, os valores de x e y são obtidos dos atributos `centerX` e `centerY` do objeto `game.world`, do tipo `Phaser.World`. 

## World

O world, classe Phaser.World, representa um local abstrato, no qual estão todos os objetos do jogo. As câmeras permitem "olhar" para o mundo, tornando os seus objetos visíveis.

O objeto `game.world`, do tipo `Phaser.World`, possui dois atributos usados no código de exemplo:

* `centerX`: retorna a posição x do centro do mundo
* `centerY`: retorna a posição y do centro do mundo

Dessa forma, o código de exemplo cria um sprite e o posiciona no centro do mundo.

## Sprite

O sprite, classe `Phaser.Sprite`, representa uma parte vital do jogo, praticamente todo objeto visual. O sprite mais básico consiste de uma posição, coordenada \(x,y\), e uma textura que é renderizada no canvas. Além disso, contém propriedades para lidar, por exemplo, com física \(`Sprite.body`\), tratamento de entrada \(`Sprite.input`\), eventos \(`Sprite.events`\) e animação \(`Sprite.animations`\).

A classe `Phaser.Sprite` possui o atributo `anchor`, do tipo `Phaser.Point`. Esse atributo define o ponto de origem da textura. O método `setTo()` aceita dois parâmetros, o par de coordenadas x,y, e possui valores-padrões:

* `0,0`: a origem da textura é o canto superior esquerdo
* `0.5,0.5`: a origem da textura é o centro
* `1,1`: a origem da textura é o canto inferior direito

Assim, no caso do código de exemplo, a textura está centralizada. 

