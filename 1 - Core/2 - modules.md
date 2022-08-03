### Módulos



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

