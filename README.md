# n8n-simple-chatbot-with-persistence


This repository demonstrates an example conversational AI workflow using:

- Ollama chat model
- Postgres chat memory
- PGVector vector store
- Ollama embeddings
- Hardware cooldown protection

<img width="1001" height="484" alt="Screenshot 2026-02-12 120446" src="https://github.com/user-attachments/assets/cf000ea5-8d0d-446c-acc5-a1c5ef8d3c9f" />

---

# 🧩 Workflow Components

## 1️⃣ Trigger — When Chat Message Received

- Activated whenever a user sends a message
- Entry point for conversational interaction

---

## 2️⃣ Hardware Cooldown

Purpose:
- Prevents overload of CPU/GPU resources
- Adds basic throttling between requests

In production, consider replacing with:
- Rate limiting
- Queue system
- Autoscaling workers
- Concurrency limits

---

## 3️⃣ AI Agent

The central orchestrator that:

- Receives user input
- Uses memory for conversational context
- Calls tools when needed (vector search)
- Generates final response

The agent connects to:

- A chat model
- A memory backend
- A vector store tool

---

## 4️⃣ Chat Model — Ollama

Local LLM used for:

- Conversation handling
- Tool calling
- Response generation

You may replace with:
- OpenAI
- Azure OpenAI
- Anthropic
- Any hosted or self-hosted LLM

---

## 5️⃣ Postgres Chat Memory

Stores:

- Conversation history
- Context per user/session
- Persistent state across interactions

You may replace with:
- Redis
- In-memory store
- Managed memory service
- Custom memory logic

---

## 6️⃣ Postgres PGVector Store (Tool)

Used by the AI Agent to:

- Perform semantic similarity search
- Retrieve relevant documents
- Enable RAG (Retrieval-Augmented Generation)

Stores:

- Document content
- Embedding vectors
- Metadata

You may replace with:
- Qdrant
- Weaviate
- Pinecone
- Milvus
- Any vector-capable database

---

## 7️⃣ Embeddings — Ollama

Generates vector embeddings for:

- Indexed documents
- User queries (for similarity search)

You may replace with:
- OpenAI embeddings
- Cohere
- Azure embeddings
- Self-hosted embedding models

Batching and concurrency limits should be tuned based on hardware capacity.

---

# 🔍 How It Works (Runtime Flow)

1. User sends message
2. Cooldown ensures system stability
3. AI Agent receives message
4. Agent:
   - Loads conversation memory
   - Decides whether to call PGVector tool
5. If needed:
   - Query is embedded
   - Similar documents retrieved
6. Agent generates final response using:
   - Retrieved context
   - Chat history
   - Model reasoning

---

# 🧱 Infrastructure Considerations

## Minimal (Local Development)

- Ollama running locally
- Local Postgres + PGVector
- Single-process execution
- Basic cooldown logic

## Production Setup

Recommended upgrades:

- Managed Postgres
- Connection pooling
- Queue-based throttling
- Horizontal scaling
- Observability (metrics + logs)
- Structured error handling
- Model version tracking

---

# 📝 Operational Notes

### 🔹 This Is a Reference Workflow
It demonstrates one possible configuration.  
It is not production-hardened by default.

### 🔹 Modify as Required
You should adjust:
- Embedding dimensions
- Index type (HNSW recommended)
- Memory retention policy
- Agent tool logic
- Security (auth, RBAC)
- Secrets management

### 🔹 Scaling Considerations
- Separate embedding service from chat model
- Add worker pools
- Use async vector queries
- Add caching for frequent queries

### 🔹 Observability
Track:
- Latency per request
- Embedding generation time
- Vector search time
- Token usage
- Error rates

---

# 🚀 Use Cases

- Internal knowledge assistant
- RAG-powered chatbot
- Technical documentation assistant
- Customer support AI
- Enterprise search interface

---

# ✅ Summary

This workflow demonstrates a modular AI agent architecture combining:

- Conversational memory
- Semantic retrieval
- Local LLM inference
- Vector search

It is designed to be modified and adapted to your environment.

**Use it as a template, not a final architecture.**

---

# ⚠️ Important Note

> **This is an example of an existing workflow configuration.**  
> It is intended as a reference implementation.

You are expected to modify:

- Models
- Memory backend
- Vector store
- Embedding provider
- Infrastructure components
- Scaling and throttling strategy

Adapt this workflow to your infrastructure, performance constraints, and security requirements.

---
