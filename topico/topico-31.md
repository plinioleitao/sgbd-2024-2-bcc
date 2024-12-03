## [Tópico 31] - Recuperação Após Falhas
###### *by Prof. Plinio Sa Leitao-Junior (INF/UFG)*

### <ins>CONTEÚDO</ins>

|_Item do conteúdo_|_Item do conteúdo_|
|-|-|
|1. Visão geral|4. Exemplos|
|2. <ins>**POLÍTICAS DE ATUALIZAÇÃO**</ins>|5. _Checkpoint_|
|3. Implementação das<br>políticas de atualização|6. |

<hr style="border:2px solid blue">

### 2. <ins>POLÍTICAS DE ATUALIZAÇÃO</ins>

As **políticas de atualização** determinam <ins>à durabilidade das atualizações</ins> do banco de dados:<br>
&#9888; As políticas definem os momentos [pertinentes à transação] em que ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... os DADOS ATUALIZADOS [pelas transações] são <ins>efetivamente aplicados ao banco de dados</ins> [em disco].<br>
&#9888; As políticas de atualização denotam os <ins>algoritmos de recuperação</ins>:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... `NO-UNDO/REDO`, `UNDO/REDO` e `UNDO/NO-REDO`.

<hr style="border:2px solid blue">

#### &#9752;&#x270D;&#9745; POLÍTICA DE ATUALIZAÇÃO &#8212; <ins> `ATUALIZAÇÃO ADIADA (NO-UNDO/REDO)` </ins>

Na política de **`ATUALIZAÇÃO ADIADA`**:<br>
&#9918; ANTES da <ins>transação ser confirmada</ins> ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... as atualizações são registradas nos _buffers_ do SGBD (ou seja, em memória),<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... e eventualmente no LOG.<br>
&#9918; APÓS a <ins>transação ser confirmada</ins> e TER o <ins>registro de _COMMIT_ gravado no LOG</ins> ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... os dados alterados [pela transação] serão aplicados ao banco de dados no disco [em algum momento].<br>
&#9918; Noutras palavras ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... Antes da confirmação da transação,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;as atualizações são registradas no arquivo de LOG [em memória secundária].<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... Após a confirmação da transação &#8212; e depois da gravação do _COMMIT_ no LOG,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;as atualizações serão gravadas no banco de dados [em algum momento],<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;a partir dos _buffers_ [em memória principal].<br>
&#10004; E <ins>se a transação falhar</ins>, ANTES de ser confirmada (ou seja, antes de atingir seu ponto de _commit_) ??<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... O banco de dados não terá sido alterado em disco pela transação !!<br>
&#10004; A operação **`UNDO NÃO É NECESSÁRIA`**:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... antes do _COMMIT_ ser gravado no LOG,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;nenhuma atualização da transação é aplicada ao banco de dados [em disco].<br>
&#10004; A operação **`REDO É NECESSÁRIA`**:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mesmo APÓS o _COMMIT_ ser gravado no LOG, não há a garantia sobre<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;quando todas as atualizações [da transação] serão aplicadas ao banco de dados [em disco].<br>
&#9888; A `atualização adiada` também é conhecida como **`Algoritmo NO-UNDO/REDO`**.

|Gravação em disco|Inicia T|Operações em T|_Commit_ T|_Commit_ no LOG|Após T|
|:-:|:-:|:-:|:-:|:-:|:-:|
|LOG|XXXXXXX|XXXXXXX||XXXXXXX||
|BD|||||XXXXXXX|

<hr style="border:2px solid blue">

#### &#9752;&#x270D;&#9745; POLÍTICA DE ATUALIZAÇÃO &#8212; <ins> `ATUALIZAÇÃO IMEDIATA (UNDO/REDO)` </ins>

