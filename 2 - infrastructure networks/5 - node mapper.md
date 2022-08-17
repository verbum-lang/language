
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

- Ao <b>migrar</b> um node real, o que ocorre é que todas as coisas componentes deste node serão copiadas para outro node. Em casos onde envolvem conexões de rede abertas, tais como se o node em questão ser algum servidor HTTP, ou coisa semelhante, tais conexões serão resetadas neste momento, podendo haver perda de dados (tal gestão das informações fica a critério do design de infraestrutura adotado).



