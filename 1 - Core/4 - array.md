### Array

Há dois tipos de array, indexado e associativo.

É permitido adicionar elementos em arrays de modo dinamico, Sem a necessidade de usar funções especiais para "push" e afins. Por exemplo, caso o index, ou a hash, não exista, os mesmos são criados em tempo de execução, e passa portanto, a existir.

<b>Array indexado:</b>

```rust
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

```rust
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


