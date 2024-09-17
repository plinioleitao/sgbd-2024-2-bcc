## [Tópico 06] - Estruturas de armazenamento (4/10)
###### *by Prof. Plinio Sa Leitao-Junior (INF/UFG)*

### <ins>CONTEÚDO</ins>

|_Item do conteúdo_|_Item do conteúdo_|
|-|-|
|1. Visão geral|8. Cabeçalho de arquivo e cabeçalho de bloco|
|2. Armazenamento físico|9. Alocação de blocos de arquivo no disco|
|3. Arquivo, bloco e registro|10. <ins>**ACESSO A REGISTROS**</ins>|
|4. _Buffering_ de blocos|11. <ins>**ORGANIZAÇÃO DE ARQUIVO _vs._ MÉTODO DE ACESSO**</ins>|
|5. Registro de tamanho fixo|12. Organização de arquivos não ordenados (_heap_)|
|6. Registro de tamanho variável|13. Organização de arquivos sequenciais|
|7. Organização de registros em blocos<br>(espalhada e não espalhada)|14. Organização de arquivos _hashing_|

<hr style="border:2px solid blue">

### 10. <ins>ACESSO A REGISTROS</ins>

O acesso a registros de um arquivo pode ocorrer com os seguintes propósitos:
- <ins>Recuperação de dados</ins>:
  - localizar determinados registros, para que seus valores de campo possam ser examinados e/ou processados.
- <ins>Atualização de dados</ins>:
  - alterar o arquivo pela inserção ou exclusão de registros, ou pela modificação de valores de campos de registros existentes no arquivo.
- <ins>Predicados (condição de busca)</ins> podem ser empregados nessas operações, para a filtragem de registros, tal que os registros que atendem ao predicado serão afetados pela operação:
  - se vários registros satisfazem o predicado, o primeiro registro – com relação à sequência física – é inicialmente localizado e designado como <ins>registro atual</ins>;
  - subsequentemente, o <ins>próximo registro</ins> que satisfaz o predicado será designado como registro atual ...

Abaixo estão algumas <ins>operações representativas</ins>, que são <ins>utilizadas pelos programas</ins>, para implementar a recuperação e a alteração de dados:

■ **_Open_.** Prepara o arquivo para leitura ou gravação:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; aloca _buffers_ (pelo menos dois _buffers_) para armazenar blocos do disco;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; recupera o cabeçalho do arquivo;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; define o <ins>ponteiro de arquivo</ins> para o início do arquivo.<br>
■ **_Reset_.** [Re]define o <ins>ponteiro de arquivo</ins> [do arquivo já aberto] para o início do arquivo.<br>
■ **_Find_.** Pesquisa o primeiro registro que satisfaz um predicado:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; se o bloco [desse registro] não estiver no _buffer pool_, transfere o bloco para um _buffer_;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; o <ins>ponteiro de _buffer_</ins> aponta para o registro no _buffer_ [e este torna o registro atual].<br>
■ **_Read_.** Copia o registro atual do _buffer_ para uma variável de programa:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; pode ser necessário avançar o ponteiro do registro atual para o próximo registro no arquivo, o que pode exigir a leitura do próximo bloco de arquivo do disco.<br>
■ **_FindNext_.** Procura o próximo registro no arquivo que satisfaz o predicado de pesquisa:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; se o bloco [desse registro] não estiver no _buffer pool_,  transfere o bloco para um _buffer_;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; o <ins>ponteiro de _buffer_</ins> aponta para o registro no _buffer_ [e este torna o registro atual].<br>
■ **_Delete_.** Exclui o registro atual do _buffer_:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; eventualmente, atualiza o arquivo no disco para refletir a exclusão.<br>
■ **_Modify_.** Modifica alguns valores de campo do registro atual no _buffer_:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; eventualmente, atualiza o arquivo no disco para refletir a modificação.<br>
■ **_Insert_.** Insere um novo registro no arquivo:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; localiza o bloco onde o registro será inserido;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; se o bloco não estiver no _buffer pool_, transfere esse bloco para um _buffer_;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; grava o registro no _buffer_;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; eventualmente, grava o _buffer_ para o disco para refletir a inserção.<br>
■ **_Close_.** Conclui o acesso ao arquivo liberando os _buffers_:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; executa quaisquer outras operações de limpeza necessárias.<br>
■ **_Scan_.** Encapsula (simplifica) as operações _Find_, _FindNext_ e _Read_ em uma única operação:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; se o arquivo acabou de ser aberto ou _resetado_, retornará o primeiro registro;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; caso contrário, ele retornará o próximo registro;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; se um predicado for especificado com a operação, o registro retornado será o primeiro ou o próximo registro que satisfaça o predicadoo.

