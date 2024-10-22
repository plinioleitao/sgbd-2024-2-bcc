### Exercício

Suponha um índice baseado em Árvore B:<br>
&#x26BE; O campo de indexação é um campo-chave.<br>
&#x26BE; O campo de indexação não é o campo de ordenação (caso exista).<br>
&#x26BE; O campo de indexação ocupa 10 bytes.<br>
&#x26BE; O tamanho de bloco é B = 512 bytes.<br>
&#x26BE; A dimensão do nó é a mesma dimensão do bloco.<br>
&#x26BE; Um ponteiro de dados (ponteiro de registro) ocupa 7 (sete) bytes.<br>
&#x26BE; Um ponteiro de árvore (ponteiro de bloco) ocupa 6 (seis) bytes.<br>
&#x26BE; Cada nó da árvore está 69% cheio (suposição).<br>
Determine:

(a) A </ins>ordem **p**</ins> da árvore.

Se cada nó da árvore B pode ter, no máximo,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... p ponteiros de árvore,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... p &#8212; 1 ponteiros de dados, e<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... p &#8212; 1 valores (entradas) de campo-chave de pesquisa,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;então:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;((p-1) * 7) + ((p-1) * 10) + (p * 6) &#8924; B<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;7p - 7 + 10p - 10 + 6p &#8924; 512<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;23p - 17 &#8924; 512<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;p = piso (529 / 23) &#8756; **`p = 23`**

(b) O <ins>número de entradas</ins> e <ins>número de ponteiros de árvore</ins> em cada nó, em média, segundo a suposição **69% cheio** para os nós da árvore.

Número de ponteiros de árvore (q):<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; q = teto(p * 0.69) = teto(23 * 0.69) = teto(15,87) = 16 ponteiros por nó.<br>
Número de entradas (q &#8212; 1):<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;q &#8212; 1 = 16 &#8212; 1 = 15 entradas por nó.

(c) O número entradas do índice na árvore até o nível 3.

|Nível|Nós|Número de entradas|Número de ponteiros de árvore|Número de entradas até o nível|
|-|-|-|-|-|
|0|1|15|16|15|
|1|16|16 * 15 = 240|16 * 16 = 256|15 + 240 = 255|
|2|256|256 * 15 = 3840|256 * 16 = 4096|15 + 240 + 3840 = 4095|
|3|4096|4096 * 15 = 61.440|4096 * 16 = 65536|15 + 240 + 3840 + 61440 = 65535|

O número entradas na árvore até o nível 3 é:<br>
15 + 240 + 3840 + 61440 = 65535 entradas do índice.

