
### <b>Node Mapper</b>

****

Trata-se do elemento unificador, responsável por centralizar a gestão dos nodes, independente das camadas as quais pertencem. Bem como, dentre suas funções, possui a de conferir confiabilidade aos nodes, recurso necessário principalmente para a camada física (camada 1).

No Node Mapper ficam distinguidas as duas redes de nodes, a dos <b>nodes reais</b> de camada física, e a dos <b>nodes virtuais</b>, que são sub-processos.

As <b>funções básicas do Node Mapper</b>, tanto para os nodes reais, quanto para os nodes virtuais, são as de adicionar, excluir, e migrar.

<br>

****
### <b>Arquitetura</b>

<br> 

O Node Mapper trata-se de um <b>elemento unificador</b> para gestão dos nodes componentes, sendo eles de camada 1 ou 2.

Em linhas gerais, o <b>Node Mapper é um servidor</b> que é <b>iniciado na máquina em conjunto com a criação do primeiro processo principal</b>, isto é, o primeiro node real. O mesmo é criado em conjunto, isto é, ele funciona de modo independente, isso implica que o processo que o iniciou pode ser finalizado sem que isso afete no funcionamento do Node Mapper.

<br>

<b>Pontos importantes:</b>

- Cada <b>máquina</b> possui um <b>Node Mapper local</b> para reunir as informações pertencentes aos nodes que ali existem, sejam eles nodes reais ou virtuais.

- A existência do Node Mapper local é <b>persistente</b>, ou seja, caso o processo do mesmo seja por algum motivo finalizado, imediatamente por algum dos nodes, automaticamente e de modo concorrente, será criado um node servidor de Node Mapper local.

- Numa ação de migração <b>simples</b>, isto é, de um node para outro, onde ambos os nodes pertencem a mesma máquina física. A ação é mais simples, pois ambos nodes estão acessíveis através do Node Mapper local. Nestes casos será acessado o Node Mapper local e obtido os ID de ambos os nodes envolvidos na migração, e a migração será então realizada.

- No entanto, há casos onde ocorre a migração mais <b>complexa</b>, isto é, de um node para outro em posição distante na rede de nodes reais, ou seja, de um node que existe em uma máquina física A, para uma máquina física B. Neste caso ocorre o seguinte: 

    1. É necessário informar o <b>ID</b> do node de destino, pois este ID não existe no Node Mapper local.
   
    2. É inserida uma <b>mensagem na rede</b> para confirmar a existência do node de destino. A mensagem é então propagada em toda a rede até chegar no destino, passando assim por todos os pontos da rede. A mensagem possui uma <b>assinatura única</b>, para na sua propagação a mesma não ser propagada de modo duplicado, ou seja, quando um node já enviou aquela mensagem para outro node, fica um registro, para assim evitar reenvia-la sem necessidade (tendo em vista que toda troca de informações entre os nodes exige uma confirmação, para ter certeza que a mensagem foi enviada pro node conectado mais próximo).
   
    3. Quando a mensagem <b>encontra seu destino</b>, ou seja, é confirmado que há naquela máquina o respectivo <b>node de destino</b>, então é enviado por esta mesma máquina que validou a ação, também uma mensagem de resposta, a mesma é propagada na rede, desta vez confirmando a existência do node em questão.
   
    4. Note que tais mensagens são trafegadas através da rede de nodes reais (camada 1).

    5. Quando o devido node recebe a <b>mensagem de confirmação</b>, ele passa então a realizar propriamente a migração.
    
    6. Congelando o estado do node a ser migrado, copiando suas informações, e transmitindo-as através dos nodes da rede de nodes reais, até que todos os dados cheguem no node destinatário e sejam então carregados.
    
    7. Após tudo ser realizado, é também enviada uma mensagem de confirmação final para o node que iniciou a ação. E quando o node que iniciou a ação recebe esta mensagem, ele limpa todos os dados de memória e ações semelhantes do node migrado, deixando o mesmo "zerado".
   
    8. E assim finalizando a migração.
    
<br>

****
### <b>Layer 1 - Nodes Reais</b>

<br>

Se tratando da camada 1, isto é, da camada física, a ideia deste conceito é dar um dinamismo para a infraestrutura física, podendo adicionar, remover, ou alterar, nodes componentes desta mesma infraestrutura.

Os nodes de camada 1 são gestionados através das operações do Node Mapper, podendo então adicionar, excluir e realizar ações semelhantes.

<br>

<b>Questões gerais:</b>

- Ao <b>criar</b> um node de camada física manualmente ou dinamicamente, em todos os casos é de modo conjunto criado um node virtual (que é um sub-processo num processo principal). Pois na medida em que vai se formando a rede de nodes, também vai automaticamento sendo criada a abstração de camada 2, isto é, dos nodes virtuais. De modo que, <b>proporcionalmente à topologia dos nodes de camada 1, será também criado uma topologia identica de nodes de camada 2.</b> Ficando assim duas redes sobrepostas, uma de camada 1, outra de camada 2. Sendo a topologia básica da camada 2, inicialmente proporcionalmente equivalente a topologia da camada 1. 

- Mesmo que os nodes virtuais proporcionais à topologia da camada 1 não estejam sendo utilizados, os mesmos existem necessariamente em conjunto com o node real. Pois o mesmo trata-se da camada de abstração de recursos criada, e é sobre esta (camada 2) que será executado o sistema (camada 3).

<br>

<b>Funcionalidades básicas do Node Mapper:</b>

- Ao <b>criar/adicionar</b> um novo node em máquinas que não possuem nenhum node executando, necessariamente se exige que o primeiro node seja criado <b>manualmente</b> utilizando da suite da linguagem.

