## [Tópico 02c] - Exercícios de revisão (3/4)
###### *by Prof. Plinio Sa Leitao-Junior (INF/UFG)*

<hr style="border:2px solid blue">

Para ilustrar as operações da SQL, considere o esquema lógico do BD Empresa.

<img src="../media/fig-esquema-logico-bdempresa.jpg" width="450">

<hr style="border:2px solid blue">

#### <ins>EXERCÍCIO:</ins> Escreva em SQL as operações (1), (2) e (3).

|(1)|
|-|
|π <sub>Pnome, **F.Sexo**, Nome_dependente, **D.Sexo**</sub><br>&nbsp;&nbsp;&nbsp;&nbsp;(**ρ <sub>F</sub>** (FUNCIONARIO) ⨝ <sub>Cpf = Fcpf</sub> **ρ <sub>D</sub>** (DEPENDENTE))|

|(2)|
|-|
|D(Cpf, Nome_dependente, Sexo_dependente) ←<br>&nbsp;&nbsp;&nbsp;&nbsp;π <sub>Fcpf, Nome_dependente, Sexo</sub> (DEPENDENTE)<br>RESULT ← π <sub>Pnome, Sexo, Nome_dependente, Sexo_dependente</sub> (FUNCIONARIO * D)|

|(3)|
|-|
|FUNC(**Cpf**, Pnome_func, Unome_func) ← <br>&nbsp;&nbsp;&nbsp;&nbsp;π <sub>**Cpf_supervisor**, Pnome, Unome</sub> (FUNCIONARIO)<br>SUPER ← π <sub>Cpf, Pnome, Unome</sub> (FUNCIONARIO)<br>RESULT ← π <sub>Pnome_func, Unome_func, Pnome, Unome (FUNC * SUPER)|

<hr style="border:2px solid blue">

#### <ins>EXERCÍCIO:</ins> Interprete as expressões a seguir (veja a tabela).

&#9888; (5 + NULL)<br>
&#9888; (5 < NULL)<br>
&#9888; (NULL <> NULL)<br>
&#9888; (NULL = NULL)<br>
&#9888; NULL OR TRUE<br>
&#9888; NULL OR FALSE<br>
&#9888; NULL OR NULL<br>
&#9888; TRUE AND NULL<br>
&#9888; FALSE AND NULL<br>
&#9888; NULL AND NULL<br>
&#9888; NOT NULL

<img src="../media/fig-valor-nulo.jpg" width="450">

<hr style="border:2px solid blue">

#### <ins>EXERCÍCIO:</ins> Reescreva a junção abaixo sem usar a cláusula HAVING. Em seguida, transforme a solução em junção natural.

|(1)|
|-|
SELECT Pnome, Unome, COUNT(Fcpf)<br>FROM FUNCIONARIO JOIN DEPENDENTE<br>&nbsp;&nbsp;&nbsp;&nbsp;ON Cpf = Fcpf<br> GROUP BY Fcpf, Pnome, Unome<br>HAVING COUNT(Fcpf) >= 2|

<hr style="border:2px solid blue">

#### <ins>EXERCÍCIO:</ins> A construção abaixo é válida?

|(1)|
|-|
|SELECT Pnome, Unome, COUNT(Fcpf)<br>FROM FUNCIONARIO JOIN DEPENDENTE<br>&nbsp;&nbsp;&nbsp;&nbsp;ON Cpf = Fcpf<br> GROUP BY Fcpf, Pnome, Unome<br>HAVING COUNT(Fcpf) >= 2<br>ORDER BY 3 DESC, 1|

<hr style="border:2px solid blue">

#### <ins>EXERCÍCIO:</ins> Qual o propósito do comando abaixo?

|(1)|
|-|
|SELECT Salario FROM FUNCIONARIO WHERE Salario > <br>&nbsp;&nbsp;( SELECT MIN(Salario) FROM FUNCIONARIO WHERE Salario < <br>&nbsp;&nbsp;&nbsp;&nbsp;( SELECT MAX(Salario) FROM FUNCIONARIO WHERE Salario < <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;( SELECT MAX(Salario) FROM FUNCIONARIO ) ) )|

<hr style="border:2px solid blue">

#### <ins>EXERCÍCIO:</ins> Qual o propósito dos comandos abaixo?

