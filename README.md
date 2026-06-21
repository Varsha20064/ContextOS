# 🚀 ContextOS Proxy
### The Operating Layer for AI Context

> **Smarter Context. Lower Cost. Better AI.**

ContextOS Proxy is an **OpenAI-compatible semantic context gateway** that sits transparently between AI applications and Large Language Models (LLMs).

Instead of sending raw documents directly to an LLM, ContextOS Proxy intercepts every request, retrieves relevant knowledge from a semantic graph, optimizes the context, intelligently routes the request to the best model, and returns a fully OpenAI-compatible response.

No changes to application logic.
Simply replace your API endpoint.

<img width="1600" height="723" alt="image" src="https://github.com/user-attachments/assets/e7010b9f-006e-41cf-a5b7-ed69d31289a9" />

---

## 📖 Why ContextOS?

The biggest challenge in AI today isn't the model.

It's the **context**.

Modern AI applications retrieve thousands of tokens from documents, repositories, Slack conversations, APIs, and databases—even when only a few facts are actually needed.

This leads to:

- 💸 High inference costs
- 🐢 Slow responses
- 🤯 Hallucinations
- 📚 Irrelevant context
- 🔍 Poor explainability
- 🔧 Complex prompt engineering

ContextOS Proxy solves this by making **context intelligent** before it reaches the model.

---

# ⚡ How It Works

```text
Application
      │
      ▼
ContextOS Proxy
      │
      ▼
Prompt Interceptor
      │
      ▼
Semantic Graph Engine
      │
      ▼
Context Optimizer
      │
      ▼
Prompt Compiler
      │
      ▼
Model Router
      │
      ▼
OpenAI / FastRouter / Claude / Gemini
      │
      ▼
Optimized Response
```
<img width="1226" height="911" alt="image" src="https://github.com/user-attachments/assets/e4893a9a-0344-49f3-a3fc-9ae001e938a6" />

---

# ✨ Features

<img width="1600" height="703" alt="image" src="https://github.com/user-attachments/assets/89e2a720-0c29-4a0d-af65-8fa09f6421c9" />

## 🧠 Semantic Knowledge Graph

Convert documents into structured knowledge.

Instead of

```
OrbitGuard uses CelesTrak.
OrbitGuard uses LSTM.
```

ContextOS stores

```
OrbitGuard
    │
    ├── uses ───────► CelesTrak
    ├── model ──────► LSTM
    └── predicts ───► Collision Risk
```

Retrieval happens over relationships—not raw text.

---

## ⚡ Context Optimization

Before an LLM receives a prompt, ContextOS:

- removes duplicate context
- ranks relevance
- compresses information
- respects token budgets
- calculates token savings

Result:

- lower cost
- lower latency
- better responses

---

## 🔀 Intelligent Model Routing

Automatically select the best model.

```
Simple Summary
        │
        ▼
GPT-4.1 Mini

Reasoning
        │
        ▼
GPT-4.1

Coding
        │
        ▼
Claude

Low-cost Tasks
        │
        ▼
FastRouter
```

Developers simply use

```python
model="auto"
```

---

## 🔍 Semantic Retrieval

Traditional RAG retrieves text.

ContextOS retrieves knowledge.

Instead of

```
20 pages of documentation
```

the model receives

```
Authentication Service

↓

uses OAuth

↓

depends on Redis

↓

calls User Database
```

---

## 📊 Token Analytics

Every request returns

- Original Tokens
- Optimized Tokens
- Compression Ratio
- Estimated Cost Savings
- Model Used

---

## 🎥 Replay & Observability

Replay every request.

See

- Original Prompt
- Optimized Prompt
- Retrieved Graph Facts
- Model Selected
- Tokens Saved
- Final Response

Perfect for debugging AI systems.

---

# 🚀 Installation

```bash
git clone https://github.com/<username>/contextos-proxy

cd contextos-proxy

pip install -e .
```

---

# 🔑 Environment

Create

```
.env
```

```
OPENAI_API_KEY=

FASTROUTER_API_KEY=

DEFAULT_PROVIDER=openai

TOKEN_BUDGET=4000
```

---

# ▶️ Running the Proxy

```bash
uvicorn contextos_proxy.server:app --host 0.0.0.0 --port 8787
```

The proxy now behaves like an OpenAI endpoint.

---

# 💻 Usage

Instead of

```python
from openai import OpenAI

client = OpenAI(api_key="OPENAI_KEY")
```

use

```python
from openai import OpenAI

client = OpenAI(
    api_key="contextos-local",
    base_url="http://localhost:8787/v1"
)

response = client.chat.completions.create(
    model="auto",
    messages=[
        {
            "role":"user",
            "content":"Explain OrbitGuard architecture"
        }
    ]
)
```

No other code changes are required.

---

# 📂 Ingest Knowledge

```bash
contextos-proxy ingest docs/
```

or

```bash
POST /v1/context/ingest
```

ContextOS automatically

- extracts entities
- builds relationships
- creates semantic graph
- indexes knowledge

---

# 📡 API

### Chat Completion

```
POST /v1/chat/completions
```

OpenAI-compatible.

---

### Ingest Context

```
POST /v1/context/ingest
```

---

### Graph

```
GET /v1/graph
```

---

### Replay

```
GET /v1/replay/{id}
```

---

### Stats

```
GET /v1/stats
```

---

# 🏗 Project Structure

```
contextos-proxy/

├── contextos_proxy/
│
├── semantic_graph.py
├── context_optimizer.py
├── prompt_compiler.py
├── router.py
├── replay.py
├── providers/
├── storage/
│
├── examples/
│
├── tests/
│
└── README.md
```

---

# 🎯 Use Cases

✅ Enterprise AI Copilots

✅ Coding Assistants

✅ IDE Extensions

✅ Customer Support AI

✅ Internal Knowledge Bases

✅ Autonomous Agents

✅ Multi-Agent Systems

✅ RAG Applications

---

# 📈 Why ContextOS?

| Traditional RAG | ContextOS Proxy |
|-----------------|-----------------|
| Retrieves document chunks | Retrieves semantic relationships |
| Large prompts | Optimized prompts |
| Manual prompt engineering | Automatic prompt compilation |
| Static retrieval | Context-aware retrieval |
| Single model | Intelligent model routing |
| No replay | Full observability |
| High token cost | Cost-aware optimization |

---

# 🛣 Roadmap

- Multi-agent orchestration
- Distributed semantic graphs
- Enterprise connectors
- Policy engine
- Context caching
- Hybrid graph + vector retrieval
- Local LLM support
- Kubernetes deployment
- AI Context Operating System

---

# 🤝 Contributing

Contributions are welcome!

Please open an issue or submit a pull request.

---

# 📜 License

MIT License

---

# 🌍 Vision

The future of AI isn't about building bigger models.

It's about giving models the right knowledge at the right time.

ContextOS Proxy is building the infrastructure that every future AI application will rely on.

**Instead of making models smarter, we make context smarter.**
