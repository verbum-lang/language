### <b>Exemplos</b>

****

Cria o equivalente ao funcionamento de uma <b>thread assíncrona</b>. 

Observação: no final da execução do bloco de código em questão, ao qual a variável pertence (instance), a instância do node <b>não é destruída</b>. Para destruí-lo é necessário utilizar a função <b>node_destroy</b>, passando como parâmetro a variável <b>instance</b>, ou utilizando o retorno das informações do node (como é demonstrado mais abaixo).

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

print("Value: { result['data'] }\n");
```

