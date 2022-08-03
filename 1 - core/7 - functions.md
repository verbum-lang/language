### Funções

O modo de uso das funções é semelhante ao da linguagem Rust.

Alguns exemplos.

```rust
fn example (a:int, b:int) -> int {
    ret (a * b) + 31337;
}

fn function () {
    print("Iesus Verbum!\n");
}
```

Note que caso seja necessário retornar dados diferentes, isto é, equivalente a noção de retornar uma <b>struct</b> como na linguagem C. Para isto basta utilizar um array, seja ele indexado ou associativo, desta maneira é possível ter uma estrutura de dados.

```rust
fn function () -> array {
    // ...
    ret { result: 333 };
}
```