As operações acima são chamadas de <ins>operações registro-por-registro</ins>:<br>
&nbsp;&nbsp;&nbsp;&#9888; cada operação é aplicada a um único registro (exceto _open_ e _close_).

Outras operações, que podem ser <ins>aplicadas a múltiplos registros</ins>:<br>
■ **_FindAll_.** Busca todos os registros no arquivo que atendem a um predicado.<br>
■ **_Find n_.** Busca **n** registros que satisfazem um predicado:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; localiza o primeiro registro que satisfaz o predicado;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; continua a localizar os próximos **n − 1** registros que satisfazem o predicado:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9745; transfere os blocos contendo os **n** registros para _buffers_ da memória principal.<br>
■ **_FindOrdered_.** Recupera todos os registros do arquivo em alguma ordem especificada.<br>
■ **_Reorganize_.** Inicia o processo de reorganização.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; algumas organizações de arquivos exigem reorganização periódica:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#9888; por exemplo, reordenar os registros do arquivo, conforme um campo especificado.

<hr style="border:2px solid blue">

### 11. <ins>ORGANIZAÇÃO DE ARQUIVO _vs._ MÉTODO DE ACESSO</ins>

A <ins>organização de arquivo</ins>:
- refere-se à organização dos dados de um arquivo em registros, blocos e estruturas de acesso;
- inclui a forma como os registros e blocos são colocados no meio de armazenamento e interligados.

O <ins>método de acesso</ins>:
- refere-se ao grupo de operações, que podem ser aplicadas a um arquivo.

Os termos são mutuamente relacionados, pois é possível <ins>aplicar diversos métodos de acesso</ins> a um arquivo organizado em uma determinada organização:
- há exceções, por exemplo, não podemos aplicar um método de acesso indexado a um arquivo que não possui índices.

> **A organização escolhida para um arquivo deve ser tal que <ins>traga eficiência às operações</ins> aplicadas ao arquivo, por meio de seus métodos de acesso.**

#### &#x267B;&#x26BE;&#x270D; <ins>ARQUIVOS ESTÁTICOS _vs._ ARQUIVOS DINÂMICOS</ins>

<ins>Arquivos estáticos</ins>:
- Operações de atualização são raramente executadas.

<ins>Arquivos dinâmicos</ins>:
- Operações de atualização são frequentemente aplicadas.

> **Perfis de arquivos estáticos e dinâmicos <ins>impactam a escolha</ins> da organização de arquivo e dos métodos de acesso.**

#### &#x267B;&#x26BE;&#x270D; <ins>CONHECIMENTO PRÉVIO DAS OPERAÇÕES</ins>

O <ins>conhecimento _a priori_ das operações</ins> sobre os dados é ponto também importante para a escolha da organização de arquivo e dos métodos de acesso. Por exemplo, para um arquivo de FUNCIONARIOS:<br>
&#9888; inserir registros (quando os funcionários são contratados);<br>
&#9888; excluir registros (quando empregados deixam a empresa);<br>
&#9888; modificar registros (por exemplo, alterar o salário de um funcionário);<br>
&#9888; excluir ou modificar um registro requer um predicado para identificar um registro específico ou um conjunto de registros;<br>
&#9888; recuperar um ou mais registros também requer um predicado de seleção.

A <ins>escolha da organização de arquivo e dos métodos de acesso</ins> pode ser um <ins>dilema</ins> [para o DBA - administrador do banco de dados]:
- Se há duas pesquisas 'importantes' em FUNCIONARIO, <ins>qual das duas priorizar</ins> no processo de seleção da organização de arquivo e dos métodos de acesso?
  - por exemplo, pesquisa de funcionários por CPF e pesquisa de funcionários por departamento;
  - ordenar fisicamentes os dados por _\<CPF\>_ ou por _\<departamento, nome do funcionário\>_?
  - em geral, a decisão (escolha) é tomada com base na importância esperada e na combinação de operações de recuperação e atualização.

<hr style="border:2px solid blue">