Na politica de **`ATUALIZAÇÃO IMEDIATA`**:<br>
&#9918; ANTES da <ins>transação ser confirmada</ins> ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... o banco de dados pode ser atualizado [em disco] por algumas operações da transação;<br>
&#10004; E <ins>se a transação falhar, antes de ser confirmada</ins> (ou seja, antes de atingir seu ponto de _commit_) ??<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; A recuperação é possível pois ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... as operações aplicadas ao banco de dados [em disco] ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... estão também presentes no LOG [em disco] ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... portanto tais operações podem ser desfeitas.<br>
&#10004; A operação **`UNDO É NECESSÁRIA`**:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;para as transações QUE NÃO POSSUEM o registro _COMMIT_ no LOG.<br>
&#10004; A operação **`REDO É NECESSÁRIA`**:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;para as transações QUE POSSUEM o registro _COMMIT_ no LOG.<br>
&#9888; A `atualização imediata` também é conhecida como **`Algoritmo UNDO/REDO`**.

|Gravação em disco|Inicia T|Operações em T|_Commit_ T|_Commit_ no LOG|Após T|
|:-:|:-:|:-:|:-:|:-:|:-:|
|LOG|XXXXXXX|XXXXXXX||XXXXXXX||
|BD||XXXXXXX|||XXXXXXX|

<hr style="border:2px solid blue">

#### &#9752;&#x270D;&#9745; POLÍTICA DE ATUALIZAÇÃO &#8212; <ins> `ATUALIZAÇÃO IMEDIATA MODIFICADA (UNDO/NO-REDO)` </ins>

Na politica de **`ATUALIZAÇÃO IMEDIATA MODIFICADA`**:<br>
&#9918; ANTES da <ins>transação ser confirmada</ins> ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... o banco de dados será atualizado [em disco] para todas as operações da transação;<br>
&#9918; AO TER o registro de COMMIT no LOG ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... os dados alterados [pela transação] já estarão aplicados ao banco de dados [em disco].<br>
&#10004; A operação **`UNDO É NECESSÁRIA`**:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;para as transações QUE NÃO POSSUEM o registro _COMMIT_ no LOG.<br>
&#10004; A operação **`REDO NÃO É NECESSÁRIA`**:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;para as transações QUE POSSUEM o registro _COMMIT_ no LOG.<br>
&#9888; A `atualização imediata modificada` também é conhecida como **`Algoritmo UNDO/NO-REDO`**.

|Gravação em disco|Inicia T|Operações em T|_Commit_ T|_Commit_ no LOG|Após T|
|:-:|:-:|:-:|:-:|:-:|:-:|
|LOG|XXXXXXX|XXXXXXX||XXXXXXX||
|BD||XXXXXXX||||

<hr style="border:2px solid blue">

#### &#9752;&#x270D;&#9745; COMPARAÇÃO DAS POLÍTICAS DE ATUALIZAÇÃO </ins>

|Algoritmo|Gravação em disco|Inicia T|Operações em T|_Commit_ T|_Commit_ no LOG|Após T|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|&#8212;|LOG|XXXXXXX|XXXXXXX||XXXXXXX||
|NO-UNDO/REDO|BD|||||XXXXXXX|
|UNDO/REDO|BD||XXXXXXX|||XXXXXXX|
|UNDO/NO-REDO|BD||XXXXXXX||||

<hr style="border:2px solid blue">

#### &#9752;&#x270D;&#9745; IDEMPOTÊNCIA DAS OPERAÇÕES `UNDO` E `REDO` </ins>

As operações UNDO e REDO são IDEMPOTENTES:<br>
&#9918; Executar a operação múltiplas vezes equivale a executá-la apenas uma vez.<br>
&#9918; Se houver <ins>alguma falha durente o processo de recuperação</ins> ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... o algoritmo de recuperação poderia repetir as operações da tentativa anterior ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... para ter o mesmo que o resultado da recuperação (quando não há falha durante a recuperação).<br>
&#9918; Noutras palavras:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... durante o processo de recuperação, várias operações UNDO e REDO são executadas;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... se o processo de recuperação falhar, operações UNDO e REDO poderão ser reexecutadas.


