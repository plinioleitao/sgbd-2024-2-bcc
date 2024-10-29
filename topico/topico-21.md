## [Tópico 21] - Estruturas de indexação (9/9)
###### *by Prof. Plinio Sa Leitao-Junior (INF/UFG)*

### <ins>CONTEÚDO</ins>

|_Item do conteúdo_|_Item do conteúdo_|
|-|-|
|1. Visão geral|4. Índice secundário|
|2. Índice primário|5. Índice multinível|
|3. Índice de agrupamento|6. <ins>**ÍNDICE EM ÁRVORE (3/3)**</ins>|

<hr style="border:2px solid blue">

### 6. <ins>ÍNDICE EM ÁRVORE (3/3)</ins>

&#x270D;&#x270D; Implementações de um <ins>índice multinível dinâmico</ins>:<br>
&#10004; **`Árvore B`**:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... cada valor do campo de indexação (campo de pesquisa) aparece uma única vez na árvore, em algum nível da árvore,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... ponteiros de dados estão dispersos em em todos os nós da árvore.<br>
&#10004; **`Árvore B+`:**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... os nós folha possuem uma entrada para cada valor do campo de indexação (campo de pesquisa),<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... ponteiros de dados são armazenados apenas nos nós folhas da árvore.<br>
&#10004; Em ambas as árvores (`B e B+`):<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... se o campo de indexação (campo de pesquisa) for campo não-chave,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... o ponteiro de dados aponta para um bloco que contém ponteiros para os registros de dados,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... e tal caracteriza um nível extra de indireção.

### &#x270D;&#x270D;&#x270D; `ÍNDICE EM ÁRVORE` &#8212; <ins>`ÁRVORE B+`</ins>

#### &#9918;&#9918;&#9918; <ins>`NÓS INTERNOS`</ins> &#8212; Árvore B+:

&#10004; A **ESTRUTURA** dos <ins>nós internos</ins> é:

|P|Dados|P|Dados| ... | ... |P|Dados|P|
|-|-|-|-|-|-|-|-|-|
|P<sub>1</sub>|_&#8249;&#8249; K<sub>1</sub>&#8250;&#8250;_|P<sub>2</sub>|_&#8249;&#8249; K<sub>2</sub>&#8250;&#8250;_| ... | ... |P<sub>q-1</sub>|_&#8249;&#8249; K<sub>q-1</sub>&#8250;&#8250;_|P<sub>q</sub>|

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Onde:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**q &#8924; p** (**p** é o número máximo de ponteiros),<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**P<sub>i</sub>** é um ponteiro de árvore,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ou seja, não há ponteiro de dados nos nós internos.<br>
&#10004; Os valores do campo de indexação (campo de pesquisa) são ordenados: K<sub>1</sub> < K<sub>2</sub> < … < K<sub>q−1</sub>.<br>
&#10004; &#9745; &#8704; X : X &#8712; { valores do campo-chave de pesquisa na subárvore apontada por P<sub>i</sub> }<br>

|Cenário|Restrição|
|-|-|
|i = 1|X ≤ K<sub>i</sub>|
|1 < i < q|K<sub>i−1</sub> < X ≤ K<sub>i</sub>|
|i = q|K<sub>i−1</sub> < X|

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... para i = 1: X < K<sub>i</sub><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... para 1 < i < q: K<sub>i−1</sub> < X < K<sub>i</sub><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... para i = q: K<sub>i−1</sub> < X

&#10004; Cada nó interno possui, <ins>no máximo</ins>, **p** ponteiros de árvore.<br>
&#10004; Cada nó interno possui, <ins>no mínimo</ins>, **⎡(p/2)⎤** ponteiros de árvore, exceto o nó raiz.<br>
&#10004; Se o nó raiz for um nó interno, o nó raiz terá, <ins>no mínimo</ins>, três ponteiros de árvore.<br>
&#10004; Um nó interno com **q** ponteiros de árvore (q ≤ p) possui **q − 1** valores do campo de indexação (campo de pesquisa).

