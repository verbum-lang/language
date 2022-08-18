### <b>INC - Inter-node communication</b>

****

A INC trata-se da abstração responsável por realizar a comunicação entre os contextos e nodes. Podendo realizar a troca de mensagens de um node para com o contexto hierarquicamente superior em um nível, e vice-versa. Bem como realizar esta troca de mensagens de um node para com o outro, independente de seus níveis hierárquicos.

<br>

<b>Funções especiais:</b>

- <b>node_send_message</b>: envia mensagem para contexto acima.

- <b>node_recv_message</b>: recebe mensagem de contexto acima.

- <b>node_get_id</b>: retorna ID de node baseado no seu handle.

- <b>node_send_message_to</b>: envia mensagem para node específico.

- <b>node_recv_message_from</b>: recebe mensagem de node específico.

<br>

<b>Exemplo de comunicação entre contextos diferentes.</b>

```php
// Função para ser executada num node.
fn function1 (node_id :int) {
    for () {
        var command = node_recv_message();

        if (command['status'] == NODE_OK) {
            if (command['data'] == 'cmd1') {
                
                var data_struct = [];

                // ...
                
                var data = {
                    node_id: node_id,
                    data: data_struct
                };

                // ...
                
                node_send_message(data);
            }
        }
    }
}
```

<br>

Cria vários nodes e realiza a troca de mensagens com todos.

```js
// Cria nodes.
var instances = [];

for (var a=0; a<3; a++) {
    var instance :node = function1(a);

    instances[a] = {
        instance: instance, // Handle do node.
        status: 0,          // Flag para controle da troca de mensagens.
                            //  0 = Não enviou mensagem ainda.
                            //  1 = Enviou mensagem, e está aguardando resposta.
    };
}

// Controlador das mensagens.
for () {

    // Envia comando para os nodes.
    for (var a=0; a<3; a++) {
        if (instances[a]['status'] == 0) {
            instances[a]['status'] == 1;

            node_send_message_to( node_get_id(instances[a]['instance']), 'cmd1' );
        }
    }

    // Verifica resposta dos nodes.
    for (var a=0; a<3; a++) {
        if (instances[a]['status'] == 1) {

            var response = node_recv_message_from( node_get_id(instances[a]['instance']) );

            if (response['status'] == NODE_OK) {
                
                // Processa dados...

                instances[a]['status'] == 0; // Libera flag.
            }
        }
    }
}
```

<br>

****

### <b>Manipulação de visibilidade de nodes</b>

<br>


<p align="center" >
<br>
<img src="../0%20-%20extras/diagram/general-4.png" />
<br>
<br>
</p>




