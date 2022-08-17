
### <b>Layer 1 - Node Físico</b>

****

A camada 1 é criada ao interconectar máquinas físicas numa infraestrutura de baseada em rede. Essa conexão entre as máquinas é realizada utilizando a suite da linguagem.

Na prática, utilizando a suite da linguagem se terá <b>um node rodando num único processo</b>. É possível abrir quantos processos quiser em uma máquina física, ou seja, é possível criar uma infraestrutura de camada 1 utilizando vários nodes, sem necessariamente precisar executar apenas um processo principal por máquina física. Ficando a critério de cada um como será organizada propriamente a infraestrutura física.

Tratando-se de uma infraestrutura física, deve-se possuir um meio de conferir confiabilidade a algum determinado node desta camada 1. Para isto existe o conceito de <b>Node Mapper</b> (mais adiante é abordado o mesmo).

<b>Exemplo de organização da rede na infraestrutura física:</b>

<p align="center" >
<br>
<img src="../0%20-%20extras/diagram/general-3.png?v=1" />
<br>
<br>
</p>

<b>Pontos importantes:</b>

- <b>Organização livre.</b> Pode-se organizar uma rede de nodes físicos como preferir.

- <b>Um node pode ter infinitas conexões</b>, e isto se aplica às noções de cliente e servidor. Ou seja, um node pode ter quantos clientes quiser, também pode se conectar em quantos servidores quiser. Claro que estes limites estão sujeitos aos limites físicos da própria máquina em questão onde o node está existindo.

- <b>As conexões de rede TCP/IP são todas persistentes</b>. Se não houver comunicação, o node ficará persistindo eternamentem, isto é, enquanto ele existir como processo ou sub-processo na máquina física.

- Quando <b>um novo node</b> de camada 1 vai se conectar a algum outro node da mesma camada, ou seja, será mais um novo node na rede em questão, <b>é necessário o endereço IP da máquina em rede, ou o ID do node</b>, caso ele exista como processo na mesma máquina em questão (neste caso este node será procurado no Node Mapper local).

- <b>Os nodes de camada física podem se conectar apenas a outros nodes da mesma camada.</b> Para as abstrações acima, isto é, de camada 2 (node virtual) e 3 (sistema), apenas o <b>Node Mapper</b> é acessível. Vale citar que através do Node Mapper é possível realizar a gestão dos nodes de camada 1. O importante a se ter em mente é que as abstrações maiores (camadas 2 e 3) são criadas sobre a abstração da camada 1, e por isto não pode um node virtual (camada 2) se comportar como um node real (camada 1), pois o sistema/aplicação será executado sobre a camada 2, isto é, dos nodes virtuais.

<br>

****

### <b>Node Mapper</b>

<br>

Trata-se do elemento unificador, responsável por centralizar a gestão dos nodes, independente das camadas as quais pertencem. Bem como, dentre suas funções, possui a de conferir confiabilidade aos nodes, recurso necessário principalmente para a camada física.

Se tratando da camada 1, isto é, da camada física, a ideia deste conceito é dar um dinamismo para a infraestrutura física, podendo adicionar, remover, ou alterar, nodes componentes desta mesma infraestrutura.

Os nodes de camada 1 são gestionados através das operações do Node Mapper, podendo então adicionar, excluir e realizar ações semelhantes.

<br>

<b>Questões gerais:</b>

- Ao <b>criar</b> um node de camada física manualmente ou dinamicamente, em todos os casos é de modo conjunto criado um node virtual (que é um sub-processo num processo principal). Pois na medida em que vai se formando a rede de nodes, também vai automaticamento sendo criada a abstração de camada 2, isto é, dos nodes virtuais. De modo que, <b>proporcionalmente à topologia dos nodes de camada 1, será também criado uma topologia identica de nodes de camada 2.</b> Ficando assim duas redes sobrepostas, uma de camada 1, outra de camada 2.

- 

<br>

<b>Funcionalidades do Node Mapper:</b>

- Ao <b>criar</b> um novo node em máquinas que não possuem nenhum node executando, necessariamente se exige que o primeiro node seja criado <b>manualmente</b> utilizando da suite da linguagem.
  
- Também pode-se criar <b>dinamicamente</b> (via código, camada 3 / sistema) novos nodes de camada 1, tais nodes serão novos processos na máquina. Do mesmo modo, pode-se gestioná-los (excluir, migrar, etc). Tal ação é realizada através de algum node virtual (camada 2) já existente.
  

<br>


