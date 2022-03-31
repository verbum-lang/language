## :arrow_right: Descrição geral da sintaxe Verbum.

### Elementos
<b>Componentes gerais:</b>
- Operadores
- Comandos especiais
- Importações
- Tipos simples
- Constantes
- Array
- Condicionais
- Loops
- Funções

<b>OOP:</b>
- Interface
- Abstração
- Classe
- Herança (apenas simples)
- Encapsulamento / visibilidade
- Polimorfismo estático
- Polimorfismo dinâmico
- Funções especiais

### Operadores
```
Aritméticos.
+                       Soma
-                       Subtração
*                       Multiplicação
/                       Divisão
%                       Módulo
++                      Incremento
--                      Decremento

Relacionais.            
==                      Igual
!=                      Não igual
>                       Maior que
<                       Menor que
>=                      Maior ou igual
<=                      Menor ou igual

Lógicos.            
!                       Not (Negação)
||                      Or (Ou)
&&                      And (E)

Atribuições.            
=                       Atribui valor
+=                      Atribui com soma
-=                      Atribui com subtração
*=                      Atribui com multiplicação
/=                      Atribui com divisão
%=                      Atribui com módulo

Outros / gerais.
()                      Definição de escopo (expressões)
{}                      Definição de escopo (código), e inclusão de dados em strings
[]                      Definição de escopo de array
;                       Finalização de comando
: ->                    Prefixação para uso tipos, uso nas importações, e declaração em arrays associativos
.                       Acessa elemento de objeto, e arrays
\                       Caracteres especiais dentro de strings
<>                      Utilizado com o comando "use" para importar múltiplos pacotes, especificar o tipo em arrays associativos
" '                     Aspas simples e duplas são aceitas para caracteres e strings
::                      Acesso a métodos estáticos de uma classe
/**/ //                 Comentários
```


### Comandos especiais
```
use                                 Importação de módulos / bibliotecas
var                                 Declaração de variáveis
if, elif, else                      Condicionais
for, break, next                    Loops
fn                                  Funções
ret                                 Retorno usado em funções e métodos
null                                Valor nulo

interface                           Definição de interface
abstract                            Definição de abstração
class                               Definição de classe
extends                             Realização de herança
implements                          Realização de implementação de interface
pub, priv, pro, static, final       Definição de atributos e métodos
this, self                          Referência ao objeto instanciado e aos recursos estáticos
parent                              Acessa recursos de classe base e não da implementação atual
new                                 Instancia novo objeto

clone                               Função especial: clona objeto
destroy                             Função especial: destroi objeto
serialize, unserialize              Função especial: realiza serialização de objeto
```


### Importações
```php
// Todos arquivos dentro de um pacote instalado, ou de diretório específico.
use 'std:*';
use 'path/*';

// Importações únicas.
use 'std:io';
use 'std:io/file';
use 'test';
use 'path/path/test';

// Importações múltiplas (dentro de um único módulo ou diretório).
use 'std:<io, net, os, string>';
use 'path/<file1, file2, file3>';

// Importações múltiplas em uma única linha.
use 'std:<io,net>', 'path/test', 'util';
use 'path2/*', 'mysql:*', 'json:unicode';
```


### Tipos simples
```javascript
// Para valores comuns o tipo é inferido automaticamente.
// Os caracteres e strings são UNICODE.
// É aceito aspas simples ou duplas para as strings e caracteres.
var variable :int       = 31337;
var variable :int       = -1337;
var variable :float     = 0.1337;
var variable :double    = 3.1337;
var variable :double    = -1.337;
var variable :bool      = true;
var variable :char      = '♥';
var variable :string    = 'Verbum 😍';
var variavle :stream    = file.open('archive.bin');

// O UNICODE é aceito no uso comum da linguagem.
var λ = "Verbum ♥";
var π = 3.14;

// String de múltiplass linhas.
var variable = "
    In princípio
    erat Verbum!
";
```


### Constantes
```javascript
// Constantes aceitam apenas valores comuns.
var variable :const     = 31337;
var variable :const     = 3.1337;
var variable :const     = true;
var variable :const     = "Verbum 😍";
```


