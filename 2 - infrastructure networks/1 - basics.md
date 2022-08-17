### <b>Esquema Geral</b>

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


