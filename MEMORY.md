# AGENT MEMORY INDEX

**Canonical location:** `/home/node/.openclaw/knowledge/agent-memory/MEMORY.md` (in container)
**Repo:** https://github.com/chic2020/agent-memory

## MANDATORY FIRST STEP — READ BEFORE WEB SEARCHING

Before searching the web for anything, grep this file. The answer is often already here.

    grep -i "<keywords>" /home/node/.openclaw/knowledge/agent-memory/MEMORY.md

This file is a keyword->link index. One line per topic, keywords on the same line
as the link, so `grep -i` always hits. Append new entries; never delete.

## HOW TO ADD TO THIS FILE

When chic supplies a repo/link in a prompt, append it under the matching section in
the SAME reply. Format: `- <topic keywords> | <one-line why it's useful> | <url>`
Keep one entry per line. No secrets, ever — this repo is shared.

---

## SECRETS — NEVER STORE HERE

API keys, tokens, wallet keys, and signers do NOT go in this repo. This is a
shared knowledge index. Secrets live in mode-600 files on the VPS only.
The Agent Mail key chic pasted on 2026-10-05 must be rotated; it was exposed in
plaintext and is intentionally NOT recorded here.

---

## RESEARCH QUEUE — GITHUB SEARCH LEADS (chic, 2026-10-05)

Unvetted topic searches. These are lead generators, not vetted software. Review
before running anything.

- agent social media automation repos | grow reach | https://github.com/search?q=agent+social+media&type=repositories
- social media for AI agents repos | distribution tooling | https://github.com/search?q=social+media+for+ai+agents&type=repositories
- ai trading repos | trading research only, no auto-execution w/o approval | https://github.com/search?q=ai+trading&type=repositories
- openclaw skills repos | extend team capability | https://github.com/search?q=openclaw+skills&type=repositories
- openclaw .md docs/guides repos | reference material | https://github.com/search?q=openclaw+.md&type=repositories
- supermemory repos | memory/recall layer, candidate for MEMORY.md scaling | https://github.com/search?q=supermemory&type=repositories
- airdrop repos recently updated | RESEARCH ONLY, not approved for install | https://github.com/search?q=Airdrop&type=repositories&s=updated&o=desc
- openclaw repos | upstream ecosystem | https://github.com/search?q=openclaw&type=repositories
- agentic repos | agent frameworks | https://github.com/search?q=agentic&type=repositories
- OpenClaw Mission Control repos | orchestration dashboards | https://github.com/search?q=OpenClaw+Mission+Control&type=repositories
- memecoin repos | RESEARCH ONLY, not approved for install | https://github.com/search?q=memecoin&type=repositories

**Approval gate on this section.** Airdrop and memecoin tooling commonly ships
sybil/farming automation. Per the standing finance rules (approval required for
transfers, $25/tx cap, $100/day cap, no keys or signer on the VPS), nothing in
this section gets installed or executed without chic's explicit per-item go-ahead.
Treat them as reading material only.

---

## TOOLS REQUESTED FOR TEAM USE (chic, 2026-10-05)

| Tool | Category | Status | Blocked on |
|---|---|---|---|
| posthog | product analytics | NOT SET UP | needs account + API key |
| cal.diy | booking | NOT SET UP | needs account, unclear self-host path |
| frappe crm | CRM | CANNOT SELF-HOST HERE | needs >=4GB RAM; 1.8GB box |
| mautic | marketing automation | CANNOT SELF-HOST HERE | needs >=2GB RAM alone |
| openseo | SEO | NOT SET UP | needs account + key |
| autumn | billing | NOT SET UP | needs account + API key |
| chatwoot | support desk | CANNOT SELF-HOST HERE | needs >=2GB RAM alone |
| typebot | chat/forms | CANNOT SELF-HOST HERE | heavy; run on Mac instead |
| invoice ninja | invoicing | CANNOT SELF-HOST HERE | needs DB; run on Mac instead |