### Array
```javascript
// Indexados, com acesso via número do index.
var variable :array = [ 3, 1, 3, 3, 7 ];
var variable :array = [ 'V', '♥', true, "Verbum 😍" ];
var variable :array = [ 10 :int, 20 :int, 30.3, 40 :float, true, n ];
var variable :array = [ ];

var variable :array = [
    1, 2, 3,
    [
        'a', 'b', 'c',
        "Verbum", "Divinus",
        3.1337
    ],
    [
        a, b, c,
        10 :int, 20 :int, 30 :float
    ]
];

// Associativos, com acesso via chave/hash.
var variable :array = {
    items: [
        { name: "Verbum"  },
        { name: "Divinus" },
        {
            values: [
                10, 20, 30:float, { name: "Member" }
            ]
        },
        31337
    ]
};

var variable = {
    value: 1.337 :double
};

// Exemplo de acessos em arrays associativos.
variable.items[0].name              // Verbum
variable.items[1].name              // Divinus
variable.items[2].values[0]         // 10
variable.items[2].values[3].name    // Member
variable.items[3]                   // 31337

// Outros exemplos.
var variable :array = [
    { name: "Verbum" },
    10, 20, 30,
    {
        values: [
            31337 :double, { name: "Divinus" }
        ] 
    }
];
```


### Aplicações específicas de variáveis e valores relacionados
```javascript
// Operações como valores.
// Obs: caso não seja especificado tipo na variável, em operações aritméticas
// o valor final é automaticamente convertido para inteiro. Caso queira converter
// o valor final para outro, é obrigatório especificar o tipo da variável, ex.: :float
var variable = (10 + (variable++) + (3.14 * 3) / --abc);

var variable = [
    1, 2, 3,
    (10 + ( 20 * 3 ) / 4),
    'str 1', "str 2"
];

var variable :array = [
    { name:  "Verbum" },
    {
        value: 'Divino',
        operation:  (3 + ( 3 ) + 3)
    }
];

var variable = [
    1, 2, 3,
    (10 + 20),
    'str 1', "str 2"
];

variable[3]     // Contêm valor 30.

// Função anônima como valor em variável.
var variable = (fn (a :int) -> int {
    ret a + 10;
});

// Função anônima com array indexado.
var variable = [
    31337,
    (fn (a :int, b :int) -> int {
        ret a + b;   
    })
];

var value = variable[1](10, 20);

// Função anônima com array associativo.
var variable = {
    identifier : 'onclick',
    callback   : (fn (a :int, b :int) -> int {
        ret a + b;   
    })
};

var value = variable.callback(10, 20);

// Tipos de valores recebidos em variáveis.
var variable = true;
var variable = 'a';
var variable = 'string 1';
var variable = "string 2";
var variable = 123;
var variable = 3.14;
var variable = 0.12345;
var variable = [ 1, 2, 3 ];
var variable = { values: [ 1, 2, 3 ] };
var variable = anotherVariable;

var variable = functionName(10, 20, 30);
var variable = obj::functionName(10, 20, 30);
var variable = obj.functionName(10, 20, 30);

var variable = (10 + 20);
var variable = (variable * 10 + 20 / 30);
```


### Condicionais
```python
if (expression) 
    print("value 1");
elif (expression)
    print("value 2");
else
    print("value 3");

```

### Loops
```c++
// Comum.
for (var a = 0; a<100; a++)
    print("Hello world\n");

for (var a = 0; ; a++) {
    if (a >= 100)
        break;
}

for (var a = 0; ; a++) {
    if (a < 100)
        next;
}

// Equivalente ao while.
for (a < 10)
    print("a: {}\n", a);

// Loop infinito.
for ()
    print("Infinite...\n");
```

### Funções
```rust
// Uso comum.
fn example (a: int, b: int) -> int {
    ret (a * b) + 31337;
}

// Concatenação de funções.
fn primary (a: int, b: int) -> int {
    var value = 31337;

    fn secondary (a: int, b: int) -> int {
        ret (a * b) + value;
    }

    ret secondary(a, b);
}

// Funções anonimas.
print("Value: {}\n", 
    (fn (value :int) -> int { 
        ret value * 3; 
    })(31337)
);

// Função sem retorno.
fn function () {
    print("Verbum\n");
}
```

---
### OOP

<b>Conceitos:</b>
- Interface: definição dos métodos que devem necessariamente ser implementados.
- Abstração: permite criar uma abstração de uma classe, contendo métodos não implementados (abstratos). É um mecanismo que representa os recursos essenciais sem incluir detalhes de implementação. Ou seja, ocultação de implementação.
- Herança: quando uma classe ou interface, herda as propriedades de outra.
- Encapsulamento/visibilidade: com os comandos pub, priv, pro e static, se define a visibilidade dos atributos e métodos. Encapsulamento é o empacotamento de "dados" e "funções operando nesses dados" em um único componente e restringindo o acesso a alguns dos componentes do objeto. Encapsulamento significa que a representação interna de um objeto geralmente fica oculta fora da definição do objeto. Ou seja, ocultação de implementação.
- Polimorfismo estático (sobrecarga): quando há vários métodos com o mesmo nome, mas com assinatura diferente (todos válidos).
- Polimorfismo dinâmico (sobrescrita): quando se sobrescreve um método herdado de uma outra classe.

