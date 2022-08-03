### Variáveis

Obs: é aceito <b>:string</b> e <b>: string</b>, é dois-pontos seguido de um token (que é o tipo de dado).

```c
variable :int       = 31337;
variable :double    = 0.1337;
variable :bool      = true;
variable :char      = '♥'; // Aponta para um único caractere.
variable :string    = 'Verbum 😍'; // aceita aspas simples e duplas.
variable            = calc(10, 20); // Chamada a função, com retorno int (inferência).
variable :stream    = fopen('archive.bin', 'r'); // Chamada a função, com retorno stream.
variable :array     = []; // indexado.
variable :array     = {}; // associativo.
variable :double    = 10 * 10 + (a + 20); // operação aritmética, retorna valor numérico (int, double).

// O UNICODE é aceito no uso comum da linguagem.
// Isto é, em nome de variáveis, e caracteres dentro de strings.
λ = "Verbum ♥";
π = 3.14;

// String de múltiplas linhas.
// Obs: os \n estão incluso dentro da string.
variable = "
    In princípio
    erat Verbum!
";
```

