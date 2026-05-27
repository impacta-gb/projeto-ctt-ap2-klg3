# 5. Structs e Métodos

Durante o desenvolvimento de sistemas, frequentemente precisamos representar entidades do mundo real.

Exemplos:

- Usuários
- Produtos
- Clientes
- Funcionários
- Carros
- Pedidos
- Contas bancárias

Para organizar esses dados, Go utiliza:

- Structs
- Métodos

---

# 🧠 O que é uma Struct?

Uma `struct` é uma estrutura que agrupa múltiplos dados relacionados em um único tipo.

Ela funciona de forma parecida com:

- Classes simplificadas
- Objetos
- Registros
- Modelos de dados

---

# 📌 Exemplo do mundo real

Imagine uma pessoa.

Uma pessoa possui:

- Nome
- Idade
- Altura
- CPF
- Email

Em vez de criar várias variáveis separadas:

```go
var nome string
var idade int
var email string
```

Podemos agrupar tudo em uma `struct`.

---

# ✅ Exemplo Básico

```go
type Pessoa struct {
    Nome  string
    Idade int
}
```

---

# 🔍 Explicação Detalhada

| Parte | Função |
|---|---|
| `type` | Cria um novo tipo |
| `Pessoa` | Nome da struct |
| `struct` | Define estrutura de dados |
| `Nome` | Campo da struct |
| `string` | Tipo do campo |
| `Idade` | Outro campo |
| `int` | Tipo inteiro |

---

# 📌 O que o Go cria internamente?

A struct funciona como um molde.

---

# 🔍 Representação visual

```txt
Pessoa
├── Nome  -> string
└── Idade -> int
```

---

# 📌 Structs agrupam dados relacionados

A ideia principal é:

> Organizar informações que pertencem à mesma entidade.

---

# 🚀 Criando Objetos (Instâncias)

Depois de criar a struct, podemos criar variáveis baseadas nela.

Essas variáveis são chamadas de:

- Objetos
- Instâncias

---

# ✅ Exemplo

```go
p := Pessoa{
    Nome: "Kassia",
    Idade: 20,
}
```

---

# 🔍 Explicação

| Parte | Função |
|---|---|
| `p` | Variável criada |
| `Pessoa` | Tipo da struct |
| `Nome:` | Campo sendo preenchido |
| `"Kassia"` | Valor do campo |
| `Idade:` | Outro campo |
| `20` | Valor inteiro |

---

# 📌 O que foi criado?

```txt
Pessoa
├── Nome  -> Kassia
└── Idade -> 20
```

---

# 📌 Acessando Campos

Usamos o operador `.`

---

# ✅ Exemplo

```go
fmt.Println(p.Nome)
fmt.Println(p.Idade)
```

---

# 🔍 Saída

```txt
Kassia
20
```

---

# 📌 Alterando Valores

Campos podem ser modificados.

---

# ✅ Exemplo

```go
p.Idade = 25
```

---

# 🔍 Resultado

```txt
Idade -> 25
```

---

# 📌 Inicialização Posicional

Também é possível criar structs sem nomear os campos.

---

# ✅ Exemplo

```go
p := Pessoa{"Kassia", 20}
```

---

# ⚠️ Problema dessa abordagem

Pode gerar confusão:

```go
Pessoa{"Kassia", 20}
```

O que é `20`?

- idade?
- altura?
- peso?

---

# ✅ Boa prática

Prefira inicialização nomeada.

---

# ✔️ Recomendado

```go
Pessoa{
    Nome: "Kassia",
    Idade: 20,
}
```

---

# 📌 Valores Zero em Structs

Se um campo não for preenchido, Go utiliza o valor zero.

---

# ✅ Exemplo

```go
p := Pessoa{}
```

---

# 🔍 Resultado

| Campo | Valor |
|---|---|
| Nome | `""` |
| Idade | `0` |

---

# 📌 Structs Aninhadas

Uma struct pode conter outra struct.

