# 2. Sintaxe Básica e Variáveis

## Estrutura Básica de um Programa Go

Todo programa em Go começa com um **pacote** (`package`).  
O ponto de entrada de uma aplicação executável é a função `main()`.

## Exemplo Básico

```go
package main

import "fmt"

func main() {
    fmt.Println("Olá Mundo")
}
```

---

## Explicação do Código

| Linha | Explicação |
|---|---|
| `package main` | Define o pacote principal da aplicação |
| `import "fmt"` | Importa o pacote de formatação e saída |
| `func main()` | Função principal executada ao iniciar o programa |
| `fmt.Println()` | Imprime texto no terminal |

---

# Pacotes e Importações

Go utiliza pacotes para organizar o código.

## Exemplo de múltiplas importações

```go
import (
    "fmt"
    "math"
    "strings"
)
```

---

## Conceitos Importantes

### Encapsulamento

- Identificadores iniciados com **letra maiúscula** são públicos/exportados.
- Identificadores iniciados com **letra minúscula** são privados do pacote.

```go
var Publico string = "Visível fora do pacote"
var privado string = "Visível apenas no pacote"
```

---

### Namespace

Cada pacote possui seu próprio escopo, evitando conflitos de nomes.

---

# Declaração de Variáveis

Go é uma linguagem de **tipagem estática**.

Isso significa que:

- O tipo da variável é conhecido em tempo de compilação.
- Erros de tipo são detectados antes da execução.
- O compilador consegue otimizar melhor o código.

---

# Declaração Tradicional com `var`

```go
var nome string = "Kassia"
var idade int = 20
```

---

## Sintaxe

```go
var nomeDaVariavel tipo = valor
```

---

# Variáveis sem Inicialização

Quando uma variável não recebe valor, Go utiliza o **valor zero** do tipo.

```go
var nome string
var idade int
var ativo bool
var preco float64
```

---

## Valores Recebidos

| Tipo | Valor Zero |
|---|---|
| `string` | `""` |
| `int` | `0` |
| `bool` | `false` |
| `float64` | `0.0` |

---

# Múltiplas Declarações

## Em bloco

```go
var (
    nome   string = "João"
    idade  int    = 30
    cidade string = "São Paulo"
)
```

---

## Na mesma linha

```go
var x, y int = 10, 20
var nome, idade = "Maria", 25
```

> O Go consegue inferir automaticamente os tipos quando possível.

---

# Declaração Curta com `:=`

A forma mais comum em Go moderno.

## Exemplo

```go
cidade := "São Paulo"
```

---

## Múltiplas variáveis

```go
nome, idade := "Carlos", 28
x, y := 10, 20
ativo, preco := true, 99.90
```

---

# Importante sobre `:=`

```go
cidade := "São Paulo"
```

O operador `:=`:

- Só funciona **dentro de funções**
- Não pode ser usado no escopo global

---

# Tipos Primitivos

## Tipos mais utilizados

| Tipo | Exemplo |
|---|---|
| `int` | `10` |
| `string` | `"Go"` |
| `bool` | `true` |
| `float64` | `10.5` |

---

# Tipos Numéricos

| Categoria | Tipos | Descrição |
|---|---|---|
| Inteiros padrão | `int`, `uint` | Dependem da arquitetura |
| Inteiros 8 bits | `int8`, `uint8` | -128 a 127 |
| Inteiros 16 bits | `int16`, `uint16` | Valores maiores |
| Inteiros 32 bits | `int32`, `uint32` | Utilizados em Unicode |
| Inteiros 64 bits | `int64`, `uint64` | Grandes valores |
| Ponto flutuante | `float32`, `float64` | Números decimais |
| Complexos | `complex64`, `complex128` | Parte real + imaginária |

---

# Exemplos Numéricos

```go
var inteiro int = 42
var pequeno int8 = 127
var grande int64 = 9223372036854775807
var decimal float64 = 3.14159
```

---

# Tipo `string`

Strings são imutáveis e armazenadas em UTF-8.

```go
var nome string = "Go Lang"

saudacao := "Olá, mundo!"
vazia := ""
```

---

# Tipo `bool`

Representa verdadeiro ou falso.

```go
var ativo bool = true
var logado bool = false
```

---

# `byte` e `rune`

## `byte`

Alias para `uint8`.

```go
var letra byte = 'A'
```

---

## `rune`

Alias para `int32`, utilizado para Unicode.

```go
var simbolo rune = '😀'
```

---

# Valores Zero (Zero Values)

Go inicializa automaticamente variáveis não definidas.

## Exemplo

```go
var a int
var b string
var c bool
var d float64
```

---

## Resultado

| Variável | Valor |
|---|---|
| `a` | `0` |
| `b` | `""` |
| `c` | `false` |
| `d` | `0.0` |

---

# Constantes

Constantes não podem ser alteradas durante a execução.

## Exemplo

```go
const pi = 3.14159

const nomeApp string = "MeuApp"
```

---

## Bloco de constantes

```go
const (
    segundosPorMinuto = 60
    minutosPorHora    = 60
    horasPorDia       = 24
)
```

---

# Escopo e Visibilidade

| Escopo | Localização | Visibilidade |
|---|---|---|
| Global | Fora de funções | Todo o pacote |
| Função | Dentro da função | Apenas na função |
| Bloco | Dentro de `{}` | Apenas no bloco |

---

# Exportação em Go

## Público (Exportado)

```go
func FuncaoPublica() {}
```

---

## Privado (Não exportado)

```go
func funcaoPrivada() {}
```

---

# Conversão de Tipos

Go não faz conversões automáticas entre tipos.

## Conversão explícita

```go
var x int = 10
var y float64 = float64(x)
```

---

## Conversão entre inteiros

```go
var a int32 = 42
var b int64 = int64(a)
```

---

## Conversão para byte

```go
var i int = 65
var c byte = byte(i)
```

---

# Regras Importantes

## Regra 1

Toda variável declarada deve ser utilizada.

```go
var nome string // erro se não usar
```

---

## Regra 2

`:=` só funciona dentro de funções.

```go
func main() {
    nome := "Go"
}
```

---

## Regra 3

Go não possui operador ternário.

❌ Errado:

```go
x := condicao ? 1 : 2
```

✅ Correto:

```go
if condicao {
    x = 1
} else {
    x = 2
}
```

---

## Regra 4

Go pode inferir tipos automaticamente.

```go
nome := "Kassia"
idade := 20
```

---

# Boas Práticas

| Prática | Motivo |
|---|---|
| Prefira `:=` | Código mais limpo |
| Use `camelCase` | Padrão da comunidade |
| Variáveis próximas do uso | Melhor legibilidade |
| Evite globais | Código mais seguro |
| Use constantes | Evita valores mágicos |

---

# Exemplo Completo

```go
package main

import "fmt"

// Constante global
const appName = "Documentação Go"

// Variáveis globais
var versao string = "1.24"

var (
    autor string = "Equipe CTT"
    ano   int    = 2026
)

func main() {

    // Declaração curta
    mensagem := "Olá, mundo!"

    // Múltiplas variáveis
    nome, idade := "Kassia", 20

    // Conversão explícita
    var x int = 10
    var y float64 = float64(x)

    fmt.Println(mensagem)
    fmt.Println("Nome:", nome)
    fmt.Println("Idade:", idade)
    fmt.Println("Conversão:", y)
}
```

---

# 💡 Dica 

> Em Go, a declaração curta `:=` é a forma mais utilizada no dia a dia.  
> Use `var` principalmente para variáveis globais ou quando precisar do valor zero explicitamente.

---
