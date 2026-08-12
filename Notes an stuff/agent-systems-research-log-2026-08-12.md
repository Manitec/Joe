# Agent Systems Research Log — 2026-08-12

## Purpose

A decision-oriented scan of agent runtimes, web-research access, model gateways, model providers, and evaluation surfaces relevant to ONE / Manitec. This is a research backlog, not an adoption decision.

## Working Architecture Map

| Architecture need | Candidate | Decision use |
| --- | --- | --- |
| Persistent, self-improving agent | Hermes Agent | Reference implementation for memories, generated skills, and learning loops. |
| Research acquisition tools | Agent-Reach | Potential sandboxed Scout capability for public web and social-source research. |
| Multi-provider model gateway | OmniRoute | Local routing/fallback experiment; compare against managed gateway options. |
| External agent benchmark surface | Agent Arena | Source of evaluation-task ideas and a model for user-centered agent scoring. |
| Hosted/self-hostable inference lane | NVIDIA Build / NIM | Provider benchmark and potential GPU deployment path. |
| Disposable agentic coding surface | Kilo Code | Development-time experimentation, not a trusted private-code or data lane. |
| Free-tier discovery | free-for.dev | Discovery index only; validate every service independently. |

## Findings

### Hermes Agent — high-priority reference probe

- Hermes presents a persistent, self-improving agent model with built-in memory/skill learning, conversation history, tool output, and messaging/local-environment capabilities.
- The useful idea is not necessarily its runtime. It is the artifact loop: work produces observations, observations become rules or skills, and later work reuses and corrects them.
- Study: skill representation, confidence and provenance, promotion/revision rules, scheduled reflection, isolation for subagents, and inspection/audit UX.
- Decision: run a bounded real-project probe before borrowing its patterns.

Sources:
- https://github.com/nousresearch/hermes-agent
- https://hermes-agent.nousresearch.com/docs/
- https://hermes-agent.org/

### Agent-Reach — high-priority sandbox test

- Agent-Reach advertises a CLI/tool layer for reaching public platforms and web sources, including GitHub, Reddit, YouTube, RSS, X, LinkedIn, and arbitrary URLs. It also describes upstream health checks.
- The relevant ONE role is a constrained research Scout, not blanket web access for all agents.
- Risk: claims around avoiding API fees may imply scraping, proxy/cookie handling, rate-limit exposure, source instability, or platform-policy risk.
- Test criteria: source quality, failure behavior, cleanup, data retention, credential handling, rate-limit resilience, and provenance capture.

Sources:
- https://github.com/Panniantong/Agent-Reach
- https://github.com/Panniantong/Agent-Reach/blob/main/llms.txt

### OmniRoute — high-priority local gateway evaluation

- OmniRoute describes itself as a free, open-source, OpenAI-compatible AI gateway with multi-provider routing, automatic fallback, MCP/A2A-related capabilities, and routing strategies.
- It is relevant as a local development and experimentation control plane, especially if ONE needs provider switching without rewriting agent code.
- It must sit behind a narrow internal model-provider interface rather than leak provider-specific logic into crews, memory, or tool policy.
- Security review is required before it receives real prompts, credentials, user data, or multiple provider accounts.

Sources:
- https://omniroute.online/
- https://www.hostinger.com/in/applications/omniroute

### Agent Arena — evaluation reference, not runtime

- Agent Arena evaluates agents on real-user work such as coding, debugging, web research, and document creation.
- Its value is methodological: use representative tasks, inspect artifacts/trajectories, and collect human judgments rather than judging an agent only by chat quality.
- ONE should maintain a small versioned task suite with fixtures, success criteria, stored traces, cost/latency, and a manual preference scorecard.

Sources:
- https://arena.ai/blog/agent-arena-methodology
- https://arena.ai/agent

### NVIDIA Build / NIM — provider and deployment lane

- NVIDIA Build exposes a catalog of hosted AI models, while NIM provides API access and a route toward NVIDIA-accelerated inference deployment.
- Use it as a provider benchmark and self-hosting investigation, not a default architectural dependency.
- The key comparison is model quality, tool-calling reliability, price, latency, rate limits, privacy posture, and the operational cost of GPU deployment.

Sources:
- https://build.nvidia.com/models
- https://docs.api.nvidia.com/nim/reference/llm-apis
- https://developer.nvidia.com/nim

### Kilo Code — useful with a strict data boundary

- Kilo Code supports free model configurations for agentic interactions, autocomplete, and background tasks.
- Its free-model documentation notes that prompts can be routed to providers that retain inputs and may use them to improve models.
- Use only with public/disposable code and non-sensitive prompts unless routing and retention are independently controlled.

Sources:
- https://kilo.ai/docs/getting-started/using-kilo-for-free
- https://kilo.ai/docs/getting-started

### free-for.dev — discovery only

- free-for.dev is a curated directory of free developer offerings.
- It is useful for discovery of evaluation, observability, hosting, and model experimentation options, but no production component should be selected merely because it appears in the directory.

Source:
- https://github.com/ripienaar/free-for-dev

### Unresolved: Echo LLM and genx.sh

- The supplied name “Echo LLM” does not uniquely identify a product from the available evidence.
- https://genx.sh/ did not return retrievable page content during this scan.
- Do not assign either a role until a canonical URL, repository, or product description is available.

## Design Principles Extracted

1. Keep agent runtime, source context, durable memory, tool access, and model routing as separate layers with explicit contracts.
2. Give public-web acquisition to constrained specialist agents, with provenance and failure reporting, rather than universal browser access.
3. Treat memory as an inspectable operational artifact system: episodes, distilled facts, rules, skills, confidence, provenance, revision, and deletion.
4. Put provider choice, cost caps, fallback, redaction, and auditability behind one gateway boundary.
5. Make evaluation a first-class loop before expanding autonomy: versioned tasks, expected artifacts, quality score, task success, cost, latency, and failure taxonomy.
6. Treat free inference and account-aggregation products as untrusted until their retention, routing, credentials, and sustainability are verified.

## Recommended Experiments

- [ ] Run Hermes on one recurring, multi-day project; inspect every memory and generated-skill artifact.
- [ ] Run Agent-Reach in an isolated container without production credentials; test research quality across GitHub, one social source, and one media source.
- [ ] Benchmark OmniRoute with a small model matrix and forced-provider failure; record compatibility, fallback, traces, cost, latency, and data-handling behavior.
- [ ] Define five to ten ONE evaluation tasks with fixtures, explicit success criteria, required artifacts, and human scoring.
- [ ] Benchmark NVIDIA NIM against the current provider lane for tool use, code edits, latency, rate limits, and operating cost.
- [ ] Require canonical source links before evaluating Echo LLM or genx.sh further.

## Decision Status

| Item | Status |
| --- | --- |
| Hermes Agent | Probe as a learning-loop/memory reference. |
| Agent-Reach | Sandbox test as a Scout research tool. |
| OmniRoute | Local gateway benchmark. |
| Agent Arena | Mine for eval design; no platform commitment. |
| NVIDIA Build / NIM | Provider/deployment benchmark. |
| Kilo Code | Disposable development experiments only. |
| free-for.dev | Discovery index only. |
| Echo LLM / genx.sh | Hold pending identification. |