---

# ✅ Exemplo

```go
type Endereco struct {
    Cidade string
    Estado string
}

type Pessoa struct {
    Nome string
    Endereco Endereco
}
```

---

# 🔍 Estrutura criada

```txt
Pessoa
├── Nome
└── Endereco
    ├── Cidade
    └── Estado
```

---

# ✅ Criando objeto

```go
p := Pessoa{
    Nome: "Kassia",
    Endereco: Endereco{
        Cidade: "São Paulo",
        Estado: "SP",
    },
}
```

---

# 📌 Acessando dados aninhados

---

# ✅ Exemplo

```go
fmt.Println(p.Endereco.Cidade)
```

---

# 🔍 Saída

```txt
São Paulo
```

---

# 🚀 Métodos em Go

Métodos são funções associadas a uma struct.

Eles representam comportamentos da estrutura.

---

# 📌 Exemplo do mundo real

Uma pessoa pode:

- Falar
- Andar
- Comer
- Apresentar-se

Essas ações podem virar métodos.

---

# ✅ Exemplo do arquivo

```go
func (p Pessoa) Apresentar() {
    fmt.Println("Olá,", p.Nome)
}
```

---

# 🔍 Explicação Detalhada

| Parte | Função |
|---|---|
| `func` | Declara função |
| `(p Pessoa)` | Receiver |
| `Apresentar()` | Nome do método |
| `p.Nome` | Campo acessado |

---

# 📌 O que é Receiver?

O receiver conecta o método à struct.

---

# 🔍 Exemplo

```go
(p Pessoa)
```

Significa:

> "Esse método pertence à struct Pessoa"

---

# 📌 Receiver funciona parecido com `this`

Em outras linguagens:

| Linguagem | Palavra |
|---|---|
| Java | `this` |
| C# | `this` |
| JavaScript | `this` |
| Go | receiver |

---

# 📌 Chamando Métodos

---

# ✅ Exemplo

```go
p.Apresentar()
```

---

# 🔍 Saída

```txt
Olá, Kassia
```

---

# 📌 O que acontece internamente?

O Go transforma:

```go
p.Apresentar()
```

em algo parecido com:

```go
Apresentar(p)
```

---

# 🚀 Métodos com Retorno

Métodos podem retornar valores.

---

# ✅ Exemplo

```go
func (p Pessoa) Saudacao() string {
    return "Olá " + p.Nome
}
```

---

# ✅ Utilizando

```go
mensagem := p.Saudacao()

fmt.Println(mensagem)
```

---

# 🔍 Saída

```txt
Olá Kassia
```

---

# 🚀 Métodos com Ponteiros

Métodos podem alterar os dados da struct.

Para isso usamos ponteiros.

---

# ✅ Exemplo

```go
func (p *Pessoa) FazerAniversario() {
    p.Idade++
}
```

---

# 📌 Explicação

| Parte | Função |
|---|---|
| `*Pessoa` | Ponteiro |
| `p.Idade++` | Incrementa idade |

---

# 📌 Sem ponteiro não altera original

---

# ❌ Exemplo incorreto

```go
func (p Pessoa) FazerAniversario() {
    p.Idade++
}
```

---

# 🔍 Problema

Nesse caso:

- Go cria cópia da struct
- Alteração acontece apenas na cópia

---

# ✅ Correto

```go
func (p *Pessoa) FazerAniversario() {
    p.Idade++
}
```

---

# 📌 Utilizando

```go
p.FazerAniversario()
```

---

# 🔍 Resultado

```txt
Idade aumentada
```

---

# 📌 Métodos podem receber parâmetros

---

# ✅ Exemplo

```go
func (p Pessoa) Cumprimentar(nome string) {
    fmt.Println("Olá", nome)
}
```

---

# ✅ Chamando

```go
p.Cumprimentar("Carlos")
```

---

# 🔍 Saída

```txt
Olá Carlos
```

---

