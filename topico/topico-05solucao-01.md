### Exercício

Um arquivo de clientes tem r = 20.000 registros de comprimento fixo. Cada registro tem os seguintes campos: Nome (30 bytes), CPF (9 bytes), Endereço (40 bytes), Telefone (9 bytes), Data de nascimento (8 bytes), Sexo (1 byte), Estado civil (4 bytes), Cor ou raça (4 bytes), Categoria de cliente (4 bytes, integer), e Grau de escolaridade (3 bytes). Um byte adicional é utilizado como um marcador de exclusão. O arquivo é armazenado no disco com tamanho de bloco B = 512 bytes.<br>
(a) Calcule o tamanho de registro **R** (incluindo o marcador de exclusão) em bytes.<br>
(b) Calcule o fator de bloco **bf**r e o número de blocos de arquivo **b**, considerando uma organização não espalhada.<br>
(c) Calcule o <ins>número médio de blocos acessados</ins> necessários para pesquisar um <ins>registro arbitrário</ins> no arquivo, usando <ins>busca linear</ins>.<br>
(d) Suponha que o arquivo é <ins>ordenado pelo CPF</ins>, calcular o tempo que leva para procurar um registro a partir do valor de CPF, por meio de <ins>busca binária</ins>.

UMA SOLUÇÃO

(a) Calcule o tamanho de registro R (incluindo o marcador de exclusão) em bytes.<br>
R = (30 + 9 + 40 + 9 + 8 + 1 + 4 + 4 + 4 + 3) + 1 = 113 bytes

(b) Calcule o fator de bloco bfr e o número de blocos de arquivo b, considerando uma organização não espalhada.<br>
bfr = ⎣B / R⎦ = ⎣512 / 113⎦ = 4 registros por bloco<br>
b = ⎡r / bfr⎤ = ⎡20000 / 4⎤ = 5000 blocos

(c) Calcule o número médio de blocos acessados necessários para pesquisar um registro arbitrário no arquivo, usando busca linear.<br>
i. procurar no campo de chave:<br>
se o registro for encontrado, a metade dos blocos de arquivos são pesquisados em média: b / 2 = 5000/2 blocos<br>
se o registro não for encontrado, todos os blocos de arquivos são pesquisados: B = 5000 blocos<br>
ii. pesquisar no campo não-chave:<br>
todos os blocos de arquivos devem ser pesquisados: B = 5000 blocos

(d) Suponha que o arquivo é ordenado pelo Cpf, calcular o número de blocos acessados a partir do seu valor Cpf, fazendo uma busca binária.<br>
⎡log2 b⎤ = ⎡log2 5000⎤

<hr style="border:2px solid blue">
