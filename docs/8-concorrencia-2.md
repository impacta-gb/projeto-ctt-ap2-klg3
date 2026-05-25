# 8. Concorrência II: Channels

Channels permitem comunicação entre goroutines.

## Criando Channel

```go
canal := make(chan string)
```

## Enviando Dados

```go
canal <- "Olá"
```

## Recebendo Dados

```go
mensagem := <-canal
```

## Exemplo Completo

```go
package main

import "fmt"

func main() {
    canal := make(chan string)

    go func() {
        canal <- "Olá Go"
    }()

    msg := <-canal

    fmt.Println(msg)
}
```
