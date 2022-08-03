### Variáveis

Para criar uma variável basta colocar seu nome, seguido de uma atribuição qualquer. Essa atribuição pode ser um número, string ou qualquer tipo de dado suportado.

```c
// Alguns exemplos.
example = 10;
example = 'Iesus Verbum';
example = true;
```

Observe que o tipo é sempre inferido, mas para os casos onde é desejado especificar o tipo para evitar alguma ambiguidade, é possível utilizando a expressão <b>: tipo</b>.

- Note que, por exemplo, é aceito <b>:string</b> e <b>: string</b>, é dois-pontos seguido de um token (que é o tipo de dado).

Alguns exemplos, onde ao mesmo tempo é exposto os tipos de dados suportados.

```c
example :int       = 31337;
example :double    = 0.1337;
example :bool      = true;
example :char      = '♥';                           // Aponta para um único caractere.
example :string    = 'Verbum 😍';                   // aceita aspas simples e duplas.
example            = calc(10, 20);                  // Chamada a função, com retorno int (inferência).
example :stream    = fopen('archive.bin', 'r');     // Chamada a função, com retorno stream.
example :array     = [];                            // indexado.
example :array     = {};                            // associativo.
example :double    = 10 * 10 + (a + 20);            // operação aritmética, retorna valor numérico (int, double).
```


// O UNICODE é aceito no uso comum da linguagem.
// Isto é, em nome de variáveis, e caracteres dentro de strings.
λ = "Verbum ♥";
π = 3.14;

// String de múltiplas linhas.
// Obs: os \n estão incluso dentro da string.
example = "
    In princípio
    erat Verbum!
";
```

