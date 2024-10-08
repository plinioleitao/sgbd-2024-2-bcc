**2a. Questão)** Sobre o arquivo da questão anterior, suponha que há um índice primário:<br>
_(i)_ a chave de ordenação do arquivo de dados tem V = 9 bytes de comprimento, e<br>
_(ii)_ um ponteiro de bloco tem P = 6 bytes de comprimento.<br>
Determine:

(a) O tamanho **R<sub>i</sub>** de cada entrada (registro) no arquivo de índice primário.<br>
(b) O fator de bloco **bfr<sub>i</sub>** do arquivo de índice primário.<br>
(c) O número total de entradas (registros) **r<sub>i</sub>** no arquivo de índice primário.<br>
(d) O número de blocos **b<sub>i</sub>** do arquivo de índice primário.<br>
(e) O custo **c<sub>i</sub>** da busca binária no arquivo de índice primário.<br>
(f) O custo **c<sub>dados</sub>** para localizar um registro de dados, via busca binária no arquivo de índice primário.<br>
(g) Quantos bytes ocuparia a estrutura completa de índice primário? É possível ter essa estrutura em memória? 

UMA SOLUÇÃO:

(a) **R<sub>i</sub>** = (9 + 6) = 15 bytes.<br>
(b) **bfr<sub>i</sub>** = ⎣(B/Ri)⎦ = ⎣(4096/15)⎦ = 273 entradas por bloco.<br>
(c) **r<sub>i</sub>** 7500 registros (mesmo número de blocos no arquivo de dados).<br>
(d) **b<sub>i</sub>** = ⎡(r<sub>i</sub>/bfr<sub>i</sub>)⎤ = ⎡(7500/273)⎤ = 28 blocos.<br>
(e) **c<sub>i</sub>** = ⎡(log<sub>2</sub> b<sub>i</sub>)⎤ = ⎡(log<sub>2</sub> 28)⎤ = 5 blocos acessados.<br>
(f) **c<sub>dados</sub>** = c<sub>i</sub> + 1 = 5 + 1 = 6 blocos acessados.<br>
(g) O arquivo de índice de primário possui 28 blocos, então tais blocos ocupam 28 * 4 KBytes, ou seja, 112 KBytes.
