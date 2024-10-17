Seja o índice secundário do exercício presente no [Tópico 16](./topico-16.md), conforme os dados abaixo:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Fator de bloco do índice &#8213; bfr<sub>i</sub> = 273 entradas (registros) por bloco<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Número de blocos do índice &#8213; b<sub>i</sub> = 1.099 blocos<br>

Se o índice secundário for convertido para um índice multinível (o índice secundário seria índice de **1<sup>o</sup>** nível), determine:<br>
(a) O número de blocos de índice de **2<sup>o</sup>** nível.<br>
(b) O número de blocos de índice de **3<sup>o</sup>** nível.<br>
(c) A número de níveis **t** para o índice multinível.<br>
(d) O custo **c<sub>dados</sub>** para acessar um registro de dados via o índice multinível.<br>
(e) Compare com o custo de acesso ao registro de dados via o índice de único nível.

UMA SOLUÇÃO:

(a) Sejam bfr<sub>i1</sub> = bfr<sub>i</sub> e b<sub>i1</sub> = b<sub>i</sub>, então:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;b<sub>i2</sub> = ⎡(b<sub>i1</sub> / bfr<sub>i1</sub>)⎤ = ⎡(1099 / 273)⎤ = 5 blocos.<br>
(b) b<sub>i3</sub> = ⎡(b<sub>i2</sub> / bfr<sub>i2</sub>)⎤ = ⎡(5 / 273)⎤ = 1 bloco.<br>
(c) t = 3 níveis, pois o índice de **3<sup>o</sup>** nível possui 01 (um) bloco.<br>
(d) c<sub>dados</sub> = t + 1 = 4 blocos acessados.<br>
(e) 04 blocos acessados _versus_ 12 blocos acessados (⎡(log<sub>2</sub>1099)⎤ + 1).
