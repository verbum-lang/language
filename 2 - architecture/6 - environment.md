### <b>Ambiente de Desenvolvimento</b>

****

Devido a linguagem ainda estar em desenvolvimento, até o momento o ambiente de desenvolvimento Verbum é composto por um conjunto de ferramentas separadas. Desta maneira as ações (de complexidade variável) que a linguagem precisa realizar, são realizadas por noções de módulos.

É chamado de <b>suite</b> o conjunto total das ferramentas e utilitários que compõem todo o ambiente de desenvolvimento.

<br>

<b>Noções Gerais (ferramentas):</b>

- <b>verbum</b>: utilitário responsável por unificar todas as ferramentas da suite e proporcionar uma boa experiência no uso da linguagem, contendo shell interativa, com interfaces para acessar todas as funcionalidades das ferramentas da suite, e noções semelhantes.

- <b>verbum-network</b>: aplicação responsável por realizar a criação/gestão da Layer 1 e 2, cria e gestiona todos os nodes de camada 1 e 2. Contendo as noções e controles relacionados ao Node Mapper, questões do Fault Tolerance e outras questões relacionadas.

- <b>verbum-parser</b>: responsável por realizar todas as etapas de análise léxica, sintática e semântica, bem como realizar a geração final da AST. O produto do parser é a AST, podendo ela ser exportada para uso em outras aplicações.

- <b>verbum-vm</b>: responsável por processar a AST, realizando todas as coisas referentes ao core e as features da linguagem.


