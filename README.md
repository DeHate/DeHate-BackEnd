
# .DeHate - API de Moderação de Comentários Ofensivos

**.DeHate** é uma API desenvolvida em **Python com FastAPI** que conecta-se à conta do YouTube de um criador de conteúdo, coleta os vídeos e comentários de seu canal e utiliza uma LLM (Large Language Model) para detectar e remover automaticamente comentários ofensivos.
 
---

## 📌 Índice

- [🚀 Funcionalidades](#-funcionalidades)
- [🧠 Tecnologias Utilizadas](#-tecnologias-utilizadas)
- [🧩 Estrutura do Projeto](#-estrutura-do-projeto)
- [⚙️ Configuração do Ambiente](#️-configuração-do-ambiente)
- [▶️ Como Executar](#️-como-executar)
- [📡 Endpoints Disponíveis](#-endpoints-disponíveis)

---

## 🚀 Funcionalidades

- Autenticação via OAuth2 com o Google/YouTube
- Listagem de vídeos (mídias) do canal autenticado
- Filtros por número de visualizações, curtidas e comentários
- Detecção de comentários ofensivos com LLM (Google Gemini)
- Remoção automática dos comentários detectados como negativos

---

## 🧠 Tecnologias Utilizadas

- **Python 3.13.3**
- **FastAPI** — Framework web assíncrono
- **Pydantic** — Validação de dados
- **Google API Client** — Integração com YouTube
- **Google Generative AI (Gemini)** — Classificação de comentários
- **OAuth 2.0** — Autenticação segura
- **python-dotenv** — Gerenciamento de variáveis de ambiente

---

## 🧩 Estrutura do Projeto

```
dehate/
├── app/
│   ├── main.py
│   ├── core/
│   ├── api/
│   ├── domain/
│   ├── interfaces/
│   ├── services/
│   └── infrastructure/
├── tests/
├── .env
├── requirements.txt
└── README.md
```

---

## ⚙️ Configuração do Ambiente

1. Crie um arquivo `.env` na raiz do projeto com as seguintes variáveis de ambiente:

```
REDIRECT_URI=http://localhost:8000/auth/callback
GEMINI_API_KEY=your-gemini-api-key
FRONTEND_URL=meuapp://auth
```

2. Adicione também o arquivo `client_secret.json` (obtido no [Google Developer Console](https://console.cloud.google.com/)) com suas credenciais OAuth2.

---

## ▶️ Como Executar

1. Crie um ambiente virtual:

```
python -m venv .venv
```

2. Ative o ambiente:

```
.venv\Scripts\activate
```

3. Instale as dependências:

```
pip install -r requirements.txt
```

4. Execute o servidor:

```
uvicorn app.main:app --reload
```

A API estará disponível em:  
👉 `http://localhost:8000`

Documentação Swagger:  
👉 `http://localhost:8000/docs`

Para maiores informações, consulte os arquivos em "infos".

---

## 📡 Endpoints Disponíveis

### 🔐 Autenticação

- `GET /auth/login`  
  Redireciona o usuário para o login via Google OAuth.

- `GET /auth/callback`  
  Processa o código de autorização e gera o token.

---

### 🎞️ Mídias

- `GET /medias/`  
  Lista os vídeos do canal com filtros e ordenação.

- `POST /medias/clean-comments`  
  Limpa comentários ofensivos de mídias informadas.

**Exemplo de requisição:**

```
["abc123", "def456"]
```
