### <b>Fault Tolerance</b>

****

Em linhas gerais a alta tolerância a erros se traduz principalmente nas seguintes características:

- Caso ocorra erro em uma conexão de rede, fica-se em loop realizando tentativas de conexão infinitamente, até a conexão ser re-estabelecida.

- Caso ocorra algum erro de execução, como acessar algum dado nulo, em branco, ou noção semelhante, bem como caso ocorrer algum acesso a algum recurso inacessível, ou retornar erros em funções, dentre erros semelhantes, a aplicação não se encerra.

- Caso ocorra uma falha em alguma execução, o estado do erro é armazenado em log para realizar a depuração.

- Ver texto a respeito do Hot Code Reloading para informações sobre esse ponto.

<br>

****

### <b>Log e depuração</b>

<br>

Seguindo a mesma lógica de funcionamento do Node Mapper local, ocorre também com a existência de um controle local para gestão de logs de erros de execução.

Tais informação ficam armazenadas num controlador local, que poderá posteriormente compartilhar suas informações com algum outro node. Isto é, através de comandos especiais do Node Mapper, é possível baixar/acessar logs de erros para acompanhamentos e análises em tempo real.

Coisas importantes para se ter:

- <b>Histórico</b> de erros, com data e informações precisas.

- <b>Mecanismos</b> de depuração, aqui, de modo conjunto, entram noções como os recursos de Hot Code Reloading, Meta programação, e outros.


