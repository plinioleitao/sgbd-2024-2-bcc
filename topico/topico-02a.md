## [Tópico 02a] - Exercícios de revisão (1/4)
###### *by Prof. Plinio Sa Leitao-Junior (INF/UFG)*

<hr style="border:2px solid blue">

#### <ins>EXERCÍCIO:</ins> Qual a distinção entre ?
- Esquema conceitual, esquema lógico e esquema físico.
- Requisitos de software e requisitos de dados.
- Independência lógica e independência física.
- Dado e metadado.
- Definição, construção e manipulação de banco de dados.
- Banco de dados e sistema gerenciador de banco de dados.
- Tipo de dado e restrição de integridade.
- Modelo de dados e esquema de banco de dados.
- Redundância e redundância controlada.
- Independência física e independência lógica.
- Modelo entidade relacionamento e modelo relacional.

<hr style="border:2px solid blue">

#### <ins>EXERCÍCIO:</ins> Quais as possíveis inconsistências no diagrama abaixo ?

<img src="../media/revisao-der-00.jpg" width="600">

<hr style="border:2px solid blue">

#### <ins>EXERCÍCIO:</ins> Quais as possíveis inconsistências no diagrama abaixo ?

<img src="../media/revisao-der-01.jpg" width="500">

<hr style="border:2px solid blue">

#### <ins>EXERCÍCIO:</ins> Que esquema conceitual de banco de dados, segundo o MER, pode ser empregado para suportar consultas por quaisquer parentes de determinada pessoa ?

<hr style="border:2px solid blue">

#### <ins>EXERCÍCIO:</ins> Por que a <ins>ordenação de _tuplas_</ins> não é relevante no contexto do <ins>modelo relacional</ins> ?

<hr style="border:2px solid blue">

#### <ins>EXERCÍCIO:</ins> O que significa <ins>valor nulo</ins> no jargão de banco de dados ? Quais as semelhanças e distinções entre ?
- Valor nulo e valor ausente.
- Valor nulo e informação.

<hr style="border:2px solid blue">

#### <ins>EXERCÍCIO:</ins> No contexto do modelo relacional, qual a distinção entre os conceitos:
- Restrição de integridade de chave, restrição de integridade de entidade, restrição de integridade de domínio e restrição de integridade referencial.
- Superchave, chave candidata, chave primária e chave estrangeira.
- Distintos valores que um atributo pode ter e número total de distintos valores que um atributo pode ter.

<hr style="border:2px solid blue">

#### <ins>EXERCÍCIO:</ins> No contexto do modelo relacional, analisar as sentenças:
- Um banco de dados é tipicamente composto por várias relações.
- Em geral, cada _tupla_ de um banco de dados se relaciona com uma ou mais _tuplas_ (via a associação entre chave estrangeira e chave primária).

<hr style="border:2px solid blue">

#### <ins>EXERCÍCIO:</ins> No contexto do modelo relacional, que conceito se refere em ?

- Conjunto de esquemas de relação: { R1, R2, ..., Rm }.
- Conjunto de relações: { r1(R1), r2(R2), ..., rm(Rm) }.
- R(A1, A2, ...,An).
- Conjunto de n-tuplas: { t1, t2, ..., tm }.
- Lista ordenada de n valores: <v1, v2, ..., vn>.
- Nenhum valor de chave primária pode ser NULL.

<hr style="border:2px solid blue">

#### <ins>EXERCÍCIO:</ins> Qualquer relação é um <ins>subconjunto</ins> do <ins>produto cartesiano</ins> entre os <ins>conjuntos de domínios</ins> dos atributos da relação ?
- Se R(A1, A2, ...,An), então
- r(R) ⊆ ( dom(A1) × dom(A2) × ... × dom(An) ) ?

<hr style="border:2px solid blue">

#### <ins>EXERCÍCIO:</ins> Um banco de dados simples (**BD Simples**):

> <ins>Esquema conceitual</ins>:

<img src="../media/fig-der-simples-1.jpg" width="350">

> <ins>Esquema lógico</ins>:

&#8718; PRODUTO(<ins>CodProduto</ins>, Descrição, Preço, _Categ_)<br>
&#8718; CATEGORIA(<ins>CodCateg</ins>, Nome)<br>
&#8718; PRODUTO(Categ) REFERENCIA CATEGORIA(CodCateg)<br>

> <ins>Ilustração</ins>:

CATEGORIA
| <ins>CodCateg</ins> | Nome |
|-|-|
| **papel** | Papelaria e escritório |
| **esporte** | Material esportivo |

PRODUTO
| <ins>CodProduto</ins> | Descrição | Preço | _Categ_ |
|-|-|-|-|
| **1234** | Lápis | 0.70 | _papel_ |
| **1111** | Bola | 20.00 | _esporte_ |
| **2222** | Caneta | 1.20  | _papel_ |
| **1212** | Meião | 12.40 | _esporte_ |
| **1112** | Viseira| 12.40 | _esporte_ |

Quais as restrições de integridade - _domínio_, _chave_, _integridade de entidade_ e _integridade referencial_ - são violadas em cada uma das seguintes operações?<br>
**(a)** Incluir a _tupla_ **<NULL,"Boné",12.00,"vestuário">** em PRODUTO.<br>
**(b)** Incluir a _tupla_ **<1212,"Borracha",2.10,"papel">** em PRODUTO.<br>
**(c)** Incluir a _tupla_ **<1212,2.10,"Borracha","papel">** em PRODUTO.<br>
**(d)** Alterar a _tupla_ **<"papel","Papelaria e escritório">** para **<"papeis","Papelaria e Outros">** em CATEGORIA.<br>
**(e)** Excluir a _tupla_ **<"papel","Papelaria e escritório">** em CATEGORIA.<br>
**(g)** Alterar a _tupla_ **<"papel","Papelaria e escritório">** para **<"papelaria","Papelaria e Escritório">** em CATEGORIA.<br>
**(h)** Excluir a _tupla_ **<1111,"Bola",20.00,"esporte">** em PRODUTO.

IMPORTANTE:<br>
&#8718; Para analisar cada operação, considere o banco de original conforme a ilustração. Por exemplo, para analisar a operação em (d), desconsidere possíveis modificações no banco de dados pelas operações em (a), (b) e (c).<br>
&#8718; Ao responder, calcule o somatório dos números que identificam cada restrição violada pela operação:<br>
(01) Restrição de domínio<br>
(02) Restrição de chave<br>
(04) Restrição de integridade de entidade<br>
(08) Restrição de integridade referencial<br>

<hr style="border:2px solid blue">
