# 9. Gerenciamento de Pacotes

## Inicializando Projeto

```bash
go mod init meu-projeto
```

## Instalando Dependências

```bash
go get github.com/gin-gonic/gin
```

## Arquivo go.mod

```txt
module meu-projeto

go 1.24
```

## Atualizando Dependências

```bash
go mod tidy
```

!!! note "Boa prática"
    Sempre mantenha o go.mod organizado.
