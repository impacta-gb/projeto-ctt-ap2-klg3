# 4. Arrays, Slices e Maps

Ao desenvolver programas, muitas vezes precisamos armazenar vários valores.

Exemplo:

- Lista de usuários
- Produtos de um sistema
- Idades de pessoas
- Notas de alunos
- Dados vindos de APIs

Para isso, Go fornece estruturas de dados específicas.

As principais são:

| Estrutura | Função |
|---|---|
| Array | Armazena vários valores com tamanho fixo |
| Slice | Lista dinâmica baseada em arrays |
| Map | Estrutura chave e valor |

---

# 🧠 O que são Estruturas de Dados?

Estruturas de dados são formas de organizar informações na memória.

Elas ajudam em:

- Performance
- Organização
- Manipulação de dados
- Busca de informações
- Escalabilidade

---

# 📌 Arrays

Arrays armazenam múltiplos valores do mesmo tipo.

O tamanho do array é definido no momento da criação e NÃO pode ser alterado depois.

---

# ✅ Exemplo Básico

```go
var numeros [3]int
```

---

# 🔍 Explicação Detalhada

| Parte | Função |
|---|---|
| `var` | Declara uma variável |
| `numeros` | Nome do array |
| `[3]` | Quantidade de posições |
| `int` | Tipo dos valores armazenados |

---

# 📌 Como o Array funciona na memória?

Quando criamos:

```go
var numeros [3]int
```

O Go cria automaticamente:

```txt
[0] [0] [0]
```

Porque o valor padrão (`zero value`) do tipo `int` é `0`.

---

# 📌 Índices do Array

Arrays utilizam índices numéricos.

O primeiro índice sempre começa em `0`.

---

# 🔍 Exemplo visual

| Índice | Valor |
|---|---|
| `0` | Primeiro elemento |
| `1` | Segundo elemento |
| `2` | Terceiro elemento |

---

# ✅ Atribuindo valores

```go
var numeros [3]int

numeros[0] = 10
numeros[1] = 20
numeros[2] = 30
```

---

# 🔍 Resultado na memória

| Índice | Valor |
|---|---|
| `0` | `10` |
| `1` | `20` |
| `2` | `30` |

---

# ✅ Acessando valores

```go
fmt.Println(numeros[0])
```

---

# 🔍 Saída

```txt
10
```

---

# 📌 O que acontece aqui?

```go
numeros[0]
```

Significa:

> "Pegue o valor armazenado na posição 0"

---

# ⚠️ Cuidado com índices inválidos

---

# ❌ Errado

```go
fmt.Println(numeros[10])
```

---

# 🔥 Erro

```txt
panic: runtime error
```

---

# 📌 Porque acontece?

O array possui apenas:

```txt
0, 1, 2
```

Não existe posição `10`.

---

# 📌 Inicialização Direta

Podemos criar arrays já preenchidos.

---

# ✅ Exemplo

```go
numeros := [3]int{10, 20, 30}
```

---

# 🔍 Explicação

| Parte | Função |
|---|---|
| `[3]` | Quantidade de elementos |
| `int` | Tipo dos elementos |
| `{10,20,30}` | Valores iniciais |

---

# 📌 Inferência de Tamanho

Go consegue descobrir o tamanho automaticamente.

---

# ✅ Exemplo

```go
numeros := [...]int{1,2,3,4}
```

---

# 🔍 O Go entende como:

```go
[4]int
```

---

# 📌 Obtendo tamanho do Array

Usamos `len()`.

---

# ✅ Exemplo

```go
numeros := [3]int{10,20,30}

fmt.Println(len(numeros))
```

---

# 🔍 Saída

```txt
3
```

---

# 📌 Arrays possuem tamanho fixo

Depois de criado:

❌ NÃO pode aumentar  
❌ NÃO pode diminuir

---

# ⚠️ Exemplo

```go
numeros := [3]int{1,2,3}
```

Esse array SEMPRE terá 3 posições.

---

# 📌 Arrays são copiados

Arrays em Go trabalham por valor.

---

# ✅ Exemplo

