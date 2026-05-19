# Structs e Métodos

## Struct

```go
type Pessoa struct {
    Nome string
    Idade int
}
```

## Criando Objeto

```go
p := Pessoa{
    Nome: "Kassia",
    Idade: 20,
}
```

## Métodos

```go
func (p Pessoa) Apresentar() {
    fmt.Println("Olá,", p.Nome)
}
```

## Chamando Método

```go
p.Apresentar()
```

!!! note "Boa prática"
    Structs organizam dados relacionados.