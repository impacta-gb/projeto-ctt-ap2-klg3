# 7. Concorrência I: Goroutines

Uma das características mais poderosas da linguagem Go é sua capacidade de trabalhar com concorrência de forma simples e eficiente.

Go foi criada pensando em:

- Sistemas escaláveis
- Alto desempenho
- Processamento paralelo
- Servidores web
- APIs
- Microsserviços
- Cloud Computing

---

# 🧠 O que é Concorrência?

Concorrência é a capacidade de executar múltiplas tarefas ao mesmo tempo.

---

# 📌 Exemplo do mundo real

Imagine um restaurante.

Enquanto:

- um cozinheiro prepara comida,
- outro atende clientes,
- outro organiza pedidos.

Tudo acontece simultaneamente.

---

# 📌 Em programação

Concorrência permite:

- baixar arquivos enquanto processa dados,
- responder múltiplos usuários,
- executar tarefas independentes,
- melhorar desempenho.

---

# 📌 Diferença entre Concorrência e Paralelismo

| Conceito | Explicação |
|---|---|
| Concorrência | Várias tarefas acontecendo de forma organizada |
| Paralelismo | Execução literalmente ao mesmo tempo |

---

# 🔍 Exemplo simples

## Concorrência

Um único núcleo alterna rapidamente entre tarefas.

---

## Paralelismo

Múltiplos núcleos executam tarefas simultaneamente.

---

# 🚀 Goroutines

Go utiliza Goroutines para concorrência.

---

# 🧠 O que é uma Goroutine?

Uma Goroutine é uma função executada concorrentemente.

Ela é extremamente leve comparada a threads tradicionais.

---

# 📌 Vantagens das Goroutines

| Vantagem | Explicação |
|---|---|
| Leves | Consomem pouca memória |
| Rápidas | Criação muito barata |
| Escaláveis | Milhares podem rodar juntas |
| Simples | Sintaxe minimalista |

---

# 📌 Comparação com Threads

| Característica | Thread | Goroutine |
|---|---|---|
| Memória | Alta | Muito baixa |
| Criação | Cara | Barata |
| Gerenciada pelo | Sistema operacional | Runtime Go |
| Escalabilidade | Menor | Muito maior |

---

# 📌 Sintaxe Básica

---

# ✅ Exemplo do arquivo

```go
go minhaFuncao()
```

---

# 🔍 Explicação

| Parte | Função |
|---|---|
| `go` | Cria Goroutine |
| `minhaFuncao()` | Função executada concorrentemente |

---

# 📌 O que acontece?

Sem `go`:

```go
minhaFuncao()
```

A função executa normalmente.

---

# 📌 Com `go`

```go
go minhaFuncao()
```

A função executa concorrentemente.

O programa NÃO espera ela terminar automaticamente.

---

# 🚀 Código Completo do Arquivo

```go
package main

import (
    "fmt"
    "time"
)

func tarefa() {
    fmt.Println("Executando...")
}

func main() {
    go tarefa()

    time.Sleep(time.Second)
}
```

---

# 🔍 Explicação Completa

---

# 📌 Importações

```go
import (
    "fmt"
    "time"
)
```

---

# 🔍 Pacote `fmt`

Usado para imprimir informações no terminal.

---

# 🔍 Pacote `time`

Usado para:

- tempo,
- pausas,
- duração,
- timers.

---

# 📌 Função `tarefa`

```go
func tarefa() {
    fmt.Println("Executando...")
}
```

---

# 🔍 O que ela faz?

Apenas imprime:

```txt
Executando...
```

---

# 📌 Criando Goroutine

```go
go tarefa()
```

---

# 🔍 O que acontece?

O Go cria uma nova Goroutine.

A função começa a executar em paralelo ao restante do programa.

---

# 📌 Problema importante

O `main()` pode terminar antes da Goroutine.

---

# ⚠️ Exemplo sem `Sleep`

