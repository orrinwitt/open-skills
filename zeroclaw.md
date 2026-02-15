---
name: zeroclaw
description: Use Zeroclaw as an AI app/runtime with configurable LLM provider and API key environment variables.
---

# Zeroclaw

GitHub: https://github.com/theonlyhennygod/zeroclaw

Logo CID: `Qmex7mP7CtY1uo7a2erXmuNrvQdY6aw5FTQtxpJjAbiu8v`

## Environment variables

### Required

- `API_KEY` or `ZEROCLAW_API_KEY` — Your LLM provider API key

### Optional

- `PROVIDER` or `ZEROCLAW_PROVIDER` — LLM provider (default: `openrouter`)
  - Options: `openrouter`, `openai`, `anthropic`, `ollama`

## Example

```bash
export ZEROCLAW_API_KEY="your_api_key"
export ZEROCLAW_PROVIDER="openrouter"
```
