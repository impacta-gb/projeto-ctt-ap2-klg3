# Concorrência I: Goroutines

Goroutines permitem executar funções concorrentemente.

## Exemplo

```go
go minhaFuncao()
```

## Código Completo

```go
package main

import (
    "fmt"
    "time"
)

func tarefa() {
    fmt.Println("Executando...")
}

func main() {
    go tarefa()

    time.Sleep(time.Second)
}
```

!!! warning "Cuidado"
    O programa pode finalizar antes da goroutine terminar.