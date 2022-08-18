### <b>Exemplos</b>

****

Os nodes (ou seja, os nodes virtuais) são norteados por algumas noções gerais, sendo elas:

- <b>Nodes criados no escopo em questão</b>, ou seja, nodes virtuais que ao serem criados, o são sobre o escopo em questão (o modo mais simples de criar um node). O próprio sistema, quando o mesmo é iniciado, deve-se explicitar o node virtual no qual ele será executado. Deste modo, este node a qual o sistema foi executado está existindo sobre um node real específico. Quando se cria um node virtual simples, o mesmo trata-se apenas de mais um sub-processo neste processo principal do node real. Ou seja, é um node de camada 2, existindo no escopo no qual o próprio sistema foi iniciado. O mesmo também encontra-se na mesma máquina a qual pertence o node virtual de nível hierárquico superior (neste caso o do próprio sistema).
<br><br>
Note que se for criado um node comum a partir de um outro node virtual, contido em outra máquina, será lá nesta máquina que serão criados novos nodes virtuais. Pois os nodes são criados a partir do escopo em que se encontram no momento de sua criação. 

- <b>Utilização de um node virtual específico</b>, neste caso é necessário especificar o ID do node destinatário. Se esse node se encontra sendo executado sobre algum node real em algum outro ponto da rede, será lá naquela máquina a qual ele pertence que será então executado o respectivo bloco de código.

- <b>Nodes criados a partir de algum node virtual específico</b>, é muito simples perceber que para este caso, basta primeiramente utilizar um node virtual específico, e partir do mesmo, criar nodes comuns, onde serão criados a partir do escopo em que se encontram. Podendo assim criar nodes virtuais a partir de um node virtual específico, herdando as características de seu escopo de execução.

<br>

Exemplo de um node comum criado no mesmo escopo de código do sistema.

```js
// Criação do node.
var instance :node = function1("Puro");

fn function1 (param: string) {
    print("Deus eh Santo {param}!\n");
}
```

<br>

Exemplo da utilização de um node virtual específico já existente.

Note que é especificado o <b>ID único</b> do node destinatário. Este ID está acessível através do Node Mapper.

```js
// Conexão com o node existente.
var instance :node { id: 'VerbumNode' } = function1("Puro");

fn function1 (param: string) {
    print("Deus eh Santo {param}!\n");
}
```

<br>

Criando um novo node virtual, a partir de outro node virtual específico.

```js
// Conexão com o node específico.
var instance :node { id: 'VerbumNode' } = function1("Puro");

fn function1 (param: string) {
    // Cria node herdando as características
    // do escopo de execução em questão.
    var instance :node = function2(param);
}

fn function2 (param: string) {
    print("Deus eh Santo {param}!\n");
}
```

<br>

****

Cria o equivalente ao funcionamento de uma <b>thread assíncrona</b>. 

Observação: no final da execução do bloco de código em questão, ao qual a variável pertence (instance), a instância do node <b>não é destruída</b>. Para destruí-lo é necessário utilizar a função <b>node_destroy</b>, passando como parâmetro a variável <b>instance</b>, ou utilizando o retorno das informações do node (como é demonstrado mais abaixo). Mesmo que a execução do próprio código do node chegue ao fim, o mesmo continua existindo e acessível via Node Mapper.

```js
fn function1 (param: string) {
    for () {
        print("Deus eh Santo {param}!\n");
        sleep(3);
    }
}

// Especifica tipo especial "node".
// Cria novo node virtual.
// O mesmo será automaticamente adicionado no Node Mapper.
var instance :node = function1("Puro");

// Verificação (garante que tudo está em ordem).
var status = node_check(instance); // Retorna um bool.

// ...
```

<br>

Exemplo destruindo node.

```js
// Baseado na variável da instãncia do node.
var status = node_destroy(instance); // Retorna bool.

// Baseado no retorno das informações carregadas do Node Mapper.
var list   = node_mapper_list();
var status = node_destroy(list['layer2'][0]['instance']);
```

