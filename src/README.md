# Código da Aplicação

Esta pasta contém o código do seu agente financeiro.

## Estrutura

```
src/
│
├── app.py              # Interface (Streamlit)
├── agente.py           # Lógica do agente
├── data_loader.py      # Carregamento dos dados
├── config.py           # Configurações (API, constantes)
├── utils.py            # Funções auxiliares
├── requirements.txt    # Dependências
│
└── data/
    ├── transacoes.csv
    ├── perfil_investidor.json
    ├── produtos_financeiros.json
    └── historico_atendimento.csv
```
## ⚙️ `config.py`

```python
import os
from dotenv import load_dotenv

load_dotenv()

OPENAI_API_KEY = os.getenv("OPENAI_API_KEY")

MODEL_NAME = "gpt-4o-mini"

```

📊 data_loader.py
```
import pandas as pd
import json

def carregar_transacoes(path):
    return pd.read_csv(path)

def carregar_perfil(path):
    with open(path, "r", encoding="utf-8") as f:
        return json.load(f)

def carregar_produtos(path):
    with open(path, "r", encoding="utf-8") as f:
        return json.load(f)

def carregar_historico(path):
    return pd.read_csv(path)
```

🧠 agente.py

Aqui está o “cérebro” do sistema.

```
from openai import OpenAI
from config import OPENAI_API_KEY, MODEL_NAME

client = OpenAI(api_key=OPENAI_API_KEY)

SYSTEM_PROMPT = """
Você é a Bia Financeira, uma assistente especializada em finanças pessoais.

REGRAS:
- Responda apenas com base nos dados fornecidos
- Não invente informações
- Seja clara, objetiva e didática
- Se faltar informação, avise o usuário
"""

def montar_contexto(transacoes, perfil, historico):
    resumo_transacoes = transacoes.head(10).to_string(index=False)

    contexto = f"""
Perfil do cliente:
{perfil}

Últimas transações:
{resumo_transacoes}

Histórico de atendimento:
{historico.head(5).to_string(index=False)}
"""
    return contexto


def gerar_resposta(pergunta, contexto):
    response = client.chat.completions.create(
        model=MODEL_NAME,
        messages=[
            {"role": "system", "content": SYSTEM_PROMPT},
            {"role": "user", "content": contexto + "\n\nPergunta: " + pergunta}
        ],
        temperature=0.3
    )

    return response.choices[0].message.content
```
🛠️ utils.py
```
def formatar_moeda(valor):
    return f"R$ {valor:,.2f}".replace(",", "X").replace(".", ",").replace("X", ".")
```
💬 app.py (Interface com Streamlit)
```
import streamlit as st
from data_loader import (
    carregar_transacoes,
    carregar_perfil,
    carregar_produtos,
    carregar_historico
)
from agente import montar_contexto, gerar_resposta

# Configuração da página
st.set_page_config(page_title="Bia Financeira", page_icon="💰")

st.title("💰 Bia Financeira")
st.write("Seu assistente inteligente para organização financeira")

# Carregar dados
transacoes = carregar_transacoes("data/transacoes.csv")
perfil = carregar_perfil("data/perfil_investidor.json")
produtos = carregar_produtos("data/produtos_financeiros.json")
historico = carregar_historico("data/historico_atendimento.csv")

# Montar contexto
contexto = montar_contexto(transacoes, perfil, historico)

# Histórico do chat
if "messages" not in st.session_state:
    st.session_state.messages = []

# Exibir mensagens anteriores
for msg in st.session_state.messages:
    with st.chat_message(msg["role"]):
        st.write(msg["content"])

# Input do usuário
pergunta = st.chat_input("Pergunte sobre seus gastos ou investimentos")

if pergunta:
    st.session_state.messages.append({"role": "user", "content": pergunta})

    with st.chat_message("user"):
        st.write(pergunta)

    resposta = gerar_resposta(pergunta, contexto)

    st.session_state.messages.append({"role": "assistant", "content": resposta})

    with st.chat_message("assistant"):
        st.write(resposta)
```
📦 requirements.txt
```
streamlit
openai
python-dotenv
pandas
```
