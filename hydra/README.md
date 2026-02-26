# HYDRA

**Part of [The Cartu Method](../README.md) — Component 2: Inference Routing**

A multi-headed inference proxy that routes AI agent traffic across frontier models, translates between API formats, and auto-escalates on quality failures — cutting costs dramatically without losing output quality.

> One proxy. Multiple model heads. Intelligent routing. Quality gating. Zero compromises.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.100+-green.svg)](https://fastapi.tiangolo.com/)

---

## The Problem

Running autonomous AI agents 24/7 is expensive. A single Opus-class model at $15/$75 per million tokens burns through $200-600/month on background tasks alone — cron jobs, monitoring, reports, health checks. Most of these tasks don't *need* frontier reasoning. But downgrading to cheaper models introduces formatting errors, hallucinations, and quality regressions that silently corrupt your agent's output.

**The choice shouldn't be "expensive and good" vs "cheap and broken."**

## The Solution

HYDRA is a transparent proxy that sits between your AI agent framework and your LLM providers. It exposes an **OpenAI-compatible** `/v1/chat/completions` API on the client side and internally translates to each provider's native format (e.g., Anthropic Messages API for Claude models). Your agent talks standard OpenAI — HYDRA handles the rest.

```
                         ┌──────────────┐
                         │   AI Agent   │
                         │  (Nanobot)   │
                         └──────┬───────┘
                                │ OpenAI-compatible API
                         ┌──────▼───────┐
                         │    HYDRA     │
                         │  :8300       │
                         └──┬───┬───┬───┘
                            │   │   │
              ┌─────────────┤   │   ├─────────────┐
              │             │   │   │             │
        ┌─────▼─────┐ ┌────▼───▼┐ ┌▼─────────┐ ┌▼──────────┐
        │  Opus 4.6 │ │Sonnet   │ │ MiniMax   │ │ Cerebras  │
        │(Anthropic)│ │  4.5    │ │ M2.5      │ │ GLM-4.7   │
        │ $15/$75   │ │ $3/$15  │ │$0.30/$2.40│ │$0.60/$0.60│
        │ Reasoning │ │Mid-tier │ │ Bulk AI   │ │Compaction │
        └───────────┘ └─────────┘ └───────────┘ └───────────┘
```

### The Heads

| Head | Model | Alias | Role | Cost/MTok (in/out) | Quality Gate |
|------|-------|-------|------|--------------------|--------------|
| **Opus** | Claude Opus 4.6 | `cartu-proxy/claude-opus-4-6` | Interactive chat, complex reasoning | $15/$75 | None (top-tier) |
| **Sonnet** | Claude Sonnet 4.5 | `cartu-proxy/claude-sonnet-4-5` | Mid-tier tasks | $3/$15 | Disabled (quality high enough) |
| **MiniMax** | MiniMax-M2.5 | `cartu-proxy/minimax-m2.5-highspeed` | Background tasks, crons, sub-agents | $0.30/$2.40 | Enabled (threshold 0.7) |
| **Cerebras** | GLM-4.7 | `cartu-proxy/cerebras-glm-4-7` | Context compaction (summarization) | $0.60/$0.60 | Enabled (threshold 0.7) |

## Architecture

### 1. Intelligent Routing

When a request arrives, HYDRA inspects the `model` field and routes to the correct upstream provider:

```python
# Agent requests "cartu-proxy/minimax-m2.5-highspeed"
#   → Routes to MiniMax API (cheap, fast)
#
# Agent requests "cartu-proxy/claude-opus-4-6"
#   → Routes to Anthropic API, translates OpenAI ↔ Anthropic format
#
# Agent requests "cartu-proxy/cerebras-glm-4-7"
#   → Routes to Cerebras (2000+ tok/s compaction)
#
# Agent requests "cartu-proxy/claude-sonnet-4-5"
#   → Routes to Anthropic API (mid-tier, cost-effective)
```

The agent framework controls which model to use per-task. Interactive chat gets Opus. Cron jobs get MiniMax. Compaction gets Cerebras. The proxy handles format translation, quality gating, and cost tracking.

### 2. Format Translation

HYDRA accepts OpenAI-format requests and translates them to each provider's native format:

- **Anthropic providers** (Opus, Sonnet): Translates OpenAI `messages` to Anthropic Messages API format, including system prompts, tool definitions, and tool_choice mapping. Responses are converted back to OpenAI format.
- **OpenAI-compatible providers** (MiniMax, Cerebras): Forwards directly with model field rewriting.

Streaming is supported for both provider types — Anthropic SSE events are translated to OpenAI-format chunks on the fly.

### 3. The Quality Gate

The critical innovation: **pre-flight quality scoring on cheap model outputs.**

When a quality-gated model (MiniMax or Cerebras) handles a **non-streaming** request, HYDRA doesn't just forward the response blindly. It:

1. **Sends the request to the cheap model** (non-streaming, for inspection)
2. **Scores the response** (0.0 → 1.0) across 5 weighted dimensions:
   - **Completeness** (25%) — Does the response address the prompt? Checks for empty/truncated/refused responses.
   - **Code Quality** (20%) — If code is present, checks balanced delimiters, Python syntax, placeholder detection.
   - **Instruction Following** (25%) — Did it follow requested format (JSON, numbered lists, tables, step-by-step)?
   - **Hallucination** (15%) — Detects fabricated references, suspicious URLs, false memory claims.
   - **Coherence** (15%) — Checks for repetitive loops, language switching, self-contradictions.
3. **If score >= 0.7**: Forward the cheap response to the client
4. **If score < 0.7**: Auto-escalate to Opus and return that instead

```python
score = score_response(prompt_text, response_text)

if score.overall >= threshold:  # default 0.7
    return cheap_response        # ~$0.001
else:
    escalated = escalate_to_opus(original_request)
    return escalated              # ~$0.20
```

**Additional safeguards:**

- **Circuit breaker**: If the escalation rate in a sliding window of 50 requests exceeds 50%, the circuit breaker opens and cheap responses pass through without escalation (prevents runaway Opus costs).
- **Tool-call bypass**: Responses containing tool_calls skip quality scoring (structured machine-consumed output doesn't benefit from heuristic text scoring).
- **Streaming bypass**: Streaming requests to quality-gated models skip the gate and stream directly (latency-sensitive path).
- **Escalation failure fallback**: If the Opus escalation itself fails, the cheap response is returned rather than erroring.

**Production results (Feb 20, 2026):**
- 173 MiniMax requests processed
- 100% quality gate pass rate (post prompt-tuning)
- 0 escalations to Opus
- $0.73 total MiniMax spend vs ~$50+ equivalent on Opus

> **Note:** These results are from initial testing. Actual quality gate pass rates and cost savings will vary depending on workload complexity, prompt quality, and task types.

### 4. Cerebras Compaction Engine

When the agent framework triggers context compaction (summarizing conversation history to free tokens), HYDRA routes it to **Cerebras GLM-4.7** — a model optimized for pure speed:

- **2,000+ tokens/second** (vs ~30 tok/s on Opus)
- **$0.60/MTok** (vs $75/MTok output on Opus)
- Perfect for summarization tasks where speed matters more than reasoning depth

The compaction is transparent — the agent requests the Cerebras alias, gets a response 60x faster at 1/125th the cost.

### 5. Error Handling

If an upstream provider returns an error, HYDRA returns the error to the client with appropriate status codes and error details. There is no automatic failover between providers — the agent framework is responsible for choosing which model to use.

The only "fallback" behavior is within the quality gate: if an escalation to Opus fails, the original cheap model response is returned rather than propagating the error.

## Real-World Results

Production benchmarks from a 24/7 autonomous agent handling 25+ daily cron jobs, interactive chat, sub-agent orchestration, and browser automation:

| Metric | Opus Only | HYDRA Pipeline |
|--------|-----------|----------------|
| Daily cost (background tasks) | ~$50-80 | ~$0.73 |
| Compaction latency | 8-12s | 0.3-0.5s |
| Quality gate pass rate | N/A | 100% |
| Models utilized | 1 | 4 |

> **Note:** These figures are from initial testing and actual results will vary depending on usage patterns, request volume, and workload mix.

## Installation

```bash
pip install fastapi uvicorn httpx python-dotenv

# Clone and configure
cd ~/cato-system/hydra
cp .env.example .env
# Edit .env with your API keys:
#   MINIMAX_API_KEY, CEREBRAS_API_KEY, ANTHROPIC_API_KEY
#   HYDRA_API_KEY (optional — for authenticating clients)

# Run
uvicorn proxy:app --host 0.0.0.0 --port 8300
# or simply:
python proxy.py
```

## Configuration

```python
# config.py

PORT = int(os.getenv("HYDRA_PORT", "8300"))

PROVIDERS = {
    "minimax": {
        "endpoint": "https://api.minimaxi.com/v1/chat/completions",
        "auth_header": "Authorization",
        "auth_prefix": "Bearer ",
        "api_key_env": "MINIMAX_API_KEY",
        "pricing": {"input": 0.30, "output": 2.40},
        "timeout": 60,
    },
    "cerebras": {
        "endpoint": "https://api.cerebras.ai/v1/chat/completions",
        "auth_header": "Authorization",
        "auth_prefix": "Bearer ",
        "api_key_env": "CEREBRAS_API_KEY",
        "pricing": {"input": 0.60, "output": 0.60},
        "role": "compaction_only",
        "timeout": 15,
    },
    "anthropic-opus": {
        "endpoint": "https://api.anthropic.com/v1/messages",
        "api_key_env": "ANTHROPIC_API_KEY",
        "anthropic": True,
        "pricing": {"input": 15.0, "output": 75.0},
        "timeout": 120,
    },
    "anthropic-sonnet": {
        "endpoint": "https://api.anthropic.com/v1/messages",
        "api_key_env": "ANTHROPIC_API_KEY",
        "anthropic": True,
        "pricing": {"input": 3.0, "output": 15.0},
        "timeout": 120,
    },
}

# Quality gate defaults (overridable via env vars)
QUALITY_GATE_DEFAULT_THRESHOLD = 0.7  # QUALITY_GATE_THRESHOLD env var
QUALITY_GATE_ESCALATION_MODEL = "claude-opus-4-6"
QUALITY_GATE_ESCALATION_PROVIDER = "anthropic-opus"

MODEL_ALIASES = {
    "cartu-proxy/minimax-m2.5-highspeed": {
        "provider": "minimax",
        "upstream_model": "MiniMax-M2.5",
        "quality_gate": {"enabled": True, "threshold": 0.7, ...},
    },
    "cartu-proxy/claude-opus-4-6": {
        "provider": "anthropic-opus",
        "upstream_model": "claude-opus-4-6",
        # No quality gate
    },
    "cartu-proxy/claude-sonnet-4-5": {
        "provider": "anthropic-sonnet",
        "upstream_model": "claude-sonnet-4-5-20250514",
        "quality_gate": {"enabled": False, ...},  # Disabled
    },
    "cartu-proxy/cerebras-glm-4-7": {
        "provider": "cerebras",
        "upstream_model": "zai-glm-4.7",
        "quality_gate": {"enabled": True, "threshold": 0.7, ...},
    },
}
```

### Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `HYDRA_PORT` | `8300` | Port to listen on |
| `HYDRA_API_KEY` | (empty) | API key for client auth (disabled if empty) |
| `MAX_OUTPUT_TOKENS` | `16384` | Max output tokens cap per request |
| `QUALITY_GATE_THRESHOLD` | `0.7` | Default quality score threshold |
| `QUALITY_GATE_ESCALATION_MODEL` | `claude-opus-4-6` | Model to escalate to |
| `QUALITY_GATE_ESCALATION_PROVIDER` | `anthropic-opus` | Provider for escalation |
| `QUALITY_GATE_CIRCUIT_BREAKER_RATE` | `0.5` | Max escalation rate before circuit opens |
| `COST_LOG_PATH` | `/app/data/cost.jsonl` | Path for cost log file |
| `ESCALATION_LOG_PROMPTS` | `false` | Include prompt text in escalation logs |
| `MINIMAX_API_KEY` | — | MiniMax API key |
| `CEREBRAS_API_KEY` | — | Cerebras API key |
| `ANTHROPIC_API_KEY` | — | Anthropic API key |

## API Endpoints

| Endpoint | Method | Auth | Description |
|----------|--------|------|-------------|
| `/v1/chat/completions` | POST | Yes | Main inference endpoint (OpenAI-compatible) |
| `/v1/models` | GET | Yes | List available model aliases |
| `/health` | GET | No | Provider health check (add `?deep=true` to probe upstream) |
| `/stats` | GET | Yes | Usage statistics and estimated costs (JSON) |
| `/dashboard` | GET | Yes | Quality gate dashboard (HTML, auto-refreshes every 10s) |

## Monitoring Dashboard

HYDRA includes a real-time HTML monitoring dashboard at `/dashboard` showing:

- **Total Requests** — overall request count
- **Quality Gate Stats** — checks performed, pass count, escalation count, escalation rate
- **Average Quality Score** — mean score across all quality gate checks
- **Cost Tracking** — estimated cost saved (cheap passes) vs escalation cost spent
- **Circuit Breaker** — current status (OPEN/CLOSED), trip count, window escalation rate
- **Streaming Bypasses** — count of streaming requests that skipped quality gating
- **Per-Model Breakdown** — table with alias, provider, request count, escalation count, threshold, estimated cost

## How It Fits Together

```
 User (Chat / API)
        │
        ▼
   ┌──────────┐     ┌─────────────┐
   │  Agent   │────▶│    HYDRA    │──▶ Opus (chat)
   │Framework │     │   :8300     │──▶ Sonnet (mid-tier)
   │          │     │             │──▶ MiniMax (crons)
   └──────────┘     └─────────────┘──▶ Cerebras (compaction)
                          │
                          ▼
                    ┌─────────────┐
                    │  Dashboard  │
                    │  /dashboard │
                    └─────────────┘
```

## Why "HYDRA"?

In mythology, the Hydra had multiple heads — cut one off and two more grow back. This pipeline works the same way: multiple model heads, each specialized for a different task. The system is resilient by design.

Also: **H**ybrid **Y**ielding **D**istributed **R**outing **A**rchitecture. But mostly the heads thing.

## Planned Features

The following features are on the roadmap but **not yet implemented**:

- **Failover chain**: Automatic cascading through providers (e.g., OAuth → free fallback → paid API) when a provider returns errors or hits rate limits. Currently, provider errors are returned directly to the client.
- **Prompt injection layer**: Model-specific prompt suffixes to prevent known failure modes (e.g., XML hallucinations in MiniMax) at generation time rather than relying solely on post-hoc quality scoring.
- **Safety layer**: Command blocking (dangerous shell commands), protected file detection, and API key scrubbing in responses before they reach the agent.
- **Free fallback provider**: Integration with a free-tier Opus provider (e.g., OpenCode Zen) as a zero-cost fallback for rate-limited scenarios.

## Related

- **[Nanobot](https://github.com/nanobot-ai/nanobot)** — The autonomous AI agent framework this pipeline was built for
- **[MiniMax](https://www.minimax.io/)** — Frontier model that makes cheap bulk inference possible
- **[Cerebras](https://cerebras.ai/)** — 2000+ tok/s inference for compaction tasks

## Contributing

PRs welcome. If you've integrated a new provider, improved the quality gate scoring, or found edge cases — open an issue or submit a patch.

## License

MIT — use it, modify it, ship it.
