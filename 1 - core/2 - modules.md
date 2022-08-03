### Módulos

O comando utilizado para realizar o uso de módulos, é o <b>use</b>.<br>
Quando se diz módulos, estamos nos referindo a arquivos de cabeçalho, ou seja, a possibilidade de utilizar bibliotecas externas.

Há dois modos de usar módulos:
- <b>módulos padrões</b>: são bibliotecas pertencentes a biblioteca padrão.
- <b>módulos locais</b>: são bibliotecas referenciadas pelo caminho do diretório onde a mesma se encontra.

O modo mais simples de utilizar um módulo é apenas colocando o nome do mesmo:

```c
use 'std';
```

No entanto, é importante saber que primeiro será verificado se trata-se de uma biblioteca padrão. E caso não seja, será verificado se trata-se de um módulo local. Assim é feito a verificação do módulo antes de ser realmente carregado.

Importante saber também que ao instalar a linguagem, será definido um diretório para servir como local onde ficarão armazenadas todas as bibliotecas instaladas, ou seja, as chamadas bibliotecas padrão.


```c
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

