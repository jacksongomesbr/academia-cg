# Introdução

## O que é Computação Gráfica?

Computação Gráfica \(CG, do inglês _Computer Graphics_\) geralmente está relacionado às seguintes tarefas: **criação**, **armazenamento** e **manipulação** de modelos e imagens.

Os modelos podem surgir de diversas áreas do conhecimento como física, biologia, matemática, arte e estruturas conceituais ou abstratas.

O termo _computer graphics_ foi utilizado pela primeira vez por _William Fetter_, em 1960, para descrever novos métodos de projeto durante o desenvolvimento de novos _cockpits_ para a _Boeing_. Em 1966 ele disse \(tradução nossa\):

> Talvez a melhor maneira de definir _computer graphics_ é descobrir o que é e o que não é. Não é uma máquina. Não é um computador, nem um grupo de programas de computador. Não é o conjunto de habilidades de um projetista, nem de um programador, escritor ou especialista em filmes.
>
> _Computer graphics_ é tudo isso -- uma tecnologia conscientemente gerenciada e documentada voltada para a **comunicação de informação** de forma precisa e descritiva.

Na prática, representar modelos e imagens utilizando computação gráfica requer técnicas bem estabelecidas e padronizadas. Além disso, é necessário também interagir com estes modelos e imagens, o que aumenta a complexidade do problema e também a sua área de abrangência.

## O que é Computação Gráfica Interativa?

Os elementos básicos de um sistema de gráficos interativos envolve:

* **entrada** \(ex.: mouse, tela de toque\)
* **processamento e armazenamento**
* **apresentação** \(ou **saída**\) \(ex.: tela, impressora\)

O primeiro sistema gráfico plenamente interativo foi o _Sketchpad_, desenvolvido em 1963 por Ivan Sutherland na sua tese de doutorado \(_Sketchpad, a Man-Machine Graphical Communication System_\). A figura a seguir ilustra a utilização do sistema.

![](/assets/ivan-sutherland-sketchpad.png)

