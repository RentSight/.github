
---

# 🏘️ RentSight – Real Estate Data Intelligence Platform

**Plataforma de Inteligência de Mercado de Aluguéis Imobiliários**
<br>
**Dataset: [Airbnb - Rio De Janeiro](https://data.insideairbnb.com/brazil/rj/rio-de-janeiro/2025-09-26/visualisations/listings.csv)**

> Este projeto nasceu da ideia de **construir algo real**, que entregue valor e demonstre conhecimentos práticos em **Databricks, ASP.NET Core, APIs, bancos de dados, arquitetura de dados e arquitetura de software**.

---

## 💡 Problema real

Investidores e locadores querem responder perguntas como:

* Onde vale mais a pena investir?
* Qual bairro está supervalorizado?
* O preço médio está subindo ou caindo?
* Airbnb compensa mais que aluguel tradicional?

Essas respostas **não vêm prontas**. Elas exigem:

* Coleta de dados
* Limpeza
* Enriquecimento
* Agregação
* Disponibilização via API

Ou seja… **ETL na veia** 🧪💉

---

## 🧱 Arquitetura Geral (visão de portfólio)

```
[ Fontes de Dados ]
        ↓
[ Databricks - ETL ]
        ↓
[ Camada Analítica ]
        ↓
[ Banco de Dados Relacional ]
        ↓
[ Backend ASP.NET Core ]
        ↓
[ Front-end demonstrativo ]
```

---

## 📁 Estrutura da Organização GitHub

```
github.com/aluguel-inteligencia-mercado/
├── data-platform/       # ETL, pipelines, seed e scripts SQL
├── backend-platform/    # Backend ASP.NET Core
└── frontend-platform/   # Front-end demonstrativo (stack em definição)
```

Cada repositório é **independente**, mas juntos formam um sistema coerente e profissional.

---

## 📊 `data-platform` — Engenharia de Dados & ETL

Responsável por **toda a camada analítica e pipelines de dados**.
Inclui:

* Notebooks Databricks (`bronze/`, `silver/`, `gold/`)
* Scripts de conversão de dados:

  * Parquet → SQLite
  * Parquet → MySQL/PostgreSQL (futuro)
* SQL scripts (`schema.sql`, `seed.sql`)
* Documentação do pipeline

> Observação: notebooks do Databricks são para **visualização da lógica ETL**. Não é necessário executá-los para avaliar a API.

**Fluxo local de execução para avaliação:**

1. Executar `schema.sql`
2. Executar `seed.sql`
3. A API consome os dados do SQLite local

---

## 🧠 `backend-platform` — Backend ASP.NET Core

* Clean Architecture
* Controllers → Services → Repositories
* DTOs explícitos
* Versionamento de API
* Cache, paginação e filtros dinâmicos
* Swagger documentado

**Endpoints principais:**

* `GET /api/analytics/top-bairros`
* `GET /api/analytics/tendencias?bairro=Centro`
* `GET /api/analytics/preco-m2`
* `GET /api/insights/rentabilidade`

O backend **consome apenas dados já processados**, desacoplado do Databricks, podendo usar:

* SQLite (desenvolvimento)
* MySQL / PostgreSQL / SQL Server (futuro)

---

## 🖥️ `frontend-platform` — Front-end demonstrativo

* Propósito: consumir a API e exibir dados analíticos
* Mostrar gráficos, tabelas e filtros básicos
* Stack / tecnologia **em definição** (React / Blazor / Next.js)

O front-end **não é protagonista**, mas valida o fluxo ponta a ponta da aplicação.

---

## 🗄️ Seed, Banco de Dados e Experiência de Execução

* Backend utiliza **SQLite** para execução local
* `schema.sql` define a estrutura do banco
* `seed.sql` popula com um **recorte temporal pequeno e coerente**

**Fluxo de execução local:**

1. Clonar os três repositórios
2. Executar scripts SQL (`schema.sql` + `seed.sql`)
3. Subir a API (`backend-platform`)
4. Abrir Swagger e testar endpoints
5. Consumir dados via front-end (`frontend-platform`)

> Quando o ETL real for executado, o banco completo pode ser migrado para MySQL, PostgreSQL ou SQL Server sem alterar a API.

---

## 🎯 Por que este projeto importa no portfólio

* Pipeline ETL completo, da ingestão à análise
* Uso correto do Databricks
* Modelagem analítica robusta
* Backend ASP.NET Core profissional e desacoplado
* Separação clara entre processamento e serving
* Foco em **DX (Developer Experience)** e experiência do avaliador
* Projeto **realista e gerador de valor**, não tutorial

---

## 🔗 Links para os Repositórios

| Repositório                                                                              | Descrição                                                    |
| ---------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| [`data-platform`](https://github.com/aluguel-inteligencia-mercado/data-platform)         | Notebooks, ETL, scripts SQL, seed e documentação do pipeline |
| [`backend-platform`](https://github.com/aluguel-inteligencia-mercado/backend-platform)   | Backend ASP.NET Core, endpoints, cache, Swagger              |
| [`frontend-platform`](https://github.com/aluguel-inteligencia-mercado/frontend-platform) | Front-end demonstrativo (stack em definição)                 |

---

## 🏷️ Badges (representativos)

![Python](https://img.shields.io/badge/python-3.11-blue?logo=python\&logoColor=white)
![Databricks](https://img.shields.io/badge/Databricks-FF6F00?logo=databricks\&logoColor=white)
![.NET](https://img.shields.io/badge/.NET-8.0-blue?logo=dotnet\&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?logo=sqlite\&logoColor=white)
![OpenAPI](https://img.shields.io/badge/OpenAPI-Swagger-brightgreen)

---

## 🚀 Getting Started (avaliador / teste local)

```bash
# 1. Clone os repositórios
git clone https://github.com/aluguel-inteligencia-mercado/data-platform.git
git clone https://github.com/aluguel-inteligencia-mercado/backend-platform.git
git clone https://github.com/aluguel-inteligencia-mercado/frontend-platform.git

# 2. Prepare o banco (SQLite)
cd data-platform/seed
sqlite3 metacritic.db < schema.sql
sqlite3 metacritic.db < seed.sql

# 3. Instale dependências e rode o backend
cd ../../backend-platform
dotnet restore
dotnet run

# 4. Abra Swagger para testar endpoints
# http://localhost:5000/swagger

# 5. Front-end (stack em definição)
# Instale dependências do front-end e aponte para a API
```
