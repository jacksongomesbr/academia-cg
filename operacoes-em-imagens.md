# Operações em imagens

## Negativo

O negativo de um pixel é dado por:


$$
I'(p) = 2^b - 1 - I(p)
$$
onde:

* $$I(p)$$ é uma função que retorna o valor do pixel $$p$$
* $$b$$ representa a profundidade de bits da imagem

## Limiarização \(ou Threshold\)

A limiarização consiste em separar uma imagem em duas regiões: frente e fundo. Matematicamente, é representada por:

* $$T(p,t) = 0$$ , se $$0 \leq I(p) \leq t$$  ou 
* $$T(p,t)=1$$, se $$I(p) \gt t$$