Um vídeo da época apresenta mais detalhes: [https://www.youtube.com/watch?v=J6UAYZxFwLc](https://www.youtube.com/watch?v=J6UAYZxFwLc).

Na sua tese sobre o _Sketchpad_, Ivan Sutherland escreveu \(tradução nossa\):

> O sistema Sketchpad usa o desenho como um novo meio de comunicação para o computador. O sistema contém entrada, saída e programas de computador que o permitem interpretar informação desenhada diretamente na tela do computador. Sketchpad mostrou-se útil como auxílio no entendimento do processo, como na movimentação de objetos, que pode ser descrita por figuras. Sketchpad também torna fácil criar desenhos repetitivos e precisos e alterar desenhos feitos anteriormente com ele.

Além do formato interativo \(comum quando se deseja interação\) há o formato _batch_, usado quando se deseja representação.

## O que é Computação Gráfica Batch?

A Computação Gráfica em formato _batch_ é não-interativa, também é conhecida como _renderização offline_. Geralmente, é utilizada em tarefas de pós-produção de vídeos e filmes \(especialmente para efeitos especiais\).

Recentemente, para o filme _The Good Dinosaur_ \(_Disney/Pixar, 2016_\) a renderização de um quadro de filme \(_frame_\) demorou, em média, 48 horas, isso utilizando um sistema da _Pixar \_conhecido como \_Render Farm_, que é composto por 30 mil núcleos.

Quer ler um pouco mais sobre isso? Leia o artigo _Making the world of Pixar's The Good Dinosaur_ \([https://www.fxguide.com/featured/making-the-world-of-pixars-the-good-dinosaur/](https://www.fxguide.com/featured/making-the-world-of-pixars-the-good-dinosaur/)\).

Na verdade, vamos um pouco além. Independentemente de você curtir ou não filmes de animação, já parou para pensar nas etapas envolvidas no processo e como a computação gráfica é utilizada? Uma colaboração entre _Pixar \_e \_Khan Academy \_resuultou no curso \_Pixar in a Box_ \([https://pt.khanacademy.org/partner-content/pixar-latam/](https://pt.khanacademy.org/partner-content/pixar-latam/)\). O curso mostra as etapas do jeito Pixar de criar filmes de animação. Dê uma olhada. O vídeo a seguir mostra uma visão geral.

[![](/assets/intro-scene-pixar-in-a-box.png)](https://www.youtube.com/watch?v=3Iu1Z0h1i1Y)

## Computação Gráfica moderna

A evolução da Computação Gráfica está diretamente ligada à evolução do hardware. Lembra da _Lei de Moore_? Segundo essa "lei", a cada 12 a 18 meses, o poder computacional dobra, enquanto o tamanho diminui. Por exemplo, as novas CPUs da Intel, com arquitetura de 64-bits, têm de 2 a 18 núcleos. Além disso, há também a evolução das placas gráficas: placas da linha GTX Titan, da NVIDIA, chegam a ter 3072 núcleos e 12 GB de memória, resultando em 7 teraflops de processamento.

Para ver um pouco mais sobre essa evolução, veja o vídeo: [https://www.youtube.com/watch?v=jznazEHJKiY](https://www.youtube.com/watch?v=jznazEHJKiY).

Além do hardware relacionado para produção e reprodução há também o relacionado aos dispositivos de entrada. Você poderia dizer: "tudo começou com o mouse...". Isso é praticamente senso comum. Entretanto, em termos de evolução, o conceito atual está mais ligado com "seu corpo é o controlador". As iniciativas mais populares são o _Kinect_, da Microsoft, _Leap Motion \_e \_Nimble UX_. Veja só o nível atual: [https://www.youtube.com/watch?v=vALW9fVOXHQ](https://www.youtube.com/watch?v=vALW9fVOXHQ).

Claramente, não para por aí. Os tempos atuais mostram uma enorme quantidade de dispositivos \(quase nem sempre considerados como "computacionais"\), como os smartphones e os smartwatches. Ainda, a indústria \(re\)descobriu mais recentemente a interação com o usuário por meio de Realidade Virtual e Realidade Aumentada. O que deu origem a uma nova corrida por um mercado ávido por tecnologia de ponta para aplicações mais diversas, de games a cirurgia médica e arquitetura. É claro que antes de chegarmos a uma aplicação mais profunda, consciente e nobre dessa tecnologia, há alguns ~~tropeços~~ aprendizados. Veja só: [https://www.youtube.com/watch?v=SlD-Yo9q2so](https://www.youtube.com/watch?v=SlD-Yo9q2so).

É claro que a evolução não é exclusiva do hardware. O software também precisa evoluir \(e o tem feito\):

* Algoritmos e estruturas de dados
  * Modelagem de materiais
  * Renderização de fenômenos naturais
  * Melhoria do desempenho de estruturas de dados para tarefas de _ray tracing_ e renderização
* Paralelização
* Computação distribuída e em nuvem
  * Envie operações para _cloud_ e receba o resultado de volta, não importa como
  * Renderização disponível como um serviço de internet

## Hardware de telas

Em termos práticos, a tela apresenta ou desenha um gráfico. As duas formas mais comumente utilizadas são **gráficos vetoriais** e **gráficos raster.**

Os gráficos vetoriais representam o desenho por uma série de comandos \(ex.: `move(x, y)`, `line(x, y)` ...\). Enquanto isso, os gráficos raster são formados por uma matriz de **pixels**. De outra forma, os gráficos vetoriais são baseados em geometria, enquanto os gráficos raster são baseados em amostragem \(_sampling_\).

![](/assets/raster-vs-vector.png)

### Gráficos baseados em raster

Por serem baseados em amostragem, os gráficos _raster _usam amostras discretas para descrever informação visual. Neste processo, os pixels podem ser criados no processo de digitalização de imagens \(usando _scanner_, por exemplo\). 

Um **Pixel** \(termo que vem de _picture element_\) representa a localização de um ponto \(em um espaço amostral\) associado a outras informações, como cor \(intensidade de luz\) e transparência.

A grande vantagem deste processo de representação de imagem é que, uma vez que ela está representada em termos de cores numa posição \(x,y\) em uma matriz, é possível alterá-la facilmente, seja alterando posição ou cor.

A grande desvantagem é a perda de informação \(qualidade\) durante ampliação e redução da imagem e não ser possível representar informação adicional \(como profundidade, já que a imagem é, naturalmente, um plano 2D\).

### Gráficos baseados em geometria

Nos gráficos baseados em geometria \(vetores\) são criados modelos geométricos \(modelos matemáticos, se preferir\) compostos por vários atributos \(cor, propriedade do material etc.\) e, num segundo momento, são _renderizados _para que seja possível vê-los conforme a necessidade do contexto \(processo chamado _síntese ou produção de imagem_\). Este tipo de gráfico não está limitado ao plano 2D, podendo ser também representado em 3D, 2D animado \(2D + tempo\) e 3D animado \(3D + tempo\).

Os elementos geométricos são chamados _primitivas_ \(ou _formas_\). É a combinação deles que permite criar modelos geométricos que, posteriormente, serão transformados em imagens. De outra forma, um modelo complexo é decomposto em partes menores, mantendo uma relação de hierarquia. 

Por exemplo, a figura a seguir ilustra esse processo considerando a composição de um prego por primitivas geométricas \(cones e cilindros\) que podem passar por _transformações_.

![](/assets/geometric-model-composition-decomposition.png)

As transformações aplicadas a primitivas geométricas são:

* **Translação: **a mudança de posição de um ponto \(x,y\) para o ponto \(z, w\)
* **Escala: **a mudança de tamanho
* **Rotação:** a alteração da posição no eixo de rotação

Pode-se representar essa representação na forma de árvore, como ilustra a figura a seguir.

![](/assets/screw-hierarchical-composition.png)

Quando a informação do modelo geométrico está representada desta forma para ser renderizado, usa-se o termo _scene graph _\(ou grafo de cena\).

Embora esse processo pareça simples \(e é\) a sua repeti-lo e alterá-lo permite gerar representações complexas, como a mostrada no vídeo a seguir.

[![](/assets/complex-eye-rendering.png)](https://www.youtube.com/watch?v=TAZIvyAJfeM)

Quer testar como anda a sua percepção? Olha só:

[![](/assets/fake-or-foto.png)](http://area.autodesk.com/fakeorfoto)