The VPS has 1.8GB RAM total and ~340MB free. Six of these nine are self-hosted
apps that cannot coexist with the gateway on this box. Heavy ones belong on the
Mac (16GB) or a new small VPS. Nothing here is installed.

---

## SEARCH + BROWSER TOOLS — INSTALLED 2026-10-05

Reviewed before install per rule 4 (lifecycle scripts read, download hosts checked,
both pull only from their own npm/github releases). Both verified working.

- qmd 2.8.3 — local BM25+vector search over docs, MCP server included
  https://github.com/tobi/qmd | `qmd search "kw"` / `qmd query "q"` / `qmd mcp`
  Index: `agent-memory` collection -> this repo. Re-index with `qmd update`.
- agent-browser 0.38.2 — headless Chrome CLI for agents, Chrome 154 installed
  https://github.com/vercel-labs/agent-browser | `agent-browser open URL`, `get title`
  MEMORY IS TIGHT: one page at a time, always `agent-browser close` after.
  Wants Node >=24 (box has v22.22.1) - native binary works, JS wrapper may warn.

---

## MODEL PROVIDERS

### OVH AI Endpoints — FREE, no key, 24 models
Base URL: `https://oai.endpoints.kepler.ai.cloud.ovh.net/v1` (OpenAI-compatible, unauthenticated)

Verified live at 2026-10-05. Registered in openclaw.json as provider `ovh` (14 chat
models, validated). HARD LIMIT: response headers show `x-ratelimit-limit-minute: 2`
and `x-ratelimit-remaining-minute: 0`. The free tier allows **2 requests/minute** -
this is a plan cap, NOT a missing key, so no credential lifts it. One agent turn
costs several requests, so OVH is NOT wired into any agent chain. Use for one-off
calls only, or with a paid AI Endpoints subscription (billing decision, needs chic).

NOTE: `api.eu.ovhcloud.com/v1|v2` is the OVHcloud **infrastructure** API (servers,
DNS, billing) - a completely different service. It does NOT affect AI Endpoints
limits. `/v1/models` works and lists:

- `Qwen3.8-27B` 262k ctx — replaces the dead groq/cerebras qwen3.8-27b ref
- `Qwen3-Coder-30B-A3B-Instruct` 262k ctx — code work, good for `coder`
- `Qwen3.5-397B-A17B` 262k ctx — strongest general
- `Qwen3.6-27B`, `Qwen3.5-9B` 262k ctx — cheap general
- `gpt-oss-120b` 131k ctx / `gpt-oss-20b` — replaces dead groq/cerebras gpt-oss refs
- `Meta-Llama-3_3-70B-Instruct` 131k ctx — https://oai.endpoints.kepler.ai.cloud.ovh.net/doc/Meta-Llama-3_3-70B-Instruct/openapi.json
- `Qwen2.5-VL-72B-Instruct` 32k ctx — vision/images | https://oai.endpoints.kepler.ai.cloud.ovh.net/doc/Qwen2.5-VL-72B-Instruct/openapi.json
- `whisper-large-v3`, `whisper-large-v3-turbo` — FREE speech-to-text, closes a `media` gap
- `nvr-tts-en-us|de-de|es-es|it-it` — FREE text-to-speech, 4 languages
- `Qwen3Guard-Gen-8B`, `Qwen3Guard-Gen-0.6B` — FREE content guard
- `Qwen3-Embedding-8B`, `bge-m3`, `bge-multilingual-gemma2` — FREE embeddings
- `stable-diffusion-xl-base-v10` — FREE image generation

The embedding + guard models are a possible fix for memory search being dead
(no OPENAI_API_KEY) and for the `media` STT/TTS gaps.

### Provider status notes
- DeepSeek / OpenAI — configured but no credit
- OpenRouter — 429 rate limit and 402 credit
- Kilo, LLM7, Baseten, Gemini, Copilot — verified working
- groq, cerebras, nvidia, anthropic — REMOVED 2026-10-05 for latency; all agent
  chains repointed. Do not reintroduce them.
