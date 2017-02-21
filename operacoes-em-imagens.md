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

### Operação lógica AND

A operação lógica AND utiliza a tabela verdade da operação lógica correspondente para gerar uma imagem binária que corresponde à intersecção dos pixels das duas imagens de entrada, considerando a seguinte equação:


$$
C_{i,j}=A_{i,j} \wedge B_{i,j}
$$
Onde $$A_{i,j}$$ representa o pixel $$(i,j)$$ da imagem $$A$$.

### Operação lógica OR

A operação lógica OR utiliza a tabela verdade da operação lógica correspondente para gerar uma imagem que resulta da união dos pixels de duas imagens de entrada, considerando a seguinte equação:


$$
C_{i,j} = A_{i,j} \vee B_{i,j}
$$


### Operação aritmética ADD \(soma\)

A operação ADD é uma operação de soma. Na prática, é realizada uma operacão tradicional de soma dos valores dos pixels para gerar uma nova imagem. A equação a seguir representa a operação ADD:


$$
C_{i,j} = A_{i,j} + B_{i,j}
$$


### Outras operações aritméticas

A seguir, as equações de outras operações aritméticas:

Operação **SUB \(subtração\):**


$$
C_{i,j} = A_{i,j} - B_{i,j}
$$
Operação** MULT \(multiplicação\)**:


$$
C_{i,j} = A_{i,j} \times B_{i,j}
$$
Operção **DIV \(divisão\)**:


$$
C_{i,j} = A_{i,j} \div B_{i,j}
$$


### Operação de escalonamento

A operação de escalonamento é utilizada para manter um valor dentro de um intervalo, considerando um conjunto de valores, o valor mínimo e o valor máximo. A equação a seguir apresenta a sua formulação matemática:


$$
r = \frac{M}{t_{max} - t_{min}} \times (t - t_{min})
$$


onde:

* $$M$$ é o limite superior desejado \(por exemplo, $$255$$\)
* $$t_{max}$$ é o maior valor de pixel encontrado na imagem
* $$t_{min}$$ é o menor valor de pixel encontrado na imagem
* $$t$$ é o valor de pixel que se deseja escalonar

> ## Exercícios
>
> 1\) Implemente as operações matemáticas e aritméticas, bem como a função de escalonamento. 
>
> 2\) Escolha uma operação lógica e aplique-a considerando duas imagens coloridas.



