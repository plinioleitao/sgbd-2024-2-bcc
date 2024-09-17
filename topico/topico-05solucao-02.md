Seja o arquivo de clientes do exercício anterior. Contudo, suponha que apenas 80% dos registros têm um valor para Telefone, 85% para Estado civil, 15% para Cor/raça, e 90% para Grau de escolaridade, e usa-se um arquivo de registros de comprimento variável. Cada registro ainda tem: um 1 byte para cada finalizar cada campo; um marcador de exclusão de 1 byte; e um marcador de fim-de-registro de 1 byte. Suponha que usemos uma organização registro estendidos, onde cada bloco possui um ponteiro de 5 bytes para o próximo bloco (este espaço não é utilizado para armazenamento de registros).

(a) Calcule o tamanho médio do registro em _bytes_.<br>
(b) Calcule o número de blocos necessários para o arquivo.

UMA SOLUÇÃO

(a) Calcule o tamanho médio do registro em _bytes_.<br>
Supondo que: cada campo tem um <ins>tipo de campo</ins> de 1 _byte_; os campos não mencionados acima (Nome, CPF, Endereço, Data de nascimento, Sexo e Categoria de cliente) têm valores em todos os registros; há 1 _byte_ para o <ins>marcador de exclusão</ins>; e há 1 _byte_ para o <ins>marcador de fim-de-registro</ins>, então calcula-se o <ins>tamanho médio da parte fixa</ins> do registro:<br>
R<sub>fixo</sub> = (30 + 1) + (9 + 1) + (40 + 1) + (8 + 1) + (1 + 1) + (4 + 1) + 1 + 1 = 100 bytes.<br>
Para os campos Telefone, Estado civil, Cor/raça e Grau de escolaridade, calcula-se o <ins>tamanho médio da parte variável</ins> do registro:<br>
R<sub>variável</sub> = ((9 + 1) \* 0,8) + ((4 + 1) \* 0,85) + ((4 + 1) \* 0,15) + ((3 + 1) \* 0.9) = 8 + 4,25 + 0,75 + 3,6 = 16,6 _bytes_.<br>
O tamanho médio de registro R = R<sub>fixo</sub> + R<sub>variável</sub> = 100 + 16,6 = 116,6 _bytes_.<br>
O total de _bytes_ necessários para todo o arquivo = r \* R = 20.000 \* 116,6 = 2332000 bytes

(b) Calcule o número de blocos necessários para o arquivo.<br>
Usando uma organização de registro espalhada com um ponteiro de 5 _bytes_ no fim de cada bloco, o número de _bytes_ disponíveis em cada bloco são (B-5) = (512-5) = 507 _bytes_.<br>
O número de blocos necessários para o arquivo é:<br>
b = ⎡(r * R) / (B - 5)⎤ = ⎡2332000/507⎤ = 4600 blocos
