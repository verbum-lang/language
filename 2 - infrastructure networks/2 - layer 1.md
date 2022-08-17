
### <b>Layer 1</b>

****

A camada 1 é criada ao interconectar máquinas físicas numa infraestrutura de baseada em rede. Essa conexão entre as máquinas é realizada utilizando a suite da linguagem.

Na prática, utilizando a suite da linguagem se terá um node rodando num único processo. É possível abrir quantos processos quiser, ou seja, é possível criar uma infraestrutura de camada 1 utilizando vários nodes, sem necessariamente ser preciso executar apenas um processo principal por máquina física. Ficando a critério de cada um como será organizada propriamente a infraestrutura física.

Tratando-se de uma infraestrutura física, deve-se possuir um meio de conferir confiabilidade a algum determinado node desta camada 1. Para isto existe o conceito de <b>Node Mapper</b> (mais adiante é abordado o mesmo).

<b>Organização da rede na infraestrutura física:</b>

<p align="center" >
<br>
<img src="../0%20-%20extras/diagram/general-3.png?v=1" />
<br>
<br>
</p>

Pontos importantes:

- Um node pode ter infinitas conexões, e isto se aplica às noções de cliente e servidor. Ou seja, um node pode ter quantos clientes quiser, também pode se conectar em quantos servidores quiser.

- As conexões de rede TCP/IP são todas persistentes. Se não houver comunicação, o node ficará persistindo eternamentem, isto é, enquanto ele existir como processo ou sub-processo na máquina física.

<br>

****

### <b>Node Mapper</b>

<br>

Trata-se de uma abstração para conferir confiabilidade aos nodes componentes da infraestrutura física.

A ideia deste conceito é dar um dinamismo para a infraestrutura física, podendo adicionar, remover, ou alterar, nodes componentes desta mesma infraestrutura.


<br>

