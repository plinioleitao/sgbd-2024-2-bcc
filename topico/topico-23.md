## [Tópico 23] - Processamento de Transações
###### *by Prof. Plinio Sa Leitao-Junior (INF/UFG)*

### <ins>CONTEÚDO</ins>

|_Item do conteúdo_|_Item do conteúdo_|
|-|-|
|1. Visão geral|5. Bloqueio de itens do banco de dados|
|2. <ins>**ESCALONAMENTO**</ins>|6. Concorrência baseada em bloqueio|
|3. Escalonamento quanto à recuperação|7. _Deadlock_ e _starvation_|
|4. Escalonamento quanto à serialização|8. Concorrência baseada em _timestamp_|

<hr style="border:2px solid blue">

### 2. <ins>ESCALONAMENTO</ins>

Relembrando ... transações executadas simultaneamente são aquelas que intersectam-se em seus períodos de execução.

Quando **n** transações (n>1) são executadas simultaneamente, a <ins>ordem de execução das operações</ins> de todas as **n** transações é conhecida como <ins>escalonamento (_schedule_)</ins>:<br>
&#x270D; Na figura abaixo, três transações são executadas de forma serial (à esquerda) e de forma não serial (à direita):<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... no escalonamento não serial, observe que a <ins>ordem de execução das operações</ins> de cada transação é preservada.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/schedule-01.jpg" width="400">

#### FORMALMENTE ...

Um <ins>Escalonamento S</ins> de **n** transações **T<sub>1</sub>, T<sub>2</sub>,…, T<sub>n</sub>** é uma ordenação das operações das transações:<br>
&#9918; `Escalonamento não serial:`<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... as operações das transações distintas em **S** são executadas de forma intercalada.<br>
&#9918; `Preservação da ordem das operações:`<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... a execução das operações de **T<sub>i</sub>** em **S** deve ocorrer na mesma ordem em que sucedem em **T<sub>i</sub>**,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... independente se **S** é um escalonamento serial ou não serial.<br>
&#9918; `Ordenação total das operações:`<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... para quaisquer duas operações em **S**, a execução de uma deve ocorrer antes da outra. 

#### MODELO SIMPLIFICADO ...

Modelo pedagógico para o escalonamento de transações:<br>
&#9752; `Operações de relevo`:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... **b** &#8212; begin_transaction<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... **r** &#8212; read_item<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... **w** &#8212; write_item<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... **e** &#8212; end_transaction<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... **c** &#8212; commit<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... **a** &#8212; abort<br>
&#9752; `Exemplo: Escalonamento Sa`  (figura à esquerda):<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... **S<sub>a</sub>** : r<sub>1</sub>(X); r<sub>2</sub>(X); w<sub>1</sub>(X); r<sub>1</sub>(Y); w<sub>2</sub>(X); w<sub>1</sub>(Y);<br>
&#9752; `Exemplo: Escalonamento Sb`  (figura à direita):<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... **S<sub>b</sub>** : r<sub>1</sub>(X); w<sub>1</sub>(X); r<sub>2</sub>(X); w<sub>2</sub>(X); r<sub>1</sub>(Y); a<sub>1</sub>;

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-68.jpg" width="250">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-69.jpg" width="250">

#### OPERAÇÕES CONFLITANTES ...

Duas operações são ditas conflitantes se:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; pertencerem a transações diferentes; E<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; acessam o mesmo item X; E<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; pelo menos uma das operações for _write_item(X)_.<br>
&#x270D; `Exemplos:`<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... r<sub>1</sub>(X) e w<sub>2</sub>(X) SÃO conflitantes;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... w<sub>1</sub>(X) e r<sub>2</sub>(X) SÃO conflitantes;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... w<sub>1</sub>(X) e w<sub>2</sub>(X) SÃO conflitantes;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... r<sub>1</sub>(X) e w<sub>2</sub>(Y) NÃO SÃO conflitantes;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... r<sub>1</sub>(X) e r<sub>2</sub>(X) NÃO SÃO conflitantes;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... r<sub>1</sub>(X) e w<sub>1</sub>(X) NÃO SÃO conflitantes.<br>
&#x270D; Noutras palavras, duas operações são conflitantes <ins>se a alteração de sua ordem _puder ocasionar_ um resultado diferente<ins>:

|Sequência 1|Sequência 2|Observação|
|-|-|-|
|r<sub>1</sub>(X); w<sub>2</sub>(X)|w<sub>2</sub>(X); r<sub>1</sub>(X)|CONFLITO read-write|
|w<sub>1</sub>(X); w<sub>2</sub>(X)|w<sub>2</sub>(X); w<sub>1</sub>(X)|CONFLITO write-write|
|r<sub>1</sub>(X); r<sub>2</sub>(X)|r<sub>2</sub>(X); r<sub>1</sub>(X)|NÃO HÁ CONFLITO|

<!-- a normal html comment 
#### ESCALONAMENTO COMPLETO ...

Um aspecto teórico ... qualquer escalonamento **S** de **n** transações T<sub>1</sub>, T<sub>2</sub>, …, T<sub>n</sub> é dito <ins>escalonamento completo</ins>, SE:<br> 
&#10004; ... as operações em **S** são exatamente as mesmas operações que compõem T<sub>1</sub>, T<sub>2</sub>, …, T<sub>n</sub>, incluindo a operação final (confirmação ou aborto) de cada transação; E<br>
&#10004; ... para qualquer par de operações da mesma transação T<sub>i</sub>, sua ordem relativa de aparecimento em **S** é a mesma que sua ordem de aparecimento em T<sub>i</sub>; E<br>
&#10004; ... para quaisquer duas operações conflitantes, uma delas deverá ocorrer [explicitamente] antes da outra em S.
-->

<hr style="border:2px solid blue">

#### Exercícios

Sejam duas transações, T<sub>1</sub> e T<sub>2</sub>, e os escalonamentos S<sub>1</sub>, S<sub>2</sub>, S<sub>3</sub>, S<sub>4</sub>, S<sub>5</sub> e S<sub>6</sub>, conforme as figuras a seguir.

1. Complemente em S<sub>2</sub> os valores dos itens de dados A e B. Compare o estado final do banco de dados entre S<sub>1</sub> e S<sub>2</sub>.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-71.jpg" width="450">

2. Complemente em S<sub>3</sub>, S<sub>4</sub>, S<sub>5</sub> e S<sub>6</sub> os valores dos itens de dados A e B. Compare o estado final do banco de dados entre S<sub>1</sub>, S<sub>2</sub>, S<sub>3</sub>, S<sub>4</sub>, S<sub>5</sub> e S<sub>6</sub>.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="../media/arquivo-72.jpg" width="750">

3. Sobre o estado final do banco de dados:
   1. O estado final dos escalonamentos não-seriais coincide com o estado final dos escalonamentos seriais?
   1. As não-coincidências ocorrem em escalonamentos não seriais em que há interferências indevidas entre as transações?

4. Para qualquer escalonamento não-serial **S** de **n** transações T<sub>1</sub>, T<sub>2</sub>, …, T<sub>n</sub>, se o estado final após a execução de **S** for o mesmo estado final de pelo menos um escalonamento serial dessas transações, é possível afirmar que as coincidências identificadas ocorrerão para qualquer estado inicial de banco de dados?
