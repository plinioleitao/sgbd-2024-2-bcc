Em uma Árvore B+, considere:<br>
&#x270D; **p** &#8212; o número máximo de ponteiros de árvore nos nós internos;<br>
&#x270D; **p<sub>folha</sub>** &#8212; o número máximo de ponteiros de dados nos nós folhas.<br>
Sejam: o tamanho do bloco B = 512 bytes, o tamanho do campo de indexação (campo de pesquisa) V = 9 bytes, o tamanho do ponteiro de registro Pr = 7 bytes, o tamanho do ponteiro de bloco (o ponteiro da árvore) P = 6 bytes.

(a) Calcule a ordem **p** para os nós internos.

(p * P) + ((p - 1) * V) ≤ B<br>
(p * 6) + ((p - 1) * 9) ≤ 512<br>
(15*p) ≤ 512 &#8756; p ≤ 512/15 &#8756; p ≤ 34.13<br>
Então, **p = 34** para os nós internos da Árvore B+.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<ins>Obs.:</ins> Em exercício anterior, **p = 23** para Árvore B (com os mesmos parâmetros).

(b) Calcule a ordem **p<sub>folha</sub>** para os nós folhas.

(p<sub>folha</sub> * (Pr + V)) + P ≤ B<br>
(p<sub>folha</sub> * (7 + 9)) + 6 ≤ 512<br>
(16 * p<sub>folha</sub>) ≤ 512 - 6 &#8756; p<sub>folha</sub> ≤ 506/16 &#8756; p<sub>folha</sub> ≤ 31.63<br>
Então, **p<sub>folha</sub> = 31** para os nós folhas da Árvore B+ (assumindo que ponteiros de dados são ponteiros de registros). 

(c) Podemos considerar informações adicionais para cada nó? Por exemplo, tipo de nó (interno ou folha), número de entradas atuais **q** no nó, ponteiros para os nós pai e irmãos imediatos, etc. A presença dessas informações podem impactar nos cálculos acima &#8212; (a) e (b) ?
