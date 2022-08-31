### <b>Verbum Network</b>

****

Aplicação responsável por realizar a criação/gestão da Layer 1 e 2, cria e gestiona todos os nodes de camada 1 e 2. Contendo as noções e controles relacionados ao Node Mapper, questões do Fault Tolerance e outras questões relacionadas.

<br>

<b>Utilitários/ferramentas (gerais):</b>

- <b>verbum-node</b>: responsável por criar node.

- <b>verbum-node-mapper</b>: aplicação responsável por realizar o controle das ações envolvendo o Node Mapper.

<br>

<b>Obs: </b> é necessário ter as ferramentas configuradas acessíveis nas <b>variáveis de ambiente</b> do sistema operacional (sudo ln -s path/name /usr/bin/name).

<br>

<b>Diretórios:</b>

- <b>build-scripts</b>: scripts de compilação do código fonte.
  
- <b>source</b>: código fonte das soluções/ferramentas.

- <b>configuration</b>: arquivos de configurações de testes/exemplos.

<br>
Obs: no ambiente local de desenvolvimento e testes, os binários ficam no diretório <b>projects/sdk-binaries</b>.

<br>

<b>Questões gerais:</b>

- <b>build-scripts/build-all.sh</b>: compila todos os projetos, salva os binários no diretório do ambiente de desenvolvimento (projects/sdk-binaries) com seus respectivos nomes (verbum-node, verbum-node-mapper).

<br>

****

### <b>Verbum Node Mapper - Protocol</b>

<br>

<b>Interface:</b>

- <b>Handshake</b>: é realizado lendo o banner.
  ```
  Verbum Node Mapper - vX.Y.Z - I Love Jesus <3
  ```

  <br>

- <b>Node generation</b>: gera novo ID para node, e cadastra ele na estrutura de controle (fica salvo no Node Mapper).
  ```
  generate-verbum-node-id:PORT
  ```
  Como resposta da requisição é retornado o ID único para o node.
  
  <br>

- <b>Ping node</b>: realiza ping periódico para garantir persistência da disponibilidade do node.
  ```
  ping-verbum-node:NODE-ID:NODE-PORT
  ```
  Um dos propósitos deste recurso é fazer com que as informações do node seja re-enviadas para o Node Mapper, mantendo o mesmo sempre atualizado com as informações mais recentes. Recurso útil caso houver algum problema com o Node Mapper e ele vier a se reinicializar (persistência).

  <br>

- <b>Get node list</b>: retorna lista dos nodes existentes no Node Mapper, com suas respectivas informações (atualmente dump para análise).
  ```
  get-node-list
  ```
  <br>

- <b>Create new node</b>: cria novo node.

  ```
  create-node
  ```

<br>

- <b>Delete node</b>: exclui node.

  ```
  delete-node
  ```

<br>

- <b>Check node exists</b>: verifica se um node existe dentro do Node Mapper, para que se possa realizar conexão com o mesmo. Caso o mesmo exista, é retornado sua porta de conexão. Caso não exista é retornado uma mensagem de erro.

  ```
  check-node-exists:NODE-ID
  ```

<br>

- <b>Check node exists</b>: verifica se um node existe dentro do Node Mapper, para que se possa realizar conexão com o mesmo. Caso o mesmo exista, é retornado sua porta de conexão. Caso não exista é retornado uma mensagem de erro.

  ```
  check-node-exists:NODE-ID
  ```

<br>

- <b>Create node client connection</b>: cria nova conexão de um node em outro (client -> server). Conexão de saída.
  ```
  create-node-client-connection:SRC-NODE-ID:DST-NODE-ID:NODE-MAPPER-IP:NODE-MAPPER-PORT
  ```

  <b>Campos:</b><br>
  1. <b>SRC-NODE-ID</b> - ID do node local.
  2. <b>DST-NODE-ID</b> - ID do node destinatário.
  3. <b>NODE-MAPPER-IP</b> - IP do Node Mapper (onde encontra-se o node destinatário).
  4. <b>NODE-MAPPER-PORT</b> - Porta do servidor Node Mapper.

  <br>

  <b>Etapas gerais:</b><br>
  1. O Node Mapper local conecta-se no endereço do Node Mapper do node destinatário, para verificar se o node destinatário existe. Caso não exista a operação é cancelada.
   
  2. O Node Mapper local conecta-se no node local, informando-o que o mesmo deve se conectar no node destinatário (no caso são informados ao node o IP do Node Mapper, e a porta do node destinatário).

<br>

- <b>Create node server connection</b>: recebe informações de algum node existente. Quando um node conecta-se em outro, o node que estava servindo (server), ao receber a nova conexão de outro node da rede, informa o Node Mapper local que possui uma conexão de entrada.

  ```
  create-node-server-connection:SRC-NODE-ID:DST-NODE-ID:NODE-MAPPER-IP:NODE-MAPPER-PORT
  ```

<br>

- <b>Delete connection</b>: remove conexão de um node, independente de ser cliente ou servidor. Quando é servidor, informa o cliente conectado que deve remover a conexão.

  ```
  delete-connection:CONNECTION-ID
  ```

<br>

****

### <b>Verbum Node - Protocol</b>

<br>

<b>Interface:</b>

- <b>Handshake</b>: é realizado lendo o banner.
  ```
  Verbum Node - vX.Y.Z - I Love Jesus <3
  ```

  <br>

- <b>Create node client connection</b>: cria nova conexão de um node em outro (client -> server).
  ```
  create-node-client-connection:NODE-MAPPER-IP:NODE-PORT
  ```

  Obs: esta mesma conexão client-server, é também utilizada para realizar a conexão reversa. Ou seja, mesmo conectado como cliente, o node funciona por esse canal também como servidor. Deixando claro que o servidor padrão, isto é, com listagem de alguma porta de rede, também fica operando.


