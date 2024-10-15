Seja um arquivo não ordenado com r = 30.000 registros, que estão gravados em um disco com bloco de tamanho B = 512 bytes. Suponha um índice secundário, cuja chave de indexação é o campo CEP (campo não-chave), onde sua implementação emprega um nível extra de indireção para armazenar ponteiros de registro (Opção 3). Suponha, também, que existam 1.000 valores distintos de CEP e que os registros do arquivo estejam distribuídos uniformemente entre esses valores. Sobre o índice secundário:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_(i)_ a <ins>campo de indexação</ins> **CEP** tem 9 bytes de comprimento, e<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_(ii)_ o ponteiro de bloco **P<sub>b</sub>** ocupa 6 bytes, ponteiro de registro **P<sub>r</sub>** ocupa 7 bytes.

Seja uma busca por <ins>registros existentes</ins> no arquivo de dados, cujo predicado é **CEP = \<valor\>**. Determine:<br>
(a) O tamanho de registro **R<sub>i</sub>** do [arquivo de] índice secundário.<br>
(b) O fator de bloco **bfr<sub>i</sub>** do índice secundário.<br>
(c) Número de registros **r<sub>i</sub>** do índice secundário.<br>
(d) Número de blocos **b<sub>i</sub>** do índice secundário.<br>
(e) Núméro médio de registros **r<sub>k</sub>** por valor do campo de indexação do índice secundário.<br>
(f) Número de bytes **n<sub>ind</sub>** no nível de indireção para cada valor do campo de indexação do índice secundário.<br>
(g) Número de blocos **b<sub>ind</sub>** no nível de indireção do índice secundário.<br>
(h) Número de blocos do [arquivo de] índice secundário.<br>
(i) Custo **c<sub>i</sub>** da busca via o índice secundário, no pior caso.<br>

UMA SOLUÇÃO:

(a) R<sub>i</sub> = 9 + 6 = 15 bytes.<br>
(b) bfr<sub>i</sub> = ⎣(B / R<sub>i</sub>)⎦ = ⎣(512 / 15)⎦ = 34 entradas (registros) por bloco.<br>
(c) r<sub>i</sub> = 1000 registros (número de distintos valores do campo de indexação).<br>
(d) b<sub>i</sub> = ⎡(r<sub>i</sub> / bfr<sub>i</sub>)⎤ =  ⎡(1000 / 34)⎤ = 30 blocos.<br>
(e) r<sub>k</sub> = r / 1000 = 30000 / 1000 = 30 registros.<br>
(f) n<sub>ind</sub> = P<sub>r</sub> * r<sub>k</sub> = 7 * 30 = 210 bytes.<br>
(g) b<sub>ind</sub> = 1000 * ⎡(n<sub>ind</sub> / B)⎤ = 1000 * ⎡(210 / 512)⎤ = 1000 blocos.<br>
(h) b<sub>i</sub> + b<sub>ind</sub> = 30 + 1000 = 1030 blocos.<br>
(i) c<sub>i</sub> = ⎡(log<sub>2</sub> b<sub>i)</sub>⎤ + 1 + 30 = ⎡(log<sub>2</sub> 30)⎤ + 1 + 30 = 36 blocos.
