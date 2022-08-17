
### <b>Node Mapper</b>

****

Trata-se do elemento unificador, responsável por centralizar a gestão dos nodes, independente das camadas as quais pertencem. Bem como, dentre suas funções, possui a de conferir confiabilidade aos nodes, recurso necessário principalmente para a camada física (camada 1).

<br>

****
### <b>Layer 1</b>

<br>

Se tratando da camada 1, isto é, da camada física, a ideia deste conceito é dar um dinamismo para a infraestrutura física, podendo adicionar, remover, ou alterar, nodes componentes desta mesma infraestrutura.

Os nodes de camada 1 são gestionados através das operações do Node Mapper, podendo então adicionar, excluir e realizar ações semelhantes.

<br>

<b>Questões gerais:</b>

- Ao <b>criar</b> um node de camada física manualmente ou dinamicamente, em todos os casos é de modo conjunto criado um node virtual (que é um sub-processo num processo principal). Pois na medida em que vai se formando a rede de nodes, também vai automaticamento sendo criada a abstração de camada 2, isto é, dos nodes virtuais. De modo que, <b>proporcionalmente à topologia dos nodes de camada 1, será também criado uma topologia identica de nodes de camada 2.</b> Ficando assim duas redes sobrepostas, uma de camada 1, outra de camada 2. Sendo a topologia básica da camada 2, inicialmente proporcionalmente equivalente a topologia da camada 1. 

- Mesmo que os nodes virtuais proporcionais à topologia da camada 1 não estejam sendo utilizados, os mesmos existem necessariamente em conjunto com o node real. Pois o mesmo trata-se da camada de abstração de recursos criada, e é sobre esta (camada 2) que será executado o sistema (camada 3).

<br>

<b>Funcionalidades básicas do Node Mapper:</b>

- Ao <b>criar</b> um novo node em máquinas que não possuem nenhum node executando, necessariamente se exige que o primeiro node seja criado <b>manualmente</b> utilizando da suite da linguagem.

- Também pode-se criar <b>dinamicamente</b> (via código, camada 3 / sistema) novos nodes de camada 1, tais nodes serão novos processos na máquina. Do mesmo modo, pode-se gestioná-los (excluir, migrar, etc). Tal ação é realizada através de algum node virtual (camada 2) já existente.
  
- Ao <b>excluir</b> um node real, tudo que há nele é perdido. Logo, antes de simplesmente excluir um node real de uma rede de nodes, deve-se realizar a migração do mesmo, isto é, das coisas contidas no mesmo, para não haver assim perdas. Excluir um node real, significa que o mesmo será removido da rede, ou seja, é enviado uma mensagem ao mesmo para que o processo seja finalizado, e assim ocorrerá, e o mesmo ficará desconectado da rede.

- Ao <b>migrar</b> um node real, o que ocorre é que todas as coisas componentes deste node serão copiadas para outro node. Em casos onde envolvem conexões de rede abertas, tais como se o node em questão ser algum servidor HTTP, ou coisa semelhante, tais conexões serão resetadas neste momento, podendo haver perda de dados (a gestão dessas informações ficam a critério do design do sistema). Do mesmo modo, interações com o sistema de arquivos pode ser afetado, logo, tais ações também devem ser previstas e melhor arquitetadas no design do sistema. <b>Migrar</b>, em poucas palavras, significa copiar os dados de memória, e toda a AST atual em execução, com todas as informações relacionadas, bem como todos os nodes virtuais criados, isto é, todas as coisas existentes no node real em questão, copiar estas coisas para outro node real destinatário, e por tudo em execução, conservando assim estados do sistema nessa migração.

<br>

<b>Questões pertinentes:</b>

- <b>Sobre como lidar com as informações</b>: quando se utiliza um node para interagir com o sistema de arquivos diretamente, bem como ser um servidor em alguma porta de rede, ou alguma ação de natureza semelhante, isto é, alguma ação que não pode simplesmente ser interrompida. Coisa que caso ocorresse acarretaria fatalmente na perda de informações importantes. Nestes casos convêm organizar a arquitetura do sistema de tal maneira que, tais nodes possam ser migrados sem perda de dados. Tal coisa pode ser feita utilizando um node de nível superior que possui como função apenas redirecionar pacotes, informações, e coisas semelhantes, para outros nodes de níveis inferiores. Ou seja, os nodes que processam propriamente informações numa interação maior, tais como com o sistema de arquivos, devem realizar o processamento livremente. E caso seja necessário paralizar este node em questão, deve-se simplesmente interromper o fluxo de informações/dados direcionados ao mesmo. Em seguida, aguardar que o node conclua o processamento de suas respectivas informações. E logo após isto, ou seja, quando o node está sem processar absolutamente nada, simplesmente, por fim, gestioná-lo. Ou seja, podendo excluí-lo, manipulá-lo alterando códigos, e ações semelhantes. Desta maneira, ou com noções semelhantes, se evitam perdas de dados/informações.




