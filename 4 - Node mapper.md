### :arrow_right: Funcionamento do Node Mapper.

O Node Mapper possui o papel de auxiliar na gestão dos nodes do sistema projetado, podendo monitorar os nodes e realizar ações nos mesmos através de sua API. Sendo possível adicionar manualmente novos nodes no Node Mapper. Bem como através da sintaxe da linguagem, poder acessar a lista de nodes e usá-los no sistema.

Dentro de cada node, há um Node Mapper para controlar os nodes acessíveis dentro do contexto em questão.
Um node fica periodicamente solicitando o Node Mapper para seus nodes filhos, de modo a manter seu Node Mapper sempre atualizado.
Deste modo é possível ter um mapa da rede de nodes, e suas respectivas informações.

Além do compartilhamento das informações do Node Mapper, os nodes também compartilham suas informações da rede de nodes em execução. Onde tais informações são atualizadas em tempo real / de execução.

O recurso de envio das informações do Node Mapper, de um node de nível inferior, para um de nível superior, deve ser possível desabilita-lo. 


#### Funcionalidades do Node Mapper.

O acesso a esta gestão é por via de shell interativo, e via código.

- Listar os nodes existentes e suas respectivas informações.
- Adicionar novos nodes diretamente no Node Mapper, pois o sistema pode usar tais recursos em tempo de execução.
- Excluir um node.
- Informações de um node em específico: para conectar-se ao node e administra-lo.


#### Instanciamento dos nodes.

É possível conectar em um node já existente (shell interativo, via código).<br>
Criar um através do interpretador (shell interativo, linha de comando).<br>
Ou criar um node em tempo de execução (via código).

<b>Ao criar um node deve-se especificar:</b>

```
Informações gerais:
    Identificador: nome único de identificação.
    Tipo da conexão:
        Direta, conexão padrão, quando o node cliente conecta no node servidor.
        Reversa, conexão para uso diverso, como atravessar redes NATs.
        Obs: inicialmente suportara apenas conexão direta.
    Porta (opcional): para conexões TCP/IP, IPv4.
        A porta é escolhida automática, quando não é diretamente especificada.
    DNS (opcional): nome de domínio que pode ser utilizado para conectar no node.
```

<b>Obs: ao criar um node o mesmo fica disponível no Node Mapper do contexto atual.</b>


#### A respeito do envio das informações do Node Mapper.

Há uma rotina no node de nível superior, que solicita periodicamente as informações do Node Mapper de seus nodes filhos.

Mas além desta rotina, há também o envio de informações atuais, do node filho para o node pai. De modo que ao atualizar suas informações do Node Mapper, imediatamente o node em questão realizará o envio das informações para todos os nodes pais que a ele se conectou (o histórico das conexões dos nodes pais ficam no node filho em questão).


