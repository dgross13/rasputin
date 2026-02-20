# The Cartu Method

**A framework for persistent memory and cost-efficient inference in autonomous AI agents.**

> Your AI agent compacts its context and forgets everything. Your inference bill is $1,000/month for cron jobs that don't need frontier reasoning. The Cartu Method fixes both — and more, as the framework grows.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![arXiv](https://img.shields.io/badge/arXiv-2026.xxxxx-b31b1b.svg)](https://arxiv.org/)

---

## What Is This?

The Cartu Method is a **modular framework** addressing the core infrastructure problems that autonomous AI agents face when running 24/7. Instead of one paper, one repo, one solution — it's a growing collection of components that work together or independently.

**Current components:**

| Component | Problem | Result |
|-----------|---------|--------|
| [Memory Rescue](#component-1-memory-rescue) | Context compaction destroys critical facts | 100% retention (vs 5% vanilla) |
| [Inference Routing](#component-2-inference-routing) | Frontier models too expensive for background tasks | 97.9% cost reduction |

**Planned components:** Retrieval optimization, best-of-N consensus, semantic quality scoring, multi-agent coordination, adaptive model selection.

All production-tested. 30+ days continuous operation, 1,400+ daily requests, 762K persistent memories.

---

## Component 1: Memory Rescue

### The Problem

Every agent framework with long-running sessions hits the context window limit. When the system compacts (summarizes the conversation to free tokens), it destroys:

- **Specific values** — port 8889, threshold 0.5, IP 192.168.1.142
- **Decision rationale** — *why* you chose Postgres over Mongo
- **Debugging context** — the 3-hour auth bug fix journey
- **Entity relationships** — who said what, when, and why

This isn't theoretical. It's the #1 pain point in long-running agent deployments.

### The Solution

Intercept the compaction event. Before the context is summarized, fire parallel calls to **fast, cheap models** (Cerebras at 2000+ tok/s, $0/MTok) to extract and commit critical facts to a vector database.

```
Context at 80% ──► COMPACTION TRIGGERED
                         │
                    ┌─────┼─────┐
                    ▼     ▼     ▼
                 Facts  Decisions  Skills
               (Cerebras, parallel, ~4 seconds)
                    │     │     │
                    └─────┼─────┘
                          ▼
                    Vector Database
                   (762K memories)
                          │
                    ▼ Compaction proceeds
```

### Results

| Metric | Vanilla Compaction | Memory Rescue |
|--------|-------------------|---------------|
| Fact retention | 5% (1/20) | **100%** (20/20) |
| Overhead per compaction | 0s | ~4s |
| Cost per compaction | $0 | ~$0.02 |
| Retrieval latency | N/A | 700ms mean |

### Quick Start

```python
from cartu_method import MemoryRescue, QdrantBackend

rescue = MemoryRescue(
    backend=QdrantBackend(url="http://localhost:6333", collection="agent_memory"),
    fast_model="cerebras/llama-3.3-70b",
    parallel_extractors=3,
)

# Call before compaction
memories = rescue.extract_and_commit(current_context)
```

---

## Component 2: Inference Routing

### The Problem

Autonomous agents run 25+ scheduled tasks daily — monitoring, reporting, scanning, aggregating. These tasks don't need Claude Opus 4.6 ($15/$75 per MTok). But they still need to not be garbage.

### The Solution

Route requests across multiple models based on task type, with a quality gate that catches bad responses and escalates automatically.

```
Request ──► Task-Type Router
               │
        ┌──────┴──────┐
    Interactive    Background
        │              │
      Opus       MiniMax ($1/$4 MTok)
        │              │
        │         Quality Gate
        │           │      │
        │        Pass    Fail → Escalate to Opus
        │           │      │
        └─────┬─────┘──────┘
              │
         Safety Layer (model-independent)
              │
           Client
```

**Five model heads:** Opus (reasoning) → MiniMax (bulk) → Cerebras (compaction) → OpenCode Zen (free fallback) → Anthropic Direct (paid fallback)

### Results

| Metric | All-Opus | Inference Routing |
|--------|----------|-------------------|
| Daily cost (background) | $35.24 | **$0.73** (97.9% savings) |
| Monthly projected | $1,057 | **$21.90** |
| Quality gate pass rate | N/A | 100% (27/27 production) |
| Escalations needed | N/A | 0 |
| Latency (budget model) | 3.79s | **2.40s** (1.58× faster) |

### Quality Gate

Rule-based scoring (0.0–1.0), no additional LLM call:
- XML hallucination detection (−0.4)
- Formatting compliance checks (−0.15 each)
- System message handling (−0.5)
- **Threshold: 0.5** → auto-escalate to stronger model

Combined with an 897-character prompt suffix injected for budget models, this achieves 100% production pass rate.

### Safety Layer (model-independent)

- 13 dangerous command patterns blocked
- 7 protected configuration files
- 8 API key / credential patterns scrubbed
- Works regardless of which model generates the response

---

## Production Numbers

Running since January 2026 on a dual-GPU server (RTX PRO 6000 + RTX 5090):

| Metric | Value |
|--------|-------|
| Persistent memories | 762,051 |
| Daily requests | 1,400+ |
| Scheduled tasks | 25+ |
| Memory retrieval latency | 700ms mean, 926ms P95 |
| Compaction amnesia incidents | 0 |
| Quality gate failures in production | 0 |
| Uptime | 30+ days continuous |

---

## Supported Backends & Models

**Vector databases:** Qdrant (recommended), ChromaDB, Pinecone. Weaviate planned.

**Fast extraction models:** Cerebras (recommended, 2000+ tok/s), Groq, local via Ollama.

**Budget routing models:** MiniMax M2.5-Highspeed (tested), any Anthropic-compatible API.

**Agent frameworks:** OpenClaw (native integration), adaptable to LangChain/CrewAI/AutoGen.

---

## Paper

The full technical paper with benchmarks, related work comparison, and limitations is available:

- **PDF:** [`paper/cartu_method.pdf`](./paper/cartu_method.pdf)
- **LaTeX source:** [`paper/cartu_method.tex`](./paper/cartu_method.tex)
- **Benchmark data:** [`paper/benchmark_results.json`](./paper/benchmark_results.json)

arXiv submission pending.

## Citation

```bibtex
@misc{cartumethod2026,
  title={The Cartu Method: A Framework for Persistent Memory and
         Cost-Efficient Inference in Autonomous AI Agents},
  year={2026},
  url={https://github.com/jcartu/rasputin}
}
```

## Contributing

PRs welcome. Especially:
- Additional vector DB backends
- Benchmark scripts and datasets
- Integration guides for agent frameworks
- New framework components
- Improved extraction prompts

## License

MIT
