# 10. Testes Automatizados em Go

Os testes automatizados são fundamentais no desenvolvimento de software moderno.

Eles ajudam a garantir que o sistema funcione corretamente mesmo após alterações no código.

Em Go, o suporte a testes já vem integrado na própria linguagem através do pacote:

```go
testing
```

Isso torna a criação e execução de testes extremamente simples.

---

# O que são Testes Automatizados?

Testes automatizados são códigos criados para validar automaticamente o comportamento de funções e sistemas.

Eles servem para:

- verificar resultados;
- evitar bugs;
- garantir estabilidade;
- facilitar manutenção;
- aumentar confiabilidade.

---

# Vantagens dos Testes

| Vantagem | Explicação |
|---|---|
| Segurança | Evita quebrar funcionalidades |
| Qualidade | Garante comportamento correto |
| Manutenção | Facilita alterações futuras |
| Automação | Executa verificações automaticamente |
| Confiabilidade | Reduz falhas em produção |

---

# Pacote `testing`

Go possui um pacote padrão para testes.

Importação:

```go
import "testing"
```

---

# Como funcionam os testes em Go?

Os testes ficam em arquivos separados.

Esses arquivos devem terminar com:

```txt
_test.go
```

---

# Exemplo

```txt
soma.go
soma_test.go
```

---

# IMPORTANTE

O Go reconhece automaticamente arquivos de teste usando o sufixo:

```txt
_test.go
```

---

# Estrutura Básica de um Teste

## Exemplo completo

```go
package main

import "testing"

func Soma(a, b int) int {
    return a + b
}

func TestSoma(t *testing.T) {
    resultado := Soma(2, 2)

    if resultado != 4 {
        t.Errorf("Esperado 4")
    }
}
```

---

# Explicação do Código

## Função `Soma`

```go
func Soma(a, b int) int {
    return a + b
}
```

Essa função:

- recebe dois números;
- retorna a soma.

---

## Função de Teste

```go
func TestSoma(t *testing.T)
```

### Regras importantes

| Regra | Explicação |
|---|---|
| Deve começar com `Test` | O Go reconhece como teste |
| Recebe `*testing.T` | Controla falhas e mensagens |
| Nome descritivo | Facilita organização |

---

# O que é `*testing.T`?

O parâmetro:

```go
t *testing.T
```

é utilizado para:

- reportar erros;
- falhas;
- mensagens de teste.

---

# Executando a função

```go
resultado := Soma(2, 2)
```

Aqui o teste executa a função real.

---

# Verificando o resultado

```go
if resultado != 4
```

O teste compara:

- resultado esperado;
- resultado obtido.

---

# Exibindo erro

```go
t.Errorf("Esperado 4")
```

Se o valor estiver incorreto:

- o teste falha;
- a mensagem é exibida.

---

# Executando Testes

Para executar todos os testes do projeto:

```bash
go test
```

---

# O que o comando faz?

O Go:

- procura arquivos `_test.go`;
- executa funções `Test`;
- mostra resultados.

---

# Resultado esperado

## Sucesso

```txt
PASS
ok      projeto 0.001s
```

---

## Falha

```txt
--- FAIL: TestSoma
Esperado 4
FAIL
```

---

# Cobertura de Testes

Cobertura mede quanto do código foi testado.

---

## Executando cobertura

```bash
go test -cover
```

---

# Exemplo de saída

```txt
PASS
coverage: 85.0% of statements
```

---

# O que significa?

Significa que:

```txt
85%
```

do código foi executado durante os testes.

---

# Por que cobertura é importante?

Ajuda a identificar:

- partes não testadas;
- funções esquecidas;
- riscos de bugs.

---

# Cobertura NÃO garante ausência de bugs

Mesmo com:

```txt
100%
```

de cobertura, ainda podem existir problemas lógicos.

---

# Testando Múltiplos Cenários

É importante testar diferentes casos.

---

## Exemplo

```go
func TestSoma(t *testing.T) {

    resultado := Soma(10, 5)

    if resultado != 15 {
        t.Errorf("Esperado 15")
    }

}
```

---

# Casos comuns de teste

Devemos validar:

- valores positivos;
- negativos;
- zero;
- limites;
- entradas inválidas.

---

# Testes com Tabela (Table Tests)

