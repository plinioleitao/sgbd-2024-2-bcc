## [Tópico 20] - Estruturas de indexação (8/9)
###### *by Prof. Plinio Sa Leitao-Junior (INF/UFG)*

### <ins>CONTEÚDO</ins>

|_Item do conteúdo_|_Item do conteúdo_|
|-|-|
|1. Visão geral|4. Índice secundário|
|2. Índice primário|5. Índice multinível|
|3. Índice de agrupamento|6. <ins>**ÍNDICE EM ÁRVORE (2/3)**</ins>|

<hr style="border:2px solid blue">

### 6. <ins>ÍNDICE EM ÁRVORE (2/3)</ins>

**`Árvores de Busca`** impõem restrições às estruturas tradicionais em árvore, tal como posto no [Tópico 19](./topico-19.md):<br>
&#10004; Por exemplo, ver a estrutura interna de cada nó da árvore de busca.

Contudo, <ins>novas restrições são necessárias</ins> para lidar com os desafios apresentados no [Tópico 19](./topico-19.md), a saber:<br>
&#9888; Minimizar o número de níveis na árvore (balanceamento!?).<br>
&#9888; Minimizar a necessidade de reestruturação (reorganização) da árvore.

### &#x270D;&#x270D;&#x270D; `ÍNDICE EM ÁRVORE` &#8212; <ins>`ÁRVORE B`</ins>

A **`Árvore B`** possui restrições adicionais às árvores de busca, visando a lidar com ambos os desafios acima:<br>
&#9745; Os algoritmos de inserção e exclusão, porém, tornam-se mais complexos.<br>
&#9745; A maioria das inserções e exclusões são processos simples, mas<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; se tornam complicados apenas em circunstâncias especiais:,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ..... uma inserção em um nó que já está cheio, ou<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ..... uma exclusão de um nó que o deixa menos da metade cheio.

&#9752;&#9752; Seja uma **`ÁRVORE B DE ORDEM p`**:

&#9918; Cada **<ins>NÓ (INTERNO e FOLHA)</ins>** possui a **`ESTRUTURA`**:

|P|Dados|P|Dados| ... | ... |P|Dados|P|
|-|-|-|-|-|-|-|-|-|
|P<sub>1</sub>|_&#8249;&#8249; K<sub>1</sub> , Pr<sub>1</sub> &#8250;&#8250;_|P<sub>2</sub>|_&#8249;&#8249; K<sub>2</sub> , Pr<sub>2</sub> &#8250;&#8250;_| ... | ... |P<sub>q-1</sub>|_&#8249;&#8249; K<sub>q-1</sub> , Pr<sub>q-1</sub> &#8250;&#8250;_|P<sub>q</sub>|

Onde:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Como  árvore de ordem **p**, então **q &#8924; p**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Cada **P<sub>i</sub>** é um ponteiro de árvore:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... um ponteiro para outro nó na árvore B.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Cada **Pr<sub>i</sub>** é um ponteiro de dados:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... um ponteiro de dados (ponteiro de registro ou de bloco !?) cujo valor do <ins>campo-chave de pesquisa</ins> é igual a **K<sub>i</sub>**.

&#9918; Cada **<ins>NÓ INTERNO</ins>** possui as **`RESTRIÇÕES`**:

&#9745; K<sub>1</sub> < K<sub>2</sub> < … < K<sub>q−1</sub>.<br>
&#9745; &#8704; X : X &#8712; { valores do campo-chave de pesquisa na subárvore apontada por P<sub>i</sub> }<br>

|Cenário|Restrição|
|-|-|
|i = 1|X < K<sub>i</sub>|
|1 < i < q|K<sub>i−1</sub> < X < K<sub>i</sub>|
|i = q|K<sub>i−1</sub> < X|

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... para i = 1: X < K<sub>i</sub><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... para 1 < i < q: K<sub>i−1</sub> < X < K<sub>i</sub><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... para i = q: K<sub>i−1</sub> < X

&#9745; Cada nó possui <ins>no máximo **p** ponteiros</ins> de árvore.<br>
&#9745; Cada nó, exceto os nós raiz e folhas, possui pelo menos ⎡(p/2)⎤ ponteiros de árvore:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... o nó raiz possui pelo menos dois ponteiros de árvore, a menos que seja o único nó na árvore.<br>
&#9745; Um nó com **q** ponteiros de árvore (**q &#8924; p**) possui **q &#8212; 1** valores de campo-chave de pesquisa:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ...  e, portanto, possui **q &#8212; 1** ponteiros de dados.<br>
&#9745; Todos os nós folha estão no mesmo nível.<br>
&#9745; Os nós folhas têm a mesma estrutura dos nós internos.<br>
&#9745; Em nós folhas, todos os ponteiros de árvore P<sub>i</sub> possuem valor NULO.

A estrutura e algumas das restrições da `Árvore B` (acima mencinadas) estão evidentes na figura abaixo:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-43.jpg" width="540">

Um exemplo de uma `Árvore B de ordem 3` é exibido abaixo:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-44.jpg" width="400">

Com respeito a `Árvore B` acima:<br>
&#9752; Os valores de pesquisa K na árvore são únicos?<br>
&#9752; Se usarmos uma Árvore B em um campo não-chave:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... os ponteiros de arquivo Pr<sub>i</sub> apontariam para um bloco &#8212; ou um cluster de blocos ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... o bloco apontado teria ponteiros para os registros que têm os mesmos valores de pesquisa ? <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; o nível extra de indireção é semelhante à <ins>Opção 3</ins>, discutida no [Tópico 17](./topico-17.md).

