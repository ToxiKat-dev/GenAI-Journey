# GenAI Engineer Roadmap

Created Oct 9, 2026. Status column in the Learning path table is the source of truth for progress.

## Where you stand

A **self-paced path** from complete GenAI beginner to an interview-ready **GenAI / AI Engineer**, with three portfolio projects and a capstone. Work through the 30 steps in order, as many each day as you can. The core path is roughly 200–250 hours of focused work, so at 7+ hours a day it takes about a month; one project grows through the phases, and fine-tuning is kept to an overview.

You are not starting from zero. Most GenAI engineering is backend engineering with an LLM in the loop, and you already have most of that stack:

| What you have | How it carries over |
| --- | --- |
| Python backend | The main language of LangChain, LangGraph, LlamaIndex, RAGAS and Hugging Face |
| Node.js backend | LangChain.js and LangGraph.js exist with near-parity; a strong differentiator for product teams |
| MongoDB | Atlas Vector Search lets you build RAG in the database you already know, no new vector DB needed to start |
| Flutter | Streaming chat UIs and AI features in mobile apps; few GenAI engineers can ship the client too |
| 2y 9m production experience | APIs, auth, deployment, debugging: the part most GenAI tutorials skip and interviews test |

**Target roles:** GenAI Engineer, AI Engineer, Applied AI / LLM Engineer, or Fullstack Engineer (AI) at product companies and GCCs. Indian postings for 3–5 years ask for RAG pipelines, agent workflows with tool calling, LangChain/LangGraph, vector databases, evaluation and deployment ([Siemens](https://jobs.siemens.com/es_ES/externaljobs/JobDetail/505185), [Siemens Healthineers](https://jobs.siemens.com/es_ES/externaljobs/JobDetail/458847)). RAG and vector-database experience is the requirement that shows up most often ([Masai](https://www.masaischool.com/blog/the-ai-skills-indian-employers-are-actually-hiring-for-in-2026/)).

**Learn on the current stack:** LangChain and LangGraph both reached 1.0 in October 2025; agents are now built with `create_agent`, which runs on the LangGraph runtime ([LangChain blog](https://www.langchain.com/blog/langchain-langgraph-1dot0)). Many tutorials online still use the older chains and `create_react_agent` style, so prefer the official docs over old YouTube videos.

## Roadmap at a glance

```
0 Foundations (steps 1-3)  ->  1 LLM APIs (4-6)  ->  2 RAG (7-13)
-> 3 Agents + LangGraph (14-19)  ->  4 Production, LLMOps (20-25)  ->  5 Capstone + job prep (26-30)
```

RAG (phase 2) gets the most time because it is the skill Indian GenAI postings ask for most; every later phase builds on that project.

## Phases in detail

Each phase ends with working code on GitHub. Python first (most jobs use it), with key parts ported to Node. Every phase also carries a **production habit**: the engineering practice your previous jobs skipped, taught where it naturally comes up.

### Phase 0 — Foundations from zero

**Learn:** what AI, machine learning, deep learning and GenAI are, and how they differ; how a model learns (data, loss, gradient descent); neural networks to transformers (tokens, embeddings, attention, next-token prediction); the model landscape (closed vs open models, context windows, pricing, hallucination, temperature and top-p); Python for AI (uv or venv, Jupyter, NumPy, pandas).

**Resources:** 3Blue1Brown *Neural Networks* series (YouTube); Andrej Karpathy, *Intro to Large Language Models*; Jay Alammar, *The Illustrated Transformer*.

**Production habit:** config and secrets — one settings module, `.env` never committed, separate dev and prod config.

- [ ] Can explain tokens, embeddings, attention and temperature without notes
- [ ] Computed embeddings and cosine similarity by hand in NumPy

### Phase 1 — LLM APIs

**Learn:** calling OpenAI, Anthropic and Gemini directly, without a framework; prompt patterns (system prompts, few-shot, chain-of-thought, delimiters); structured output with Pydantic; tool (function) calling by hand; streaming; token and cost math.

**Resources:** the official API docs of OpenAI and Anthropic (prompting and tool-use guides); DeepLearning.AI *ChatGPT Prompt Engineering for Developers*.

**Production habit:** validation at the API boundary, a consistent error format, structured logs with request IDs, timeouts on every external call, and the first pytest tests.

**Project 1 — Smart expense parser:** FastAPI endpoint that turns a receipt photo or text into validated JSON, a Flutter screen that streams the reply, and cost logged per call.

### Phase 2 — RAG, the core skill

**Learn:** RAG built twice, first from scratch and then with LangChain 1.0; chunking strategies and document loaders; **MongoDB Atlas Vector Search** with metadata filters; hybrid search (vector + keyword) and reranking; query rewriting and multi-query; citations; evaluation with RAGAS (faithfulness, answer relevance, context precision and recall); one dedicated vector DB (Qdrant) for comparison.

**Resources:** LangChain docs RAG tutorial; MongoDB Atlas Vector Search docs and its LangChain integration; RAGAS docs.

**Production habit:** MongoDB indexes and cursor-based pagination done right; slow work (document ingestion) moved to a background job queue; idempotent uploads.

**Project 2 — Docs Q&A with citations:** upload PDFs, ask questions, get answers with page citations. Includes a 30-question eval set and a before/after table of scores in the README.

### Phase 3 — Agents and LangGraph

**Learn:** the agent loop; LangChain `create_agent`, tools and middleware; LangGraph state, nodes, edges and routing; memory (MongoDB checkpointer, long-term store); human-in-the-loop interrupts; agentic RAG and multi-agent patterns (supervisor, handoffs); **MCP**, by building your own MCP server.

**Resources:** LangChain Academy *Introduction to LangGraph* (free); LangGraph docs; modelcontextprotocol.io quickstarts; Anthropic, *Building effective agents*.

**Production habit:** retries with backoff, rate limits, and per-user authorization inside every tool so the agent can only touch the caller's data.

**Project 3 — Support agent (grows from Project 2):** answers from docs, looks up orders in MongoDB through tools, asks a human before refunds, exposes its tools as an MCP server.

### Phase 4 — Production, LLMOps and open models

**Learn:** tracing (Langfuse or LangSmith); evals running in GitHub Actions on every change; OWASP Top 10 for LLM apps, prompt injection, PII redaction and guardrails; exact and semantic caching, model routing and provider fallbacks; Docker and cloud deployment; open models with Ollama and Hugging Face, and when fine-tuning (LoRA) is worth it.

**Resources:** Chip Huyen, *AI Engineering* (O'Reilly) — read the chapters on evaluation and inference optimisation; Langfuse docs; OWASP LLM Top 10.

**Production habit:** CI/CD, short-lived access tokens with refresh, cost and latency dashboards, and a written rollback plan.

**Deliverable:** Projects 2–3 live at public URLs with tracing and evals, plus a table comparing a local model to the API model on quality, latency and cost.

### Phase 5 — Capstone and job prep

**Capstone:** an AI assistant app built from the pieces you already have — Flutter client with streaming chat, a Python LangGraph service, a Node gateway for auth and rate limits, MongoDB for users, history and vectors, deployed with tracing, evals and guardrails. Because it reuses Projects 2–3, it comes together quickly.

**Portfolio checklist for every project:** README with an architecture diagram, eval scores, cost and latency numbers, and what did not work; a 2-minute demo video at the top; a live link.

**Job prep:**

1. Resume headline "Fullstack + GenAI Engineer" and an AI Projects section with numbers.
2. Interview topics: RAG trade-offs, debugging retrieval, evaluating LLM apps, agent failure modes, prompt injection, cost control.
3. Two mock interviews with me, including a system-design round ("a support chatbot for 1M users").
4. Apply to product companies, AI-first startups and GCCs on LinkedIn, Wellfound, Instahyre and career pages; ask for referrals; 5–10 tailored applications a day once the capstone is live.

## How each day works

No fixed hours or sessions: work as long as you can, and repeat this loop for each step.

1. **Learn** the step's concept: docs, a lesson or a video, with notes.
2. **Code it with me** in small exercises until you can do it without help.
3. **Build** it into the current project.
4. **Harden** it: tests, error handling, and the phase's production habit.
5. **Ship**: push to GitHub, write 5 lines of notes, take a quick quiz, mark the step done.

**Rules that keep you on track:** finish a step before starting the next; push to GitHub every day; stuck for more than 45 minutes, ask me; take real breaks and sleep 7+ hours — long days only work if you stay rested.

**How we work:** open a chat and say "Step N". I'll teach the concepts, give exercises, review your code with a production lens, and point out every gap I see in how you'd build it.

## Learning path

Thirty steps in order. Most take about a full day of focused work; do more than one a day when they go fast, and never skip ahead. Set the status as you go.

| Step | Phase | Learn | Build | Status |
| --- | --- | --- | --- | --- |
| 1 | 0 Foundations | AI vs ML vs DL vs GenAI; how models learn (loss, gradient descent) | Python for AI setup: uv, Jupyter, NumPy, pandas; config and `.env` hygiene | Not started |
| 2 | 0 Foundations | Neural nets to transformers: tokens, embeddings, attention | Tokenize text, compute embeddings and cosine similarity in NumPy | Not started |
| 3 | 0 Foundations | Model landscape: closed vs open, context, pricing, sampling, hallucination | First raw API calls in Python and Node; timeouts and a settings module | Not started |
| 4 | 1 LLM APIs | Prompt engineering: system prompts, few-shot, chain-of-thought | Structured output with Pydantic; FastAPI project skeleton and error format | Not started |
| 5 | 1 LLM APIs | Tool calling by hand; streaming | Project 1 API: expense parser; structured logs and request IDs | Not started |
| 6 | 1 LLM APIs | Streaming to Flutter over SSE | Project 1 Flutter screen; pytest tests, cost logging, README | Not started |
| 7 | 2 RAG | RAG concepts; embedding models; similarity search | RAG from scratch in Python, no framework | Not started |
| 8 | 2 RAG | Chunking strategies; PDF loaders | MongoDB Atlas Vector Search: index, `$vectorSearch`, filters; indexes and pagination | Not started |
| 9 | 2 RAG | LangChain 1.0 basics: models, prompts, splitters, retrievers | Rebuild RAG with LangChain + Atlas | Not started |
| 10 | 2 RAG | Hybrid search and reranking | Query rewriting, multi-query, page citations | Not started |
| 11 | 2 RAG | RAG evaluation with RAGAS; a 30-question test set | Measure baseline, improve, record before/after scores | Not started |
| 12 | 2 RAG | Background job queues; idempotent uploads | Project 2 ingestion pipeline and chat UI with citations | Not started |
| 13 | 2 RAG | Qdrant comparison; LangChain.js retrieval | Project 2 polish, README with eval table | Not started |
| 14 | 3 Agents | Agent loop; LangChain `create_agent`, tools, middleware | First agent with three tools | Not started |
| 15 | 3 Agents | LangGraph: state, nodes, edges, routing | Rebuild the agent as a graph | Not started |
| 16 | 3 Agents | Memory: MongoDB checkpointer, long-term store | Human-in-the-loop interrupts | Not started |
| 17 | 3 Agents | Agentic RAG; multi-agent (supervisor, handoffs) | Project 3 support agent; per-user authorization in tools | Not started |
| 18 | 3 Agents | MCP: build your own MCP server | Connect the agent to it; retries, backoff, rate limits | Not started |
| 19 | 3 Agents | Agent failure modes; testing agents | Project 3 polish, README | Not started |
| 20 | 4 Production | Tracing with Langfuse or LangSmith | Instrument Projects 2–3; cost and latency dashboard | Not started |
| 21 | 4 Production | Evals in CI with GitHub Actions | Unit and integration tests for the APIs | Not started |
| 22 | 4 Production | OWASP LLM Top 10, prompt injection, PII, guardrails | Auth done right: short-lived tokens, refresh, authorization checks | Not started |
| 23 | 4 Production | Exact and semantic caching; model routing; fallbacks | Implement them in Projects 2–3 | Not started |
| 24 | 4 Production | Docker and cloud deployment | Deploy Projects 2–3 live; start resume rewrite | Not started |
| 25 | 4 Production | Open models: Ollama, Hugging Face, when to fine-tune, LoRA | Swap Project 2 to a local model; comparison table | Not started |
| 26 | 5 Capstone | Capstone design: architecture, API contract, data model | Capstone backend: LangGraph service + Node gateway | Not started |
| 27 | 5 Capstone | Flutter streaming chat client | RAG over the user's own documents | Not started |
| 28 | 5 Capstone | Capstone tracing, evals, guardrails | Deploy; demo video, README, blog post | Not started |
| 29 | 5 Job prep | Interview prep: RAG and agent concepts | Mock system-design interview with me | Not started |
| 30 | 5 Job prep | Resume, LinkedIn and GitHub profile | Second mock interview; apply to the first 10 roles | Not started |
