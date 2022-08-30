### <b>Verbum Network</b>

****

Aplicação responsável por realizar a criação/gestão da Layer 1 e 2, cria e gestiona todos os nodes de camada 1 e 2. Contendo as noções e controles relacionados ao Node Mapper, questões do Fault Tolerance e outras questões relacionadas.

<br>

<b>Utilitários/ferramentas (gerais):</b>

- <b>verbum-network</b>: responsável por iniciar os respectivos setores da solução.

- <b>verbum-node-mapper</b>: aplicação responsável por realizar o controle das ações envolvendo o Node Mapper.

- <b>verbum-fault-tolerance</b>: responsável por controlar as ações referentes à alta tolerância a falhas (logs e semelhantes).

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

- <b>build-scripts/build-all.sh</b>: compila todos os projetos, salva os binários no diretório atual (verbum-network) com seus respectivos nomes (verbum-node-mapper, verbum-fault-tolerance).

<br>

****

### <b>Node Mapper - Protocol</b>

<br>

<b>Interface:</b>

- <b>Handshake</b>: é realizado lendo o banner.
  ```
  Verbum Node Mapper - vX.Y.Z - I Love Jesus <3
  ```

- <b>Gera node</b>: gera novo ID para node, e cadastra ele na estrutura de controle (fica salvo no Node Mapper).
  ```
  generate-verbum-node-id:PORT
  ```
  Como resposta da requisição é retornado o ID único para o node.
  
- <b>Ping node</b>: realiza ping periódico para persistir conectado, bem como informar a última conexão.
  ```
  ping-verbum-node:node-id
  ```

- <b>Get node list</b>: retorna lista dos nodes existentes no Node Mapper, com suas respectivas informações (atualmente dump para análise).
  ```
  get-node-list
  ```


