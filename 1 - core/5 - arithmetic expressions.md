### Expressões aritméticas

O seu uso é feito como geralmente o é nas linguagens populares.

Vale citar que dentro de array é possível também inserir as expressões aritméticas.

Segue alguns exemplos.

```php
// Atribuição de valores à variáveis simples.
var example = (10 + (example2++) + (3.14 * 3) / --abc) - 10;

// Como elemento em arrays indexados.
var example = [
    1, 2, 3,
    (10 + ( 20 * 3 ) / 4),
    'str 1', "str 2"
];

// Como elemento em arrays associativos.
var example = [
    { name:  "Verbum" },
    {
        value: 'Divino',
        operation:  3 + ( 3 ) + 3
    }
];
```


