### :arrow_right: Interface de controle da VM/interpretador Verbum.

#### Conectividade.
- Verificar conectividade com node / disponibilidade de conexão.
- Autenticar no node / conecta no mesmo passando pelo handshake e autenticação (caso necessário).


#### Recursos gerais.
- Enviar código Verbum para ser executado no interpretador.
- Enviar AST para ser executada no interpretador.
- Solicitar código Verbum atual executando no node.
- Solicitar AST atual executando no node.


#### Hot code reloading e meta-programação.

<b>Funcionalidades:</b>
```
Insert, Update, Delete:
    Importações (arquivos de cabeçalho / inclusões).
    Pacote / space / namespace.
    Arquivo.
    Classe.
    Método.
    Linha A.
    Linha A à Z (Update, Delete).
```

<b>Controles relacionados à execução (usado em conjunto):</b>
- Aguardar finalização da execução atual.
- Finalizar abrutamente todas execuções em aberto.


#### Informações de uso e disponibilidade de recursos do node.

<b>Informações gerais:</b>
- Informações do node: tipo, conexão, configurações, etc.
- OS, Kernel, distribuição, memória, disco, IP local/externo, usuário, etc.
- Informações de uso: data de início do node, nodes filhos criados, nodes filhos em execução.


#### Gestão dos nodes.

- Compartilhamento do Node Mapper (nodes existentes como recurso). Obs: vem com informações de data/hora.
- Rede de nodes em execução (informações atualizadas em tempo de execução).
- Funcionalidades de gestão do Node Mapper: listar, adicionar, excluir, solicitar informações (ver: 4 - Node mapper).


#### Respostas gerais que o node filho envia ao node pai.

- Informações gerais (OS, Kernel, etc).
- Node Mapper recém atualizado.
- Mensagens do interpretador, e mensagens do uso das funcionalidades de hot code reloading, e meta-programação.
- AST e código Verbum.
- Retorno de um dado complexo: funções, classes, objetos instanciados, tipos primitivos e outros.