```go
func main() {
    go tarefa()
}
```

---

# 🔍 Possível resultado

Nada será exibido.

---

# 📌 Por quê?

O programa termina antes da Goroutine executar.

---

# 🚀 Solução utilizada no exemplo

```go
time.Sleep(time.Second)
```

---

# 🔍 Explicação

Faz o programa esperar:

```txt
1 segundo
```

Assim a Goroutine consegue executar.

---

# 📌 O que é `time.Second`?

Representa:

```txt
1 segundo
```

---

# ✅ Outros exemplos

```go
time.Millisecond
time.Minute
time.Hour
```

---

# 🚀 Fluxo do Programa

---

# 🔍 Fluxo visual

```txt
main inicia

↓

cria goroutine

↓

main continua

↓

goroutine executa

↓

main espera 1 segundo

↓

programa finaliza
```

---

# 🚀 Executando múltiplas Goroutines

Podemos criar várias.

---

# ✅ Exemplo

```go
package main

import (
    "fmt"
    "time"
)

func tarefa(nome string) {

    for i := 1; i <= 3; i++ {
        fmt.Println(nome, i)

        time.Sleep(time.Millisecond * 500)
    }
}

func main() {

    go tarefa("Goroutine 1")

    go tarefa("Goroutine 2")

    time.Sleep(time.Second * 3)
}
```

---

# 🔍 Possível saída

```txt
Goroutine 1 1
Goroutine 2 1
Goroutine 1 2
Goroutine 2 2
```

---

# 📌 O que aconteceu?

As duas funções executaram concorrentemente.

---

# 📌 Ordem NÃO é garantida

A ordem pode mudar.

---

# ⚠️ Importante

Concorrência NÃO garante ordem de execução.

---

# 🧠 Scheduler do Go

Go possui um scheduler interno.

---

# 📌 O que ele faz?

O scheduler decide:

- qual Goroutine executa,
- quando executa,
- por quanto tempo executa.

---

# 📌 O desenvolvedor NÃO controla diretamente

O runtime Go gerencia automaticamente.

---

# 🚀 Goroutines são extremamente leves

---

# 📌 Thread tradicional

Consome geralmente:

```txt
1 MB ou mais
```

---

# 📌 Goroutine

Começa com aproximadamente:

```txt
2 KB
```

---

# 📌 Resultado

Go consegue executar:

- milhares
- dezenas de milhares
- milhões

de Goroutines.

---

# 🚀 Exemplo criando várias Goroutines

```go
package main

import "fmt"

func imprimir(numero int) {
    fmt.Println("Número:", numero)
}

func main() {

    for i := 0; i < 1000; i++ {
        go imprimir(i)
    }
}
```

---

# ⚠️ Problema desse código

O programa provavelmente finalizará antes.

---

# 🚀 Solução simples

```go
time.Sleep(time.Second)
```

---

# ⚠️ Mas NÃO é ideal

`Sleep()` é apenas solução temporária.

---

# 📌 Em aplicações reais usamos:

- WaitGroup
- Channels
- Context
- Sync package

---

# 🚀 Funções anônimas com Goroutines

---

# ✅ Exemplo

```go
go func() {
    fmt.Println("Executando função anônima")
}()
```

---

# 🔍 Explicação

Criamos:

- função sem nome
- executada concorrentemente

---

# 📌 Muito usado em APIs e servidores

---

# 🚀 Passando parâmetros

---

# ✅ Exemplo

```go
go func(nome string) {
    fmt.Println(nome)
}("Kassia")
```

---

# 🔍 Saída

```txt
Kassia
```

---

# 🚀 Concorrência em aplicações reais

Goroutines são utilizadas em:

- APIs REST
- Servidores web
- Downloads
- Processamento paralelo
- Filas
- Workers
- Bancos de dados
- Microserviços

---

# 📌 Exemplo real

Servidor web atendendo múltiplos usuários simultaneamente.

