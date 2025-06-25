# Deploy dbt-core

# Deploy DBT Core com Render

Este projeto configura o deploy automatizado de um pipeline `dbt Core` utilizando **Render.com**. Ele foi desenvolvido para rodar transformações de dados agendadas, conectando-se a um banco de dados **PostgreSQL** também instanciado na plataforma Render.

---

## 🎯 Objetivo

Automatizar a execução de modelos `dbt` em um ambiente de produção na nuvem:

- Sem depender do dbt Cloud.
- Utilizando **Docker** para empacotar o projeto.
- Executado periodicamente via **Cron Job do Render**.
- Conectando-se a um banco de dados **PostgreSQL** (instanciado no Render).

---

## ⚙️ Como funciona

### 1. Projeto `dbt`

- Contém estrutura padrão `dbt` com `models`, `dbt_project.yml`, `profiles.yml`, etc.
- Os modelos são executados no banco PostgreSQL em horários programados.

### 2. `Dockerfile`

- Cria uma imagem com Python e instala o `dbt-core` e `dbt-postgres`.
- Copia os arquivos do projeto e define um `ENTRYPOINT` com o script `entrypoint.sh`.

### 3. `entrypoint.sh`

Script que orquestra o pipeline:

```bash
dbt deps       # Instala dependências
dbt seed       # (Opcional) carrega dados estáticos
dbt run        # Executa os modelos
dbt test       # Roda os testes definidos