Muito comum em Go.

Permite organizar múltiplos testes.

---

## Exemplo

```go
package main

import "testing"

func Soma(a, b int) int {
    return a + b
}

func TestSoma(t *testing.T) {

    testes := []struct {
        a        int
        b        int
        esperado int
    }{
        {2, 2, 4},
        {10, 5, 15},
        {0, 0, 0},
    }

    for _, teste := range testes {

        resultado := Soma(teste.a, teste.b)

        if resultado != teste.esperado {
            t.Errorf(
                "Esperado %d mas recebeu %d",
                teste.esperado,
                resultado,
            )
        }
    }
}
```

---

# Vantagens do Table Test

| Vantagem | Explicação |
|---|---|
| Organização | Menos repetição |
| Escalabilidade | Fácil adicionar casos |
| Clareza | Código mais limpo |

---

# Testes Verbosos

Para exibir mais detalhes:

```bash
go test -v
```

---

# Exemplo de saída

```txt
=== RUN   TestSoma
--- PASS: TestSoma
PASS
```

---

# Executando Teste Específico

```bash
go test -run TestSoma
```

---

# Benchmark em Go

Go também suporta benchmark.

Usado para medir performance.

---

## Exemplo

```go
func BenchmarkSoma(b *testing.B) {

    for i := 0; i < b.N; i++ {
        Soma(10, 20)
    }
}
```

---

# Executando benchmark

```bash
go test -bench=.
```

---

# O que é `b.N`?

O Go executa a função várias vezes automaticamente para medir desempenho.

---

# Testes Falhando Intencionalmente

Às vezes usamos falhas para validar comportamento.

---

## Exemplo

```go
t.Errorf("Erro proposital")
```

---

# Diferença entre `Error` e `Fatal`

| Método | Comportamento |
|---|---|
| `t.Error()` | Marca erro e continua |
| `t.Fatal()` | Interrompe imediatamente |

---

# Exemplo

```go
if resultado != 4 {
    t.Fatal("Resultado incorreto")
}
```

---

# Estrutura comum de testes

```txt
projeto/
├── main.go
├── soma.go
├── soma_test.go
└── go.mod
```

---

# Boas Práticas

| Prática | Motivo |
|---|---|
| Use nomes claros | Facilita entendimento |
| Teste múltiplos cenários | Maior segurança |
| Automatize testes | Melhor qualidade |
| Execute testes frequentemente | Evita bugs |
| Utilize table tests | Organização |

---

# Testes em aplicações reais

Testes são usados em:

- APIs;
- microsserviços;
- bancos de dados;
- autenticação;
- regras de negócio;
- sistemas web.

---

# Integração Contínua (CI)

Em projetos profissionais, os testes geralmente executam automaticamente em pipelines CI/CD.

Exemplo:

- GitHub Actions;
- GitLab CI;
- Jenkins.

---

# Fluxo comum de desenvolvimento

## 1. Criar funcionalidade

```go
func Soma(a, b int) int {
    return a + b
}
```

---

## 2. Criar teste

```go
func TestSoma(t *testing.T)
```

---

## 3. Executar testes

```bash
go test
```

---

## 4. Verificar cobertura

```bash
go test -cover
```

---

# Problemas comuns

## Nome incorreto do teste

Errado:

```go
func somaTeste()
```

Correto:

```go
func TestSoma()
```

---

## Arquivo sem `_test.go`

O Go não reconhecerá o arquivo como teste.

---

## Comparação incorreta

Resultados esperados precisam ser comparados corretamente.

---

# IMPORTANTE

Arquivos de teste devem terminar obrigatoriamente com:

```txt
_test.go
```

Caso contrário:

- o Go ignorará o arquivo;
- os testes não serão executados.

---

# Conclusão

Os testes automatizados são essenciais para criar aplicações confiáveis e profissionais em Go.

Com o pacote `testing`, conseguimos:

- validar funções;
- automatizar verificações;
- detectar erros rapidamente;
- melhorar qualidade do software.

Testes são indispensáveis em qualquer projeto moderno.

---

!!! note "Importante"

    Arquivos de teste devem terminar com:
    
    ```txt
    _test.go
    ```
    
    Isso permite que o Go reconheça automaticamente os testes do projeto.
