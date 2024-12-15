## [Tópico 34] - Recuperação Após Falhas
###### *by Prof. Plinio Sa Leitao-Junior (INF/UFG)*

### <ins>CONTEÚDO</ins>

|_Item do conteúdo_|_Item do conteúdo_|
|-|-|
|1. Visão geral|4. <ins>**EXEMPLOS**</ins>|
|2. Políticas de atualização|5. _Checkpoint_|
|3. Implementação<br>das políticas de atualização|6. |

<hr style="border:2px solid blue">

### 4. <ins>EXEMPLOS</ins>

Este tópico explora exemplos de recuperação de banco de dados, em que a falha é do tipo **`SISTEMA`**, tal como um _system crash_, em que o SDBG é reiniciado.

#### &#9752;&#x270D;&#9745; EXEMPLO &#8212; ABORTO EM CASCATA </ins>

Na figura abaixo:<br>
&#9918; A transação T<sub>1</sub> e T<sub>3</sub> serão desfeitas (_rolled back_), pois não alcançaram o ponto de _commit_ no momento da falha.<br>
&#9918; A transação T<sub>2</sub> é desfeita (_rolled back_), pois leu o valor do Item B, o qual foi escrito por T<sub>3</sub>.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-93.jpg" width="400">

<hr style="border:2px solid blue">

#### &#9752;&#x270D;&#9745; EXEMPLO &#8212; ALGORITMO `UNDO/REDO` </ins>

&#9888; Ressalta-se que TODAS AS TRANSAÇÕES registradas no LOG corrente ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... sofrerão UNDO ou REDO.

Na figura abaixo:<br>
&#9918; As transações T<sub>3</sub> e T<sub>5</sub> SERÃO DESFEITAS (operação UNDO), pois ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... ambas as transações NÃO POSSUEM o registro _commit_ no LOG.<br>
&#9918; As transações T<sub>1</sub>, T<sub>2</sub> e T<sub>4</sub> SERÃO REFEITAS (operação REDO), pois ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... ambas as transações POSSUEM o registro _commit_ no LOG.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-94.jpg" width="400">

<hr style="border:2px solid blue">

#### &#9752;&#x270D;&#9745; EXEMPLO &#8212; ALGORITMO `UNDO/NO-REDO` </ins>

&#9888; Ressalta-se que TODAS AS TRANSAÇÕES que NÃO POSSUEM o registro _commit_ no LOG corrente ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... sofrerão UNDO.

Na figura abaixo:<br>
&#9918; A transação T<sub>4</sub> SERÁ DESFEITA (operação UNDO), pois ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... a transação CONCLUIU,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... mas NÃO TÊM o registro _commit_ no LOG;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... _&#8810; presume-se que o _commit_ não está no LOG &#8811;_<br>
&#9918; As transações T<sub>3</sub> e T<sub>5</sub> SERÃO DESFEITAS (operação UNDO), pois ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... ambas as transações NÃO CONCLUÍRAM.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-95.jpg" width="400">

<hr style="border:2px solid blue">

#### &#9752;&#x270D;&#9745; EXEMPLO &#8212; ALGORITMO `NO-UNDO/REDO` </ins>

&#9888; Ressalta-se que TODAS AS TRANSAÇÕES que POSSUEM o registro _commit_ no LOG corrente ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... sofrerão REDO.

Na figura abaixo:<br>
&#9918; As transações T<sub>1</sub> e T<sub>2</sub> SERÃO REFEITAS (operação REDO), pois ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... ambas as transações CONCLUÍRAM,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... e TÊM o registro _commit_ no LOG.<br>
&#9918; A transação T<sub>4</sub> SERÁ REFEITA (operação REDO), pois ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... a transação CONCLUIU,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... e TÊM o registro _commit_ no LOG;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... _&#8810; presume-se que o _commit_ está no LOG &#8811;_<br>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-96.jpg" width="400">

