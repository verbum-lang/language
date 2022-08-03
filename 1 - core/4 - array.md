### Array

Há dois tipos de array, indexado e associativo.

É permitido adicionar elementos em arrays de modo dinamico, Sem a necessidade de usar funções especiais para "push" e afins. Por exemplo, caso o index, ou a hash, não exista, os mesmos são criados em tempo de execução, e passa portanto, a existir.

Note que a especificação do tipo não é obrigatória, caso o mesmo não seja especificado, ocorrerá inferência de tipo.
No entanto, a depender da situação, é obrigatório a especificição.

<b>Array indexado:</b>

```php
// Examplos.

variable :array = [ 3, 1, 3, 3, 7 ];
variable :array = [ 'V', '♥', true, "Verbum 😍" ];
variable :array = [ 10 :int, 20 :int, 30.3, 40 :double, true, n ];
variable = [ ];

variable :array = [
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
// Exemplos.

variable = {};

variable :array = {
    items: [
        { name: "Verbum"  },
        { name: "Divinus" },
        {
            values: [
                10, 20, 30:double, { name: "Member" }
            ]
        },
        31337
    ]
};

variable = {
    value: 1.337 :double
};
```

Segue alguns exemplos dos modos possíveis de acessar os elementos dos arrays.

```php
variable['items'][0]['name']                    // Verbum
variable['items'][1]['name']                    // Divinus
variable['items'][2]['values'][0]               // 10
variable['items'][2]['values'][3]['name']       // Member
variable['items'][3]                            // 31337

variable[a]
variable[a+b]
variable[a+(b*2)]
```