Cada requisição pode rodar em uma Goroutine.

---

# 🚀 Problemas comuns

Concorrência pode gerar problemas.

---

# ⚠️ Race Condition

Acontece quando múltiplas Goroutines alteram os mesmos dados.

---

# ❌ Exemplo perigoso

```go
var contador int

func incrementar() {
    contador++
}
```

---

# 🔥 Problema

Duas Goroutines podem alterar ao mesmo tempo.

---

# 📌 Resultado

Valores incorretos.

---

# 🚀 Deadlock

Acontece quando Goroutines ficam esperando indefinidamente.

---

# 📌 Muito comum com Channels

---

# 🚀 Starvation

Uma Goroutine nunca recebe tempo suficiente de execução.

---

# 🚀 Scheduler cooperativo

Go pausa Goroutines automaticamente para equilibrar execução.

---

# 🚀 Runtime Go

O runtime gerencia:

- memória,
- scheduler,
- garbage collector,
- Goroutines.

---

# 📌 Go facilita concorrência

Outras linguagens geralmente exigem:

- Threads manuais
- Locks complexos
- APIs difíceis

Go simplifica isso drasticamente.

---

# 🚀 Exemplo Completo Profissional

```go
package main

import (
    "fmt"
    "time"
)

func tarefa(nome string) {

    for i := 1; i <= 5; i++ {

        fmt.Println(nome, "executando:", i)

        time.Sleep(time.Millisecond * 500)
    }
}

func main() {

    fmt.Println("Iniciando programa")

    go tarefa("Goroutine 1")

    go tarefa("Goroutine 2")

    fmt.Println("Goroutines iniciadas")

    time.Sleep(time.Second * 4)

    fmt.Println("Programa finalizado")
}
```

---

# 🔍 Possível saída

```txt
Iniciando programa

Goroutines iniciadas

Goroutine 1 executando: 1
Goroutine 2 executando: 1

Goroutine 1 executando: 2
Goroutine 2 executando: 2

Programa finalizado
```

---

# 📌 O que observar?

As funções executam:

- juntas,
- alternadamente,
- de forma concorrente.

---

# 🚀 Quando usar Goroutines?

---

# ✅ Use quando houver:

- tarefas independentes,
- operações demoradas,
- múltiplas requisições,
- processamento paralelo,
- I/O,
- APIs.

---

# ❌ Evite quando:

- tarefa é simples,
- não há ganho de performance,
- código fica mais complexo sem necessidade.

---

# 📌 Concorrência ≠ Velocidade automática

Criar Goroutines sem necessidade pode:

- piorar performance,
- aumentar complexidade,
- dificultar manutenção.

---

# 📌 Filosofia do Go

Go segue a filosofia:

> "Não compartilhe memória para se comunicar.  
> Comunique-se compartilhando mensagens."

---

# 🚀 Próximos conceitos importantes

Após Goroutines normalmente estudamos:

- Channels
- WaitGroup
- Mutex
- Context
- Worker Pools

---

# ✅ Boas Práticas

| Prática | Motivo |
|---|---|
| Use Goroutines para tarefas independentes | Melhor desempenho |
| Evite Goroutines desnecessárias | Menos complexidade |
| Use sincronização adequada | Evita bugs |
| Evite `Sleep()` em produção | Não é confiável |
| Prefira Channels e WaitGroups | Código seguro |

---

# ⚠️ IMPORTANTE

> O programa pode finalizar antes da Goroutine terminar.

Esse é um dos erros mais comuns de iniciantes em Go.

---

# 💡 Dica 

> Goroutines são uma das funcionalidades mais poderosas da linguagem Go.
>
> Elas tornam a concorrência:
>
> - simples,
> - leve,
> - eficiente,
> - escalável.
>
> Dominar Goroutines é essencial para desenvolver:
>
> - APIs performáticas
> - Sistemas concorrentes
> - Microsserviços
> - Aplicações modernas em Go.

---
