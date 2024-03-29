### Módulos

O comando utilizado para realizar o uso de módulos, é o <b>use</b>.<br>
Quando se diz módulos, estamos nos referindo a arquivos de cabeçalho, ou seja, a possibilidade de utilizar bibliotecas externas.

Há dois modos de usar módulos:
- <b>módulos padrões</b>: são bibliotecas pertencentes a biblioteca padrão. Isto é, as que vieram por padrão na instalação da linguagem, e as que foram posteriormente instaladas.
- <b>módulos locais</b>: são bibliotecas referenciadas pelo caminho do diretório onde a mesma se encontra.

O modo mais simples de utilizar um módulo é apenas colocando o nome do mesmo:

```c
use 'os';
```

No entanto, é importante saber que primeiro será verificado se trata-se de uma biblioteca padrão. E caso não seja, será verificado se trata-se de um módulo local. Assim é feito a verificação do módulo antes de ser realmente carregado.

Importante saber também que ao instalar a linguagem, será definido um diretório para servir como local onde ficarão armazenadas todas as bibliotecas instaladas, ou seja, as chamadas bibliotecas padrão.

Uma outra maneira possível, e recomendada, é a utilização de <b>sub-módulos</b>:

```c
use 'std:io';     // Carrega módulo de biblioteca padrão.
use 'path/file';  // Carrega módulo de diretório específico.
```

Note que dentro do diretório onde ficam instaladas as bibliotecas padrão, existe o diretório <b>std/io</b>. Mas para dizer a linguagem que estamos carregando um módulo das bibliotecas padrão, precisamos separar o primeiro diretório com <b>dois pontos (:)</b>.

Para os módulos carregados diretamente a partir de diretórios, simplesmente podemos inserir o caminho do respectivo diretório.

Caso existam mais diretórios, dentro de um sub-módulo, utilizamos da seguinte maneira:

```c
use 'std:io/file';     // Carrega módulo de biblioteca padrão.
use 'path/path/file';  // Carrega módulo de diretório específico.
```

Importante saber que esse modo de poder referenciar os módulos padrões foi criado para melhor organização da linguagem. De modo que tais módulos (que também podem ser chamados de pacotes), poderão ser instalados remotamente ou localmente, isto é, baixar um módulo e utilizando de comandos do gerenciador de pacote da linguagem, instalá-los no diretório das bibliotecas padrão. De modo que tais módulos possam ser utilizados em qualquer projeto, bastante especificar o módulo. Apenas em casos específicos, que realmente convir, devemos utilizar a importação de módulos locais (como por exemplo na criação de um sistema, onde dividimos suas partes em vários arquivos).

Por fim, podemos também importar vários módulos de uma vez.

Para importarmos todos os sub-módulos contidos dentro de um módulo, podemos usar o <b>asterismo (*)</b>. Isto é possível para módulos da biblioteca padrão, e para importações a partir de diretórios específicos.

Note que ainda persiste a noção de explicitarmos, com o uso do <b>dois pontos (:)</b>, ou utilizando a <b>barra (/)</b>, se estamos importando da biblioteca padrão, ou de algum diretório específico.

```c
use 'std:*';   // Importa da biblioteca padrão.
use 'path/*';  // Importa de diretório específico.
```

Para casos onde desejamos importar apenas uma sequência específica de sub-módulos, podemos especifica-los dentro das <b>setas de abertura e fechamento (< >)</b>.

```c
// Importações múltiplas (dentro de um único módulo ou diretório).
use 'std:<io, net, os, string>';
use 'path/<file1, file2, file3>';
```

Podemos também realizar várias importações em um único comando.

```c
use 'std:<io,net>', 'path/test', 'util';
use 'path2/*', 'mysql:*', 'json:unicode';

// Com quebra de linha.
use 'std:<io,net>', 
    'path/test', 
    'util';
```


