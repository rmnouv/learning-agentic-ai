# Learning Agentic AI — hands-on with Claude

A build-first course. You'll construct real agents from scratch on the Claude API,
understand *why* each piece exists, then graduate to a framework and a deployable service.

> **What is an "agent"?** A plain LLM call is one shot: text in, text out. An **agent** is
> an LLM placed inside a **loop** and given **tools** it can choose to call. The model
> decides *what to do next* — call a tool, read the result, call another, or answer — and
> keeps going until the task is done. That decision-in-a-loop is the whole idea. Everything
> else (memory, frameworks, multi-agent) is built on top of it.

## Setup (one time)

1. **Get an API key** — https://console.anthropic.com/ → Settings → API Keys.
2. **Add it:** copy `.env.example` to `.env` and paste your key.
   ```bash
   cp .env.example .env      # then edit .env
   ```
3. **Install deps** (already done for you, but for a fresh machine):
   ```bash
   python -m pip install -r requirements.txt
   ```
4. **Launch Jupyter** (the `jupyter` command isn't on PATH here, so use `python -m`):
   ```bash
   python -m jupyterlab
   ```
   Then open `notebooks/01_agent_from_scratch.ipynb`.

> **Notebook vs. real system:** notebooks are perfect for *learning and prototyping* an
> agent — the loop, tools, and in-session memory all run inside the kernel. Their limit is
> that state lives only while the kernel is alive, and they aren't how you deploy a
> long-running or multi-user agent. Module 6 shows how to move the same code into a `.py`
> service.

## Curriculum

| # | Module | You build | Status |
|---|--------|-----------|--------|
| 0 | Setup | Env + key + Jupyter | ✅ done |
| 1 | **The agent loop from scratch** | A tool-using agent with a hand-written loop | ✅ `notebooks/01_agent_from_scratch.ipynb` |
| 2 | Real tools & robustness | Multi-tool agent, error handling, parallel tool calls | ⬜ next |
| 3 | Memory & conversation | Multi-turn state, context management | ⬜ |
| 4 | Less boilerplate | The SDK `tool_runner` — same agent, fewer lines | ⬜ |
| 5 | A framework | Rebuild in LangGraph; compare to raw | ⬜ |
| 6 | Ship it | Notebook → `.py` service; intro to Managed Agents | ⬜ |

Work through them in order — each builds on the last. Start with Module 1.

## Mental model you're building toward

```
                 ┌──────────────────────────────────────────┐
   user msg ───▶ │  while not done:                          │
                 │     resp = model(messages, tools)         │
                 │     if resp wants a tool:                 │
                 │         run tool → append result          │  ◀── the agent loop
                 │     else:                                 │
                 │         done  → return resp.text          │
                 └──────────────────────────────────────────┘
```

Notebook 01 implements exactly this. Once it clicks, the rest is variations on it.
