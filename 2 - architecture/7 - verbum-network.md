### <b>Verbum Network</b>

****

Aplicação responsável por realizar a criação/gestão da Layer 1 e 2, cria e gestiona todos os nodes de camada 1 e 2. Contendo as noções e controles relacionados ao Node Mapper, questões do Fault Tolerance e outras questões relacionadas.

<br>

<b>Utilitários/ferramentas (gerais):</b>

- <b>verbum-node</b>: responsável por criar node.

- <b>verbum-node-mapper</b>: aplicação responsável por realizar o controle das ações envolvendo o Node Mapper. Aplicação principal (possui interface via rede).

- <b>Node Mapper Manager</b>: aplicação gráfica para gestão do Node Mapper.

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
  get-verbum-node-list
  ```
  <br>

- <b>Create new node</b>: cria novo node.

  ```
  create-verbum-node
  ```

<br>

- <b>Delete node</b>: exclui node.

  ```
  delete-verbum-node:NODE-ID
  ```

<br>

- <b>Check node exists</b>: verifica se um node existe dentro do Node Mapper, para que se possa realizar conexão com o mesmo. Caso o mesmo exista, é retornado sua porta de conexão. Caso não exista é retornado uma mensagem de erro.

  ```
  check-verbum-node-exists:NODE-ID
  ```

<br>

- <b>Create node client connection</b>: cria nova conexão de um node em outro (client -> server). Conexão de saída.
  ```
  create-verbum-node-client-connection:SRC-NODE-ID:DST-NODE-ID:DST-NODE-MAPPER-IP:DST-NODE-MAPPER-PORT
  ```

  <b>Campos:</b><br>
  1. <b>SRC-NODE-ID</b> - ID do node local.
  2. <b>DST-NODE-ID</b> - ID do node destinatário.
  3. <b>DST-NODE-MAPPER-IP</b> - IP do Node Mapper (onde encontra-se o node destinatário).
  4. <b>DST-NODE-MAPPER-PORT</b> - Porta do servidor Node Mapper.

  <br>
  <b>Da requisição ao Node Mapper:</b><br>

  1. Conecta-se no Node Mapper e envia as informações acima.
  2. O Node Mapper verifica se o ID existe, caso não existir retorna erro.
  3. Caso existir, envia as informações diretamente ao node, e aguarda a resposta.
  
  <br>
  <b>Do node ao controlador de requisições:</b><br>
  
  1. Node recebe a requisição, verifica se o ID é o dele, caso não seja retorna erro. Caso contrário, continua.
  2. Salva as informações em seu controlador de conexão, e acina flag para realizar o processamento da requisição. E fica aguardando a resposta para envia-la a quem realizou a requisição.
  
  <br>
  <b>Do controlador à conexão com os servidores:</b><br>

  1. O controlador das conexões identifica a ação e processa/realiza a conexão com o node destinatário: conecta no Node Mapper destinatário e verifica se existe o respectivo node, caso não, retorna erro, caso sim, continua. Note que esta ação é feita através do comando check-verbum-node-exists, onde em caso de sucesso é retornado as informações de conexão do node (porta remota da sua interface, e portas de conexão).
  2. Com as informações do node, realiza-se a conexão com o mesmo (cliente -> servidor). Note que a conexão é realiza com as portas dos servidores, e não com a interface de controle do node.
  3. A conexão é realizada, e mantida, enviando um ping periódico. Onde neste ping vai junto as devidas informações de controle e identificação da conexão (ID do node cliente, porta do Node Mapper, IP do Node Mapper [obs: o IP do node cliente, que por sua vez é o IP do Node Mapper, é pego através do socket.]).
  
  <br>
  <b>Do servidor à sua gestão das conexões:</b><br>

  1. O servidor recebe o ping periódico, e envia as informações do mesmo para o controlador das conexões.
  2. O controlador das conexões identifica a conexão através das informações do IP do Node Mapper, porta do Node Mapper, e do Node ID do cliente.

<br>
<br>

- <b>Create node server connection</b>: recebe informações de algum node existente. Quando um node conecta-se em outro, o node que estava servindo (server), ao receber a nova conexão de outro node da rede, informa o Node Mapper local que possui uma conexão de entrada.

  ```
  create-verbum-node-server-connection:SRC-NODE-ID:DST-NODE-ID:NODE-MAPPER-IP:NODE-MAPPER-PORT
  ```

<br>

- <b>Delete connection</b>: remove conexão de um node, independente de ser cliente ou servidor. Quando é servidor, informa o cliente conectado que deve remover a conexão.

  ```
  delete-connection:CONNECTION-ID
  ```

<br>

- <b>Send data</b>: envia um arquivo de dados através da infraestrutura da rede. Através do sistema de packets.

  ```
  ...
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


