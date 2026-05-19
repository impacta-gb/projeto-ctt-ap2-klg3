# Arrays, Slices e Maps

## Arrays

```go
var numeros [3]int
```

## Slices

```go
nomes := []string{"Ana", "Carlos", "Maria"}
```

## Maps

```go
idades := map[string]int{
    "Ana": 20,
    "Carlos": 25,
}
```

## Acessando Valores

```go
fmt.Println(idades["Ana"])
```

| Estrutura | Dinâmica |
|---|---|
| Array | Não |
| Slice | Sim |
| Map | Sim |

!!! warning "Cuidado"
    Arrays possuem tamanho fixo.