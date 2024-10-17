## [Tópico 18] - Estruturas de indexação (6/9)
###### *by Prof. Plinio Sa Leitao-Junior (INF/UFG)*

### <ins>CONTEÚDO</ins>

|_Item do conteúdo_|_Item do conteúdo_|
|-|-|
|1. Visão geral|4. Índice secundário|
|2. Índice primário|5. <ins>**ÍNDICE MULTINÍVEL**</ins>|
|3. Índice de agrupamento|6. Índice em árvore|

<hr style="border:2px solid blue">

#### &#x270D;&#9745; <ins>REVISÃO</ins> &#8212; TIPO DE ÍNDICE BASEADO NAS PROPRIEDADES DO CAMPO DE INDEXAÇÃO

||campo de indexação<br>**&#61;**<br>campo de ordenação <sup>(a)</sup>|campo de indexação<br>**&#8800;**<br>campo de ordenação <sup>(a)</sup>|
|-|-|-|
|Campo de indexação<br>**&#61;**<br>campo chave|ÍNDICE PRIMÁRIO|ÍNDICE SECUNDÁRIO|
|Campo de indexação<br>**&#61;**<br>campo não-chave|ÍNDICE DE AGRUPAMENTO|ÍNDICE SECUNDÁRIO|

<sup>(a)</sup> Ordenação do arquivo de dados.<br>

<hr style="border:2px solid blue">

#### &#x270D;&#9745; <ins>REVISÃO</ins> &#8212; PROPRIEDADES DE TIPOS DE ÍNDICE

|Tipo de índice|Número de entradas<br>no arquivo de índice|Se denso<br>ou esparso|Usa registro<br>âncora? <sup>(a)</sup>|
|-|-|-|-|
|PRIMÁRIO|Número de blocos<br>do arquivo de dados|esparso|sim|
|AGRUPAMENTO|Número de valores distintos<br>do campo de indexação|esparso|sim <sup>(b)</sup><br>_ou_<br>não <sup>(c)</sup>|
|SECUNDÁRIO<br>campo chave <sup>(d)</sup>|Número de registros<br>do arquivo de dados|denso|não|
|SECUNDÁRIO<br>campo não-chave <sup>(e)</sup>|Número de registros<br>do arquivo de dados <sup>(f)</sup><br>_ou_<br>Número de valores distintos<br>do campo de indexação <sup>(g)</sup>|denso <sup>(f)</sup><br>_ou_<br>esparso <sup>(g)</sup>|não|

<sup>(a)</sup> Registro âncora de cada bloco no arquivo de dados.<br>
<sup>(b)</sup> Se cada valor distinto do campo de ordenação é iniciado (alocado) em um novo bloco.<br>
<sup>(c)</sup> Se um mesmo bloco acomodar distintos valores do campo de ordenação.<br>
<sup>(d)</sup> Campo de indexação é campo chave.<br>
<sup>(e)</sup> Campo de indexação é campo não-chave.<br>
<sup>(f)</sup> Opção 1 no [Tópico 17](./topico-17.md).<br>
<sup>(g)</sup> Opções 2 e 3 no [Tópico 17](./topico-17.md).<br>

<hr style="border:2px solid blue">

### 5. <ins>ÍNDICE MULTINÍVEL</ins>

Um <ins>índice múltinível</ins> pode ser pensado como <ins>índice sobre índice</ins> &#8213; vários índices organizados em <ins>níveis</ins>:
- O <ins>índice de 1<sup>o</sup> nível</ins> é o índice que estudamos até então, ou seja, um arquivo ordenado:
  - pode ser índice primário, índice de agrupamento ou índice secundário,
  - desde que: _(i)_ o índice tenha valores distintos para K(i); e _(ii)_ os registros do índice sejam de tamanho fixo.
- O <ins>índice de 2<sup>o</sup> nível</ins> indexa o índice de 1<sup>o</sup> nível:
  - o índice de 1<sup>o</sup> nível faria o papel do arquivo de dados (arquivo ordenado);
  - o índice de 2<sup>o</sup> nível similar a um índice primário.
- O <ins>índice de 3<sup>o</sup> nível</ins> indexa o índice de 2<sup>o</sup> nível:
  - o índice de 2<sup>o</sup> nível faria o papel do arquivo de dados (arquivo ordenado);
  - o índice de 3<sup>o</sup> nível similar a um índice primário.
- _and so on_ ...

O número de registros do <ins>índice de nível j </ins> (j>1) é o número de blocos do <ins>índice de nível j-1</ins>:
- Por ser similar a índice primário, o <ins>índice de nível j </ins> baseia-se no registro âncora de cada bloco do <ins>índice de nível j-1</ins>.
- Exemplos: r<sub>i2</sub> = b<sub>i1</sub> , r<sub>i3</sub> = b<sub>i2</sub> , r<sub>i4</sub> = b<sub>i3</sub> , _and so on_ ...
- Ver figura a seguir (no exemplo, o <ins>índice de 1<sup>o</sup> nível</ins> é um índice primário):
  - _That's a two-level primary index resembling **ISAM** (indexed sequential access method) organization_.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-39.jpg" width="400">

<hr style="border:2px solid blue">

#### Exercício

Seja o índice secundário do exercício presente no [Tópico 16](./topico-16.md), conforme os dados abaixo:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Fator de bloco do índice &#8213; bfr<sub>i</sub> = 273 entradas (registros) por bloco<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Número de blocos do índice &#8213; b<sub>i</sub> = 1.099 blocos<br>

Se o índice secundário for convertido para um índice multinível (o índice secundário seria índice de **1<sup>o</sup>** nível), determine:<br>
(a) O número de blocos de índice de **2<sup>o</sup>** nível.<br>
(b) O número de blocos de índice de **3<sup>o</sup>** nível.<br>
(c) A número de níveis **t** para o índice multinível.<br>
(d) O custo **c<sub>dados</sub>** para acessar um registro de dados via o índice multinível.<br>
(e) Compare com o custo de acesso ao registro de dados via o índice de único nível.

[Uma solução](./topico-18solucao-01.md)
