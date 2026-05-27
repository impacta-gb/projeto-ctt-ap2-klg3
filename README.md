[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/dXN9WTy3)

📚 Documentação da Linguagem Go com Zensical

Projeto acadêmino desenvolvido para a disciplina Collaboration Tools for Teams (CTT) – AP2, com foco na criação de uma documentação técnica completa sobre a linguagem Go (Golang), aplicando práticas profissionais de desenvolvimento colaborativo, versionamento com Git/GitHub e automação de CI/CD com GitHub Actions.

---

🌐 Site Publicado

🔗https://impacta-gb.github.io/projeto-ctt-ap2-klg3/

---

👥 Integrantes

Nome dos Responsaveis
Guilherme Sousa - 2501248
Gabriel Albuquerque - 2403756
Kassia Isabelle - 2500203
Lucca Gomes - 2501551

---

🎯 Objetivo do Projeto

Desenvolver um site de documentação técnica da linguagem Go utilizando o gerador estático Zensical (compatível com MkDocs), aplicando:

· ✅ Fluxo colaborativo com Git e GitHub

· ✅ Feature Branches + Pull Requests com Code Review

· ✅ Proteção da branch main (commits diretos bloqueados)

· ✅ Pipeline de CI/CD automatizado com GitHub Actions

· ✅ Deploy contínuo no GitHub Pages

· ✅ Testes em múltiplas versões do Python (matrix strategy)

· ✅ Cache de dependências para otimização do pipeline

· ✅ Rebuild semanal automático via schedule

---

📁 Estrutura do Repositório

```
projeto-ctt-go-docs/
│
├── .github/
│   └── workflows/
│       ├── ci-cd.yml          # Pipeline principal (build + deploy)
│       └── docs.yml           # Pipeline secundária (validação rápida)
│
├── docs/
│   ├── index.md               # Página inicial
│   ├── 01-introducao_instalacao.md
│   ├── 02-sintaxe.md
│   ├── 03-estruturas.md
│   ├── 04-arrays_slices_maps.md
│   ├── 05-structs-metodos.md
│   ├── 06-tratamento_erros.md
│   ├── 07-concorrencias-1.md
│   ├── 08-concorrencias-2.md
│   ├── 09-gerenciamento-pacotes.md
│   ├── 10-testes-automatizados.md
│   └── markdown.md           # Guia de Markdown utilizado
│
├── requirements.txt           # Dependências Python (Zensical)
├── zensical.toml              # Configuração do Zensical
└── README.md                  # Este arquivo
```

---

🔧 Tecnologias Utilizadas

Categoria Tecnologias
Linguagem documentada Go (Golang)
Gerador estático Zensical (Python)
Formatação Markdown
Versionamento Git + GitHub
CI/CD GitHub Actions
Hospedagem GitHub Pages
Automação Matrix Build, Cache, Schedule CRON

---

🔄 Fluxo de Trabalho Colaborativo

1. Proteção da Branch main

· ✅ Commits diretos (push) bloqueados

· ✅ Pull Request obrigatório para qualquer alteração

· ✅ Aprovação de pelo menos 1 membro da equipe antes do merge


2. Feature Branches

Cada membro cria uma branch a partir da main seguindo o padrão:

```bash
feat/doc-nome-da-pagina
```

Exemplos:

· feat/doc-introducao
· feat/doc-sintaxe
· feat/doc-concorrencias
· feat/ci-cd-pipeline

3. Fluxo Completo por Página

1. Criar branch a partir da main atualizada
2. Escrever/editar o arquivo .md correspondente
3. git commit e git push da branch
4. Abrir Pull Request para main
5. Outro membro revisa, comenta e aprova o PR
6. Merge para main → dispara CI/CD → deploy automático

4. Critérios de Revisão

Cada PR passou por verificação de:

· ✅ Markdown válido e bem formatado

· ✅ Pelo menos 1 bloco de código Go com syntax highlighting

· ✅ Pelo menos 1 admonition (nota, dica, aviso) por página

· ✅ Links internos funcionando

· ✅ Conteúdo tecnicamente correto

---

⚙️ Arquitetura do CI/CD (GitHub Actions)

📁 Workflows

ci-cd.yml – Pipeline Principal

Executado em:

· pull_request para main → apenas build (validação)
· push na main → build + deploy
· schedule (cron: 0 0 * * 0) → rebuild semanal aos domingos

docs.yml – Pipeline Secundária (validação rápida)

Executado em pull_request para validar PRs sem rodar toda a matrix.

🔧 Jobs do ci-cd.yml

Job Descrição
build_site Roda em matrix (Python 3.10 e 3.11) com cache de dependências. Executa zensical build --clean. Faz upload do artefato site/ apenas da versão 3.11.
deploy_site Depende do build_site. Executa apenas em push na main ou schedule. Publica no GitHub Pages via actions/deploy-pages.

📊 Fluxo Visual

```
pull_request → build_site (3.10 + 3.11) → ✅ validação (sem deploy)
push na main  → build_site (3.10 + 3.11) → deploy_site → 🌐 GitHub Pages
schedule      → build_site (3.10 + 3.11) → deploy_site → 🌐 GitHub Pages (automático)
```

---

🚀 Como Executar Localmente

Pré-requisitos

· Python 3.10 ou 3.11
· Pip

Passos

```bash
# 1. Clone o repositório
git clone https://github.com/impacta-gb/projeto-ctt-ap2-klg3.gitt
cd projeto-ctt-ap2-klg3

# 2. Instale as dependências
pip install -r requirements.txt

# 3. Execute o servidor de desenvolvimento
zensical serve

# 4. Acesse no navegador
http://localhost:8000
```

Build estático

```bash
zensical build --clean
```

Os arquivos gerados estarão na pasta site/.

---

📝 Conteúdo da Documentação

# Tópico Arquivo
01 Introdução e Instalação 01-introducao_instalacao.md
02 Sintaxe Básica e Variáveis 02-sintaxe.md
03 Estruturas de Controle 03-estruturas.md
04 Arrays, Slices e Maps 04-arrays_slices_maps.md
05 Structs e Métodos 05-structs-metodos.md
06 Tratamento de Erros 06-tratamento_erros.md
07 Concorrência I: Goroutines 07-concorrencias-1.md
08 Concorrência II: Channels 08-concorrencias-2.md
09 Gerenciamento de Pacotes (Go Modules) 09-gerenciamento-pacotes.md
10 Testes Automatizados 10-testes-automatizados.md
— Guia de Markdown markdown.md

---

📄 Licença

Este projeto é acadêmico e foi desenvolvido para fins educacionais na disciplina CTT da Impacta Tecnologia.

---

🙌 Agradecimentos

· Professor da disciplina CTT pelo suporte

---

Desenvolvido com 💙 por Guilherme, Gabriel, Kassia e Lucca

---
