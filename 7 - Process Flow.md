### :arrow_right: Noções do processo de execução.

- Inicia execução.
- Cria N threads, 1 para cada Core da CPU.
- Estabelece o core 1 como Supervisor (da infraestrutura).
- Inicia a execução do programa a partir do Supervisor.
```Código síncrono e assíncrono é executado na infraestrutura.
Sendo as funções assíncronas threads distribuídas entre os CPU-Core disponíveis.```
- O node é sempre um Machine-Node
- Pode criar novos processos, e cada processo criado, inicia-se como um Machine-Node.
- Um Machine-Node pode criar outro Machine-Node, ou conectar-se em um Network-Node.
- Um Network-Node é um Machine-Node acessível via rede.


