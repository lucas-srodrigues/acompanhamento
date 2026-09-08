```markdown
# 📊 NEXO - Faturamento Inteligente

> Portal digital e sistema de consultoria orientada por dados para processamento, análise gerencial e inteligência de vendas/compras em PDVs[cite: 1].

![Status](https://img.shields.io/badge/status-em_desenvolvimento-yellow)
![Python](https://img.shields.io/badge/Python-3.x-blue)
![Flask](https://img.shields.io/badge/Framework-Flask-black)
![Instituição](https://img.shields.io/badge/CEUB-Projeto_Integrador_III-purple)

---

## 📌 Sumário

- [Sobre o Projeto](#-sobre-o-projeto)
- [Problema e Impacto](#-problema-e-impacto)
- [Principais Funcionalidades](#-principais-funcionalidades)
- [Arquitetura e Tecnologias](#-arquitetura-e-tecnologias)
- [Modelagem do Banco de Dados](#-modelagem-do-banco-de-dados)
- [Pré-requisitos](#-pré-requisitos)
- [Como Executar o Projeto](#-como-executar-o-projeto)
- [Variáveis de Ambiente](#-variáveis-de-ambiente)
- [Equipe](#-equipe)

---

## 📖 Sobre o Projeto

O **NEXO Faturamento Inteligente** é um sistema web desenvolvido como Projeto Integrador III do curso de Análise e Desenvolvimento de Sistemas do CEUB[cite: 1]. 

O sistema viabiliza a importação, o processamento ETL e a análise gerencial de relatórios operacionais exportados de sistemas de Ponto de Venda (PDV)[cite: 1]. Seu mercado de validação inicial é voltado para pequenos comércios independentes do segmento de construção, reforma e pintura[cite: 1].

---

## ⚠️ Problema e Impacto

* **Problema:** Pequenos varejistas acumulam dados em seus sistemas de PDV, mas dependem apenas de intuição ("feeling") para gerir estoque e compras, resultando em relatórios brutos cheios de números sem clareza operacional[cite: 1].
* **Impacto:**
  * Insumos e produtos travados em estoque (dinheiro parado)[cite: 1].
  * Falta de clareza sobre os itens de maior representatividade no faturamento[cite: 1].
  * Compras em descompasso com as vendas do período[cite: 1].

---

## ✨ Principais Funcionalidades

- 📥 **Upload Self-Service e Admin:** Suporte à importação de relatórios de Vendas e Compras nos formatos `.csv`, `.xlsx` e `.xls` com controle de integridade via Hash SHA-256[cite: 1].
- ⚙️ **Pipeline ETL em Memória (Pandas):** Sanitização, normalização e cruzamento de dados sem salvar linhas brutas intermediárias no banco[cite: 1].
- 📊 **Cálculo de KPIs e Curva ABC:** Geração automática de faturamento total, volume de compras, Indicador de Pressão de Estoque (`total_comprado - faturamento_total`) e classificação Pareto (Curva ABC)[cite: 1].
- 📈 **Dashboards Interativos Nativos:** Visualizações dinâmicas utilizando Plotly.js, sem dependência de ferramentas proprietárias externas[cite: 1].
- 🤖 **Motor de IA Assistiva (Claude / Anthropic):** Geração automática de rascunhos de relatórios executivos e pareceres estratégicos para revisão do ADMIN (com fallback determinístico local)[cite: 1].
- 📄 **Exportação em PDF:** Exportação da devolutiva estratégica gerada via ReportLab[cite: 1].
- 💬 **Central de Tickets e NexoBot:** Canal interno de suporte entre cliente/admin e assistente virtual via HuggingFace API para navegação no portal[cite: 1].
- 🔐 **Segurança e Anti-IDOR:** Autenticação com hash PBKDF2, troca de senha obrigatória no primeiro acesso, isolamento estrito de dados por empresa e renovação automática de sessões via `boot_id`[cite: 1].

---

## 🛠 Arquitetura e Tecnologias

O projeto utiliza o padrão de arquitetura em 3 camadas:

### **1. Front-end (Apresentação / View)**
* **Tecnologias:** HTML5, Jinja2 (server-side rendering), Bootstrap 5[cite: 1].
* **Gráficos:** Plotly.js[cite: 1].
* **Comunicação em Tempo Real:** WebSocket via Flask-SocketIO (notificações na navbar)[cite: 1].

### **2. Back-end (Aplicação / Controller)**
* **Linguagem/Framework:** Python com Flask (Application Factory Pattern e Blueprints)[cite: 1].
* **Processamento de Dados:** Pandas[cite: 1].
* **Inteligência Artificial:** Anthropic SDK (Modelos Claude) e HuggingFace API (NexoBot)[cite: 1].
* **Geradores / Auxiliares:** ReportLab (Geração de PDF) e Flask-Mail (Notificações SMTP)[cite: 1].

### **3. Banco de Dados e Persistência (Model)**
* **Banco:** SQLite relacional com ORM SQLAlchemy 2.x[cite: 1].
* **Integridade e Concorrência:** Configurado com `PRAGMA foreign_keys = ON` e modo `WAL` (Write-Ahead Logging)[cite: 1].
* **Migrações:** Flask-Migrate (Alembic) preparado para transição simples ao PostgreSQL[cite: 1].

---

## 🗄 Modelagem do Banco de Dados

O banco de dados relacional é composto por 12 tabelas principais[cite: 1]:
* `plano`, `segmento`, `empresa`[cite: 1]
* `usuario`[cite: 1]
* `analise`, `upload_relatorio`[cite: 1]
* `indicador_analise`, `produto_curva_abc`[cite: 1]
* `relatorio_analise`[cite: 1]
* `chamado_suporte`, `mensagem_suporte`, `notificacao`[cite: 1]

---

## ⚙️ Pré-requisitos

Antes de iniciar, certifique-se de ter instalado:
* **Python 3.10+**
* **Git**
* Gerenciador de pacotes **pip** e ambiente virtual `venv`

---

## 🚀 Como Executar o Projeto

### 1. Clonar o repositório
```bash
git clone [https://github.com/seu-usuario/nexo-faturamento-inteligente.git](https://github.com/seu-usuario/nexo-faturamento-inteligente.git)
cd nexo-faturamento-inteligente

```

### 2. Criar e ativar o ambiente virtual

```bash
# Linux/macOS
python3 -m venv venv
source venv/bin/activate

# Windows
python -m venv venv
venv\Scripts\activate

```

### 3. Instalar as dependências

```bash
pip install -r requirements.txt

```

### 4. Configurar as Variáveis de Ambiente

Crie um arquivo `.env` na raiz do projeto (veja a seção [Variáveis de Ambiente](https://www.google.com/search?q=%23-vari%C3%A1veis-de-ambiente)).

### 5. Executar as migrações do banco de dados

```bash
flask db upgrade

```

### 6. Iniciar a aplicação

```bash
flask run

```

Acesse a aplicação via navegador no endereço: `http://localhost:5000`

---

## 🔑 Variáveis de Ambiente

Crie um arquivo `.env` baseado no exemplo abaixo:

```env
FLASK_APP=app.py
FLASK_ENV=development
SECRET_KEY=sua_chave_secreta_aqui

# Banco de Dados
DATABASE_URL=sqlite:///nexo.db

# Chaves de API de Serviços Externos
ANTHROPIC_API_KEY=sua_chave_anthropic_claude
HUGGINGFACE_API_KEY=sua_chave_huggingface

# Configuração de E-mail (SMTP)
MAIL_SERVER=smtp.gmail.com
MAIL_PORT=587
MAIL_USE_TLS=True
MAIL_USERNAME=seu_email@email.com
MAIL_PASSWORD=sua_senha_de_app

```

---

## 👥 Equipe (CEUB - 5º Semestre)

* **João Vitor**

* **João César**

* **Carlos Eduardo**


**Instituição:** CEUB - Centro Universitário de Brasília

**Curso:** Análise e Desenvolvimento de Sistemas

```

```