#### &#x270D;&#x270D; `Breve algoritmo` de <ins>inserção de dados</ins> em uma <ins>Árvore B de ordem p </ins>:<br>
&#9745; A árvore começa com um único nó &#8212; o nó raiz que também é um nó folha &#8212; no nível 0 (zero).<br>
&#9752; Sobre **`nó raiz`**, dados são inseridos até que <ins>o nó raiz esteja CHEIO</ins>.<br>
&#9745; Ao tentar inserir outra entrada no nó raiz:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#8658; o nó raiz se divide em dois outros nós em nível 1,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#8658; apenas o valor do meio é mantido no nó raiz,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#8658; os demais valores são divididos igualmente entre os dois nós no nível 1;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#8658; no exemplo abaixo, uma Árvore B de ordem 5,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... no máximo 4 entradas (valores) por nó.<br>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-45.jpg" width="500">

&#9752; Sobre **`nó não-raiz`**, dados são inseridos até que <ins>um nó não-raiz esteja CHEIO</ins>.<br>
&#9745; Ao tentar inserir uma nova entrada neste nó não-raiz:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#8658; o nó é dividido em <ins>dois nós no mesmo nível</ins>,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#8658; a entrada do meio é movida para o nó pai,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#8658; junto com dois ponteiros para os dois nós [divididos];<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#8658; se o nó pai estiver cheio, ele também será dividido:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... a divisão pode se propagar até o nó raiz,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... criando um novo nível, se a raiz for dividida.<br>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-46.jpg" width="550">

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-47.jpg" width="400">

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-48.jpg" width="480">

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-49.jpg" width="460">

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-50.jpg" width="460">

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-51.jpg" width="500">

<hr style="border:2px solid blue">

### Exercício

Desenhe passo-a-passo a inserção de uma sequência de entradas &#8212; 8, 5, 1, 7, 3, 12, 9, 6 &#8212; em uma árvore B de ordem p = 3.

<hr style="border:2px solid blue">

#### &#x270D;&#x270D; `Breve comentário` sobre <ins>exclusão de dados</ins> em uma <ins>Árvore B de ordem p </ins>:<br>
&#9745; Se a exclusão de dados ocasionar que um nó fique menos da metade cheio:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#8658; o nó será combinado com seus nós vizinhos,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#8658; e tal pode poderá se propagar até a raiz,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#8658; o que pode resultar em reduzir o número de níveis de árvore:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... no exemplo abaixo, a entrada com valor 25 é removida.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-52.jpg" width="400">

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-53.jpg" width="400">

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-54.jpg" width="400">

#### &#x270D;&#x270D; Outros Comentários

Segundo a bibliografia sugerida para a disciplina:<br>
&#9745; Foi demonstrado por análise e simulação que, após numerosas inserções e exclusões aleatórias em uma Árvore B, <ins>os nós estão aproximadamente 69% cheios</ins> quando o número de valores na árvore se estabiliza.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#8658; O mesmo foi observado em Árvores B+.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#8658; Em tal contexto, a divisão e a combinação de nós ocorrerão apenas raramente,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... portanto a inserção e a exclusão se tornarão bastante eficientes.<br>
&#9745; Implementações de Árvore B podem ainda incluir em cada nó:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**(i)** o número de entradas, e<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**(ii)** um ponteito para o nó pai;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... ambas informações são úteis aos algoritmos que manipulam a árvore.

<hr style="border:2px solid blue">

### Exercício

Suponha um índice baseado em Árvore B:<br>
&#x26BE; O campo de indexação é um campo-chave.<br>
&#x26BE; O campo de indexação não é o campo de ordenação (caso exista).<br>
&#x26BE; O campo de indexação ocupa 10 bytes.<br>
&#x26BE; O tamanho de bloco é B = 512 bytes.<br>
&#x26BE; A dimensão do nó é a mesma dimensão do bloco.<br>
&#x26BE; Um ponteiro de dados (ponteiro de registro) ocupa 7 (sete) bytes.<br>
&#x26BE; Um ponteiro de árvore (ponteiro de bloco) ocupa 6 (seis) bytes.<br>
&#x26BE; Cada nó da árvore está 69% cheio (suposição).<br>
Determine:

(a) A </ins>ordem **p**</ins> da árvore.<br>
(b) O <ins>número de entradas</ins> e <ins>número de ponteiros de árvore</ins> em cada nó, em média, segundo a suposição **69% cheio** para os nós da árvore.<br>
(c) O número total de entradas na árvore até o nível 3.

[Uma solução](./topico-20solucao-01.md)

<hr style="border:2px solid blue">

#### &#x270D;&#x270D; `Breve comentário` sobre <ins>Árvore B como organização de arquivos de dados</ins>:<br>

&#9745; Registros completos [de dados] são armazenados nos nós da árvore B, em vez de apenas <chave de pesquisa, ponteiro de dados>:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#8658; **Contexto:**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... arquivos com número relativamente pequeno de registros,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... e registros de tamanho reduzido,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... para evitar o aumento do número de níveis da árvore,<br> 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... que impactaria à eficiência de acesso.
