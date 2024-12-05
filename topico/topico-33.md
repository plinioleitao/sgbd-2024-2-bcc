## [Tópico 33] - Recuperação Após Falhas
###### *by Prof. Plinio Sa Leitao-Junior (INF/UFG)*

### <ins>CONTEÚDO</ins>

|_Item do conteúdo_|_Item do conteúdo_|
|-|-|
|1. Visão geral|4. Exemplos|
|2. Políticas de atualização|5. _Checkpoint_|
|3. <ins>**IMPLEMENTAÇÃO DAS<br>POLÍTICAS DE ATUALIZAÇÃO**</ins>|6. |

<hr style="border:2px solid blue">

### 3. <ins>IMPLEMENTAÇÃO DAS POLÍTICAS DE ATUALIZAÇÃO</ins>

O [emprego de um] algoritmo de recuperação &#8212; `NO-UNDO/REDO`, `UNDO/REDO` e `UNDO/NO-REDO` &#8212; impacta:<br>
&#9888; o conteúdo dos registros de LOG;<br>
&#9888; a política de gerenciamento de _buffers_;<br>
&#9888; as estruturas de dados empregadas.

<hr style="border:2px solid blue">

#### &#9752;&#x270D;&#9745; CONTEÚDO DO _LOG_ </ins>

A depender do algoritmo de recuperação &#8212; `NO-UNDO/REDO`, `UNDO/REDO` e `UNDO/NO-REDO`, o conteúdo do LOG possui:<br>
&#9918; **_BeFore IMage (BFIM)_** &#8212; o valor do item de dados ANTES da operação de escrita; E/OU<br>
&#9918; **_AFter IMage (AFIM)_** &#8212; o valor do item de dados APÓS da operação de escrita.<br>

O conteúdo do LOG para os algoritmos:
|Algoritmo|BFIM|AFIM|
|:-:|:-:|:-:|
|NO-UNDO/REDO||XXX|
|UNDO/REDO|XXX|XXX|
|UNDO/NO-REDO|XXX||

Se o modo de <ins>escalonamento</ins> permitir o <ins>aborto em cascata</ins> de transações:<br>
&#9888; As entradas **_read_item_** no _LOG_ são consideradas entradas do tipo UNDO.

<hr style="border:2px solid blue">

#### &#9752;&#x270D;&#9745; GERÊNCIA DE _CACHE_ &#8212; _BUFFER POOL_</ins>

O termo <ins>_Cache_ do SGBD</ins> denota os _buffers_ em memória principal gerenciados pelo próprio SGBD (ou seja, o _buffer pool_):<br>
&#10004; A _cache_ inclui páginas pertinentes a:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... blocos [de arquivos] de dados,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... blocos [de arquivos] de índice e<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... **blocos [de arquivos] de _LOG_**.<br>
&#10004; Os termos <ins>_cache_ de dados</ins> e <ins>_buffer_ de dados</ins> são relacionados, e<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... se referem à área de memória para blocos de dados;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... o mesmo raciocínio serve para ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<ins>_cache_ de _LOG_</ins> e <ins>_buffer_ de _LOG_</ins> ;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<ins>_cache_ de índice</ins> e <ins>_buffer_ de índice</ins>.

Sobre os <ins>**_buffers_ de _LOG_**</ins>:<br>
&#10004; Há vários blocos no arquivo de _LOG_ ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... os últimos blocos de LOG estão no _buffers_ de _LOG_ .<br>
&#10004; Ao gravar um registro de _LOG_ ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... o registro é gravado no <ins>último _buffer_ de _LOG_</ins> ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... vale lembrar que o arquivo de _LOG_ é do tipo _append-only_.

Conforme a premissa **`write-ahead logging — WAL`**:<br>
&#9888; Quando uma operação **_write_item_** ocorre para o item de dado **X**:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; (1) um registro é gravado no último _buffer_ de LOG,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; pertinente à operação de escrita;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; (2) o item de dado X é gravado no _buffer_ de dados apropriado;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; (3) a <ins>gravação em disco</ins> do _buffer_ de dados deve ocorrer APÓS a gravação em disco do _buffer_ de LOG ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;e segundo a política de atualização adotada (atualização imediata, adiada, ...).

```diff
! QUESTÃO:
!    Quando gerenciar para que uma página da cache de dados possa ser gravada em disco?
```

**`Terminologia — Regras STEAL / NO-STEAL`** :<br>
Se alguma página em um <ins>_buffer_ de dados</ins> for MODIFICADA [por uma transação]:<br>
&#10004; **`NO-STEAL`** &#8212; A página <ins>NÃO PODE ser gravada no disco</ins> ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... ANTES QUE a transação seja confirmada E ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ANTES QUE tenha o _commit_ gravado no LOG em disco;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... O _pin-bit_ é definido como 1 (ou pin-count > 0, ver [Tópico 04](./topico-04.md)), para '_fixar a página em memória_';<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... A operação UNDO não será necessária durante a recuperação.<br>
&#10004; **`STEAL`** &#8212; A página <ins>PODE ser gravada imediatamente no disco</ins> ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... E tal libera o _buffer_ para ter seu conteúdo substituído.

**`Terminologia — Regras FORCE / NO-FORCE`** :<br>
Se uma ou mais as páginas em <ins>_buffers_ de dados</ins> forem MODIFICADAS [por uma transação]:<br>
&#10004; **`FORCE`** &#8212; TODAS as páginas <ins>DEVEM ser gravadas no disco</ins> ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... ANTES QUE a transação seja confirmada E ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ANTES QUE tenha o _commit_ gravado no LOG em disco;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;... A operação UNDO não será necessária durante a recuperação.<br>
&#10004; **`NO-FORCE`** &#8212; As páginas <ins>PODEM ser gravadas no disco</ins> ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... APÓS o término da transação.

Os SGBDs em geral empregam as regras **`STEAL`** / **`NO-FORCE`** (algoritmo `UNDO/REDO`):<br>
&#9752; `STEAL` <ins>evita ter um _buffer_ muito grande</ins> para [armazenar] todas as páginas atualizadas na memória.<br>
&#9752; `NO-FORCE` <ins>permite que uma página atualizada permaneça no _buffer_</ins> [após a transação ser confirmada] ...<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... caso outra transação [potencialmente] necessite atualizar a página,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... o que <ins>reduziria o custo de E/S</ins>, ao evitar que a página fosse gravada várias vezes no disco:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;a redução de custo é ainda maior se a página for atualizada [intensamente] por múltiplas transações.

_Write-ahead logging_ (**`WAL`**) e regra **`FORCE`** :<br>
&#x270D; A regra `FORCE` é aplicada às páginas de LOG do tipo UNDO, devido às atualizações de uma transação,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... para então habilitar a gravação dos itens modificados no banco de dados [em disco].<br>
&#x270D; A regra `FORCE` é aplicada às páginas de LOG do tipo REDO e UNDO, devido às atualizações de uma transação,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ... para então habilitar a gravação do _COMMIT_ no LOG.

Emprego de <ins>listas para a implementação das políticas</ins> recuperação:<br>
&#9888; Lista de transações ativas que foram iniciadas, mas ainda não confirmadas.<br>
&#9888; Listas de todas as transações confirmadas e abortadas desde o último _checkpoint_ (ponto de verificação).<BR>
&#9888; Dentre outras ...
