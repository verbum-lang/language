### <b>Exemplos</b>

****

Cria o equivalente ao funcionamento de uma <b>thread assíncrona</b>. Observação: no final da execução do bloco de código em questão, ao qual a variável pertence, a instância é destruída.

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

