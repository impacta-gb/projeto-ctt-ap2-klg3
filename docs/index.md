# 🐹 Documentação da Linguagem Go

Bem-vindo à documentação completa da linguagem **Go** (Golang).

---

## Sobre Go

Go é uma linguagem de programação criada pelo **Google** em 2007 e lançada publicamente em **2009**. Foi projetada por Robert Griesemer, Rob Pike e Ken Thompson para resolver problemas comuns em grandes sistemas de software, como:

- Compilação lenta
- Dependências complicadas
- Concorrência difícil
- Baixa produtividade

---

## 🚀 Características principais

| Característica | Descrição |
|----------------|-----------|
| ⚡ **Rápida** | Compila para código nativo (binário) |
| 🧼 **Limpa** | Sintaxe minimalista e fácil de aprender |
| 🔒 **Segura** | Tipagem estática com garbage collector |
| 🔄 **Concorrente** | Goroutines e channels nativos |
| 📦 **Moderna** | Gerenciamento de dependências via Go Modules |
| 🧪 **Testável** | Framework de testes embutido |
| 📚 **Documentação** | Go Doc integrado |

---

## 📊 Comparação com outras linguagens

| Característica | Go | Python | Java | C++ |
|----------------|----|--------|------|-----|
| Compilada | ✅ | ❌ | ✅ | ✅ |
| Tipagem estática | ✅ | ❌ | ✅ | ✅ |
| Garbage Collector | ✅ | ✅ | ✅ | ❌ |
| Concorrência nativa | ✅ | ❌ | ✅ | ⚠️ |
| Velocidade de compilação | ⚡⚡⚡ | N/A | ⚡ | ⚡⚡⚡⚡ |
| Curva de aprendizado | Baixa | Baixa | Média | Alta |

---

## 🎯 Para quem é Go?

| Perfil | Motivo |
|--------|--------|
| **Iniciantes** | Sintaxe simples e consistente |
| **Backend developers** | Performance e concorrência |
| **DevOps/SRE** | CLI tools eficientes e portáteis |
| **Microservices** | Baixo consumo de memória |
| **Sistemas distribuídos** | Channels e goroutines |

---

## 🏢 Quem usa Go?

| Empresa | Como usa |
|---------|----------|
| **Google** | Infrastructure, Kubernetes, Docker |
| **Uber** | Geolocalização e microserviços |
| **Netflix** | Otimização de streaming |
| **Twitch** | Sistemas de alta performance |
| **Mercado Livre** | Backend escalável |
| **CloudFlare** | DNS e proxy reverso |

---

## 🛠️ Ferramentas do ecossistema

| Ferramenta | Descrição |
|------------|-----------|
| `go fmt` | Formata código automaticamente |
| `go vet` | Analisa código suspeito |
| `go test` | Executa testes automatizados |
| `go mod` | Gerencia dependências |
| `go build` | Compila binários |
| `go run` | Executa código diretamente |
| `go doc` | Gera documentação |

---

## 💡 Exemplo: Hello World em Go

```go
package main

import "fmt"

func main() {
    fmt.Println("🐹 Olá, mundo com Go!")
}