|(1)|(2)|(3)|
|-|-|-|
|SELECT S.Cpf, S.Pnome, S.Unome<br>FROM FUNCIONARIO AS F JOIN<br>&nbsp;&nbsp;&nbsp;&nbsp;FUNCIONARIO AS S<br>&nbsp;&nbsp;&nbsp;&nbsp;ON F.Cpf_supervisor = S.Cpf<br>EXCEPT<br>SELECT F.Cpf, F.Pnome, F.Unome <br>FROM DEPENDENTE AS D JOIN<br>&nbsp;&nbsp;&nbsp;&nbsp;FUNCIONARIO AS F<br>&nbsp;&nbsp;&nbsp;&nbsp;ON D.Fcpf = F.Cpf|SELECT S.Cpf, S.Pnome, S.Unome<br>FROM FUNCIONARIO AS F JOIN<br>&nbsp;&nbsp;&nbsp;&nbsp;FUNCIONARIO AS S<br>&nbsp;&nbsp;&nbsp;&nbsp;ON F.Cpf_supervisor = S.Cpf<br>UNION<br>SELECT F.Cpf, F.Pnome, F.Unome <br>FROM DEPENDENTE AS D JOIN<br>&nbsp;&nbsp;&nbsp;&nbsp;FUNCIONARIO AS F<br>&nbsp;&nbsp;&nbsp;&nbsp;ON D.Fcpf = F.Cpf|SELECT S.Cpf, S.Pnome, S.Unome<br>FROM FUNCIONARIO AS F JOIN<br>&nbsp;&nbsp;&nbsp;&nbsp;FUNCIONARIO AS S<br>&nbsp;&nbsp;&nbsp;&nbsp;ON F.Cpf_supervisor = S.Cpf<br>INTERSECT<br>SELECT F.Cpf, F.Pnome, F.Unome <br>FROM DEPENDENTE AS D JOIN<br>&nbsp;&nbsp;&nbsp;&nbsp;FUNCIONARIO AS F<br>&nbsp;&nbsp;&nbsp;&nbsp;ON D.Fcpf = F.Cpf|

<hr style="border:2px solid blue">

#### <ins>EXERCÍCIO:</ins> Os comandos em (1) e (2) são equivalentes?

|(1)|(2)|
|-|-|
|SELECT Pnome, Unome<br>FROM FUNCIONARIO<br>WHERE EXISTS (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT \***<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM DEPENDENTE**<br>&nbsp;&nbsp;&nbsp;&nbsp;**WHERE FUNCIONARIO.Cpf = DEPENDENTE.Fcpf** )|SELECT Pnome, Unome<br>FROM FUNCIONARIO<br>WHERE EXISTS (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT NULL**<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM DEPENDENTE**<br>&nbsp;&nbsp;&nbsp;&nbsp;**WHERE FUNCIONARIO.Cpf = DEPENDENTE.Fcpf** )|
|SELECT Pnome, Unome<br>FROM FUNCIONARIO<br>WHERE Cpf IN (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT Cpf_gerente**<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM DEPARTAMENTO** )|SELECT Pnome, Unome<br>FROM FUNCIONARIO<br>WHERE Cpf = (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT Cpf_gerente**<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM DEPARTAMENTO** )|

<hr style="border:2px solid blue">

#### <ins>EXERCÍCIO:</ins> A consulta abaixo poderia retornar _tuplas_ iguais?

|(1)|
|-|
|SELECT Pnome, Unome<br>FROM FUNCIONARIO<br>WHERE (Cpf, 10) IN<br>&nbsp;&nbsp;&nbsp;&nbsp;( **SELECT Fcpf, Horas**<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**FROM TRABALHA_EM** )|

<hr style="border:2px solid blue">

#### <ins>EXERCÍCIO:</ins> Qual o propósito do comando abaixo?

|(1)|
|-|
|SELECT Pnome, Unome, Salario<br>FROM FUNCIONARIO AS EXTERNA<br>WHERE NOT EXISTS (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT \***<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM FUNCIONARIO AS INTERNA**<br>&nbsp;&nbsp;&nbsp;&nbsp;**WHERE INTERNA.Salario < EXTERNA.Salario** )|

<hr style="border:2px solid blue">

#### <ins>EXERCÍCIO:</ins> Qual o propósito do comando abaixo?

|(1)|
|-|
|SELECT Pnome, Unome, Salario<br>FROM FUNCIONARIO AS EXTERNA<br>WHERE 3 > (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT COUNT(DISTINCT Salario)**<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM FUNCIONARIO AS INTERNA**<br>&nbsp;&nbsp;&nbsp;&nbsp;**WHERE INTERNA.Salario > EXTERNA.Salario** )|

<hr style="border:2px solid blue">

#### <ins>EXERCÍCIO:</ins> Os comandos em (1), (2) e (3) são equivalentes?

|(1)|(2)|(3)|
|-|-|-|
|SELECT Pnome, Unome, Salario<br>FROM FUNCIONARIO<br>WHERE Salario >= ALL  (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT Salario**<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**FROM FUNCIONARIO** )|SELECT Pnome, Unome, Salario<br>FROM FUNCIONARIO<br>WHERE Salario NOT IN (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT Salario**<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM FUNCIONARIO**<br>&nbsp;&nbsp;&nbsp;&nbsp;**WHERE Salario < ANY (**<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**SELECT Salario**<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**FROM FUNCIONARIO )** )|SELECT Pnome, Unome, Salario<br>FROM FUNCIONARIO AS EXTERNA<br>WHERE Salario NOT IN (<br>&nbsp;&nbsp;&nbsp;&nbsp;**SELECT Salario**<br>&nbsp;&nbsp;&nbsp;&nbsp;**FROM FUNCIONARIO AS CENTRAL**<br>&nbsp;&nbsp;&nbsp;&nbsp;**WHERE EXISTS (**<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**SELECT Salario**<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**FROM FUNCIONARIO AS INTERNA<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE CENTRAL.Salario < INTERNA.Salario )** )|

<hr style="border:2px solid blue">
