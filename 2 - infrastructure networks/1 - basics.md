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

****

### <b>Layer 1</b>

A camada 1 é criada ao interconectar máquinas físicas numa infraestrutura de baseada em rede. Essa conexão entre as máquinas é realizada utilizando a suite da linguagem.

Na prática, utilizando a suite da linguagem se terá um node rodando num único processo. É possível abrir quantos processos quiser, ou seja, é possível criar uma infraestrutura de camada 1 utilizando várias conexões sem necessariamente ser preciso executar apenas um processo principal por máquina física.

Tratando-se de uma infraestrutura física, deve-se possuir um meio de conferir confiabilidade a algum determinado node desta camada 1. Para isto existe o conceito de <b>Node Mapper</b>.

