# Sintaxe Básica e Variáveis

## Estrutura Básica

```go
package main

import "fmt"

func main() {
    fmt.Println("Olá Mundo")
}
```

## Declarando Variáveis

```go
var nome string = "Kassia"
var idade int = 20
```

## Declaração Curta

```go
cidade := "São Paulo"
```

## Tipos Primitivos

| Tipo | Exemplo |
|---|---|
| int | 10 |
| string | "Go" |
| bool | true |
| float64 | 10.5 |

!!! warning "Importante"
    O operador := só funciona dentro de funções.