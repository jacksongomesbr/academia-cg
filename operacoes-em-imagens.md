# Operações em imagens

## Negativo

O negativo de um pixel é dado por:


$$
I'(p) = (2^b - 1) - I(p)
$$


onde:

* $$I(p)$$ é uma função que retorna o valor do pixel $$p$$
* $$b$$ representa a profundidade de bits da imagem

## Limiarização \(ou Threshold\)

A limiarização consiste em separar uma imagem em duas regiões: frente e fundo. Matematicamente, é representada por:

* $$T(p,t) = 0$$ , se $$0 \leq I(p) \leq t$$  ou 
* $$T(p,t)=1$$, se $$I(p) \gt t$$

Essa separação dos pixels em dois grupos \(frente e fundo\) é uma forma simples de entender uma tarefa complexa em PDI chamada segmentação e imagens \(ou segmentação de objetos da imagem\) em que o objeto é encontrar objetos e separá-los em grupos.

## Operações lógicas e aritméticas

As operações lógicas e aritméticas em imagens são usadas para modificar os valores dos pixels considerando duas imagens, por isso são operações binárias. As operações lógicas usam os conceitos básicos da lógica booleana, enquanto as operações aritméticas utilizam os conceitos da álgebra de matrizes. É importante considerar que:

* as operações lógicas consideram as imagens como sendo binárias, ou seja, contêm pixels com cores preta ou branca, apenas: 0 é falso, 1 é verdadeiro;
* as operações aritméticas devem considerar que o valor resultante da operação para cada banda de cor deve estar no intervalo $$[0, 255]$$

> Embora o valor do pixel seja um número \(natural ou real\) a convenção mais comumente aceita é representá-lo no intervalo $$[0,255]$$