<br>

****

Cria o equivalente a uma <b>thread assíncrona</b>. No entando, aguarda a sua finalização, e gerencia o retorno de dados.

```js
fn function1 (param: string) -> string {
    ret 'Deus eh Santo {param}!\n';
}

var instance :node = function1("Puro");

// Trava a execução, aguardando o retorno/finalização do node.
node_await(instance);

// retorna tipo de acordo com a função.
var result = node_result(instance);

if (result['status'] == NODE_OK)
    print("Value: { result['data'] }\n");
```

<br>

****

Acessibilidade a elementos externos (<b>equivalente ao mutex</b> de threads).

Obs: todo acesso a algo externo, como uma variável, é norteado pela mesma noção de um Mutex, independente se apenas uma instancia do node for criada. De modo que quando o node é o primeiro a acionar o Mutex (internamente), ele o aciona e o mantem ativo, de modo que o Mutex é liberado após concluir o acesso ao dado externo.

O Mutex é acionado ao incrementar a variável, e enquanto está sendo realizada esta ação na variável externa (counter), qualquer outro node que venha tentar também incrementa-la, le-la ou realizar qualquer ação com a mesma, ficará em uma fila aguardando para poder realizar sua ação.

Esta noção de mutex se aplica a variáveis, e acessos a recursos semelhantes.

```js
// Cria contador (variável de acesso global).
var counter = 0;

// Função a ser executada no node.
fn function1 (node_id :int) -> array {
    counter++;

    // Processa dados.
    var data :string;
    ...
    
    counter--;

    // Retorna dados.
    ret {
        node: 'node {node_id}',
        data: data
    };
}

// Variável para controle das instâncias.
var instances = [];

// Cria vários nodes assíncronos.
// Note que os mesmos são criados e a execução continua, ficando
// os nodes em execução submetidos à lógica do Mutex, aguardando na fila.
for (var a=0; a<3; a++) {
    var instance :node = function1(a);
    instances[a] = instance;
}

// Verifica se todos os nodes estão em ordem.
for (var a=0; a<3; a++) {
    var status = node_check(instances[a]); 
    if (!status) {
        print("Erro ao criar node {a}.\n");
        exit();
    }
}

// Monitora nodes através da variável global (contador).
for (counter > 0) {
    print("\rRunning: {counter}");
    sleep(1);
}

sleep(3);

// Exibe resultados retornados por cada node.
for (var a=0; a<3; a++) {
    var result = node_result(instances[a]); // Herda tipo da função do node.

    if (result['status'] == NODE_OK) {
        print("node id..: { result['data']['node'] }");
        print("node data: { result['data']['data'] }");
    }
}
```

<br>

****

<br>

Quando há a necessidade de criar um Mutex fixo, por exemplo, para a <b>execução de um único node de cada vez</b>, podemos usar o comando especial.

De modo que, quando outros nodes em execução, verificam o estado do mutex através da função node_lock, caso o mesmo já estiver travado/em uso por algum outro node, os mesmos solicitantes ficam em espera aguardando a liberação do respectivo mutex.

Obs: a mesma lógica de acesso a um recurso de escopo superior, se aplica ao invocar a função node_lock/node_unlock, de modo que se houver nodes (utilizando de funções diferentes) que utilizam o mesmo mutex, elas não conflitam, pois o mutex é tratado como um recurso, e portanto, é gestionado.

```php
// Tipo especial para controle do mutex.
var mutex :node_mutex;

fn function1 (node_id :int) {
    node_lock(mutex);

    // Code here...
    print("Node: {node_id}\n");

    node_unlock(mutex);
}

// Cria nodes.
var instances = [];

for (var a=0; a<3; a++) {
    var instance :node = function1(a);
    instances[a] = instance;
}

print("Nodes created!\n");
```


