### <b>Básico</b>

****

Um sistema (Layer 3) pode ter seu processamento distribuído em uma rede de nodes virtuais (Layer 2), que tratam-se de sub-processos. Por sua vez, estes sub-processos são de um processo principal, isto é, um node que roda em camada física (Layer 1).

<p align="center" >
<br>
<img src="../0%20-%20extras/diagram/general-1.png?v=1" />
<br>
<br>
</p>

Em outras palavras, o Layer 1 trata-se de uma abstração da infraestrutura física disponível, podendo configurar um agrupamento de máquinas distribuídas em rede, para posteriormente utilizá-las como uma infraestrutura computacional.

Em cima desses nodes de camada física, é executado uma rede de nodes virtuais. Sobre estes serão executados os sistemas/aplicações.

<br>

****

### <b>Nodes</b>

<br>

<b>Questões gerais:</b>

- A <b>comunicação</b> entre os nodes é sempre realizada via rede (TCP/IP), independentes do tipo dos nodes.

<br>

****

### <b>Segurança</b>

<br>

<b>Questões gerais:</b>

- Na criação dos nodes é possível especificar uma <b>chave pública</b> (de criptografia PGP), deste modo é possível garantir a segurança nas ações empregadas na rede, fazendo com que somente as mensagens assinadas digitalmente (utilizando de uma <b>chave privada</b>) possuam validade na rede.

- Bem como é possível utilizar alguma criptografia para os dados trafegados entre os nodes, ficando opcional.




