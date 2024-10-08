**1a. Questão)** Suponha que um arquivo ordenado possui r = 300.000 registros, que estão gravados em um disco com bloco de tamnho B = 4096 bytes. Os registros são de tamanho fixo R = 100 bytes, e a organização de registros em blocos é não espalhada. Determine:

(a) O fator de bloco **bfr** do arquivo.<br>
(b) O número mínimo de blocos **b** do arquivo.<br>
(c) O custo **c** da busca binária no arquivo.

UMA SOLUÇÃO:

(a) bfr = ⎣(B/R)⎦ = ⎣(4096/100)⎦ = 40 registros por bloco.<br>
(b) b = ⎡(r/bfr)⎤ = ⎡(300000/40)⎤ = 7500 blocos.<br>
(c) ⎡log<sub>2</sub> b⎤= ⎡(log<sub>2</sub> 7500)⎤ = 13 blocos.
