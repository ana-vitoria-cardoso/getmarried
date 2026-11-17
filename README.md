# 💍 GetMarried.com

Aplicação web de apoio aos noivos: reúne as informações do casamento, organiza a lista de presentes com reserva e centraliza a confirmação de presença dos convidados, com um assistente de IA integrado.

![status](https://img.shields.io/badge/status-em%20desenvolvimento-yellow)
![versão](https://img.shields.io/badge/versão-0.1.0-blue)
![licença](https://img.shields.io/badge/licença-MIT-green)

## 📌 Sumário

- [Sobre o projeto](#-sobre-o-projeto)
- [Funcionalidades](#-funcionalidades)
- [Ficha técnica](#-ficha-técnica)
- [Estrutura do repositório](#-estrutura-do-repositório)
- [Como executar](#-como-executar)
- [Documentação](#-documentação)
- [Roadmap](#-roadmap)
- [Autora](#-autora)

## 🎯 Sobre o projeto

**Problema:** os noivos precisam evitar presentes repetidos e controlar confirmações de presença que ficam espalhadas entre mensagens e planilhas.

**Solução:** um único app onde o convidado faz login uma vez e realiza todas as ações (reservar presente e confirmar presença) sem precisar repetir seus dados.

## ✨ Funcionalidades

### Login do convidado
- Identificação única; os dados ficam registrados para todas as ações seguintes.

### Informativos do casamento
- Data, local, horário, observações e fotos do casal.
- Navegação por menu lateral (aba vertical).

### Lista de presentes
- Cada produto tem valor estimado e um link que abre uma busca na web com opções de compra em várias lojas.
- Ordenação por preço (menor → maior e maior → menor).
- Filtro por valor que o convidado pretende gastar, com margem de variação para mais e para menos.
- **Reserva exclusiva:** após confirmar na caixa de confirmação, o presente fica indisponível (sem link) para os demais convidados.
- O convidado pode cancelar a própria reserva, e o presente volta para a lista.
- Reservas protegidas contra cliques simultâneos: só um convidado consegue reservar cada item.
- Registro de convidado + presente reservado, exportável em Excel.

### Confirmação de presença
- Nome e telefone vêm do login.
- O convidado informa os acompanhantes da família, sem que cada um precise fazer login.
- Para cada acompanhante: indicação de criança menor de 10 anos (sim/não) e, se sim, a idade.
- Dados exportáveis em Excel.

### Painel dos noivos
- Visão de reservas e confirmações.
- Contagem automática de adultos e crianças confirmados.
- Exportação das planilhas em `.xlsx`.

### Inteligência artificial
- **Assistente de dúvidas:** responde perguntas dos convidados com base nas informações do casamento (RAG).
- **Sugestão de presentes:** recomenda itens da lista conforme orçamento e estilo informados.
- **Agente do painel:** responde perguntas dos noivos sobre confirmações e reservas consultando o banco (function calling).

## 🧾 Ficha técnica

| Item | Descrição |
|---|---|
| Nome | GetMarried.com |
| Tipo | Aplicação web responsiva |
| Público-alvo | Noivos (administração) e convidados |
| Frontend | HTML, CSS e JavaScript |
| Backend | Python + FastAPI |
| Banco de dados | MySQL 8 |
| IA | API de LLM (RAG, embeddings e function calling) |
| Infraestrutura | Docker e Docker Compose |
| Exportação | Arquivos Excel (`.xlsx`) |
| Versionamento | Git e GitHub (Conventional Commits) |
| Versão | 0.1.0 |
| Licença | MIT |

## 🗂 Estrutura do repositório

```
getmarried/
├── README.md
├── .env.example
├── .gitignore
├── docker-compose.yml
├── Dockerfile
├── requirements.txt
├── docs/
│   ├── requisitos.md
│   ├── modelo-de-dados.md
│   ├── arquitetura.md
│   ├── api.md
│   ├── lgpd.md
│   ├── decisoes.md
│   └── prototipos/
├── db/
│   └── init.sql
├── src/
│   ├── main.py
│   ├── auth/
│   ├── gifts/
│   ├── rsvp/
│   ├── admin/
│   ├── ai/
│   └── db/
├── frontend/
├── data/
│   └── casamento.md
└── tests/
```

## ▶️ Como executar

**Pré-requisitos:** Git e Docker.

```bash
git clone https://github.com/SEU-USUARIO/getmarried.git
cd getmarried
cp .env.example .env    # preencha as variáveis
docker compose up
```

Variáveis do `.env` (nunca versionar este arquivo):

```
DB_PASSWORD=
LLM_API_KEY=
```

> Esta seção será atualizada conforme o projeto evoluir.

## 📚 Documentação

A pasta [`docs/`](docs/) reúne:

- **Requisitos:** funcionais, não funcionais e histórias de usuário
- **Modelo de dados:** diagrama ER e dicionário de dados
- **Arquitetura:** componentes e decisões técnicas
- **API:** endpoints
- **LGPD:** dados coletados, finalidade e como solicitar exclusão
- **Decisões:** escolhas técnicas e uso de IA no desenvolvimento
- **Protótipos:** telas

## 🗺 Roadmap

- [ ] Documentação e protótipos
- [ ] Login do convidado
- [ ] Tela de informativos
- [ ] Lista de presentes e reservas
- [ ] Confirmação de presença (adultos e crianças)
- [ ] Exportação Excel
- [ ] Painel dos noivos
- [ ] Módulo de IA
- [ ] Testes e deploy

## 👩‍💻 Autora

**Ana Vitória Cardoso Queiroz**
