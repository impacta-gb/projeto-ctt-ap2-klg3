# 10. Testes Automatizados em Go

## Arquivo de Teste

```go
package main

import "testing"

func Soma(a, b int) int {
    return a + b
}

func TestSoma(t *testing.T) {
    resultado := Soma(2, 2)

    if resultado != 4 {
        t.Errorf("Esperado 4")
    }
}
```

## Executando Testes

```bash
go test
```

## Cobertura

```bash
go test -cover
```

!!! note "Importante"
    Arquivos de teste devem terminar com _test.go
