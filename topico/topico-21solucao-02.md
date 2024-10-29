Assuma que, em média, cada nó da árvore acima está 69% cheio.

(d) Determine o <ins>número de entradas</ins> nos nós internos e nos nós folhas (nível 3). 

Nós internos: p * 0.69 = 34 * 0.69 &#8756; **p = 23**.<br>
Nós folhas: p<sub>folha</sub> * 0.69 = 31 * 0.69 &#8756; **p<sub>folha</sub> = 21**.

|Nível|Nós|Número de entradas|Número de ponteiros<br>de árvore|Número de ponteiros<br>de dados|
|-|-|-|-|-|
|0|1|1 * 22 = 22|1 * 23 = 23|-|
|1|23|23 * 22 = 506|23 * 23 = 529|-|
|2|529|529 * 22 = 11638|529 * 23 = 12167|-|
|3|12167|12167 * 21 = 255507|-|255507|

(e) O número total de entradas do índice na Árvore B+ até o nível 3 (nível folha).

255507 entrada do índice (número de entradas nos nós folhas).

(f) É correto afirmar que a Árvore B tende a acomodar menos número de chaves, para um determinado número de níveis de índice, em relação a Árvore B+? Justifique.

Como uma árvore B inclui um ponteiro de dados junto com cada chave de pesquisa em todos os níveis da árvore, ela tende a acomodar menos número de chaves para um determinado número de níveis de índice.<br>
Esta é a principal razão pela qual as árvores B+ são preferidas às árvores B como índices para arquivos de banco de dados. A maioria dos SGBDs, como o Oracle, está criando todos os índices como árvores B+.
