## [Tópico 19] - Estruturas de indexação (7/9)
###### *by Prof. Plinio Sa Leitao-Junior (INF/UFG)*

### <ins>CONTEÚDO</ins>

|_Item do conteúdo_|_Item do conteúdo_|
|-|-|
|1. Visão geral|4. Índice secundário|
|2. Índice primário|5. Índice multinível|
|3. Índice de agrupamento|6. <ins>**ÍNDICE EM ÁRVORE (1/3)**</ins>|

<hr style="border:2px solid blue">

### 6. <ins>ÍNDICE EM ÁRVORE (1/3)</ins>

As estruturas orientadas por árvore são estudadas e empregadas em muitas das soluções baseadas em software.

#### &#9752; ESTRUTURAS EM ÁRVORE &#8212; <ins>BREVE TERMINOLOGIA</ins>

&#x270D; <ins>**Árvore**</ins> &#8212; Estrutura formada por nós:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &#10004; define uma <ins>hierarquia</ins> ... desde o <ins>nó raiz</ins>, até os <ins>nós folhas</ins>.<br>
&#x270D; <ins>**Nó raiz**</ins> &#8212; Nó singular na árvore:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &#10004; qualquer nó tem um <ins>nó pai</ins>, exceto o nó raiz.<br>
&#x270D; <ins>**Nós folhas**</ins> &#8212; Nós sem descendentes:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &#10004; qualquer nó tem um ou mais <ins>nós filhos</ins>, exceto os nós folhas.<br>
&#x270D; <ins>**Nós internos**</ins> &#8212; Nós que possuem filhos:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &#10004; qualquer nó é um nó interno, exceto os nós folhas.<br>
&#x270D; <ins>**Nível do nó**</ins> &#8212; O nível de um nó é sempre um a mais que o nível de seu pai:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &#10004; o nível do nó raiz é 0 (zero).<br>
&#x270D; <ins>**Subárvode de um nó**</ins> &#8212; Uma subárvore de um nó consiste naquele nó e todos os seus descendentes:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &#10004; seus nós filhos, os nós filhos de seus nós filhos e assim por diante.<br>
&#x270D; Os conceitos estão ilustrados na figura abaixo.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-40.jpg" width="350">

#### &#9752; ESTRUTURAS EM ÁRVORE &#8212; <ins>ÁRVORE DE BUSCA</ins>

&#x26BE; <ins>Índices multiníveis</ins> definem uma estrutura hierarquica de busca:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; Os valores dos campos de indexação (em cada nó &#8212; bloco) nos guiam para o próximo nó,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... até chegarmos ao bloco do arquivo de dados, que contém os registros pesquisados.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; Seguindo um ponteiro, restringimos nossa pesquisa em cada nível [do índice] a uma subárvore,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... determinando um <ins>caminho</ins> até os blocos de dados.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; <ins>**Índices multiníveis podem ser considerados como uma variação de uma árvore de busca**</ins>.

&#x270D; <ins>**Árvores de busca**</ins> são usadas para orientar a pesquisa de um registro, dado o valor de um dos campos do registro:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; Uma <ins>árvore de busca de ordem **p**</ins> é uma árvore tal que cada nó contém, <ins>no máximo</ins>:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **p − 1** valores de busca e<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **p** ponteiros,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; A <ins>estrutura de cada nó</ins> é:<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; \< P<sub>1</sub>, K<sub>1</sub>, P<sub>2</sub>, K<sub>2</sub>, P<sub>3</sub>, K<sub>3</sub>, ... , P<sub>q−1</sub>, K<sub>q−1</sub>, P<sub>q</sub> \>, onde **q &#8804; p**,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **P<sub>i</sub>** é um ponteiro para um nó filho (ou um ponteiro NULL),<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **K<sub>i</sub>** é um valor de pesquisa de algum conjunto ordenado de valores,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<ins>todos os valores de pesquisa **K<sub>i</sub>** são considerados únicos</ins>.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; <ins>Duas restrições</ins> são aplicadas à arvore de busca:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <ins>**(i)**</ins> dentro do nó &#8212; K<sub>1</sub> < K<sub>2</sub> < ... < K<sub>q−1</sub><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <ins>**(ii)**</ins> para todos os valores **X** na subárvore apontada por **P<sub>i</sub>**  (**1 &#8804; i &#8804; q**):<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;se <ins>1 < i < q </ins>, então **K<sub>i−1</sub> < X < K<sub>i</sub>**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;se <ins>i = 1 </ins>, então **X < K<sub>i</sub>**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;se <ins>i = q </ins>, então **K<sub>i−1</sub> < X**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; Ver figura abaixo: restrições (à esq.); árvore de busca de ordem p=3 (à dir).

<img src="../media/arquivo-41.jpg" width="350">&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-42.jpg" width="350">

#### &#9752; ÁRVORE de BUSCA &#8212; <ins>REQUISITOS</ins>

**Minimizar o número de níveis na árvore.**<br>
&#x26BE; O nível de uma árvore de busca é considerado o <ins>maior nível de nó</ins>, dentre os nós da árvore:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... reduzir a profundidade da árvore,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... diminuir a distância entre o nó raiz e qualquer nó folha.<br>
&#x26BE; Essa redução evita que a árvore torne-se desbalanceada:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... nós folha em níveis distintos entre si.<br>
&#x26BE; O balanceamento da árvore torna a 'velocidade de pesquisa' uniforme:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... o tempo médio para encontrar qualquer chave aleatória seja aproximadamente o mesmo.

**Minimizar a necessidade de reestruturação (reorganização) da árvore.**<br>
&#x26BE; O emprego de algoritmos para que a árvore não precise de muita reestruturação à medida que os registros são inseridos e excluídos:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... nas inclusões, promover que nós estejam tão cheios quanto possível;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... nas exclusões, evitar nós com poucas chaves, ou mesmo vazios.

#### &#9752; ÁRVORE de BUSCA &#8212; <ins>ESTRUTURA EM MEMÓRIA SECUNDÁRIA</ins>

&#x26BE; Uma árvore de pesquisa é um mecanismo para pesquisar registros armazenados em um arquivo de disco.<br>
&#x26BE; Os valores na árvore podem ser os valores de um dos campos de indexação do arquivo:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... a árvore implementa um dos índices.<br>
&#x26BE; Cada valor na árvore está associado a um ponteiro para os dados:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... ponteiro de registro [ou de bloco] para o arquivo de dados.<br>
&#x26BE; A própria árvore de pesquisa pode ser armazenada em disco:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... cada nó da árvore é um bloco de disco.<br>
&#x26BE; Quando um novo registro é inserido no arquivo:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... um novo valor do campo de indexação é inserido na árvore,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... bem como um ponteiro para os dados.

<hr style="border:2px solid blue">
