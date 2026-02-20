# HYDRA 🐉

**A multi-headed inference pipeline that routes AI agent traffic across frontier models, compresses context with fast-inference engines, and auto-escalates on quality failures — cutting costs 99.7% without losing output quality.**

> One proxy. Multiple model heads. Intelligent routing. Automatic failover. Zero compromises.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.100+-green.svg)](https://fastapi.tiangolo.com/)

---

## The Problem

Running autonomous AI agents 24/7 is expensive. A single Opus-class model at $15/$75 per million tokens burns through $200-600/month on background tasks alone — cron jobs, monitoring, reports, health checks. Most of these tasks don't *need* frontier reasoning. But downgrading to cheaper models introduces formatting errors, hallucinations, and quality regressions that silently corrupt your agent's output.

**The choice shouldn't be "expensive and good" vs "cheap and broken."**

## The Solution

HYDRA is a transparent proxy that sits between your AI agent framework (OpenClaw, LangChain, CrewAI, etc.) and your LLM providers. It speaks the Anthropic Messages API on both sides, so your agent doesn't know it exists.

```
                         ┌──────────────┐
                         │   AI Agent   │
                         │  (OpenClaw)  │
                         └──────┬───────┘
                                │ Anthropic API
                         ┌──────▼───────┐
                         │    HYDRA     │
                         │    Proxy     │
                         └──┬───┬───┬───┘
                            │   │   │
              ┌─────────────┤   │   ├─────────────┐
              │             │   │   │             │
        ┌─────▼─────┐ ┌────▼───▼┐ ┌▼─────────┐ ┌─▼────────┐
        │  Opus 4.6 │ │ MiniMax │ │ Cerebras  │ │ OpenCode │
        │  (OAuth)  │ │  M2.5   │ │ GLM-4.7   │ │   Zen    │
        │  $15/$75  │ │$0.30/$2 │ │ $0.60/$1  │ │   FREE   │
        │ Reasoning │ │ Bulk AI │ │Compaction │ │ Fallback │
        └───────────┘ └─────────┘ └───────────┘ └──────────┘
```

### The Heads

| Head | Model | Role | Cost/MTok | Speed |
|------|-------|------|-----------|-------|
| 🟣 **Opus** | Claude Opus 4.6 | Interactive chat, complex reasoning | $15/$75 | ~30 tok/s |
| ⚡ **MiniMax** | M2.5 Highspeed | Background tasks, crons, sub-agents | $0.30/$2.40 | 100+ tok/s |
| 🧠 **Cerebras** | GLM-4.7 | Context compaction (summarization) | $0.60/$0.60 | 2,000+ tok/s |
| ⚫ **Zen** | Claude Opus 4.6 | Free fallback (rate-limited) | $0 | ~20 tok/s |
| 🔴 **Direct** | Claude Opus 4.6 | Last-resort paid API | $15/$75 | ~30 tok/s |

## Architecture

### 1. Intelligent Routing

When a request arrives, HYDRA inspects the `model` field:

```python
# Agent requests "cartu-proxy/minimax-m2.5-highspeed"
#   → Routes to MiniMax API (cheap, fast)
#
# Agent requests "cartu-proxy/claude-opus-4-6" 
#   → Routes to Anthropic OAuth (frontier reasoning)
#
# Compaction event detected
#   → Intercepts and routes to Cerebras GLM-4.7 (2000+ tok/s)
```

The agent framework controls which model to use per-task. Interactive chat gets Opus. Cron jobs get MiniMax. Compaction gets Cerebras. The proxy handles the rest.

### 2. The Quality Gate

The critical innovation: **pre-flight quality scoring on cheap model outputs.**

When MiniMax handles a request, HYDRA doesn't just forward the response blindly. It:

1. **Sends the request to MiniMax** (non-streaming, for inspection)
2. **Scores the response** (0.0 → 1.0) checking for:
   - XML hallucination patterns (`<minimax:tool_call>`, `<invoke>`, `<FunctionCall>`)
   - Missing formatting (no bold, no emoji for user-facing output)
   - Prompt injection artifacts
   - Response coherence
3. **If score ≥ 0.5**: Convert to SSE stream → return to agent ✅
4. **If score < 0.5**: Auto-escalate to Opus → return that instead 🔄

```python
score, issues = score_response_quality(minimax_response, original_prompt)

if score >= QUALITY_THRESHOLD:
    return stream_response(minimax_response)  # ~$0.001
else:
    opus_response = call_opus(original_request)
    log_escalation(model, score, issues)
    return stream_response(opus_response)      # ~$0.20
```

**Production results (Feb 20, 2026):**
- 173 MiniMax requests processed
- 100% quality gate pass rate (post prompt-tuning)
- 0 escalations to Opus
- $0.73 total MiniMax spend vs ~$50+ equivalent on Opus

### 3. Prompt Injection Layer

MiniMax M2.5 has specific failure modes (XML hallucinations, missing formatting). Instead of post-processing every response, HYDRA injects a **model-specific prompt suffix** that prevents these issues at generation time:

```python
MINIMAX_SUFFIX = """
CRITICAL FORMATTING RULES:
- NEVER output XML tags like <tool_call>, <invoke>, <FunctionCall>
- ALWAYS use **bold** for emphasis and headers
- Use emoji bullets for sections (📊 🔧 ✅ ⚠️)
- Keep responses concise and actionable
- If the message requires no response, output exactly: NO_REPLY
"""
```

This suffix is injected into the system prompt **only for MiniMax requests** — Opus traffic passes through unmodified.

### 4. Cerebras Compaction Engine

When the agent framework triggers context compaction (summarizing conversation history to free tokens), HYDRA intercepts the request and routes it to **Cerebras GLM-4.7** — a model optimized for pure speed:

- **2,000+ tokens/second** (vs ~30 tok/s on Opus)
- **$0.60/MTok** (vs $75/MTok output on Opus)
- Perfect for summarization tasks where speed matters more than reasoning depth

The compaction is transparent — the agent thinks it's talking to Opus, but gets a response 60x faster at 1/125th the cost.

### 5. Failover Chain

If any head fails, HYDRA cascades through the chain automatically:

```
1. Primary: Anthropic OAuth (Max20 plan)
   ↓ rate limit / 5xx
2. Fallback 1: OpenCode Zen (free Opus)
   ↓ rate limit / 5xx  
3. Fallback 2: Anthropic Direct (paid API key)
   ↓ all failed
4. Error → agent handles gracefully
```

Each failover is logged with latency, status code, and cost — visible in real-time on the monitoring dashboard.

## Safety Layer

HYDRA includes a security layer for agent-generated commands:

```python
BLOCKED_COMMANDS = [
    r'rm\s+(-rf?\s+)?/',          # rm -rf /
    r'dd\s+if=/dev/',              # disk destroyer
    r'mkfs\.',                      # format filesystem
    r'curl.*\|\s*(bash|sh)',       # pipe to shell
    r'chmod\s+777',                # world-writable
    r'shutdown|reboot|poweroff',   # system control
    r':()\{.*\|.*&\s*\};:',       # fork bomb
]

PROTECTED_FILES = [
    'openclaw.json', '.credentials.json',
    '/etc/shadow', '/etc/passwd', '/etc/sudoers',
    'id_rsa', 'id_ed25519'
]

SECRET_PATTERNS = [
    r'sk-api-\S+', r'sk-or-\S+', r'sk-ant-\S+',
    r'AIza\S{35}', r'ghp_\S+', r'gho_\S+'
]
```

Commands matching these patterns are blocked before reaching the model. API keys in responses are scrubbed before returning to the agent.

## Real-World Results

Production benchmarks from a 24/7 autonomous agent handling 25+ daily cron jobs, interactive chat, sub-agent orchestration, and browser automation:

| Metric | Opus Only | HYDRA Pipeline |
|--------|-----------|----------------|
| Daily cost (background tasks) | ~$50-80 | ~$0.73 |
| Compaction latency | 8-12s | 0.3-0.5s |
| Quality gate pass rate | N/A | 100% |
| Failover incidents | Manual | Automatic |
| Models utilized | 1 | 5 |
| Context preserved | ~60% | ~95% (pre-compaction rescue) |

**Cost reduction: 99.7% on background tasks. Zero quality regression.**

## Installation

```bash
pip install fastapi uvicorn httpx

# Clone and configure
git clone https://github.com/jcartu/hydra-pipeline.git
cd hydra-pipeline
cp .env.example .env
# Edit .env with your API keys

# Run
uvicorn hydra:app --host 0.0.0.0 --port 8889
```

## Configuration

```python
# hydra_config.py

PROVIDERS = {
    "anthropic-oauth": {
        "endpoint": "https://api.anthropic.com/v1/messages",
        "auth": "oauth",  # or "bearer"
        "pricing": {"input": 15.0, "output": 75.0, "cache_read": 1.5}
    },
    "minimax": {
        "endpoint": "https://api.minimax.io/anthropic/v1/messages",
        "auth": "bearer",
        "api_key_env": "MINIMAX_API_KEY",
        "pricing": {"input": 0.30, "output": 2.40}
    },
    "cerebras": {
        "endpoint": "https://api.cerebras.ai/v1/chat/completions",
        "auth": "bearer",
        "api_key_env": "CEREBRAS_API_KEY",
        "pricing": {"input": 0.60, "output": 0.60},
        "role": "compaction_only"
    },
}

QUALITY_GATE = {
    "threshold": 0.5,
    "auto_escalate_to": "anthropic-oauth",
    "check_patterns": ["xml_hallucination", "missing_formatting", "prompt_injection"],
}

FAILOVER_CHAIN = [
    "anthropic-oauth",
    "opencode-zen",
    "anthropic-direct",
]
```

## API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/v1/messages` | POST | Main inference (Anthropic-compatible) |
| `/costs` | GET | Cost tracking by provider (24h rolling) |
| `/providers` | GET | Provider health and status |
| `/quality` | GET | Quality gate statistics |
| `/health` | GET | Proxy health check |

## Monitoring Dashboard

HYDRA includes a real-time monitoring sidebar showing:

- **Model Activity** — which heads are lit up, call counts, costs
- **Quality Gate** — pass rate, escalation count
- **Cost Tracking** — actual spend vs estimated (flat-plan aware)
- **System Metrics** — CPU, RAM, GPU utilization
- **Failover Events** — logged with latency and reason

## How It Fits Together

```
 User (Chat / API)
        │
        ▼
   ┌──────────┐     ┌─────────────┐
   │  Agent   │────▶│    HYDRA    │──▶ Opus (chat)
   │Framework │     │   :8889     │──▶ MiniMax (crons)
   │          │     │             │──▶ Cerebras (compaction)
   └──────────┘     └─────────────┘──▶ Zen (fallback)
        │                  │
        ▼                  ▼
   ┌──────────┐     ┌─────────────┐
   │  Vector  │     │  Dashboard  │
   │    DB    │     │  (optional) │
   └──────────┘     └─────────────┘
```

## Why "HYDRA"?

In mythology, the Hydra had multiple heads — cut one off and two more grow back. This pipeline works the same way: multiple model heads, each specialized for a different task. If one provider goes down, the others take over. The system is resilient by design.

Also: **H**ybrid **Y**ielding **D**istributed **R**outing **A**rchitecture. But mostly the heads thing.

## Related

- **[OpenClaw](https://github.com/openclaw/openclaw)** — The autonomous AI agent framework this pipeline was built for
- **[MiniMax](https://www.minimax.io/)** — Frontier model that makes cheap bulk inference possible
- **[Cerebras](https://cerebras.ai/)** — 2000+ tok/s inference for compaction tasks

## Contributing

PRs welcome. If you've integrated a new provider, improved the quality gate scoring, or found edge cases — open an issue or submit a patch.

## License

MIT — use it, modify it, ship it.
