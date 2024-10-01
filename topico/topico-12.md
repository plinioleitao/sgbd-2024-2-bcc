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
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; ou seja, é empregada a função **h<sub>j+1</sub> (K)**.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#x26BE; senão o valor resultante de **h<sub>j</sub> (K)** determina o _bucket_ para a inserção do registro.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; ou seja, é empregada a função **h<sub>j</sub> (K)**.<br>

Observar o conteúdo da figura abaixo:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-19.jpg" width="400">

<hr style="border:2px solid blue">

#### &#x267B;&#x26BE;&#x270D; <ins>_HASHING_ LINEAR - EXEMPLO</ins>

Apresente o processo de inserção da seguinte sequência de chaves:<br>
&#x26BE; 3, 2, 4, 1, 8, 14, 5, 10, 7, 24, 17, 13, 15.

Parâmetros:<br>
&#x26BE; Regra para divisão de _buckets_: fator de carga (_load factor_) = 0.7<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; a divisão de _bucket_ ocorre quando **ocupação > 0.7**.<br>
&#x26BE; Inicialmente **M = 4** (M: tamanho da área primária)<br>
&#x26BE; Função _hash_: **h<sub>j</sub> (K) = K mod (2<sup>j</sup> * M)** , para j = 0, 1, 2, ...<br>
&#x26BE; Capacidade de _bucket_ = 02 registros.

<hr style="border:2px solid blue">

#### &#x267B; FASE 0 &#8212; n = 0

Na figura abaixo:<br>
&#x270D; Quatro _buckets_ foram inicialmente alocados (M=4).<br>
&#x270D; O fator **n** denota o <ins>número de novo _buckets_ alocados</ins>:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; **n** é inicializado com zero (**n=0**).<br>
&#x270D; Registros são <ins>inseridos e distribuídos</ins> entre os _buckets_ baseando-se na função **h<sub>0</sub> (K) = K mod (2<sup>0</sup> * M)**:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; são inseridos os registros com os valores 3, 2, 4, 1, 8;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; a ocupação da estrutura é 62,5\% (5/8).

<table>
    <tbody>
       <tr>
            <td><b><i>Bucket</i></b></td>
            <td><b>4 ; 8</b></td>
            <td><b>1</b></td>
            <td><b>2</b></td>
            <td><b>3</b></td>
       </tr>      
       <tr>
            <td><b><i>Bucket id</i></b></td>
            <td><b>#0</b></td>
            <td><b>#1</b></td>
            <td><b>#2</b></td>
            <td><b>#3</b></td>
       </tr>      
    </tbody>
</table>

<hr style="border:2px solid blue">

#### &#x267B; FASE 0 &#8212; n = 1

&#x270D; Ao inserir o registro com valor 14, a estrutura alcança 75% de ocupação (satisfaz regra para a divisão de _bucket_ &#8213; **ocupação > 0.7**):<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; um novo _bucket_ é criado (_bucket_ 4);<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; O fator **n** é incrementado &#8213; **n = 0 + 1 = 1**;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; ocorre a redistribuição de registros entre _bucket_ original (_bucket_ 0) e novo _bucket_ (_bucket_ 4);<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; registros no _bucket_ 0 são redistribídos com a função **h<sub>1</sub> (K) = K mod (2<sup>1</sup> * M) = K mod (2M)**.

<table>
    <tbody>
       <tr>
            <td><b></b></td>
            <td colspan=4><b>ANTES DA DIVISÃO (n=0)</b></td>
            <td>---</td>
            <td colspan=5><b>APÓS A DIVISÃO (n=1)</b></td>
       </tr>
       <tr>
            <td><b><i>Bucket</i></b></td>
            <td><b>4 ; 8</b></td>
            <td><b>1</b></td>
            <td><b>2 ; 14</b></td>
            <td><b>3</b></td>
            <td>---</td>
            <td><b>8</b></td>
            <td><b>1</b></td>
            <td><b>2 ; 14</b></td>
            <td><b>3</b></td>
            <td><b>4</b></td>
       </tr>      
       <tr>
            <td><b><i>Bucket id</i></b></td>
            <td><b>#0</b></td>
            <td><b>#1</b></td>
            <td><b>#2</b></td>
            <td><b>#3</b></td>
            <td>---</td>
            <td><b>#0</b></td>
            <td><b>#1</b></td>
            <td><b>#2</b></td>
            <td><b>#3</b></td>
            <td><b>#4</b></td>
       </tr>      
    </tbody>
</table>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-20.jpg" width="400">

O registro com valor 5 é inserido:<br>
&#x270D; A estrutura passa a ter 70% de ocupação:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; alcança o limite do fator de carga,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; mas não há a divisão de _bucket_.

