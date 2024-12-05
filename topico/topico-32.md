## [Tópico 32] - Recuperação Após Falhas - Exercícios
###### *by Prof. Plinio Sa Leitao-Junior (INF/UFG)*

**Questão 01)** O uso registro de _log_ e atualização adiada implica que o sistema de recuperação deverá:<br>
(a) armazenar o valor antigo do item atualizado no _log_.<br>
(b) armazenar o novo valor do item atualizado no _log_.<br>
(c) armazenar o valor antigo e o novo do item atualizado no _log_. <br>
(d) armazenar somente os registros _Begin Transaction_ e _Commit Transaction_ no _log_.<br>

**Questão 02)** O protocolo _write-ahead logging_ (WAL) significa que:<br>
(a) a escrita de um item de dados deve ser feita antes de qualquer operação no _log_.<br>
(b) o registro de _log_ para uma dada operação deve ser escrito antes que os dados sejam gravados.<br>
(c) todos os registros de _log_ devem ser escritos antes que uma nova transação inicie sua execução.<br>
(d) o _log_ não precisa ser escrito para o disco.<br>

**Questão 03)** Em caso de falha de transação quando se usa registro de _log_ e atualização adiada, que operação(ões) é(são) necessária(s) ?<br>
(a) uma operação _undo_<br>
(b) uma operação _redo_<br>
(c) operações _undo_ e _redo_<br>
(d) nenhum das respostas acima<br>

**Questão 04)** O uso registro de _log_ e atualização imediata, um registro de _log_ para uma transação conteria ...<br>
(a) um nome de transação, um nome de item de dados e os valores antigo e novo do item.<br>
(b) um nome de transação, um nome de item de dados e o valor antigo do item.<br>
(c) um nome de transação, um nome de item de dados e o novo valor do item.<br>
(d) um nome de transação e um nome de item de dados.<br>

**Questão 05)** Para o comportamento correto durante a recuperação, as operações _undo_ e _redo_ devem ser ...<br>
(a) comutativas.<br>
(b) associativas.<br>
(c) idempotentes.<br>
(d) distributivas.<br>

**Questão 06)** Quando ocorre uma falha, o _log_ é consultado e cada operação é desfeita ou refeita. Este é um problema porque ...<br>
(a) pesquisar todo o _log_ é demorado.<br>
(b) muitos _redo_'s são desnecessários.<br>
(c) ambos (a) e (b).<br>
(d) nenhuma das opções acima.<br>

**Questão 07)** Em um esquema de recuperação baseado em _log_, o desempenho da recuperação pode ser melhorado por ...<br>
(a) escrever os registros de _log_ para o disco em cada commit da transação.<br>
(b) escrever os registros de _log_ apropriados para o disco durante a execução da transação.<br>
(c) esperar para escrever os registros de _log_ até que várias transações concluam (escrita em lote).<br>
(d) nunca escrever os registros de _log_ para o disco.<br>

**Questão 08)** Existe a possibilidade de rollback em cascata quando ...<br>
(a) uma transação escreve itens que foram escritos apenas por uma transação confirmada.<br>
(b) uma transação escreve um item que foi escrito anteriormente por uma transação não confirmada.<br>
(c) uma transação lê um item que foi escrito anteriormente por uma transação não confirmada.<br>
(d) ambos (b) e (c).<br>

**Questão 09)** Para lidar com falhas de mídia (disco), é necessário ...<br>
(a) que o SGBD apenas execute transações em um ambiente de usuário único.<br>
(b) manter uma cópia redundante do banco de dados.<br>
(c) nunca abortar uma transação.<br>
(d) tudo o que precede. <br>