<b>Comandos e operadores:</b>
- interface, abstract, class
- extends, implements
- priv, private, pub, public, pro, protected
- static, final
- new, this, self, parent, ::, . (ponto, acessa componente de objeto)

<b>Funções especiais:</b>
- clone, destroy, serialize, unserialize

```php
// Interface comum...
interface FirstTemplate {
    pub fn getValues () -> array;
    pub fn getValues (index :int) -> int;
}

// Interface com herança.
interface ExampleTemplate extends FirstTemplate {
    pub fn checkString (string :string);
}

// Classe abstrata.
abstract AbstrationCommon {
    pro fn abstractMethod ();
}

// Classe.
class Common extends AbstractClass {
    // ...
    pub fn checkString (string :string) -> int { /* ... */ }

    // Implementa método abstrato.
    pro fn abstractMethod (){
        // ...
    }

    // Testa "parent" na classe herdeira.
    pub fn exampleA () -> str {
        ret "Verbum";
    }

    pub fn getExampleA () -> str {
        ret this.exampleA();
    }
}

// Classe com herança e implementação de interface.
final class Example extends Common implements ExampleTemplate {

    // Atributos.
    priv var attributeA :uint = 31337;
    pub var attributeB :string  = "Verbum 😃";
    pub static var subVersion :string = "1337";

    // Construtor.
    Example (a: uint, b :string) {
        this.attributeA = a;
        this.attributeB = b;
    }

    // Método estático.
    pub static fn getVersion () -> str {
        ret "1.0.0";
    }

    pub static fn getVersion (flag :bool) -> str {
        if (flag)
            ret self::getVersion();
        ret self::subVersion;
    }

    // Declaração dos métodos e sobrecarga.
    pub fn getValues () -> array {
        ret [
            this.attributeA,
            this.attributeB
        ];
    }

    pub fn getValues (index :int) -> int {
        if (index == 1)
            ret this.attributeA;
        ret -1;
    }

    // Sobrescreve método herdado (polimorfismo).
    final pro fn abstractMethod () {
        print("Verbum\n");
    }

    // Acessando uma implementação da classe base e não da atual (parent).
    pub fn exampleA () -> str {
        ret "Divinus";
    }

    pub fn getExampleB () -> str {
        ret parent::exampleA();
    }
}

// Instanciamento e uso.
var obj     :Example  = new Example(31337, "Verbum");
var resultA :array    = obj.getValues();
var resultB :int      = obj.getValues(1);
var resultC :int      = obj.checkString("Verbum Divinus");

print("Version: {}\n", Example::getVersion());
print("Sub version: {}\n", Example::subVersion);
print("ResultA = a: {}, b: {}\n", resultA[0], resultA[1]);
print("resultB = {}\n", resultB);
print("Check String = {}\n", resultC);

// Exemplo com "parent".
var obj1 = new Common();
obj1.exampleA();            // Verbum
obj1.getExampleA();         // Verbum

var obj2 = new Example();
obj2.exampleA();            // Divinus
obj2.getExampleA();         // Divinus
obj2.getExampleB();         // Verbum
```

<b>Método em cascata (fluent interface, method cascading, concretely method chaining).</b>

```php
class Example {
    priv var value :int = 0;

    pub fn foo (a :int) -> this {
        this.value += a;
        ret this;
    }

    pub fn bar (a :int) -> this {
        this.value += a;
        ret this;
    }

    pub fn show () {
        print("Value: {}\n", this.value);
    }
}

var obj = new Example();
obj.foo(10).show().bar(20).show();
```

<b>Classe anônima.</b>

```php
obj.setLogger(new class {
    pub fn log (msg :string) {
        print("{}\n", msg);
    }
});

(new class {
    pub fn show () {
        print("Verbum\n");
    }
}).show();
```

<b>Outros recursos/funções especiais:</b>

```php
// Clona objeto.
var objB :ClassName = clone(objA);

// Destrói objeto.
destroy(objA);

// Serialization.
var stringObject :string = serialize(objA);
var objN :ClassName = unserialize(stringObject);
```


