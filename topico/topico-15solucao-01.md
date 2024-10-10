[**1a. Questão)** Suponha que um arquivo ordenado possui r = 300.000 registros, que estão gravados em um disco com bloco de tamanho B = 4096 bytes. O arquivo está ordenado pelo campo CEP (Código de Endereçamento Postal), e há cerca 1000 CEPs distintos nos registros do arquivo (média de 300 registros por CEP, assumindo distribuição uniforme entre CEPs). Suponha que há um índice de agrupamento:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_(i)_ a chave de ordenação do arquivo de dados tem V = 5 bytes de comprimento, e<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_(ii)_ um ponteiro de bloco tem P = 6 bytes de comprimento.<br>
Determine:<br>
(a) O tamanho **R<sub>i</sub>** de cada entrada (registro) no arquivo de índice de agrupamento.<br>
(b) O fator de bloco **bfr<sub>i</sub>** do arquivo de índice de agrupamento.<br>
(c) O número total de entradas (registros) **r<sub>i</sub>** no arquivo de índice de agrupamento.<br>
(d) O número de blocos **b<sub>i</sub>** do arquivo de índice de agrupamento.<br>
(e) O custo **c<sub>i</sub>** da busca binária no arquivo de índice de agrupamento.<br>
(f) O custo **c<sub>dados</sub>** para localizar os registros de dados, via busca binária no arquivo de índice de agrupamento.<br>
(g) Quantos bytes ocuparia a estrutura completa de índice de agrupamento? É possível ter essa estrutura em memória?  

UMA SOLUÇÃO:

(a) R<sub>i</sub> = 5 + 6 = 11 bytes.<br>
(b) bfr<sub>i</sub> =  ⎣(B/R<sub>i</sub>)⎦ = ⎣(4096/11)⎦ = 372 entradas de índice por bloco.<br>
(c) r<sub>i</sub> = 1000 registros (o número de CEPs distintos no arquivo de dados).<br>
(d) b<sub>i</sub> = ⎡(r<sub>i</sub>/bfr<sub>i</sub>)⎤ = ⎡(1000/372)⎤ = 3 blocos.<br>
(e) c<sub>i</sub> =  ⎡(log<sub>2</sub> b<sub>i</sub>)⎤ = ⎡(log<sub>2</sub> 3)⎤ = 2 blocos acessados.<br>
(f) Visto que há, em média, 300 registros por CEP, os registros com mesmo CEP podem estar dispersos em vários blocos de dados.<br>
No pior caso, c<sub>dados</sub> = c<sub>i</sub> +  ⎡(300 / ⎣(B/R)⎦ )⎤ + 1, onde R é o tamanho do registro de dados.<br>
(g) O arquivo de índice de agrupamento possui 3 blocos, então tais blocos ocupam 3 * 4 KBytes, ou seja, 12 KBytes.
