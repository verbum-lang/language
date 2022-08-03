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

Note que nos exemplos acima foram utilizados caracteres unicode dentro de strings.<br>
No entanto é bom saber que o suporte unicode é aplicável em toda a linguagem.

```c
λ = "Verbum ♥";
π = 3.14;
```

Importante saber também que na declaração de strings, é aceito strings de uma única linha, mas também é aceito quebra de linha dentro das strings.

```c
// String de múltiplas linhas.
// Obs: os \n estão incluso dentro da string.
example = "
    In princípio
    erat Verbum!
";
```

Concatenação de dados em string.

```c
str = 'Santo';
print('Deus é {str}\n');

num = 10;
print('Value: {str}\n');
```

Comparação de strings. Note que o que é comparado, é sempre os dados.

```c
if ('str1' == 'str1')
    print("Strings iguais.\n");

// Caso utilizando variável.
str = 'str1';
if (str == 'str1')
    print("Strings iguais.\n");
```


