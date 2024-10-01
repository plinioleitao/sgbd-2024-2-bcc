## [Tópico 12] - Estruturas de armazenamento (10/10)
###### *by Prof. Plinio Sa Leitao-Junior (INF/UFG)*

### <ins>CONTEÚDO</ins>

|_Item do conteúdo_|_Item do conteúdo_|
|-|-|
|1. Visão geral|8. Cabeçalho de arquivo e cabeçalho de bloco|
|2. Armazenamento físico|9. Alocação de blocos de arquivo no disco|
|3. Arquivo, bloco e registro|10. Acesso a registros|
|4. _Buffering_ de blocos|11. Organização de arquivo _vs._ Método de acesso|
|5. Registro de tamanho fixo|12. Organização de arquivos não ordenados (_heap_)|
|6. Registro de tamanho variável|13. Organização de arquivos sequenciais (ordenados)|
|7. Organização de registros em blocos<br>(espalhada e não espalhada)|14. <ins>**ORGANIZAÇÃO DE ARQUIVOS _HASHING_ (4/4)**</ins>|

<hr style="border:2px solid blue">

### 14. <ins>ORGANIZAÇÃO DE ARQUIVOS _HASHING_ (4/4)</ins>
<br>

#### &#x267B;&#x26BE;&#x270D; <ins>TÉCNICA _HASHING_ LINEAR</ins>

A <ins>técnica _hashing_ linear</ins> promove que o arquivo <ins>expanda e reduza dinamicamente</ins> o seu número de _buckets_, contudo sem ter uma estrutura de diretório (diferentemente da técnica _hashing_ extensível).

Inicialmente, o arquivo possui **M** <ins>_buckets_ primários</ins>, numerados &#8212; **0, 1, ..., M-1**.

O processo é dividido em várias fases: Fase **0**, Fase **1**, Fase **2**, …

Na <ins>**Fase j**</ins>, a localização de registros em _buckets_ é determinada por duas funções &#8212; **h<sub>j</sub> (K)** e **h<sub>j+1</sub> (K)**:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#x26BE; h<sub>j</sub> (K) = K mod (2<sup>j</sup> * M)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#x26BE; h<sub>j+1</sub> (K) = K mod (2<sup>j+1</sup> * M)

Dessa forma, as funções aplicadas em cada fase são:

|Fase j|h<sub>j</sub> (K)|h<sub>j+1</sub> (K)|
|-|-|-|
|Fase **0**|**h<sub>0</sub> (K) = K mod (2<sup>0</sup> * M)**|**h<sub>1</sub> (K) = K mod (2<sup>1</sup> * M)**|
|Fase **1**|**h<sub>1</sub> (K) = K mod (2<sup>1</sup> * M)**|**h<sub>2</sub> (K) = K mod (2<sup>2</sup> * M)**|
|Fase **2**|**h<sub>2</sub> (K) = K mod (2<sup>2</sup> * M)**|**h<sub>3</sub> (K) = K mod (2<sup>3</sup> * M)**|
|Fase **3**|**h<sub>3</sub> (K) = K mod (2<sup>3</sup> * M)**|**h<sub>4</sub> (K) = K mod (2<sup>4</sup> * M)**|
|..........|.................................................|.................................................|

<br>

&#x270D; <ins>DIVISÃO DE _BUCKET_:</ins><br>

Dividir um _bucket_ significa:<br>
&#x267B; <ins>Criar</ins> um novo _bucket_.<br>
&#x267B; <ins>Redistribuir os registros</ins> entre dois _buckets_:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#x26BE; _bucket_ original e novo _bucket_.<br><br>
A <ins>divisão de _bucket_</ins> ocorre de acordo com <ins>regras específicas</ins>:<br>
&#x267B; Um _overflow_ ocorreu:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#x26BE; ao tentar inserir um novo registro em um _bucket_ cheio,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#x26BE; então ocorre: (i) a criação de novo _bucket_; e (ii) a redistribuição de registros entre o _bucket_ original e o novo _bucket_.<br>
&#x267B; Um <ins>fator de carga</ins> (_load factor_) foi excedido:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#x26BE; por exemplo, se o fator de carga do conjunto [completo] de _buckets_ alocados for 70%,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#x26BE; quando a ocupação de _buckets_ superar 70%,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#x26BE; então ocorre: (i) a criação de novo _bucket_; e (ii) a redistribuição de registros entre o _bucket_ original e o novo _bucket_.<br>
&#x267B; Ou outra regra.

<br>

&#x270D; <ins>FATOR **n**:</ins>

O <ins>**fator n**</ins> é um <ins>contador</ins>, que determina o <ins>número de _buckets_ criados</ins> durante a <ins>**Fase j**</ins>.<br>
&#x267B; Ao iniciar a <ins>**Fase j**</ins>:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#x26BE; **n = 0**.<br>
&#x267B; Se um <ins>um novo _bucket_ for criado</ins> durante a <ins>**Fase j**</ins>:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#x26BE; **n** é incrementado por 1 (um) &#8213; **n = n + 1**.<br>
&#x267B; IMPORTANTE: Ao aplicar **h<sub>j</sub>** ao valor <ins>**K**</ins> do **campo _hash_** do registro:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#x26BE; se **h<sub>j</sub> (K) < n**,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#x26BE; então o valor resultante de **h<sub>j+1</sub> (K)** determina o _bucket_ para a inserção do registro,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; ou seja, é empregada a função `**h<sub>j+1</sub> (K)**`.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#x26BE; senão o valor resultante de **h<sub>j</sub> (K)** determina o _bucket_ para a inserção do registro.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; ou seja, é empregada a função `**h<sub>j</sub> (K)**`.<br>

Observar o conteúdo da figura abaixo:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-19.jpg" width="400">

<hr style="border:2px solid blue">

#### &#x267B;&#x26BE;&#x270D; <ins>_HASHING_ LINEAR - EXEMPLO</ins>

**_`UNDER CONSTRUCTION ...`_** :factory:
