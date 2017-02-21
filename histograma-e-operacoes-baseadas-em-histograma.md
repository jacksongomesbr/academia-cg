# Histograma de imagem e operações baseadas em histograma

Histograma representa a probabilidade ou a distribuição dos valores de intensidade presentes nos pixels de uma imagem. Pode ser representado de quatro formas:

* Histograma básico
* Histograma normalizado
* Histograma acumulado
* Histograma acumulado normalizado

O histograma também é conhecido com PDF \(Função de Densidade de Probabilidade\). Estatisticamente, o histograma representa a probabilidade de ocorrer um valor de intensidade na imagem.

## Histograma básico

O histograma básico é uma função que gera a distribuição dos valores de intensidade presentes em uma imagem. Em termos matemáticos, tem-se:


$$
h(I,l) = \sum_{p \in I} \mbox{ se } p = l
$$


A função $$h$$ resulta em um vetor de $$2^b$$ elementos onde:

* $$b$$ representa a profundidade de bits da imagem
* $$l$$ corresponde a um valor de intensidade no intervalo $$[0,2^b-1]$$

A função $$h$$ deve ser aplicada para cada nível de intensidade presente na imagem. Por exemplo, para calcular a quantidade de pixels com intensidade $$150$$ usa-se $$h(I,150)$$. Para uma imagem com $$8$$ bit de cores, seria necessário calcular o conjunto:


$$
\{ h(I,l) \mid l \in \{0, ..., 255\} \}
$$
De um modo geral deseja-se encontrar o conjunto:


$$
\{ h(I,l) \mid l \in \{0, ..., (2^b - 1)\} \}
$$


## Histograma normalizado

O histograma normalizado é baseado no histograma básico \(não normalizado\). Em termos matemáticos, tem-se:


$$
h_{\mbox{norm}}(I,l) = \frac{h(I,l)}{M \times N}
$$


Onde $$M \times N$$ é o número total de pixels na imagem. O valor da função $$h_{\mbox{norm}}$$ está no intervalo $$[0,1]$$ .

## Histograma acumulado

O histograma acumulado assemelha-se ao histograma não normalizado. A diferença é que aplica-se a equação:


$$
\begin{align*}
h_{\mbox{acum}}(I,l) &= h(I,l) + h(I,l-1), \mbox{ para } l \gt 0 \mbox{ e }\\
h_{\mbox{acum}}(I,l) &= h(I,l), \mbox{ para } l = 0 
\end{align*}
$$


ou


$$
h_{\mbox{acum}}(I,l) = \sum_{j=0}^{l} h(I,j)
$$


## Histograma acumulado normalizado

O histograma acumulado normalizado reúne os conceitos dos histogramas normalizado e acumulado. Sua representação matemática é a seguinte:


$$
\begin{align*}
h_{\mbox{acum_norm}}(I,l) &= h_{\mbox{norm}}(I,l) + h_{\mbox{norm}}(l-1), \mbox{ para } l \gt 0 \mbox{ ou } \\ 
h_{\mbox{acum_norm}}(I,l) &= h_{\mbox{norm}}(I,l), \mbox{ para } l = 0
\end{align*}
$$


ou


$$
h_{\mbox{acum_norm}}(I,l) = \sum_{j=0}^{l} h_{\mbox{norm}}(I,j)
$$


## Histogramas de imagens coloridas \(multibandas\)

As funções de histogramas apresentadas anteriormente consideram imagens em tons de cinza \(uma única banda\). No caso de imagens coloridas, como sistemas de cores as representam utilizando mais de uma banda, é necessário encontrar o histograma  para cada banda de cor. Por exemplo, no caso de uma imagem com cores representadas em RGB, seria necessário encontrar o histograma para as bandas R \(vermelho\), G \(verde\) e B \(azul\).

## Equalização de histograma

A equalização de histograma é uma operação de processamento de imagem que tem como objetivo realçar a imagem, aproximando o histograma da imagem de um histograma uniforme. Para isso, usa-se a função $$h_{\mbox{acum_norm}}$$ da seguinte forma:


$$
I' = h_{\mbox{acum_norm}}(I, l) \times (2^b - 1), \forall p \in I \wedge \forall l \ in \{0, ..., (2^b-1)\}
$$
 

> ## Exercício
>
> 1\) Implemente as funções de histograma \(básico, normalizado, acumulado e acumulado normalizado\), aplique-as sobre uma imagem \(de sua escolha\) e apresente seus gráficos.
>
> 2\) Implemente a operação de equalização de histograma sobre uma imagem \(de sua escolha\) e apresente a imagem resultante. Comente os resultados obtidos.



