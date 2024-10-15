**1a. Questão)** Suponha um arquivo com r = 300.000 registros de tamanho fixo (R = 100 bytes), que estão gravados em um disco com bloco de tamanho B = 4096 bytes. Os registros estão distribuídos em 7500 blocos de disco. Suponha que há um índice secundário:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_(i)_ a <ins>chave de indexação</ins> **K** do arquivo de índice tem 9 bytes de comprimento, e<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_(ii)_ o ponteiro de bloco **P** tem 6 bytes de comprimento.<br>
Considere uma busca por um <ins>registro existente</ins> no arquivo de dados, cujo predicado é **K = \<valor\>**. Determine:<br>

(a) O custo médio **c** da busca no arquivo de dados (busca linear).<br>
(b) O comprimento **R<sub>i</sub>** do registro do arquivo de índice secundário.<br>
(c) O fator de bloco **bfr<sub>i</sub>** do arquivo de índice secundário.<br>
(d) O número total de entradas (registros) **r<sub>i</sub>** no arquivo de índice secundário.<br>
(e) O número de blocos **b<sub>i</sub>** do arquivo de índice secundário.<br>
(f) O custo **c<sub>i</sub>** da busca binária no arquivo de índice secundário.<br>
(g) O custo **c<sub>dados</sub>** para localizar o registro de dados, via busca binária no arquivo de índice secundário.<br>
(h) Compare o custo da busca via o índice secundário com:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_(i)_ busca linear no arquivo de dados; e<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_(ii)_ busca via o arquivo de índice primário (ver [Tópico 14](./topico-14.md)).

UMA SOLUÇÃO:

(a) c = 7500 / 2 = 3750 blocos acessados.<br>
(b) R<sub>i</sub> = 9 + 6 = 15 bytes.<br>
(c) bfr<sub>i</sub> = ⎣(B/R<sub>i</sub>)⎦ = ⎣(4096/15)⎦ = 273 entradas (registros) por bloco.<br>
(d) r<sub>i</sub> = 300.000 registros (índice denso).<br>
(e) b<sub>i</sub> =  ⎡(r<sub>i</sub>/bfr<sub>i</sub>)⎤ = ⎡(300000/273)⎤ = 1099 blocos.<br>
(f) c<sub>i</sub> = ⎡(log<sub>2</sub> b<sub>i</sub>)⎤ = ⎡(log<sub>2</sub>1099)⎤ = 11 blocos acessados.<br>
(g) c<sub>dados</sub> = c<sub>i</sub> + 1 = 11 + 1 = 12 blocos acessados.<br>
(h) Custo da busca via índice secundário: 12 (11+1) blocos acessados.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_(i)_ Custo da busca linear no arquivo de dados: 3750 blocos acessados.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_(ii)_ Custo da busca via índice primário: 6 (5+1) blocos acessados<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(o arquivo de índice primário possui 28 blocos).
