## Tópico 22: Processamento de Transações

### Conteúdo

| Item |
| --- |
| 1. Visão Geral |
| 2. Escalonamento |
| 3. Escalonamento quanto à Recuperação |
| 4. Escalonamento quanto à Serialização |
| 5. Bloqueio de Itens do Banco de Dados |
| 6. Concorrência Baseada em Bloqueio |
| 7. Deadlock e Starvation |
| 8. Concorrência Baseada em Timestamp |

---

### 1. Visão Geral

**O que é uma Transação de Banco de Dados?**

- **Definição:** Mecanismo para descrever e caracterizar unidades lógicas de processamento em sistemas de banco de dados.
- **Função:** É uma unidade de execução que pode acessar e atualizar vários itens de dados.

**Características da Transação:**

- Delimitada por instruções como `início de transação` e `final de transação`.
- Escrita geralmente em SQL ou em uma linguagem de programação como C++ ou Java (via JDBC/ODBC).

**Exemplo de Transação:**

**Script para SQL Server:**

```sql
DROP TABLE IF EXISTS CONTA_CORRENTE;
CREATE TABLE CONTA_CORRENTE (numConta char(6), saldoConta money);
BEGIN TRANSACTION;
INSERT INTO CONTA_CORRENTE VALUES ('029820', 10000.00);
INSERT INTO CONTA_CORRENTE VALUES ('407302', 10000.00);
COMMIT TRANSACTION;
SELECT * FROM CONTA_CORRENTE;

DECLARE @contaDe char(6), @contaPara char(6), @Valor money;
SET @contaDe= '029820';
SET @contaPara= '407302';
SET @Valor= 1200.99;
BEGIN TRANSACTION;
UPDATE CONTA_CORRENTE SET saldoConta= saldoConta - @Valor WHERE numConta = @contaDe;
UPDATE CONTA_CORRENTE SET saldoConta= saldoConta + @Valor WHERE numConta = @contaPara;
COMMIT;
SELECT * FROM CONTA_CORRENTE;
