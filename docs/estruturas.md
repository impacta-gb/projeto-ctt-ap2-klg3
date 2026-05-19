# Estruturas de Controle

## If

```go
idade := 18

if idade >= 18 {
    fmt.Println("Maior de idade")
}
```

## For

```go
for i := 0; i < 5; i++ {
    fmt.Println(i)
}
```

## Switch

```go
dia := 2

switch dia {
case 1:
    fmt.Println("Domingo")
case 2:
    fmt.Println("Segunda")
default:
    fmt.Println("Outro dia")
}
```

!!! note "Curiosidade"
    Go não possui while. O for substitui esse comportamento.