# Crie Agentes de IA — Projeto do Curso

Este repositório contém o projeto do curso **“Crie Agentes de IA”**, com um exemplo completo de **agente de atendimento ao cliente** com:

- **Chat UI** em **Streamlit**
- **API** em **Flask** (endpoint `POST /ask`)
- **RAG (Retrieval-Augmented Generation)** com **LangChain + FAISS**
- **Memória de conversa**
- **SQLite** para consultar **status de atendimentos**
- Base documental em `.txt` (manual/garantia/autorizadas)

---

## ✅ O que você encontra aqui

- Um **chat** (Streamlit) que envia perguntas para uma API.
- Uma **API Flask** que:
  - identifica perguntas sobre **atendimentos** e consulta o **SQLite**
  - para demais perguntas, usa **RAG** para responder com base em documentos
- Scripts e arquivos de exemplo:
  - `cria_db.py` cria/popula `atendimentos.db`
  - `documents/*.txt` alimenta o índice FAISS

---

## 🧱 Estrutura sugerida do projeto

> Ajuste conforme a organização do seu repositório.

```text
.
├─ app.py                  # Frontend Streamlit (chat)
├─ chat.py                 # Backend Flask + RAG + SQLite
├─ cria_db.py              # Cria e popula atendimentos.db
├─ atendimentos.db         # Base SQLite (gerada ou exemplo)
├─ config.yaml             # Config (API KEY / modelo)
├─ requirements.txt        # Dependências
├─ relogio.jpg             # Imagem usada no Streamlit
└─ documents/
   ├─ Manual.txt
   ├─ Garantia.txt
   └─ Autorizadas.txt
```

---

## 🔧 Requisitos

- Python 3.10+ (recomendado)
- Dependências em `requirements.txt`

---

## 🚀 Como rodar o projeto

### 1) Clone o repositório

```bash
git clone <URL_DO_SEU_REPO>
cd <PASTA_DO_REPO>
```

### 2) Crie e ative um ambiente virtual (opcional, recomendado)

```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# Linux/Mac
source .venv/bin/activate
```

### 3) Instale as dependências

```bash
pip install -r requirements.txt
```

### 4) Configure o `config.yaml`

O backend lê a chave e define `OPENAI_API_KEY` a partir do YAML.

Exemplo (ajuste para o seu formato atual):

```yaml
api_key:
  key: "SUA_OPENAI_API_KEY"
model:
  name: "gpt-4o-mini"  # exemplo
```

> **Importante:** mantenha sua chave fora do GitHub (use `.gitignore` ou variáveis de ambiente).

### 5) Garanta os documentos em `documents/`

Coloque os arquivos `.txt` (ex.: `Manual.txt`, `Garantia.txt`, `Autorizadas.txt`) dentro da pasta `documents/`.
Eles serão usados para montar o índice FAISS do RAG.

### 6) (Opcional) Crie/popule o banco SQLite

```bash
python cria_db.py
```

Isso cria (ou recria) a tabela de atendimentos e insere registros de exemplo.

---

## ▶️ Executando

### A) Suba o backend (Flask)

Em um terminal:

```bash
python chat.py
```

Por padrão, a API sobe em:

- `http://127.0.0.1:5000`
- Endpoint: `POST /ask`

### B) Suba o frontend (Streamlit)

Em outro terminal:

```bash
streamlit run app.py
```

Abra o link exibido no terminal do Streamlit.

---

## 🧪 Exemplos de perguntas

### Perguntas sobre atendimentos (SQLite)

- “Qual o status do **atendimento número 2**?”
- “Qual foi o defeito do **atendimento número 3**?”
- “Qual a data do **atendimento número 1**?”

### Perguntas sobre produto/garantia (RAG)

- “O que a garantia cobre?”
- “Como funciona a manutenção?”
- “Quais são as assistências autorizadas?”

---

## 🧠 Como funciona (visão rápida)

1. O **Streamlit** coleta a pergunta do usuário e chama a API `/ask`.
2. A **API Flask**:
   - tenta detectar se a pergunta é sobre **atendimento número X**
   - se for, consulta o **SQLite**
   - se não for, chama o pipeline **RAG** (FAISS + LangChain) e responde com base nos documentos.

---

## 🔒 Boas práticas (recomendado)

- Adicione `config.yaml` ao `.gitignore` (para não vazar chave)
- Use `.env`/variáveis de ambiente em produção
- Versione seus documentos em `documents/` quando fizer sentido (ou use storage externo)

---

## 📄 Licença

Use a licença que preferir (MIT, Apache-2.0 etc.).  
Se você for publicar este repo como material do curso, recomenda-se incluir uma licença explícita.

---

## 📬 Contato / Links

- Plataforma: **EIA.ai**
- Autor: **Fernando Amaral**
