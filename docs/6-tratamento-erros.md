# 6. Tratamento de Erros

## Erros acontecem em qualquer sistema

Exemplos:

- Divisão por zero
- Arquivo inexistente
- Erro de conexão
- Falha no banco de dados
- API indisponível
- Entrada inválida do usuário

Toda linguagem precisa possuir uma forma de lidar com erros.

---

## Como Go trata erros?

Diferente de linguagens como:

- Java
- C#
- Python
- JavaScript

Go NÃO utiliza:

```txt
try
catch
finally
```

---

## Go utiliza retorno de erros

Em Go:

> Funções retornam erros como valores.

---

## Filosofia do Go

Os criadores da linguagem acreditam que:

- Erros fazem parte do fluxo normal
- O código deve ser explícito
- Tratamento deve ser visível
- Evitar exceções ocultas melhora manutenção

---

## Comparação com outras linguagens

### JavaScript

```javascript
try {
   codigo()
} catch(err) {
   console.log(err)
}
```

### Go

```go
resultado, err := funcao()

if err != nil {
    fmt.Println(err)
}
```

---

## Interface `error`

Go possui uma interface chamada `error`.

---

## Definição simplificada

```go
type error interface {
    Error() string
}
```

---

## O que isso significa?

Qualquer valor que implemente:

```go
Error() string
```

pode ser tratado como erro.

---

## Estrutura do retorno

Funções normalmente retornam:

```go
(valor, erro)
```

---

## Exemplo do arquivo

```go
func dividir(a, b int) (int, error) {
    if b == 0 {
        return 0, errors.New("divisão por zero")
    }

    return a / b, nil
}
```

---

# Explicação Completa

## Assinatura da função

```go
func dividir(a, b int) (int, error)
```

---

## Significado

| Parte | Função |
|---|---|
| `func` | Declara função |
| `dividir` | Nome da função |
| `a, b int` | Parâmetros inteiros |
| `(int, error)` | Dois retornos |

---

## O que a função retorna?

| Retorno | Significado |
|---|---|
| `int` | Resultado da divisão |
| `error` | Possível erro |

---

## Verificando divisão por zero

```go
if b == 0 {
```

---

## Explicação

Antes de dividir:

- Verificamos se `b` é zero
- Evitamos erro matemático

---

## Criando erro

```go
errors.New("divisão por zero")
```

---

## O que isso faz?

Cria um erro com mensagem personalizada.

---

## Retornando erro

```go
return 0, errors.New("divisão por zero")
```

---

## Significado

| Valor | Motivo |
|---|---|
| `0` | Valor padrão |
| `error` | Informação do erro |

---

## Retorno de sucesso

```go
return a / b, nil
```

---

## Explicação

| Valor | Significado |
|---|---|
| `a / b` | Resultado da divisão |
| `nil` | Sem erro |

---

## O que é `nil`?

`nil` representa ausência de valor.

Muito usado com:

- Ponteiros
- Interfaces
- Maps
- Slices
- Errors

---

# Verificando Erros

## Exemplo do arquivo

```go
resultado, err := dividir(10, 0)

if err != nil {
    fmt.Println(err)
}
```

---

# Explicação Completa

## Chamando função

```go
resultado, err := dividir(10, 0)
```

---

## O que acontece?

A função tenta:

```txt
10 / 0
```

---

## Resultado retornado

```go
0, error
```

---

## Variável `err`

Recebe o erro retornado pela função.

---

## Verificação padrão do Go

```go
if err != nil
```

---

## Significado

| Situação | Resultado |
|---|---|
| `err == nil` | Sem erro |
| `err != nil` | Existe erro |

---

## Imprimindo erro

```go
fmt.Println(err)
```

---

## Saída

```txt
divisão por zero
```

---

## IMPORTANTE

Essa é uma das estruturas MAIS utilizadas em Go.

Você verá isso constantemente:

```go
if err != nil {
    return err
}
```

---

# Fluxo Completo do Programa

## Fluxo visual

```txt
Usuário chama dividir()

↓

Go verifica se b == 0

↓

Se verdadeiro:
    retorna erro

↓

Se falso:
    retorna resultado
```

---

## Exemplo Completo

```go
package main

import (
    "fmt"
    "errors"
)

func dividir(a, b int) (int, error) {

    if b == 0 {
        return 0, errors.New("divisão por zero")
    }

    return a / b, nil
}

func main() {

    resultado, err := dividir(10, 0)

    if err != nil {
        fmt.Println("Erro:", err)
        return
    }

    fmt.Println("Resultado:", resultado)
}
```

---

## Saída

```txt
Erro: divisão por zero
```

---

## Exemplo sem erro

```go
resultado, err := dividir(10, 2)
```

---

## Resultado

```txt
Resultado: 5
```

---

## Por que Go usa esse modelo?

### Vantagens

| Vantagem | Explicação |
|---|---|
| Código explícito | Erros ficam visíveis |
| Mais previsível | Sem exceções escondidas |
| Fácil manutenção | Fluxo claro |
| Melhor performance | Menos custo que exceptions |

