# 9. Gerenciamento de Pacotes

Em Go, o gerenciamento de dependências é feito através do sistema de módulos chamado **Go Modules**.

Ele permite:

- organizar projetos;
- instalar bibliotecas externas;
- controlar versões;
- compartilhar código;
- garantir reprodutibilidade do projeto.

O Go Modules tornou o gerenciamento de pacotes muito mais simples e moderno.

---

# O que é um módulo?

Um módulo é um projeto Go.

Ele contém:

- código fonte;
- dependências;
- versão do Go;
- informações do projeto.

Todo módulo possui um arquivo chamado:

```txt
go.mod
```

Esse arquivo é o coração do gerenciamento de dependências em Go.

---

# Inicializando um Projeto Go

Para iniciar um projeto com Go Modules usamos:

```bash
go mod init meu-projeto
```

---

## Explicação do comando

| Parte | Função |
|---|---|
| `go` | Executa ferramenta Go |
| `mod` | Trabalha com módulos |
| `init` | Inicializa um novo módulo |
| `meu-projeto` | Nome do módulo |

---

# O que acontece ao executar?

O Go cria automaticamente:

```txt
go.mod
```

---

## Estrutura inicial

```txt
meu-projeto/
├── go.mod
└── main.go
```

---

# Exemplo do arquivo `go.mod`

```txt
module meu-projeto

go 1.24
```

---

# Explicação do `go.mod`

| Linha | Significado |
|---|---|
| `module meu-projeto` | Nome do módulo |
| `go 1.24` | Versão do Go utilizada |

---

# Importância do `go.mod`

O `go.mod` controla:

- dependências;
- versões;
- compatibilidade;
- resolução automática de pacotes.

Sem ele, o Go não consegue gerenciar corretamente bibliotecas externas.

---

# Instalando Dependências

Em Go, bibliotecas externas podem ser instaladas usando:

```bash
go get github.com/gin-gonic/gin
```

---

# O que é essa dependência?

A biblioteca:

```txt
github.com/gin-gonic/gin
```

é um framework web muito popular em Go.

Muito utilizado para:

- APIs REST;
- servidores web;
- microsserviços.

---

# Explicação do comando

| Parte | Função |
|---|---|
| `go get` | Baixa dependências |
| `github.com/gin-gonic/gin` | Biblioteca instalada |

---

# O que acontece após instalar?

O Go:

- baixa a dependência;
- adiciona no `go.mod`;
- gera o arquivo `go.sum`.

---

# Arquivo `go.sum`

O `go.sum` armazena verificações de segurança das dependências.

Ele garante:

- integridade;
- segurança;
- consistência das bibliotecas.

---

# Estrutura após instalar dependência

```txt
meu-projeto/
├── go.mod
├── go.sum
└── main.go
```

---

# Importando Bibliotecas

Após instalar, podemos importar normalmente.

---

## Exemplo

```go
package main

import "github.com/gin-gonic/gin"

func main() {
    r := gin.Default()

    r.GET("/", func(c *gin.Context) {
        c.JSON(200, gin.H{
            "mensagem": "Olá Go",
        })
    })

    r.Run()
}
```

---

# O que esse código faz?

Cria uma API simples utilizando o framework Gin.

Ao acessar:

```txt
http://localhost:8080
```

o servidor retorna:

```json
{
  "mensagem": "Olá Go"
}
```

---

# Atualizando Dependências

Com o tempo, dependências podem ficar:

- desatualizadas;
- sem uso;
- inconsistentes.

Para organizar isso usamos:

```bash
go mod tidy
```

---

# O que o `go mod tidy` faz?

Esse comando:

- remove dependências não utilizadas;
- adiciona dependências faltantes;
- organiza o `go.mod`;
- atualiza o `go.sum`.

---

# Boa prática importante

Execute frequentemente:

```bash
go mod tidy
```

principalmente antes de:

- commits;
- pull requests;
- deploys.

---

# Baixando Dependências do Projeto

