### <b>Infrastructure Networks</b>

****

Também chamado de <b>Layer 1</b>, trata-se do setor responsável pela configuração e gestão da organização da infraestrutura física. 

Um sistema (Layer 3) pode ter seu processamento distribuído em uma rede de nodes (Layer 2). Por sua vez, estes nodes podem ser processos e sub-processos (Layer 1).

<p align="center" >
<br>
<img src="../0%20-%20extras/diagram/general-1.png" />
<br>
<br>
</p>

Em outras palavras, o Layer 1 trata-se de uma abstração da infraestrutura física disponível, podendo configurar um agrupamento de máquinas distribuídas em rede, para posteriormente utilizá-las como uma infraestrutura computacional unificada, ou algo semelhante.

<br>

****

### <b>Layer 1</b>

<br>

A camada 1 é criada ao interconectar máquinas físicas numa infraestrutura de baseada em rede. Essa conexão entre as máquinas é realizada utilizando a suite da linguagem.

Na prática, utilizando a suite da linguagem se terá um node rodando num único processo. É possível abrir quantos processos quiser, ou seja, é possível criar uma infraestrutura de camada 1 utilizando vários nodes, sem necessariamente ser preciso executar apenas um processo principal por máquina física.

Tratando-se de uma infraestrutura física, deve-se possuir um meio de conferir confiabilidade a algum determinado node desta camada 1. Para isto existe o conceito de <b>Node Mapper</b> (mais adiante é abordado o mesmo).

Canais de comunicação entre os nodes:

<p align="center" >
<br>
<img src="../0%20-%20extras/diagram/general-2.png" />
<br>
<br>
</p>

Pontos importantes:

- Note que pode haver apenas um sentido num canal de comunicação de um node para outro. E segue a estrutura de cliente e servidor. De modo que o sentido da conexão entre os nodes dão forma a infraestrutura de rede. 

- Vale mencionar também que isso não implica em ser utilizado apenas uma única conexão TCP/IP, esta regra define apenas ao sentido do canal de comunicação. Ou seja, uma vez que um node é tratado como cliente de outro node, podem ser abertas múltiplas e simultâneas conexões TCP/IP entre os mesmos, mas o sentido da comunicação fica definido por padrão (cliente ou servidor) para estas mesmas comunicações.

- Todo node é simultâneamente cliente e servidor (mesmo que não tenha nenhum cliente conectado no mesmo).

<br>

****

### <b>Node Mapper</b>

<br>

Trata-se de uma abstração para conferir confiabilidade aos nodes componentes da infraestrutura física.



<br>


