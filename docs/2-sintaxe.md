# 2. Sintaxe Básica e Variáveis

## Estrutura Básica de um Programa Go

Um programa Go é organizado em **pacotes** (packages). Todo arquivo fonte Go pertence a exatamente um pacote, declarado na primeira linha do arquivo com a palavra-chave `package`.

O ponto de entrada para qualquer aplicação executável em Go é a função `main()`, que deve pertencer ao pacote `main`.

### Exemplo de estrutura básica:

```go
package main

import "fmt"

func main() {
    fmt.Println("Olá Mundo")
}
Explicação do código:
Linha	Explicação
package main	Declara que este arquivo pertence ao pacote principal
import "fmt"	Importa o pacote fmt para formatação e saída de texto
func main()	Função principal, ponto de entrada do programa
fmt.Println()	Função que imprime texto no console
Pacotes e Importações
O conceito de pacotes em Go é fundamental para organizar código e gerenciar dependências. Pacotes permitem:

Encapsulamento: Identificadores começados com letra maiúscula são exportados (públicos), enquanto letra minúscula indica visibilidade interna ao pacote.

Reutilização: Pacotes podem ser importados por outros pacotes usando a palavra-chave import.

Namespace: Cada pacote cria seu próprio escopo, evitando conflitos de nomes.

Múltiplas importações:
go
import (
    "fmt"
    "math"
    "strings"
)
Declaração de Variáveis
Go é uma linguagem de tipagem estática, o que significa que o tipo de uma variável é conhecido em tempo de compilação. Isso traz benefícios como:

Segurança: Erros de tipo são detectados antes da execução.

Performance: O compilador pode otimizar o código com base nos tipos.

Manutenibilidade: O código se torna mais previsível e documentado.

Declaração explícita com var:
go
var nome string = "Kassia"
var idade int = 20
Sintaxe da declaração com var:
go
var nomeDaVariavel tipo = valor
Declaração sem valor inicial (recebe valor zero):
go
var nome string     // recebe "" (string vazia)
var idade int       // recebe 0
var ativo bool      // recebe false
var preco float64   // recebe 0.0
Múltiplas declarações em bloco:
go
var (
    nome  string = "João"
    idade int    = 30
    cidade string = "São Paulo"
)
Múltiplas variáveis em uma linha:
go
var x, y int = 10, 20
var nome, idade = "Maria", 25  // tipos inferidos
Declaração Curta com :=
Disponível apenas dentro de funções, é a forma mais concisa e amplamente utilizada em código Go moderno. O compilador infere automaticamente o tipo da variável com base no valor atribuído.

go
cidade := "São Paulo"
Múltiplas declarações curtas:
go
nome, idade := "Carlos", 28
x, y := 10, 20
ativo, preco := true, 99.90
Tipos Primitivos
Tipos Numéricos
Categoria	Tipos	Descrição
Inteiros padrão	int, uint	Tamanho dependente da plataforma (32 ou 64 bits)
Inteiros 8 bits	int8, uint8	-128 a 127 / 0 a 255
Inteiros 16 bits	int16, uint16	-32768 a 32767 / 0 a 65535
Inteiros 32 bits	int32, uint32	-2³¹ a 2³¹-1 / 0 a 2³²-1
Inteiros 64 bits	int64, uint64	-2⁶³ a 2⁶³-1 / 0 a 2⁶⁴-1
Bytes e runes	byte, rune	byte = uint8, rune = int32 (Unicode)
Ponto flutuante	float32, float64	Números decimais
Números complexos	complex64, complex128	Parte real e imaginária
Exemplos de uso:
go
var inteiro int = 42
var pequeno int8 = 127
var grande int64 = 9223372036854775807
var decimal float64 = 3.14159
var letra byte = 'A'
var simbolo rune = '😀'
Tipo Booleano
O tipo bool representa valores verdadeiros ou falsos:

go
var ativo bool = true
var logado bool = false
teste := true
Tipo String
Strings em Go são imutáveis e representam sequências de bytes UTF-8:

go
var nome string = "Go Lang"
saudacao := "Olá, mundo!"
vazia := ""
Tabela de Tipos Primitivos
Tipo	Exemplo	Valor zero
int	10	0
string	"Go"	"" (vazio)
bool	true	false
float64	10.5	0.0
byte	'A'	0
rune	'ç'	0
Valores Zero (Zero Values)
Um conceito fundamental em Go: toda variável declarada sem inicialização explícita recebe automaticamente o valor zero do seu tipo:

Tipo	Valor Zero
Numérico (int, float, etc.)	0
Booleano (bool)	false
String (string)	"" (string vazia)
Ponteiros, slices, maps, channels, funções, interfaces	nil
go
var a int       // a = 0
var b string    // b = ""
var c bool      // c = false
var d float64   // d = 0.0
Constantes
Constantes são valores que não podem ser alterados durante a execução do programa:

go
const pi = 3.14159
const nomeApp string = "MeuApp"
const (
    segundosPorMinuto = 60
    minutosPorHora    = 60
    horasPorDia       = 24
)
Escopo e Visibilidade
Escopo	Localização	Visibilidade
Pacote (global)	Fora de qualquer função	Todo o pacote
Função	Dentro de uma função	Apenas na função
Bloco	Dentro de {}	Apenas no bloco
Exportado	Nome com letra MAIÚSCULA	Outros pacotes podem acessar
Exemplo de visibilidade:
go
var Publico string = "Posso ser acessado de fora"     // Exportado (Maiúsculo)
var privado string = "Só dentro do meu pacote"        // Não exportado (Minúsculo)

func FuncaoPublica() {}     // Exportada
func funcaoPrivada() {}     // Não exportada
Conversão de Tipos
Go não permite conversão implícita entre tipos. É necessário conversão explícita:

go
var x int = 10
var y float64 = float64(x)  // Conversão explícita

var a int32 = 42
var b int64 = int64(a)      // Conversão entre inteiros

var i int = 65
var c byte = byte(i)        // 65 -> 'A'
Regras e Limitações Importantes
!!! warning "Regra 1"
Toda variável declarada deve ser usada. Variáveis não utilizadas geram erro de compilação.

!!! warning "Regra 2"
O operador := só funciona dentro de funções. Não pode ser usado no escopo global do pacote.

!!! warning "Regra 3"
O operador := redeclara variáveis em novos escopos. Cuidado ao usá-lo dentro de blocos if/for, pois pode criar uma nova variável local em vez de reutilizar a externa.

!!! warning "Regra 4"
Go não possui o operador ternário (cond ? a : b). Use if/else explícito.

!!! note "Regra 5"
O compilador Go infere o tipo quando você omite na declaração, mas a tipagem continua estática.

Boas Práticas
Prática	Por quê?
Prefira := dentro de funções	Código mais limpo e conciso
Use blocos var agrupados	Melhor organização no escopo global
Nomeie variáveis em camelCase	Padrão da comunidade (nomeCompleto)
Use nomes curtos para escopos pequenos	i para loop, s para string
Declare variáveis perto do uso	Melhora a legibilidade
Evite variáveis globais	Prefira passar parâmetros explicitamente
Constantes: use PascalCase ou camelCase	Evite SCREAMING_SNAKE_CASE
Exemplo Completo
go
package main

import "fmt"

// Constante global
const appName = "Documentação Go"

// Variáveis globais
var versao string = "1.24"
var (
    autor   string = "Equipe CTT"
    ano     int    = 2026
)

func main() {
    // Declaração curta dentro da função
    mensagem := "Olá, mundo!"
    
    // Múltiplas declarações curtas
    nome, idade := "Kassia", 20
    
    // Conversão explícita
    var x int = 10
    var y float64 = float64(x)
    
    fmt.Println(mensagem)
    fmt.Println("Nome:", nome, "Idade:", idade)
    fmt.Println("Conversão:", y)
}
!!! tip "Dica Final"
A declaração curta := é a forma mais comum em código Go. Use var apenas quando precisar de um valor zero explícito ou no escopo global do pacote.