```go
a := [3]int{1,2,3}

b := a

b[0] = 100

fmt.Println(a)
fmt.Println(b)
```

---

# 🔍 Saída

```txt
[1 2 3]
[100 2 3]
```

---

# 📌 O que aconteceu?

Quando fazemos:

```go
b := a
```

O Go cria uma cópia completa do array.

Ou seja:

- `a` continua igual
- `b` é independente

---

# 📌 Percorrendo Arrays

---

# ✅ Usando `for`

```go
numeros := [3]int{10,20,30}

for i := 0; i < len(numeros); i++ {
    fmt.Println(numeros[i])
}
```

---

# 🔍 Explicação

| Parte | Função |
|---|---|
| `i := 0` | começa no índice 0 |
| `i < len()` | percorre até o final |
| `i++` | aumenta o índice |

---

# ✅ Usando `range`

```go
numeros := [3]int{10,20,30}

for indice, valor := range numeros {
    fmt.Println(indice, valor)
}
```

---

# 🔍 Saída

```txt
0 10
1 20
2 30
```

---

# 📌 O que o `range` faz?

O `range` percorre automaticamente estruturas como:

- Arrays
- Slices
- Maps
- Strings

---

# 🚀 Slices

Slices são estruturas dinâmicas construídas sobre arrays.

Na prática:

> Slices são MUITO mais usados que arrays.

---

# 📌 Por que slices existem?

Arrays possuem limitações:

- Tamanho fixo
- Pouca flexibilidade
- Difíceis de manipular

Slices resolvem isso.

---

# ✅ Exemplo Básico

```go
nomes := []string{"Ana", "Carlos", "Maria"}
```

---

# 🔍 Explicação

| Parte | Significado |
|---|---|
| `[]string` | Slice de strings |
| `{}` | Valores armazenados |

---

# 📌 Estrutura interna do Slice

Internamente um slice possui:

| Campo | Função |
|---|---|
| Pointer | Aponta para array |
| Length | Quantidade atual |
| Capacity | Capacidade máxima |

---

# 📌 Comprimento do Slice

Usamos `len()`.

---

# ✅ Exemplo

```go
nomes := []string{"Ana", "Carlos"}

fmt.Println(len(nomes))
```

---

# 🔍 Saída

```txt
2
```

---

# 📌 Capacidade do Slice

Usamos `cap()`.

---

# ✅ Exemplo

```go
fmt.Println(cap(nomes))
```

---

# 📌 Adicionando elementos

Usamos `append()`.

---

# ✅ Exemplo

```go
nomes := []string{"Ana"}

nomes = append(nomes, "Carlos")
```

---

# 🔍 Resultado

```txt
[Ana Carlos]
```

---

# 📌 O que o append faz?

Quando necessário:

1. Go cria novo array
2. Copia valores antigos
3. Adiciona novo elemento
4. Expande capacidade

---

# 📌 Slice compartilhando memória

Slices apontam para arrays.

---

# ✅ Exemplo

```go
numeros := [5]int{1,2,3,4,5}

slice := numeros[1:4]

fmt.Println(slice)
```

---

# 🔍 Resultado

```txt
[2 3 4]
```

---

# 📌 Explicação do corte

```go
[1:4]
```

Significa:

| Parte | Função |
|---|---|
| `1` | índice inicial |
| `4` | índice final (não incluso) |

---

# 📌 Alterando slice altera array

---

# ✅ Exemplo

```go
numeros := [3]int{1,2,3}

slice := numeros[:]

slice[0] = 100

fmt.Println(numeros)
```

---

# 🔍 Saída

```txt
[100 2 3]
```

---

# ⚠️ Importante

Slices compartilham memória com arrays.

---

# 📌 Iterando Slices

---

# ✅ Exemplo

```go
nomes := []string{"Ana", "Carlos", "Maria"}

for indice, valor := range nomes {
    fmt.Println(indice, valor)
}
```

---

# 🗺️ Maps

Maps armazenam dados no formato:

```txt
chave -> valor
```

Muito parecido com:

- Objetos JavaScript
- Dicionários Python
- HashMaps Java

---

# 📌 Exemplo visual

