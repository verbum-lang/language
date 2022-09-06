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

- <b>Create node output connection</b>: cria nova conexão de um node em outro (client -> server). Conexão de saída.
  ```
  create-verbum-node-output-connection:SRC-NODE-ID:DST-NODE-ID:DST-NODE-MAPPER-IP:DST-NODE-MAPPER-PORT
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
  4. Note que é mantida apenas uma conexão (de ping periódico), e caso necessário, através de multi-threading, são criadas N-conexões e enviados dados por elas (Send Data).
  5. Ao receber a mensagem de sucesso do ping periódico, é especificado no controlador que a conexão foi realizada.

  <br>
  <b>Do servidor à sua gestão das conexões:</b><br>

  1. O servidor recebe o ping periódico, e confirma seu recebimento com uma mensagem de sucesso. 
  2. O servidor envia as informações do mesmo para o controlador das conexões.
  3. O controlador das conexões identifica a conexão através das informações do IP do Node Mapper, porta do Node Mapper, e do Node ID do cliente.
  4. Ao processar as informações, periódicamente, envia para o Node Mapper local, junto com as informações do próprio node, que o mesmo possui uma conexão de INPUT.

<br>
<br>

- <b>Create node input connection</b>: cria uma conexão de entrada no node.
  ```
  create-verbum-node-input-connection:SRC-NODE-ID:DST-NODE-ID:DST-NODE-MAPPER-IP:DST-NODE-MAPPER-PORT
  ```

  <b>Campos:</b><br>
  1. <b>SRC-NODE-ID</b> - ID do node local.
  2. <b>DST-NODE-ID</b> - ID do node de interesse.
  3. <b>DST-NODE-MAPPER-ID</b> - ID do NM. É necessário apenas para conexão reversa. Recurso não necessário para conexão direta.
  4. <b>DST-NODE-MAPPER-IP</b> - IP do Node Mapper (onde encontra-se o node de interesse). Recurso necessário apenas para conexão direta. Na conexão reversa o recurso é ignorado.
  5. <b>DST-NODE-MAPPER-PORT</b> - Porta do servidor Node Mapper.

  <br>
  <b>Noções gerais:</b><br>

  1. É verificado se há conexão direta com o Node Mapper especificado, caso sim, continua e envia uma requisição de conexão do tipo output, do node de interesse ao node local. Se tudo for realizado com sucesso, então a conexão será criada e se terá uma resposta de sucesso.
  
  2. Caso não possa ser realizado uma conexão direta com o Node Mapper, entra em cena o recurso de <b>conexão reversa</b>. Onde a requisição é enviada para as conexões cliente, ou seja, os Node Mapper que se conectam neste Node Mapper em questão. Onde na resposta da verificação do ping é enviada a requisição. O outro Node Mapper, ao recebe-la, processa-a, ou seja, realizando a devida conexão do node de interesse com o node local.
   
  3. <b>Nota</b>: para realizar a conexão reversa, é necessário que exista conexão de entrada no Node Mapper em questão, caso não existir nenhum Node Mapper, retorna o erro para quem realizou a requisição.
  4. <b>Nota</b>: caso exista dois ou mais Node Mapper com ID repetido, a requisição é enviada aos mesmos.

  <br>

  <b>Noções gerais da conexão reversa:</b><br>

  1. Nas respostas do ping, há sempre um "verbum-node-ok". Quando ocorre de alguma outra informação ser necessário de enviar ao node que se conecta, a mesma é enviada nesta resposta. De modo que o ping também funciona como um verificador de requisições destinadas a ele.
   
  2. Ao receber uma requisição para processar, a mesma é enviada para o mesmo processador das requisições, no qual o servidor (input connection) utiliza.

<br>
<br>

- <b>Delete connection</b>: remove conexão de um node, independente de ser input ou output. Quando é input, informa o cliente conectado que deve remover a conexão.

  ```
  delete-connection:NODE-ID:CONNECTION-ID
  ```

<br>
<br>

- <b>Create Node Mapper connection</b>: realiza o pareamento de um Node Mapper com outro, através da conexão de um Node Mapper em outro.
  
  ```
  create-verbum-node-mapper-connection:DST-NODE-MAPPER-IP:DST-NODE-MAPPER-PORT
  ```

  Ao realizar a conexão, o mesmo retorna também seu ID.<br><br>

  Este recurso é importante, pois através dele ocorre o envio de requisições via conexão reversa entre os Node Mapper existentes.<br><br>

  <b>Nota</b>: quando um NM conecta-se em outro, o que funciona como servidor, também salva as devidas informações, tais como o NM ID, NM IP e NM Port. De modo que essa mesma informação possa vir a ser utilizada posteriormente.

<br>
<br>

- <b>Send data</b>: envia um bloco de dados através da infraestrutura da rede. Através do sistema de packets.

  ```
  ...
  ```

  <b>Noções gerais da conexão reversa:</b><br>

  1. Nas respostas do ping, há sempre um "verbum-node-ok". Quando ocorre de alguma outra informação ser necessário de enviar ao node que se conecta, a mesma é enviada nesta resposta. De modo que o ping também funciona como um verificador de requisições destinadas a ele. Sendo isto também um servidor.
   
  2. Ao receber uma requisição para processar, a mesma é enviada para o mesmo processador das requisições, no qual o servidor (input connection) utiliza. E a mesma é então processada.

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


