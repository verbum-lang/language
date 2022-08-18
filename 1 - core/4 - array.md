### Array

Há dois tipos de array, <b>indexado</b> e <b>associativo</b>.

É permitido adicionar elementos em arrays de modo dinamico, Sem a necessidade de usar funções especiais para "push" e afins. Por exemplo, caso o index, ou a hash, não exista, os mesmos são criados em tempo de execução, e passa portanto, a existir.

Vale lembrar que a especificação do tipo não é obrigatória, caso o mesmo não seja especificado, ocorrerá inferência de tipo.

Também vale lembrar que é possível mesclá-los.

<b>Array indexado:</b>

```php
var example = [ 3, 1, 3, 3, 7 ];
var example = [ 'V', '♥', true, "Verbum 😍" ];
var example = [ 10 :int, 20 :int, 30.3, 40 :double, true, n ];
var example = [ ];

var example :array = [
    1, 2, 3,
    [
        'a', 'b', 'c',
        "Verbum", "Divinus",
        3.1337
    ],
    [
        a, b, c,
        10 :int, 20 :int, 30 :double
    ]
];
```

<b>Array associativo:</b>

```php
var example = {};

var example = {
    value: 1.337 :double
};

var example = {
    items: [
        { name: "Verbum"  },
        { name: "Divinus" },
        {
            values: [
                10, 20, 30 :double, { name: "Member" }
            ]
        },
        31337
    ]
};
```

Segue alguns exemplos dos modos possíveis de acessar os elementos dos arrays.

```php
example['items'][0]['name']                    // Verbum
example['items'][1]['name']                    // Divinus
example['items'][2]['values'][0]               // 10
example['items'][2]['values'][3]['name']       // Member
example['items'][3]                            // 31337

// Outros casos de exemplo.
example[a]
example[ a + b ]
example[ a + (b*2) ]
```

Os casos de acesso permitidos nos elementos de um array:

- <b>string</b>, sendo utilizadas para acesso aos elementos de arrays associativos.
- <b>expressões resultando um número inteiro</b>, ou seja, é permitido o uso de números inteiros, variáveis, e expressões aritméticas. Note que para as <b>expressões aritméticas</b>, se a mesma retornar um valor diferente de um número inteiro, será realizada a conversão do valor para um número inteiro (casting).


