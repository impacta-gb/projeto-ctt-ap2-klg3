# 3. Estruturas de Controle

As estruturas de controle são responsáveis por definir o fluxo de execução de um programa. Com elas, é possível tomar decisões, repetir tarefas e executar diferentes blocos de código de acordo com determinadas condições.

Em Go, as principais estruturas de controle são:

- If (decisões condicionais)
- For (repetições e laços)
- Switch (seleção entre múltiplas opções)

---

## If

A estrutura `if` é utilizada para executar um bloco de código somente quando uma condição for verdadeira.

Ela permite que o programa tome decisões com base em valores, comparações ou resultados de expressões lógicas.

### Sintaxe

```go
if condicao {
    // código executado se a condição for verdadeira
}
```

### Exemplo

```go
idade := 18

if idade >= 18 {
    fmt.Println("Maior de idade")
}
```

Neste exemplo, a mensagem será exibida apenas se a variável `idade` possuir valor maior ou igual a 18.

### Utilizando Else

O bloco `else` permite executar um código alternativo quando a condição não for atendida.

```go
idade := 16

if idade >= 18 {
    fmt.Println("Maior de idade")
} else {
    fmt.Println("Menor de idade")
}
```

---

## For

O `for` é a única estrutura de repetição existente na linguagem Go.

Ele é utilizado quando uma ação precisa ser executada várias vezes, seja por uma quantidade definida de repetições ou enquanto uma condição for verdadeira.

### Sintaxe Tradicional

```go
for i := 0; i < 5; i++ {
    fmt.Println(i)
}
```

Resultado:

```text
0
1
2
3
4
```

### For como While

Como Go não possui a estrutura `while`, o `for` também pode ser utilizado dessa forma:

```go
contador := 0

for contador < 5 {
    fmt.Println(contador)
    contador++
}
```

O laço continuará executando enquanto a condição for verdadeira.

### Loop Infinito

Também é possível criar loops infinitos:

```go
for {
    fmt.Println("Executando...")
}
```

Esse tipo de estrutura é comum em servidores e aplicações que precisam permanecer em execução continuamente.

---

## Switch

A estrutura `switch` é utilizada quando existem várias condições possíveis para uma mesma variável.

Ela torna o código mais organizado e legível do que utilizar diversos blocos `if` e `else if`.

### Sintaxe

```go
switch valor {
case opcao1:
    // código
case opcao2:
    // código
default:
    // código padrão
}
```

### Exemplo

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

Neste caso, como o valor de `dia` é igual a `2`, será exibida a mensagem "Segunda".

### Utilizando Múltiplos Valores

```go
nota := "B"

switch nota {
case "A":
    fmt.Println("Excelente")
case "B", "C":
    fmt.Println("Bom")
default:
    fmt.Println("Precisa melhorar")
}
```

---

## Comparação entre as Estruturas

| Estrutura | Finalidade |
|------------|------------|
| If | Executar código com base em uma condição |
| For | Repetir instruções várias vezes |
| Switch | Selecionar entre múltiplas opções |

!!! note "Curiosidade"
    Diferentemente de linguagens como C, Java e JavaScript, o Go não possui a estrutura `while`. Todas as repetições são realizadas utilizando o comando `for`.

!!! tip "Boa prática"
    Utilize `switch` quando houver muitas condições relacionadas à mesma variável. Isso torna o código mais limpo e fácil de manter.