# 📌 Structs em aplicações reais

Structs são utilizadas em:

- APIs
- Bancos de dados
- JSON
- Microsserviços
- Sistemas web
- ORM
- Frameworks

---

# 📌 Exemplo de usuário

```go
type Usuario struct {
    ID    int
    Nome  string
    Email string
}
```

---

# 📌 Exemplo de produto

```go
type Produto struct {
    Nome  string
    Preco float64
    Estoque int
}
```

---

# 📌 Exemplo de conta bancária

```go
type Conta struct {
    Titular string
    Saldo float64
}
```

---

# 🚀 Método de depósito

```go
func (c *Conta) Depositar(valor float64) {
    c.Saldo += valor
}
```

---

# 🚀 Método de saque

```go
func (c *Conta) Sacar(valor float64) {

    if valor > c.Saldo {
        fmt.Println("Saldo insuficiente")
        return
    }

    c.Saldo -= valor
}
```

---

# 📌 Encapsulamento em Go

Go não possui `private/public` tradicional.

A visibilidade depende da letra inicial.

---

# ✅ Público

```go
Nome
Idade
Pessoa
```

---

# ✅ Privado

```go
nome
idade
pessoa
```

---

# 📌 Regras

| Tipo | Visibilidade |
|---|---|
| Maiúscula | Público |
| Minúscula | Privado |

---

# 📌 Structs Anônimas

Go permite criar structs sem nome.

---

# ✅ Exemplo

```go
usuario := struct {
    Nome string
    Idade int
}{
    Nome: "Kassia",
    Idade: 20,
}
```

---

# 📌 Quando usar?

Structs anônimas são úteis para:

- Testes
- Respostas rápidas
- Dados temporários

---

# 📌 Composição em Go

Go não possui herança tradicional.

Em vez disso utiliza composição.

---

# ✅ Exemplo

```go
type Motor struct {
    Potencia int
}

type Carro struct {
    Marca string
    Motor Motor
}
```

---

# 🔍 Estrutura

```txt
Carro
├── Marca
└── Motor
    └── Potencia
```

---

# 📌 Vantagens da composição

- Código mais desacoplado
- Reutilização
- Menos complexidade
- Melhor manutenção

---

# 🚀 Exemplo Completo

```go
package main

import "fmt"

type Pessoa struct {
    Nome  string
    Idade int
}

// Método simples
func (p Pessoa) Apresentar() {
    fmt.Println("Olá,", p.Nome)
}

// Método com retorno
func (p Pessoa) Saudacao() string {
    return "Bem-vindo " + p.Nome
}

// Método com ponteiro
func (p *Pessoa) FazerAniversario() {
    p.Idade++
}

func main() {

    // Criando struct
    p := Pessoa{
        Nome: "Kassia",
        Idade: 20,
    }

    // Acessando campos
    fmt.Println(p.Nome)

    // Chamando método
    p.Apresentar()

    // Método com retorno
    msg := p.Saudacao()

    fmt.Println(msg)

    // Alterando idade
    p.FazerAniversario()

    fmt.Println(p.Idade)
}
```

---

# 🔍 Saída Esperada

```txt
Kassia

Olá, Kassia

Bem-vindo Kassia

21
```

---

# ✅ Boas Práticas

| Prática | Motivo |
|---|---|
| Use structs para agrupar dados | Organização |
| Prefira inicialização nomeada | Legibilidade |
| Use métodos para comportamentos | Encapsulamento |
| Use ponteiros quando alterar dados | Performance |
| Prefira composição ao invés de herança | Flexibilidade |

---

# 💡 Dica

> Structs são uma das partes mais importantes da linguagem Go.
>
> Quase todos os sistemas Go utilizam structs para:
>
> - Modelagem de dados
> - APIs
> - Bancos de dados
> - JSON
> - Microsserviços
> - Comunicação entre sistemas
>
> Aprender structs e métodos é essencial para dominar Go.

---