#### &#9918;&#9918;&#9918; <ins>`NÓS FOLHAS`</ins> &#8212; Árvore B+:

&#10004; A **ESTRUTURA** dos <ins>nós folhas</ins> é:

|Dados|Dados| ... | ... |Dados|P|
|-|-|-|-|-|-|
|_&#8249;&#8249; K<sub>1</sub> , Pr<sub>1</sub> &#8250;&#8250;_|_&#8249;&#8249; K<sub>2</sub> , Pr<sub>2</sub> &#8250;&#8250;_| ... | ... |_&#8249;&#8249; K<sub>q-1</sub> , Pr<sub>q-1</sub> &#8250;&#8250;_|P<sub>next</sub>|

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Onde:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**q &#8924; p**,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Pr<sub>i</sub>** é um ponteiro de dados,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ou seja, os ponteiros de dados estão somente nos nós folhas,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**P<sub>next</sub>** é um ponteiro de árvore que aponta para o próximo nó folha,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ou seja, <ins>os nós folhas formam uma lista de nós</ins>, com todos os valores do campo de indexação,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;um ponteiro para o nó folha anterior (**P<sub>previous</sub>**) também pode ser incluído em cada nó folha.<br>
&#10004; Os valores do campo de indexação (campo de pesquisa) são ordenados: K<sub>1</sub> ≤ K<sub>2</sub>, ..., K<sub>q−1</sub>, q ≤ p.<br>
&#10004; Cada nó folha tem, <ins>no mínimo</ins>, ⎡(p/2)⎤ values do campo de indexação.<br>
&#10004; Todos os nós folha estão no mesmo nível.

A Figura abaixo ilustra a estrutura de ambos os tipos de nó (interno e folha).

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-55.jpg" width="450">

A Figura abaixo exemplifica uma Árvore B+:<br>
&#9888; Observe que **p = 4**.<br>
&#9888; Considere a área de dados dividida em vários blocos.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-56.jpg" width="540">

O custo da busca está associado ao número de níveis da Árvore B+:<br>
&#9888; O custo é limitado a **⌈ log<sub>⌈ p∕2 ⌉</sub> N ⌉** blocos acessados,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;N é o número de entradas no índice.

<hr style="border:2px solid blue">

### Exercício

Em uma Árvore B+, considere:<br>
&#x270D; **p** &#8212; o número máximo de ponteiros de árvore nos nós internos;<br>
&#x270D; **p<sub>folha</sub>** &#8212; o número máximo de ponteiros de dados nos nós folhas.<br>
Sejam: o tamanho do bloco B = 512 bytes, o tamanho do campo de indexação (campo de pesquisa) V = 9 bytes, o tamanho do ponteiro de registro Pr = 7 bytes, o tamanho do ponteiro de bloco (o ponteiro da árvore) P = 6 bytes.

(a) Calcule a ordem **p** para os nós internos.

(b) Calcule a ordem **p<sub>folha</sub>** para os nós folhas.

(c) Podemos considerar informações adicionais para cada nó? Por exemplo, tipo de nó (interno ou folha), número de entradas atuais **q** no nó, ponteiros para os nós pai e irmãos imediatos, etc. A presença dessas informações podem impactar nos cálculos acima &#8212; (a) e (b) ?

[Uma solução](./topico-21solucao-01.md)

<hr style="border:2px solid blue">

### Exercício

Assuma que, em média, cada nó da árvore acima está 69% cheio.

(d) Determine o <ins>número de entradas</ins> nos nós internos e nos nós folhas (nível 3). 

(e) O número total de entradas do índice na Árvore B+ até o nível 3 (nível folha).

(f) É correto afirmar que a Árvore B tende a acomodar menos número de chaves, para um determinado número de níveis de índice, em relação a Árvore B+? Justifique.

[Uma solução](./topico-21solucao-02.md)