Ao clonar um projeto Go, geralmente executamos:

```bash
go mod download
```

---

# O que esse comando faz?

Baixa todas as dependências listadas no:

```txt
go.mod
```

---

# Verificando Dependências

Também podemos listar dependências instaladas:

```bash
go list -m all
```

---

# Resultado esperado

```txt
meu-projeto
github.com/gin-gonic/gin
github.com/go-playground/validator
...
```

---

# Versionamento de Dependências

Go Modules suporta versionamento.

Exemplo:

```bash
go get github.com/gin-gonic/gin@v1.10.0
```

---

# Explicação

| Parte | Função |
|---|---|
| `@v1.10.0` | Define versão específica |

---

# Vantagens do versionamento

Permite:

- estabilidade;
- controle de versões;
- evitar incompatibilidades;
- reproduzir builds.

---

# Atualizando Bibliotecas

Para atualizar dependências:

```bash
go get -u
```

---

# O que significa `-u`?

A flag:

```txt
-u
```

significa:

```txt
update
```

---

# Dependências Diretas e Indiretas

No `go.mod` podem existir:

- dependências diretas;
- dependências indiretas.

---

## Exemplo

```txt
require (
    github.com/gin-gonic/gin v1.10.0
)
```

---

# Dependências indiretas

Algumas bibliotecas dependem de outras bibliotecas.

O Go instala automaticamente essas dependências secundárias.

---

# Cache de Dependências

O Go possui cache automático.

Isso melhora:

- velocidade;
- performance;
- reutilização de pacotes.

---

# Onde as dependências ficam?

Normalmente em:

```txt
$GOPATH/pkg/mod
```

---

# Gerenciamento moderno em Go

Antes do Go Modules, era necessário usar ferramentas externas.

Hoje o Go já possui gerenciamento nativo.

Isso trouxe:

- simplicidade;
- padronização;
- melhor manutenção.

---

# Fluxo comum de desenvolvimento

## 1. Criar projeto

```bash
go mod init meu-projeto
```

---

## 2. Instalar bibliotecas

```bash
go get github.com/gin-gonic/gin
```

---

## 3. Desenvolver aplicação

```bash
go run main.go
```

---

## 4. Organizar dependências

```bash
go mod tidy
```

---

# Estrutura comum de projeto Go

```txt
meu-projeto/
├── go.mod
├── go.sum
├── main.go
├── handlers/
├── services/
├── repositories/
└── models/
```

---

# Boas Práticas

| Prática | Motivo |
|---|---|
| Utilize Go Modules | Padronização |
| Execute `go mod tidy` frequentemente | Organização |
| Utilize versões específicas | Estabilidade |
| Evite dependências desnecessárias | Menos complexidade |
| Mantenha `go.mod` limpo | Melhor manutenção |

---

# Problemas comuns

## Dependência não encontrada

Erro comum:

```txt
cannot find module
```

### Solução

Executar:

```bash
go mod tidy
```

ou:

```bash
go get nome-da-biblioteca
```

---

## Conflito de versões

Pode ocorrer quando bibliotecas usam versões incompatíveis.

---

## Solução

Atualizar dependências:

```bash
go get -u
```

---

# IMPORTANTE

Os arquivos:

```txt
go.mod
go.sum
```

devem ser enviados para o Git.

Eles garantem que outras pessoas consigam instalar exatamente as mesmas dependências.

---

# Conclusão

O sistema de gerenciamento de pacotes do Go é simples, moderno e eficiente.

Com Go Modules conseguimos:

- instalar bibliotecas;
- controlar versões;
- organizar projetos;
- garantir compatibilidade;
- facilitar deploys.

Isso torna o desenvolvimento em Go muito mais profissional e escalável.

---

!!! note "Boa prática"

    Sempre mantenha o `go.mod` organizado.
    
    Utilize:
    
    ```bash
    go mod tidy
    ```
    
    regularmente para remover dependências desnecessárias e manter o projeto limpo.