<table>
    <tbody>
       <tr>
            <td><b><i>Bucket</i></b></td>
            <td><b>8</b></td>
            <td><b>1 ; 5</b></td>
            <td><b>2 ; 14</b></td>
            <td><b>3</b></td>
            <td><b>4</b></td>
       </tr>      
       <tr>
            <td><b><i>Bucket id</i></b></td>
            <td><b>#0</b></td>
            <td><b>#1</b></td>
            <td><b>#2</b></td>
            <td><b>#3</b></td>
            <td><b>#4</b></td>
       </tr>      
    </tbody>
</table>

<hr style="border:2px solid blue">

#### &#x267B; FASE 0 &#8212; n = 2

&#x270D; Ao inserir o registro com valor 10:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; o _bucket_ 2 está cheio,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; então o registro é inserido em _bucket_ de _overflow_;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; a estrutura alcança 80% de ocupação (satisfaz regra para a divisão de _bucket_ &#8213; **ocupação > 0.7**):<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; um novo _bucket_ é criado (_bucket_ 5);<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; O fator **n** é incrementado &#8213; **n = 1 + 1 = 2**;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; ocorre a redistribuição de registros entre _bucket_ original (_bucket_ 1) e novo _bucket_ (_bucket_ 5);<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; registros no _bucket_ 1 são redistribídos com a função **h<sub>1</sub> (K) = K mod (2<sup>1</sup> * M) = K mod (2M)**;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; após, a ocupação passa a ser 66,7\% (8/12).

<table>
    <tbody>
       <tr>
            <td><b></b></td>
            <td colspan=5><b>ANTES DA DIVISÃO (n=1)</b></td>
            <td>---</td>
            <td colspan=6><b>APÓS A DIVISÃO (n=2)</b></td>
       </tr>
       <tr>
            <td><b><i>Bucket</i></b></td>
            <td><b>8</b></td>
            <td><b>1 ; 5</b></td>
            <td><b>2 ; 14</b></td>
            <td><b>3</b></td>
            <td><b>4</b></td>
            <td>---</td>
            <td><b>8</b></td>
            <td><b>1</b></td>
            <td><b>2 ; 14</b></td>
            <td><b>3</b></td>
            <td><b>4</b></td>
            <td><b>5</b></td>
       </tr>      
       <tr>
            <td><b><i>Bucket Overflow</i></b></td>
            <td><b></b></td>
            <td><b></b></td>
            <td><b>10</b></td>
            <td><b></b></td>
            <td><b></b></td>
            <td>---</td>
            <td><b></b></td>
            <td><b></b></td>
            <td><b>10</b></td>
            <td><b></b></td>
            <td><b></b></td>
            <td><b></b></td>
       </tr>      
       <tr>
            <td><b><i>Bucket id</i></b></td>
            <td><b>#0</b></td>
            <td><b>#1</b></td>
            <td><b>#2</b></td>
            <td><b>#3</b></td>
            <td><b>#4</b></td>
            <td>---</td>
            <td><b>#0</b></td>
            <td><b>#1</b></td>
            <td><b>#2</b></td>
            <td><b>#3</b></td>
            <td><b>#4</b></td>
            <td><b>#5</b></td>
       </tr>      
    </tbody>
</table>

<hr style="border:2px solid blue">

#### &#x267B; Demais inserções de registros ...

<img src="../media/arquivo-23.jpg" width="300">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-24.jpg" width="300">

<img src="../media/arquivo-25.jpg" width="300">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-26.jpg" width="300">

<img src="../media/arquivo-27.jpg" width="300">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-28.jpg" width="300">

<img src="../media/arquivo-29.jpg" width="300">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-30.jpg" width="300">

<hr style="border:2px solid blue">

#### Em sintese ...

A divisão de _buckets_ pode ocorrer pela monitoração do fator de carga:<br>
&#x270D; Tal evita que haja a divisão de _buckets_ sempre que ocorrer um _overflow_.<br>
&#x270D; O fator de carga (_load factor_) pode ser calculado pela fórmula **lf = r/ (bfr * N)**:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; **r** = número [corrente] de registros do arquivo,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; **bfr** = número máximo de registros em um _bucket_,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; **N** = número [corrente] de _buckets_.<br>
&#x270D; O Fator de carga pode ser usado para dividir ou recombinar _buckets_:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; _buckets_ podem ser recombinados ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; se o fator de carga for reduzido abaixo de um certo limite,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; nesse caso, o **fator n** é decrementado.<br>
&#x270D; Ou seja, a carga dos _buckets_ pode ser mantida em uma faixa de fator de carga.

Algoritmo de busca para <ins>_Hashing_ Linear</ins>:

function getBucketID (K, j, n)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;m ← h<sub>j</sub> (K)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if m < n then m ← h<sub>j+1</sub> (K)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return m

Onde:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**h<sub>j</sub> (K)** e **h<sub>j+1</sub> (K)** são **funções _hash_** aplicadas durante a Fase j<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**n** é um número de _buckets_ criados na **Fase j**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**m** é o resultado do cálculo de uma **função _hash_** para o valor K (**campo _hash_**).

