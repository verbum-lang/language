### <b>Hot Code Reloading</b>

****

Em linhas gerais a utilidade deste recurso é de poder atualizar partes do sistema em execução, em produção, sem a necessidade de pará-lo por completo.

<b>Noções de migração relacionadas ao hot code reloading e meta programming:</b>

- Ao enviar um código modificado, o mesmo passa a ser prioritário, mas para as ações já iniciadas, seguirá utilizando o código atual (antigo).

- É criado um histórico dos códigos em execução. De modo que caso falhar a nova implementação, automaticamente o sistema volta para a solução anterior e a utiliza.

- A quantidade de códigos em histórico deve ser definada em configuração.

- Bem como esta noção só deve ser aplicada para coisas como funções, sendo a função tratada como um todo. Qualquer modificação nela acarretará na existência de uma nova versão da função. Tendo em vista que código fora de funções pertencem a uma função oculta. Também tendo em vista que o que muda é tanto a organização dos comandos, como os próprios comandos, do ponto de vista da AST, e não simplesmente a organização do código tratado como texto formatado.

- Se a versão atual do código falhar, e as antigas também (caso ocorrer modicações em outras áreas do sistema, que acarrete nesse ponto), o sistema passa a priorizar a mais recente atualização.

Tais noções são realizadas através da suite da linguagem.


