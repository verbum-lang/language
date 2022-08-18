### Variáveis

Para criar uma variável basta colocar o prefixo <b>var</b>, seguido de seu nome, e de uma atribuição qualquer. Essa atribuição pode ser um número, string ou qualquer tipo de dado suportado.

```javascript
// Alguns exemplos.
var example = 10;
var example = 'Iesus Verbum';
var example = true;
```

Observe que o tipo é sempre inferido, mas para os casos onde é desejado especificar o tipo para evitar alguma ambiguidade, é possível utilizando a expressão <b>: tipo</b>.

- Note que, por exemplo, é aceito <b>:string</b> e <b>: string</b>, é dois-pontos seguido de um token (que é o tipo de dado).

Alguns exemplos, onde ao mesmo tempo é exposto os tipos de dados suportados.

```javascript
var example :int       = 31337;
var example :double    = 0.1337;
var example :bool      = true;
var example :char      = '♥';                           // Aponta para um único caractere.
var example :string    = 'Verbum 😍';                   // aceita aspas simples e duplas.
var example            = calc(10, 20);                  // Chamada a função, com retorno int (inferência).
var example :stream    = fopen('archive.bin', 'r');     // Chamada a função, com retorno stream.
var example :array     = [];                            // indexado.
var example :array     = {};                            // associativo.
var example :double    = 10 * 10 + (a + 20);            // operação aritmética, retorna valor numérico (int, double).
```

Note que nos exemplos acima foram utilizados caracteres unicode dentro de strings.<br>
No entanto é bom saber que o suporte unicode é aplicável em toda a linguagem.

```js
var λ = "Verbum ♥";
var π = 3.14;
```

Importante saber também que na declaração de strings, é aceito strings de uma única linha, mas também é aceito quebra de linha dentro das strings.

```php
// String de múltiplas linhas.
// Obs: os \n estão incluso dentro da string.
var example = "
    In princípio
    erat Verbum!
";
```

Concatenação de dados em string.

```php
var str = 'Santo';
print('Deus é {str}\n');

var num = 10;
print('Value: {str}\n');
```

Comparação de strings. Note que o que é comparado, é sempre os dados.

```php
if ('str1' == 'str1')
    print("Strings iguais.\n");

// Caso utilizando variável.
var str = 'str1';
if (str == 'str1')
    print("Strings iguais.\n");
```