- Também pode-se criar <b>dinamicamente</b> (via código, camada 3 / sistema) novos nodes de camada 1, tais nodes serão novos processos na máquina. Do mesmo modo, pode-se gestioná-los (excluir, migrar, etc). Tal ação é realizada através de algum sistema que está sendo executado em algum node virtual (camada 2) já existente.
  
- Ao <b>excluir</b> um node real, tudo que há nele é perdido. Logo, antes de simplesmente excluir um node real de uma rede de nodes, deve-se realizar a migração do mesmo, isto é, das coisas contidas no mesmo, para não haver assim perdas. Excluir um node real, significa que o mesmo será removido da rede, ou seja, é enviado uma mensagem ao mesmo para que o processo seja finalizado, e assim ocorrerá, e o mesmo ficará desconectado da rede.

- Ao <b>migrar</b> um node real, o que ocorre é que todas as coisas componentes deste node serão copiadas para outro node. Em casos onde envolvem conexões de rede abertas, tais como se o node em questão ser algum servidor HTTP, ou coisa semelhante, tais conexões serão resetadas neste momento, podendo haver perda de dados (a gestão dessas informações ficam a critério do design do sistema). Do mesmo modo, interações com o sistema de arquivos pode ser afetado, logo, tais ações também devem ser previstas e melhor arquitetadas no design do sistema. <b>Migrar</b>, em poucas palavras, significa copiar os dados de memória, e toda a AST atual em execução, com todas as informações relacionadas, bem como todos os nodes virtuais criados, isto é, todas as coisas existentes no node real em questão, copiar estas coisas para outro node real destinatário, e por tudo em execução, conservando assim estados do sistema nessa migração.

- Vale citar que na migração o node real em questão não é excluído, apenas suas informações são migradas para outro node real destinatário. A topologia da rede de nodes reais não é afetada em absolutamente nada.

<br>

<b>Questões pertinentes:</b>

- <b>Sobre como lidar com as informações</b>: quando se utiliza um node para interagir com o sistema de arquivos diretamente, bem como ser um servidor em alguma porta de rede, ou alguma ação de natureza semelhante, isto é, alguma ação que não pode simplesmente ser interrompida. Coisa que caso ocorresse acarretaria fatalmente na perda de informações importantes. Nestes casos convêm organizar a arquitetura do sistema de tal maneira que, tais nodes possam ser migrados sem perda de dados. Tal coisa pode ser feita utilizando um node de nível superior que possui como função apenas redirecionar pacotes, informações, e coisas semelhantes, para outros nodes de níveis inferiores. Ou seja, os nodes que processam propriamente informações numa interação maior, tais como com o sistema de arquivos, devem realizar o processamento livremente. E caso seja necessário paralizar este node em questão, deve-se simplesmente interromper o fluxo de informações/dados direcionados ao mesmo. Em seguida, aguardar que o node conclua o processamento de suas respectivas informações. E logo após isto, ou seja, quando o node está sem processar absolutamente nada, simplesmente, por fim, gestioná-lo. Ou seja, podendo excluí-lo, manipulá-lo alterando códigos, e ações semelhantes. Desta maneira, ou com noções semelhantes, se evitam perdas de dados/informações.

<br>

****
### <b>Layer 2 - Nodes Virtuais</b>

<br>

Assim como na camada 1, o Node Mapper possui como propósito a também dar um certo dinamismo para a camada 2.

Podendo então realizar as mesmas operações básicas de <b>adicionar</b>, <b>excluir</b> e <b>migrar</b> nodes virtuais.

<br>

<b>Esclarecimentos:</b>

- Ao <b>adicionar</b> um novo node, tal operação pode ser feita manualmente através da suite da linguagem, ou dinamicamente através do uso da própria linguagem (código).
  
- Do mesmo modo que acima, podem ser realizadas as operações de <b>exclusão</b> e <b>migração</b> de nodes virtuais.

- A respeito da <b>migração</b>, serão migrados todas as coisas hierarquicamente inferiores ao próprio node virtual em questão, isto é, outros nodes criados a partir do mesmo, AST das coisas em execução, e todas as informações relacionadas.

<br>

****
### <b>Node Mapper - Unificação</b>

<br>

Há a necessidade de se possuir um <b>ponto de controle central</b> de toda a rede de nodes. Ou seja, algum ponto onde funcione como uma central de comandos e que possui acesso as informações de todos os nodes componentes da rede.

Para suprir essa necessidade existe um comando especial no Node Mapper, para realizar a <b>varredura</b> da rede.

É então, no Node Mapper local, criada a noção de unificação da rede, ou seja, um ponto da rede que possui acesso as informações das coisas que compõem a própria rede.

<br>

<b>Questões gerais:</b>

- É inserida uma mensagem na rede, e nela propagada, solicitando as informações de seus Node Mapper locais (comando de varredura).

- Tais informações são então reunidas no Node Mapper da máquina em questão, a através do mesmo podem ser realizadas as ações de adicionar, excluir e migrar nodes, sejam eles nodes reais ou virtuais. 

- É recomendado que através desta mesma máquina seja então iniciado a execução do sistema (camada 3), pois o mesmo, possuindo seu core na mesma máquina, fica mais facilmente acessível as informações dos nodes da rede. Ou também, pode-se executar um node especial, servindo como serviço para informar aos solicitantes os nodes existentes na rede, desta maneira, outro node de alguma parte da rede, pode solicitar ao mesmo as informações de algum node de interesse em específico.
  

