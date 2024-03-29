### <b>Básico</b>

****

A abstração dos <b>nodes</b>, isto é, dos <b>nós de processamento</b>, possuem o propósito de executar blocos de código de maneira isolada. Desta maneira possuindo suas noções equivalentes ao funcionamento de threads síncronas e assíncronas, noções de mutex (na acessibilidade de dados), noções de IPC (comunicação entre processos, troca de mensagens), bem como noções semelhantes a estas.

Em outras palavras, os nodes procuram suprir as necessidades envolvendo os conceitos:

- Sincronismo e assincronismo (await, mutex).

- Gestão (e retorno) de dados/informações dos nodes.

- Troca de mensagens entre os nodes.

<br>

<b>Noções Gerais:</b>

1. Os nodes são todos, por padrão, <b>assíncronos</b>.

2. Qualquer node pode requisitar acesso a <b>estruturas de dados</b>, como uma variável externa. Ocorre que há um <b>sistema de gestão dos recursos</b>, onde essa mesma gestão deixa, quando necessário, nodes em espera. Caso a acessibilidade não for de permissão de múltiplos acessos simultaneos. Como ocorre com uma variável global que é incrementada.

3. Uma função chamada por um node, faz parte do mesmo escopo de processamento deste node. Seu código vai junto com o node, por exemplo, em casos com nodes de rede.

5. No uso da linguagem, é necessário especificar o tipo especial <b>node</b> ou <b>Node</b>, para ser capaz de utilizar os nodes.

6. Importante saber que para os nodes de rede é sempre realizado a verificação do <b>handshake</b>, de modo que se vier a falhar a criação de algum node, como questões de comunicação, e não houver nenhuma verificação posterior para a conexão, o processamento continuará de acordo com o fluxo sequencial da execução dos comandos do código em questão. De modo que tais erros são enviados para o controlador interno de erros do sistema (abstração do <b>Fault Tolerance</b>). Para verificações em tempo de execução, pode-se usar a função especial chamada <b>node_check_connection</b>.

7. Quando um node de rede retorna alguma informação de maneira nativa, ou seja, através do uso comum da linguagem, como no acesso a algum recurso externo (como uma variável global) ele utiliza da abstração do <b>Protocolo de Comunicação (INC)</b> para se comunicar com os nodes de nível hierarquico superior.

8. A organização hierárquica dos nodes (definindo a topologia), é definida pelas noções de cliente/servidor, as conexões de uns para com os outros definem a topologia da rede de nodes.

<br>

****

### <b>Funções especiais</b>

<br>

A existência da abstração dos nodes se dá através de sua interface na linguagem, logo existe um conjunto de funções especiais para realizar/acessar tais recursos.

<br>

<b>Funções:</b>

- <b>node_check</b>: verifica estado do node. Utilizado para garantir que a comunicação está em ordem, para caso não estiver, tomar alguma ação.

- <b>node_await</b>: aguarda finalização da função. Trava a execução sequencial.

- <b>node_result</b>: retorna resultado da função. Retorna array, para verificação. <br> 
  Componentes do array: 
```
    data: dados do resultado.
    status:
        NODE_OK                 - Resultado OK (recebidos).
        NODE_RESULT_RECEIVING   - Recebendo dados.
        NODE_RESULT_EMPTY       - Nenhum resultado retornado.
```

- <b>node_lock</b>, <b>node_unlock</b>: controle do mutex. Noção de fila de espera.
  
- <b>node_information</b>: retorna informações do node, tais como seu ID e outras.

- <b>node_destroy</b>: destroi um node.

- <b>node_mapper_list</b>: retorna array contendo a lista dos nodes existentes no Node Mapper local.

- <b>get_node_instance</b>: retorna o handle do node em questão.


