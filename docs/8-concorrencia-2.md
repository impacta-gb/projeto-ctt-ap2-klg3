# 8. Concorrência II: Channels em Go

## O que são Channels?

Os **Channels** em Go são mecanismos de comunicação entre **goroutines**. Eles permitem que diferentes partes do programa troquem informações de forma segura.

A ideia principal é:

> "Não compartilhe memória para se comunicar. Comunique-se para compartilhar memória."

Ou seja, ao invés de várias goroutines acessarem a mesma variável diretamente (o que pode causar problemas de concorrência), elas trocam dados através dos channels.

---

# O que é uma Goroutine?

Antes de entender channels, é importante lembrar o que são goroutines.

Uma **goroutine** é uma função executada de forma concorrente.

Exemplo:

```go
package main

import "fmt"

func mensagem() {
    fmt.Println("Executando goroutine")
}

func main() {
    go mensagem()

    fmt.Println("Executando main")
}
```

## Explicação

* A palavra-chave `go` cria uma goroutine.
* A função `mensagem()` executa separadamente da `main()`.
* Ambas podem rodar ao mesmo tempo.

Problema:

A `main()` pode terminar antes da goroutine executar.

É exatamente aqui que os **channels** ajudam.

---

# O que é um Channel?

Um channel é um canal de comunicação.

Ele serve para:

* enviar dados;
* receber dados;
* sincronizar goroutines;
* evitar conflitos de concorrência.

---

# Criando um Channel

```go
canal := make(chan string)
```

## Explicação

* `make()` cria o channel.
* `chan string` significa que ele transporta valores do tipo `string`.

Também pode existir:

```go
chan int
chan bool
chan float64
```

Exemplos:

```go
idade := make(chan int)
ativo := make(chan bool)
```

---

# Enviando Dados para o Channel

```go
canal <- "Olá"
```

## Explicação

O operador `<-` serve para enviar valores.

Nesse caso:

* o valor `"Olá"` está sendo enviado para o channel.

---

# Recebendo Dados do Channel

```go
mensagem := <-canal
```

## Explicação

Aqui o programa está:

* esperando um valor chegar;
* recebendo o valor;
* armazenando na variável `mensagem`.

---

# Exemplo Completo

```go
package main

import "fmt"

func main() {
    canal := make(chan string)

    go func() {
        canal <- "Olá Go"
    }()

    msg := <-canal

    fmt.Println(msg)
}
```

---

# Explicação Detalhada do Exemplo

## 1. Criando o Channel

```go
canal := make(chan string)
```

Foi criado um channel que transporta textos (`string`).

---

## 2. Criando uma Goroutine

```go
go func() {
    canal <- "Olá Go"
}()
```

Aqui:

* uma função anônima é executada em paralelo;
* ela envia a mensagem para o channel.

---

## 3. Recebendo o Valor

```go
msg := <-canal
```

A `main()` fica esperando até receber um valor.

Quando recebe:

```go
"Olá Go"
```

ela continua a execução.

---

## 4. Exibindo o Resultado

```go
fmt.Println(msg)
```

Saída:

```go
Olá Go
```

---

# Comunicação Bloqueante

Channels são bloqueantes por padrão.

Isso significa:

* ao enviar dados, a goroutine espera alguém receber;
* ao receber dados, a goroutine espera alguém enviar.

Exemplo:

```go
package main

import "fmt"

func main() {
    canal := make(chan string)

    canal <- "Olá"

    fmt.Println(<-canal)
}
```

## O que acontece?

Esse código gera erro:

```go
fatal error: all goroutines are asleep - deadlock!
```

---

# O que é Deadlock?

Deadlock acontece quando:

* uma goroutine fica esperando outra;
* mas nenhuma consegue continuar.

No exemplo anterior:

* o programa tentou enviar dados;
* mas ninguém estava recebendo.

Então o programa trava.

---

# Corrigindo o Deadlock

```go
package main

import "fmt"

func main() {
    canal := make(chan string)

    go func() {
        canal <- "Olá"
    }()

    fmt.Println(<-canal)
}
```

Agora funciona porque:

* uma goroutine envia;
* a main recebe.

---

# Channels com Inteiros

```go
package main

import "fmt"

func main() {
    numeros := make(chan int)

    go func() {
        numeros <- 10
    }()

    valor := <-numeros

    fmt.Println(valor)
}
```

Saída:

```go
10
```

---

# Channels com Funções

```go
package main

import "fmt"

func somar(a int, b int, resultado chan int) {
    resultado <- a + b
}

func main() {
    canal := make(chan int)

    go somar(10, 20, canal)

    resultado := <-canal

    fmt.Println(resultado)
}
```

## Explicação

A função:

```go
somar()
```

recebe:

* dois números;
* um channel.

Depois envia o resultado:

```go
resultado <- a + b
```

---

# Channels Bidirecionais

Um channel normal consegue:

* enviar;
* receber.

Exemplo:

```go
chan int
```

---

# Channels Somente Envio

```go
chan<- int
```

Exemplo:

```go
func enviar(canal chan<- int) {
    canal <- 100
}
```

Essa função só envia dados.

Ela não consegue receber.

---

# Channels Somente Recebimento

```go
<-chan int
```

Exemplo:

```go
func receber(canal <-chan int) {
    valor := <-canal

    fmt.Println(valor)
}
```

Essa função apenas recebe dados.

---

# Buffered Channels

Channels normais armazenam apenas quando existe alguém recebendo.

