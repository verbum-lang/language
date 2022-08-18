### <b>INC - Inter-node communication</b>

****

Exemplo de comunicação entre contextos diferentes.

```php
// Função para ser executada num node.
fn function1 (node_id :int) {
    for () {
        var command = node_recv_message();

        if (command['status'] == NODE_OK) {
            if (command['data'] == 'cmd1') {
                
                var data_struct :array = [];

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

            var response = node_recv_message_from(                                node_get_id(instances[a]['instance']));

            if (response['status'] == NODE_OK) {
                
                // Processa dados...

                instances[a]['status'] == 0; // Libera flag.
            }
        }
    }
}
```


