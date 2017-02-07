# Processamento Digital de Imagens

## Modelo matemático de formação de imagem

Uma imagem pode ser definida como uma função bidimensional $$f(x,y)$$ em que $$x$$ e $$y$$ são coordenadas espaciais \(plano\) e a amplitude de $$f$$ em qualquer par de coordenadas $$(x,y)$$ é chamada **intensidade** ou **nível de cinza** da imagem nesse ponto. Quando $$x$$, $$y$$ e os valores de intensidade de $$f$$ são quantidades finitas e discretas, chamamos de **imagem digital**.

A função $$f(x,y)$$ pode ser caracterizada por dois componentes:
1. **iluminação**: representada por $$i(x,y)$$, indica a quantidade de iluminação da fonte que incide na cena que está sendo vista; e
2. **refletância**: representada por $$r(x,y)$$, indica a quantidade de iluminação refletida pelos objetos na cena.

Ao combinar as duas funções temos:

$$
f(x,y) = i(x,y) \times r(x,y)
$$

onde:
* $$0 \lt i(x,y) \lt \infty$$
* $$0 \lt r(x,y) \lt 1$$

Os limites da refletância são chamados de: 
* $$0$$: absorção total
* $$1$$: refletância total 

## Representação do pixel (valores de intensidade)

A imagem digital é composta por elementos chamados **pixels**, cada qual armazenando um valor de intensidade. O valor de intensidade é representado em um intervalo:

$$
[0, 2^b - 1]
$$

onde $$b$$ representa a quantidade de bits ou a **profundidade de bits** da imagem. Geralmente, este valor é limitado em 8 bits por banda do espectro de cor. No caso de imagens monocromáticas, há apenas uma banda (por isso são geralmente chamadas **imagens em tons de cinza**). No caso de imagens coloridas, pode haver mais de duas bandas. O sistema de cor RGB (do inglês _Red, Green, Blue_) representa três bandas baseadas nas cores primárias vermelho, verde e azul.

A forma mais comum de representar $$f$$ é a matricial, em que os pixels possuem coordenadas $$(x, y)$$ conforme os eixos: $$x$$ representando colunas e $$y$$ representando linhas.

Outra forma de representar $$f$$ é utilizando um vetor em que a relação entre o índice do vetor e o pixel da matriz é dada por:

$$
i = x + M \times y, \mbox{ com } x=0...M-1 \mbox{ e } y = 0...N-1
$$

As posições $$x$$ e $$y$$ de um pixel para um índice $$i$$ do vetor podem ser obtidas por:

$$
x = i \mbox{ mod } M \\
y = \frac{i}{M}
$$

> Sugestão de leitura: Capítulo 1 de \(GONZALEZ e WOODS, 2011\)