---

## Ignorando retornos

Às vezes queremos ignorar um retorno.

Usamos `_`.

---

## Exemplo

```go
resultado, _ := dividir(10, 2)
```

---

## Atenção

Ignorar erros NÃO é recomendado.

---

## ❌ Problema

Você pode esconder falhas importantes.

---

# Criando Erros Personalizados

## Exemplo

```go
func sacar(saldo, valor float64) error {

    if valor > saldo {
        return errors.New("saldo insuficiente")
    }

    return nil
}
```

---

## Uso

```go
err := sacar(100, 200)

if err != nil {
    fmt.Println(err)
}
```

---

## Saída

```txt
saldo insuficiente
```

---

## Pacote `errors`

O pacote `errors` fornece ferramentas para criação de erros.

---

## Importação

```go
import "errors"
```

---

## Função `errors.New()`

Cria erro simples.

---

## Exemplo

```go
errors.New("erro personalizado")
```

---

## Pacote `fmt` com erros

Também podemos criar erros formatados.

---

## Exemplo

```go
fmt.Errorf("idade inválida: %d", idade)
```

---

## Saída

```txt
idade inválida: -10
```

---

# Tratando erros de arquivos

## Exemplo

```go
arquivo, err := os.Open("dados.txt")

if err != nil {
    fmt.Println("Erro ao abrir arquivo")
    return
}
```

---

## Possíveis erros

- Arquivo não existe
- Permissão negada
- Caminho inválido

---

# Tratando entrada do usuário

## Exemplo

```go
var idade int

_, err := fmt.Scan(&idade)

if err != nil {
    fmt.Println("Entrada inválida")
}
```

---

# Erros em APIs

Erros são MUITO utilizados em:

- APIs REST
- Bancos de dados
- Microserviços
- Sistemas distribuídos

---

## Exemplo HTTP

```go
resp, err := http.Get("https://google.com")

if err != nil {
    fmt.Println(err)
    return
}
```

---

# Padrão mais comum do Go

## Estrutura padrão

```go
if err != nil {
    return err
}
```

---

## Significado

Se existir erro:

- interrompe função
- retorna imediatamente

---

## Isso reduz complexidade

Evita:

- ifs gigantes
- try/catch aninhados
- código difícil

---

# Múltiplos retornos

Go permite múltiplos retornos.

---

## Exemplo

```go
func calcular() (int, string, error) {
    return 10, "ok", nil
}
```

---

## Recebendo valores

```go
numero, status, err := calcular()
```

---

# Panic

Go possui `panic`.

---

## MAS:

Panic NÃO é usado para erros comuns.

---

## Panic serve para:

- Erros críticos
- Situações irreversíveis
- Falhas graves

---

## Exemplo ruim

```go
panic("erro simples")
```

---

## Use panic apenas em casos extremos

---

# Recover

Go possui `recover()` para capturar panic.

---

## Pouco utilizado no dia a dia

Muito usado em:

- Frameworks
- Middleware
- Bibliotecas internas

---

## Exemplo simples com panic

```go
func main() {
    panic("algo deu errado")
}
```

---

## Saída

```txt
panic: algo deu errado
```

---

# Exemplo Completo Profissional

```go
package main

import (
    "errors"
    "fmt"
)

func dividir(a, b int) (int, error) {

    if b == 0 {
        return 0, errors.New("não é possível dividir por zero")
    }

    return a / b, nil
}

func main() {

    resultado, err := dividir(20, 0)

    if err != nil {
        fmt.Println("Erro encontrado:")
        fmt.Println(err)
        return
    }

    fmt.Println("Resultado:", resultado)
}
```

---

## Saída

```txt
Erro encontrado:
não é possível dividir por zero
```

---

# Fluxo Real em Aplicações

## Fluxo em sistemas reais

```txt
Usuário envia dado

↓

Sistema processa

↓

Função pode retornar erro

↓

Erro é tratado

↓

Sistema responde adequadamente
```

---

# Boas Práticas

| Prática | Motivo |
|---|---|
| Sempre trate erros | Segurança |
| Nunca ignore `err` | Evita bugs |
| Use mensagens claras | Melhor manutenção |
| Retorne cedo com erro | Código limpo |
| Evite panic desnecessário | Melhor estabilidade |

---

# Más práticas

## ❌ Ignorar erros

```go
resultado, _ := dividir(10, 0)
```

---

## ❌ Panic para erros simples

```go
panic("arquivo não encontrado")
```

---

## ❌ Mensagens genéricas

```go
errors.New("erro")
```

---

## Prefira

```go
errors.New("usuário não encontrado")
```

---

!!! tip "Boa prática"

   > O tratamento de erros é uma das características mais importantes da linguagem Go.
>
> Em Go:
>
> - Erros fazem parte do fluxo normal
> - Tudo é explícito
> - O código fica mais previsível
> - Sistemas ficam mais estáveis
>
> Dominar tratamento de erros é essencial para desenvolver aplicações profissionais em Go.