Já os buffered channels possuem um buffer.

---

# Criando Buffered Channel

```go
canal := make(chan int, 3)
```

O número `3` significa:

* o channel pode armazenar até 3 valores.

---

# Exemplo Buffered Channel

```go
package main

import "fmt"

func main() {
    canal := make(chan int, 3)

    canal <- 1
    canal <- 2
    canal <- 3

    fmt.Println(<-canal)
    fmt.Println(<-canal)
    fmt.Println(<-canal)
}
```

Saída:

```go
1
2
3
```

---

# Vantagem do Buffered Channel

Permite:

* reduzir bloqueios;
* armazenar mensagens temporariamente;
* melhorar performance em alguns cenários.

---

# Fechando Channels

```go
close(canal)
```

## Exemplo

```go
package main

import "fmt"

func main() {
    canal := make(chan int)

    go func() {
        canal <- 10
        close(canal)
    }()

    valor := <-canal

    fmt.Println(valor)
}
```

---

# Por que Fechar um Channel?

Fechar channels informa:

> "Não existirão mais valores enviados"

Muito usado em:

* loops;
* workers;
* pipelines.

---

# Range em Channels

O `range` consegue percorrer valores de um channel.

Exemplo:

```go
package main

import "fmt"

func main() {
    canal := make(chan int)

    go func() {
        for i := 1; i <= 5; i++ {
            canal <- i
        }

        close(canal)
    }()

    for valor := range canal {
        fmt.Println(valor)
    }
}
```

Saída:

```go
1
2
3
4
5
```

---

# Explicação

Enquanto o channel estiver aberto:

```go
for valor := range canal
```

continua recebendo valores.

Quando:

```go
close(canal)
```

é executado, o loop termina automaticamente.

---

# Select

O `select` permite esperar múltiplos channels.

É parecido com um `switch`, mas para concorrência.

---

# Exemplo com Select

```go
package main

import "fmt"

func main() {
    canal1 := make(chan string)
    canal2 := make(chan string)

    go func() {
        canal1 <- "Mensagem do canal 1"
    }()

    go func() {
        canal2 <- "Mensagem do canal 2"
    }()

    select {
    case msg1 := <-canal1:
        fmt.Println(msg1)

    case msg2 := <-canal2:
        fmt.Println(msg2)
    }
}
```

---

# Explicação do Select

O `select`:

* espera múltiplas operações;
* executa a primeira disponível.

Muito usado em:

* sistemas concorrentes;
* APIs;
* servidores;
* processamento paralelo.

---

# Default no Select

```go
select {
case msg := <-canal:
    fmt.Println(msg)

default:
    fmt.Println("Nenhuma mensagem")
}
```

## Explicação

Se nenhum channel estiver pronto:

* o `default` executa.

---

# Concorrência vs Paralelismo

## Concorrência

É lidar com várias tarefas ao mesmo tempo.

Exemplo:

* alternar entre várias tarefas rapidamente.

---

## Paralelismo

É executar várias tarefas literalmente ao mesmo tempo.

Exemplo:

* múltiplos núcleos do processador trabalhando simultaneamente.

---

# Vantagens dos Channels

## Segurança

Evita problemas de acesso simultâneo à memória.

---

## Simplicidade

Facilita comunicação entre goroutines.

---

## Organização

Melhora arquitetura concorrente.

---

## Performance

Permite processamento concorrente eficiente.

---

# Desvantagens dos Channels

## Deadlocks

Se usados incorretamente podem travar o programa.

---

## Complexidade

Sistemas concorrentes podem ficar difíceis de entender.

---

## Debug Difícil

Bugs concorrentes costumam ser difíceis de identificar.

---

# Casos Reais de Uso

Channels são muito usados em:

* APIs;
* microsserviços;
* sistemas distribuídos;
* filas;
* processamento paralelo;
* workers;
* pipelines;
* comunicação entre serviços.

---

# Exemplo Real: Worker Simples

```go
package main

import "fmt"

func worker(id int, tarefas <-chan int) {
    for tarefa := range tarefas {
        fmt.Printf("Worker %d processando tarefa %d\n", id, tarefa)
    }
}

func main() {
    tarefas := make(chan int)

    go worker(1, tarefas)
    go worker(2, tarefas)

    for i := 1; i <= 5; i++ {
        tarefas <- i
    }

    close(tarefas)
}
```

---

# Explicação do Worker

Os workers:

* ficam esperando tarefas;
* recebem dados do channel;
* processam simultaneamente.

Isso é muito usado em:

* filas;
* sistemas de processamento;
* aplicações escaláveis.

---

# Resumo Geral

## Channels

Servem para comunicação entre goroutines.

---

## Goroutines

Executam funções concorrentemente.

---

## Operador `<-`

Usado para:

* enviar;
* receber.

---

## Buffered Channels

Possuem armazenamento interno.

---

## Select

Espera múltiplos channels.

---

## Close

Fecha o channel.

---

# Conclusão

Os channels são uma das funcionalidades mais importantes da linguagem Go.

Eles tornam a concorrência:

* mais segura;
* mais organizada;
* mais eficiente.

A combinação entre:

* goroutines;
* channels;
* select;
* buffered channels;

permite construir aplicações extremamente performáticas e escaláveis.

Por isso Go é muito utilizado em:

* back-end;
* cloud computing;
* servidores;
* microsserviços;
* sistemas distribuídos;
* aplicações de alta performance.
