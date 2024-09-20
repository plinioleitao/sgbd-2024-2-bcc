## Resultado

Clique [AQUI](../media/sgbd-2024-2-bcc-resumo.pdf) para ver as notas.

#### Avaliação em 12/09/2024

(V) Uma página em um _buffer_ do SGBD... (F) O _buffer pool_ do SGBD é tipicamente... (V) O acesso a dados por meio... (F) Em um sistema em que a CPU fica ociosa... (V) Quando o gerenciador de _buffer_ precisa... (F) Uma página é substituída de... (F) Se a memória principal e a memória _cache_... (V) Se os registradores e a _cache_... (V) No contexto da hierarquia de memória... (V) O custo de armazenamento por unidade de dados... (F) As várias camadas de _cache_... (V) O emprego de _pin-count_ nas páginas... (V) O processo de _design_ de banco de dados... (V) A organização de arquivos determina... (V) Em cada transação, aplicações... (V) Na hierarquia de memória, a _cache_... (F) Quanto mais "perto"... (F) O _dirty bit_ pode ser aplicado... (V) Várias transações do banco de dados... (V) Uma modificação da política _clock policy_... 

#### Avaliação em 19/09/2024

(F) A função teto é em geral... (V) A função piso é em geral... (V) Quando o tamanho do bloco... (V) Em alocação de blocos... (F) Na política FIFO de gerência... (F) A política FIFO requer... (F) Na organização de registros não espalhada, é previsto... (V) A organização de registros não espalhada é aplicável... (F) O _pin-count_ determina se... (F) Se o _pin-count_ de uma página... (F) Independente do predicado de busca... (V) A busca binária em arquivos de dados requer conhecer o endereço de cada bloco.
(V) O tamanho do buffer pool em geral é um parâmetro para o SGBD, que é especificado pelo administrador de banco de dados. (F) Em arquivos com registros de tamanho fixo, o cabeçalho de bloco necessariamente possui a posição inicial de cada registro.
(V) Registros de comprimento variável são aplicáveis às organizações de registros espalhada e não espalhada. (F) Em registros de tamanho variável, qualquer ponteiro externo ao bloco deve apontar diretamente para qualquer dos registros no bloco.
(V) O cabeçalho de arquivo em geral contém informações necessárias para o efetivo acesso aos registros do arquivo. (V) A estratégia double buffering permite a leitura ou gravação contínua de dados em blocos consecutivos em disco.
(V) Em arquivos de registros de tamanho fixo e variável, os registros podem ser movimentados dentro de uma página para mantê-los contíguos. (V) Há cenários em que o SGBD necessita gravar buffers em determinados blocos no disco, mesmo que seu buffer não tenha sido selecionado para substituição.

