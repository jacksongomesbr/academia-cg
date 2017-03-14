# Filtragem Espacial

O termo "filtro" refere-se a aceitar \(deixar passar\) ou rejetiar certos componentes. Por exemplo, um filtro que aceita baixas frequências é chamado "passa-baixa", cujo efeito é borrar \(suavizar\) uma imagem.

Um filtro espacial consiste de:

1. uma vizinhança \(normalmente um retângulo pequeno\)
2. uma operação predefinida realizada sobre os pixels da imagem incluídos na vizinhança

Uma imagem processada \(filtrada\) é gerada à medida que o centro do filtro percorre cada pixel na imagem de entrada. A figura a seguir ilustra esse processo.

  
![](/assets/filtragem-espacial-mascara-3-3.png)

Em qualquer ponto $$(x,y)$$ da imagem, a resposta, $$g(x,y)$$, do filtro é a soma dos produtos dos coeficientes do filtro com os pixels da imagem englobados pelo filtro:


$$
g(x,y) = w(-1,-1) \times f(x-1, y-1) + w(-1,0) \times f(x-1, y) + ... + w(0,0) \times f(x,y) + ... + w(1,1) \times f(x+1, y+1)
$$


Em geral, a filtragem espacial linhar de uma imagem de dimensões $$M\times N$$ com um filtro de dimensões $$m \times n$$ é dada pela expressão:


$$
g(x,y) = \sum_{s=-a}^{a} \sum_{t=-b}^{b} w(s,t) \times f(x+s, y+t)
$$
onde:

* $$a = (m-1)/2$$
* $$b=(n-1)/2$$



Leia mais em [http://www.dpi.inpe.br/spring/teoria/filtrage/filtragem.htm](http://www.dpi.inpe.br/spring/teoria/filtrage/filtragem.htm).