```txt
"Ana" -> 20
"Carlos" -> 25
```

---

# ✅ Exemplo Básico

```go
idades := map[string]int{
    "Ana": 20,
    "Carlos": 25,
}
```

---

# 🔍 Explicação

| Parte | Significado |
|---|---|
| `map` | Estrutura map |
| `string` | Tipo da chave |
| `int` | Tipo do valor |

---

# 📌 Acessando valores

---

# ✅ Exemplo

```go
fmt.Println(idades["Ana"])
```

---

# 🔍 Saída

```txt
20
```

---

# 📌 Adicionando valores

---

# ✅ Exemplo

```go
idades["Maria"] = 30
```

---

# 📌 Alterando valores

---

# ✅ Exemplo

```go
idades["Ana"] = 50
```

---

# 📌 Removendo valores

Usamos `delete()`.

---

# ✅ Exemplo

```go
delete(idades, "Carlos")
```

---

# 📌 Verificando se chave existe

---

# ✅ Exemplo

```go
idade, existe := idades["Ana"]

fmt.Println(idade)
fmt.Println(existe)
```

---

# 🔍 Saída

```txt
20
true
```

---

# 📌 Explicação

| Variável | Função |
|---|---|
| `idade` | Valor encontrado |
| `existe` | Verifica se a chave existe |

---

# 📌 E se não existir?

```go
idade, existe := idades["Pedro"]
```

---

# 🔍 Resultado

```txt
0
false
```

---

# ⚠️ Importante

O map retorna:

- Valor zero do tipo
- `false`

---

# 📌 Percorrendo Maps

---

# ✅ Exemplo

```go
for chave, valor := range idades {
    fmt.Println(chave, valor)
}
```

---

# ⚠️ Ordem dos maps

Maps NÃO possuem ordem fixa.

A ordem pode mudar em cada execução.

---

# 📌 Criando maps com `make`

---

# ✅ Exemplo

```go
idades := make(map[string]int)
```

---

# 🔍 Explicação

`make()` aloca memória para:

- Maps
- Slices
- Channels

---

# 📌 Diferença entre Array, Slice e Map

| Característica | Array | Slice | Map |
|---|---|---|---|
| Tamanho fixo | ✅ | ❌ | ❌ |
| Dinâmico | ❌ | ✅ | ✅ |
| Índices numéricos | ✅ | ✅ | ❌ |
| Chaves personalizadas | ❌ | ❌ | ✅ |
| Muito usado | ❌ | ✅ | ✅ |

---

# 🚀 Exemplo Completo

```go
package main

import "fmt"

func main() {

    // ARRAY
    numeros := [3]int{10,20,30}

    // SLICE
    nomes := []string{"Ana", "Carlos"}

    nomes = append(nomes, "Maria")

    // MAP
    idades := map[string]int{
        "Ana": 20,
        "Carlos": 25,
    }

    fmt.Println(numeros)

    fmt.Println(nomes)

    fmt.Println(idades)

    fmt.Println(idades["Ana"])

    // LOOP ARRAY
    for i, valor := range numeros {
        fmt.Println(i, valor)
    }

    // LOOP SLICE
    for i, nome := range nomes {
        fmt.Println(i, nome)
    }

    // LOOP MAP
    for chave, valor := range idades {
        fmt.Println(chave, valor)
    }
}
```

---

# 🔍 Saída Esperada

```txt
[10 20 30]

[Ana Carlos Maria]

map[Ana:20 Carlos:25]

20

0 10
1 20
2 30
```

---

# ✅ Boas Práticas

| Prática | Motivo |
|---|---|
| Prefira slices | Mais flexíveis |
| Use maps para buscas rápidas | Melhor performance |
| Use `range` | Código mais limpo |
| Evite arrays grandes | Pouco flexíveis |
| Verifique existência em maps | Evita erros |

---

# 💡 Dica 

> Em projetos reais Go, arrays são pouco utilizados diretamente.
>
> As estruturas mais usadas no dia a dia são:
>
> - Slices
> - Maps
>
> Elas oferecem mais flexibilidade, desempenho e facilidade de manutenção.

---
