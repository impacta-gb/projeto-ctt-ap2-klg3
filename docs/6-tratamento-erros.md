# 6. Tratamento de Erros

Go utiliza retorno de erros ao invés de try/catch.

## Exemplo

```go
package main

import (
    "fmt"
    "errors"
)

func dividir(a, b int) (int, error) {
    if b == 0 {
        return 0, errors.New("divisão por zero")
    }

    return a / b, nil
}
```

## Verificando Erros

```go
resultado, err := dividir(10, 0)

if err != nil {
    fmt.Println(err)
}
```

!!! warning "Importante"
    Sempre trate erros retornados pelas funções.
