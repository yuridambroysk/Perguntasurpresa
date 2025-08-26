# Retro Questions Bot (FastAPI)

Gere **perguntas engraçadas para retrospectivas** e incorpore a UI no **Miro** via iframe/app.

## 🚀 Rodando localmente

```bash
python -m venv .venv && source .venv/bin/activate  # (Windows: .venv\Scripts\activate)
pip install -r requirements.txt
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```
Acesse: http://localhost:8000

## 🐳 Docker

```bash
docker build -t retro-bot:latest .
docker run --rm -p 8000:8000 retro-bot:latest
```

## 🔌 Endpoints principais
- `GET /health` — status
- `GET /categories` — lista de categorias
- `GET /questions?category=Comida%20%26%20Bebidas&shuffle=true&limit=20` — lista perguntas (filtros opcionais)
- `GET /random?category=Animais` — retorna 1 pergunta aleatória (opcional filtrar por categoria)
- `POST /add` — adiciona nova pergunta (headers: `X-Admin-Token` se definir `ADMIN_TOKEN` no ambiente)

## 🧭 Front-end embutido
A UI está em `/` e foi feita para rodar em **iframe**. Você pode usá-la direto ou criar seu front próprio.

## 🧩 Como **incorporar no Miro**
Opções comuns:
1) **Embed Website / iFrame**: cole a URL pública da sua aplicação no board.
2) **Miro App (Web SDK)**: crie um app simples que abre um painel apontando para a URL do seu bot (esta página `index.html`).  
   - No front do app (JS), use `miro.board.ui.openPanel({url: "https://SEU_DOMINIO/"})`.

> Observação: deixe sua URL pública acessível (sem autenticação) ou use regras de token que seu time possa usar.

## 🔐 Segurança (opcional)
- Defina `ADMIN_TOKEN` no ambiente para proteger o endpoint `POST /add`.
- Se publicar atrás de Nginx, não envie `X-Frame-Options: DENY`. Este projeto não seta esse cabeçalho.

## 🗃️ Banco de perguntas
O arquivo `app/questions.json` contém 100+ perguntas categorizadas.  
Você pode editar esse JSON e reiniciar o servidor para atualizar o conteúdo.

---

Feito com ❤️ em FastAPI.
