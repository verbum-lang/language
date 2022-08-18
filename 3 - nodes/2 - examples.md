### <b>Exemplos</b>

****

Cria o equivalente ao funcionamento de uma <b>thread assíncrona</b>. Observação: no final da execução do bloco de código em questão, ao qual a variável pertence, a instância é destruída.

```php
fn function1 (param: string) {
    for ()
        print("Deus eh Santo {param}!\n");
}

// Especifica tipo especial "node".
var instance :node = function1("Puro");

// Node de rede.
var instance :node {
    host: 'sv1.intranet', 
    port: 333
} = function1("Puro");

// Com autenticação.
var instance :node {
    host: 'sv1.intranet', 
    port: 333
    username: 'user',
    password: 'pass'
} = function1("Puro");

// Verificação da conexão (garante que tudo está em ordem).
var status = node_check_connection(instance); // Retorna um bool.
```

