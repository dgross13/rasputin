# Compaction Summary: Gemini 3 Flash

**Time:** 42.2s
**Tokens:** 22046 in / 8192 out
**Summary length:** 29822 chars

---

## Goal
1. Review and discuss Josh's health/biohacking stack, especially MOTS-c peptide history and current protocol
2. Plan and execute IVF logistics with Almond Blossoms (Dubai) + Orchid Health (NJ) for embryo genetic screening
3. Draft legal documents required by Almond Blossoms clinic for IVF without Josh physically present
4. Investigate Rivalry Corp (TSXV: RVLY) — Canadian esports betting operator in distress/selling
5. Monitor iGaming M&A market for buy/sell opportunities relevant to Josh's grey-market operation
6. Analyze latest Grok social intel signals and translate them into actionable business moves
7. Security audit and hardening of OpenClaw gateway + Rasputin server infrastructure
8. Investigate potential umbilical hernia / diastasis recti — book surgeon appointment
9. Diagnose OpenClaw gateway pipeline behavior — rate limiting, model switching/failover frequency, cron lane health
10. Set up gog OAuth for josh@cartu.com and enable all Google Workspace APIs for full CLI access
11. Check Google AI subscriptions on josh@cartu.com and j@mail99.me; configure Antigravity provider for free Claude Opus access
12. Deep-dive all Opus 4.6 provider rate limits and optimize pipeline fallback order
13. Set up Opus pipeline monitoring observatory — probe every 30 min, daily morning report, optimize for 1 week (Feb 17-24)
14. Star Citizen account evaluation — help Josh with RSI hangar valuation / account details
15. **Research tai chi classes/instructors in Toronto for Dad (Lazar) post-lung transplant** — both studio classes and in-home instructors, ideally with post-surgical/respiratory rehab experience. PINNED until Lazar is a few days from hospital release.
16. **Build production-quality Manus competitor for Russian/CIS market** — architecture for millions, ship for 5 users. NOT a hack/Frankenstein of existing pieces. Build once, scale later. Use parallel OpenCode + Claude Code + sub-agents + local GPU inference to build in ~5-7 days.
17. **Draft outreach to Extradition Law Firm (ELF)** for Interpol Red Notice defense + Russian residency protection
18. **Resolve ВНЖ (blue book) conversion** — convert old-format (2028 expiration) permanent residence permit to new indefinite format via migration lawyer (Tarasenko)
19. **Evaluate Ashley McDonald's Rasputin Production architecture** — production-grade affiliate platform already in repo, assess readiness for deployment on existing K3s cluster
20. **Fix Grok intel scan deduplication** — scanner delivers same digest 3x/day without diffing against previously delivered content
21. **Investigate OpenClaw adaptive thinking support** — determine whether OpenClaw 2026.2.15 translates `thinkingDefault: "high"` to new Anthropic adaptive thinking API format (`thinking: {type: "adaptive"}` + `output_config: {effort}`) or still uses deprecated `budget_tokens`
22. **Fix OpenCode Black as OpenClaw provider/fallback** — configure proper provider definition and verify working as pipeline fallback
23. **Run full 20-category Grok social intel scan** — all forums/topics across casino regulation, brand monitoring, affiliate/traffic, payments, player sentiment, new markets, M&A, AI, crypto, geopolitics, cars, health, gaming, luxury, gadgets, audio, Russia/expat, VR/XR
24. **Develop "The Cartu Method" — a website, beautiful, modern design. Show the research, the benchmarks, the plugin. Make it look professional but not corporate. Like a tech research lab vibe. Host it on rasputin.to or rasputin.studio.**
25. **Benchmark local and cloud models for context compaction** — Qwen 72B, Qwen Coder 30B, Gemini Flash, Gemini Pro, Sonnet

## Constraints & Preferences
- Josh cannot travel internationally (Interpol Red Notice — binary options fraud case)
- Legal documents must NOT reference criminal matters, Interpol, or specific jurisdictions — keep vague ("ongoing legal proceedings")
- Sasha doesn't want to do IVF in Mexico (Orchid's other international option)
- Josh's sperm is stored at NGC Clinic, St. Petersburg, Russia — export restrictions and sanctions complicate shipping
- Josh operates grey-market iGaming brands (WikiLuck, BetOBet, 24Slots, BattleBet, Pure Casino, Peer Casino — INSINE KFT/NewEra B.V., Curaçao licensed)
- **Brazil is NOT a primary market** — focus is English-speaking grey markets (Canada, NZ, India, Northern Europe likely). Need casino admin panel access to verify player geo/language breakdown.
- **No SecureClaw install** — Josh rejected the Adversa AI third-party security tool; manual hardening preferred over behavioral context tax
- Server is behind NAT (192.168.1.94, router 192.168.1.1) — public IP 193.186.162.74 shows ports filtered; LAN exposure only, not internet exposure
- Only Josh's wife has WiFi access — LAN attack surface is minimal
- **gog keyring**: file backend, `GOG_KEYRING_PASSWORD=***PASSWORD_REDACTED***`, `GOG_ACCOUNT=josh@cartu.com` (both exported in `~/.bashrc`)
- **OAuth client "Second Brain Health"** is set to **Internal** user type — only cartu.com org users can auth. Does NOT support classroom, chat, cloud-platform, contacts.other.readonly, or directory.readonly scopes.
- **Morning briefing preference**: Josh wants pipeline health monitoring delivered as part of his morning casino updates — NOT as separate alerts. Bundle all into one morning shot.
- **Pipeline cost priority**: Flat-fee subs first (Max20, OpenCode Black — already paying), then free (Antigravity), then per-token last. anthropic-direct is absolute worst case ("costs a fortune").
- **.env file keys are STALE** — auth-profiles.json (`/home/josh/.openclaw/agents/main/agent/auth-profiles.json`) is the real source of truth for API keys. `.env` ANTHROPIC_API_KEY and OPENROUTER_API_KEY differ from auth-profiles.
- **Rewrite tone preference**: When drafting messages for Josh to send to his brothers, write as one paragraph, no dashes (—), no AI-style formatting. Older brother telling younger brothers how it is.
- **Manus competitor: build once, scale later** — Architecture decisions that are impossible to change later (tenant isolation, event protocol, API contract, stateless backend, interface-based services) must be right from day 1. Everything else (monitoring, CI/CD, CDN, rate limiting, billing) can wait.
- **Manus competitor: $0 build + $0 run** — OpenCode Black ($200/mo flat, already paying) for build. Ollama Qwen 72B + Coder 30B on GPUs for product inference. Zero per-token API costs.
- **Grey-market regulatory news is NOT a fire drill** — worth a mention in intel digests, not 🚨 red alerts with action items. Josh knows he's grey, always has been. Curacao blocks are "just Tuesday."
- **Don't repeat the same analysis/intel multiple times in one day** — Josh explicitly called this out 3 times. Grok scanner dedup must be fixed.

## Progress
### Done
- [x] Reviewed MOTS-c history, mechanisms, and Josh's previous dosing (28mg/week, 3-4x standard)
- [x] Updated Josh's health profile: new stack is TB-500, BPC-157, Somatropin 1iu/day, TRT 10mg/day (~70mg/week), Mounjaro 7.5mg/week — committed to memory
- [x] Confirmed Josh & Sasha married January 14, 2026 in Moscow — committed to memory
- [x] Assessed fertility impact of 2 weeks back on TRT — pipeline sperm still viable, not yet fully suppressed
- [x] Confirmed 6 portions of sperm banked; IVF target April 2027 cycle (late March/early April retrieval)
- [x] Drafted legal restrictions letter → `/home/josh/.openclaw/workspace/drafts/almond-blossoms-legal-restriction-letter.md`
- [x] Drafted notarized consent letter → `/home/josh/.openclaw/workspace/drafts/almond-blossoms-consent-letter.md`
- [x] Sent both drafts to Josh via Telegram (messages 10922, 10923 to chat 1031217602)
- [x] Researched Russia→Dubai sperm shipping options (IVF Couriers hand-carry service, Sasha hand-carry as backup)
- [x] Researched Russia→US embryo biopsy shipping — confirmed near-impossible
- [x] Identified Rivalry Corp (TSXV: RVLY) winding down operations as of Feb 13, 2026
- [x] Committed M&A monitoring directive to memory
- [x] Analyzed latest Grok intel scans and mapped signals to Josh's operation
- [x] Confirmed OpenClaw version 2026.2.15 (latest on stable channel)
- [x] Ran `openclaw status` — built-in security audit found **3 CRITICAL + 2 WARN + 1 INFO** issues
- [x] Retrieved full gateway configuration via `gateway config.get`
- [x] Researched Adversa AI / SecureClaw — recommended against installing
- [x] **OpenClaw security hardening — all 6 priority fixes applied** (chmod 700, Telegram allowFrom locked, elevated exec locked, trustedProxies fixed, Discord disabled, API key moved to .env)
- [x] **Phase 1 server hardening — internal services bound to localhost:** Second brain (7777), Embedding server (8003), Reranker (8006 already ok), ttyd (7681 — **CRITICAL: was exposing bash shell on 0.0.0.0 with plaintext creds**), ADB (5037 killed)
- [x] **Full Rasputin server audit completed**: 58 services on 0.0.0.0 inventoried. Behind NAT. Score: 0 CRITICAL (was 3), 4 WARN remaining.
- [x] Identified Josh's likely medical issue: **umbilical hernia** + possible diastasis recti
- [x] Wrote Russian-language instructions for Sasha to book хирург-герниолог appointment
- [x] **Pipeline/rate-limit investigation**: Gateway runs as systemd user service (PID 3864893, started 12:04). Model history mapped. Failover issues identified. Cron lanes verified.
- [x] **gog keyring configured**: Switched from `auto` to `file` backend, password `***PASSWORD_REDACTED***`, config at `/home/josh/.config/gogcli/config.json`
- [x] Translated Russian audio from "Motos" re vehicle import — utilization fee + VAT paid, customs conclusion needs 2-3 more days
- [x] **gog OAuth for josh@cartu.com — COMPLETE with ALL scopes**: Gmail (read/modify/send/settings), Calendar (events/readonly), Drive, Sheets, Docs, Contacts, Fitness (activity/heart_rate/body/sleep), OpenID/userinfo. Verified all APIs working.
- [x] **Google AI subscription identified**: josh@cartu.com has **Google One AI Premium** (AI Pro tier) — 8,790 HUF/mo (~$23) via PayPal since Oct 19, 2025. Monthly billing on the 19th. NOT Ultra ($250/mo).
- [x] **Gemini API key tested**: `GEMINI_API_KEY=***GEMINI_API_KEY_REDACTED***` works with all 44 models including Gemini 3 Pro, 2.5 Pro, Imagen 4 Ultra. 1M token context.
- [x] **Antigravity plugin enabled**: `@openclaw/google-antigravity-auth` enabled in OpenClaw, gateway restarted, plugin loaded.
- [x] **Opus 4.6 provider deep dive COMPLETED** — all sources tested and verified.
- [x] **Pipeline fallback order APPLIED** (Josh approved)
- [x] **Antigravity OAuth COMPLETED for j@mail99.me**
- [x] **Opus Pipeline Monitoring System DEPLOYED** (Feb 17-24)
- [x] **Full pipeline test completed** (Feb 17, 15:56 MSK) — 5/6 providers live
- [x] **Star Citizen hangar data retrieved from memory**
- [x] **Rasputin/JARVIS integration audit completed**
- [x] **Full Russian Manus codebase audit completed** — LangGraph 7-node orchestrator, 41 tools, model gateway routing, event-sourced PostgreSQL, Keycloak, 13-service Docker Compose, Russian NLP, cyberpunk Next.js frontend
- [x] **OpenManus audit completed** — running at `manus.rasputin.to`, uses `claude-sonnet-4-20250514`, ManusAgent with BrowserTools/FileTools/ShellTools/ScaffoldingTools/HostingTools, 10+ published projects
- [x] **Drafted IVF document reply to Chloe** — consent + legal restrictions letters with fill-in-the-blanks
- [x] **Diagnosed Grok scanner crash** — OOM'd/timed out, auto-recovers next run
- [x] **OpenCode Black CLI verified WORKING** — v1.2.5, `opencode/claude-opus-4-6`, $200/mo flat
- [x] **Claude Code CLI verified available** — v2.1.2
- [x] **Manus competitor architecture fully specced** — architecture for millions, ship for 5
- [x] **Parallel build strategy designed** — 8-10 workers across OpenCode/Claude Code/sub-agents
- [x] **Drafted family update message for Josh's brothers** about Dad (Lazar)
- [x] **Manus competitor build plan REASSESSED with deep analysis** — layered 4-stage sequential build
- [x] **Found ELF contact info**: Email: info@extraditionlaw.net, phones: +7-995-260-4147 / +7-911-601-0417, address: Paveletskaya Embankment 8B, Moscow 115114. Also found on UK FCDO professional services directory and Justia.
- [x] **Drafted full inquiry email to ELF/Kshevitsky** — covers Interpol Red Notice, US indictment (Case No. 8:21-cr-00331-PX, D. Md., Aug 25 2021), binary options fraud charges (2013-2017 scheme), 2024 St. Petersburg detention, brothers' Dubai release (US never sent extradition docs), requests for extradition defense + Red Notice challenge + ВНЖ protection. Mentions existing US counsel (ArentFox Schiff) and Israeli counsel. Professional tone. Draft shown to Josh for approval.
- [x] **Retrieved and analyzed Ashley McDonald's Rasputin Production architecture** — fetched full doc via `gog docs cat`, saved to `/home/josh/.openclaw/workspace/reference/rasputin-production-ashley-spec.md`.
- [x] **Confirmed Ashley's repo exists and is active** — Bitbucket Server at `git.shuhari.tools/projects/RAS/repos/workspace/browse` (behind SSO). Commits by Ashley McDonald on Jan 9-10, 2026.
- [x] **Confirmed Rick = Ashley McDonald** — Rick (@rick_the_alien, rick@mail99.me) is Ashley McDonald, Josh's CTO
- [x] **Provided architecture analysis to Josh** — PostgREST and event outbox pattern praised, concerns raised about missing AI layer, K8s operational overhead, Knative premature for current scale, no CI/CD/timeline in spec
- [x] **Clarified Tarasenko is migration lawyer, not developer** — Josh needs him for ВНЖ blue book conversion, not Rasputin platform
- [x] **Recommended Tarasenko for ВНЖ conversion** — cheaper than ELF for administrative procedure, keep ELF as backup if МВД flags Red Notice
- [x] **Confirmed Opus 4.6 already has adaptive thinking** — launched with it on Feb 5, 2026. Sonnet 4.6 also dropped today (Feb 17). Josh's config has `thinking=high` which locks to max; adaptive would let model decide per-request.
- [x] **Researched Anthropic adaptive thinking API** — new format: `thinking: {type: "adaptive"}` + `output_config: {effort: "medium"|"low"|"high"|"max"}`. Old `budget_tokens` is deprecated on Opus 4.6/Sonnet 4.6. `max` effort is Opus 4.6 only.
- [x] **Pipeline monitoring Day 1 data analysis COMPLETED** — 72 probes over 8 hours (Feb 17, 15:17-23:18 MSK). Results: anthropic-direct 17/18 up (1 "Overloaded"), avg 2,931ms; openrouter 18/18 up, avg 3,027ms; opencode-zen 0/18 (16 down + 2 auth err); google-antigravity 0/18 (proxy not running).
- [x] **Confirmed Antigravity proxy not running** — all 18 probes show "proxy not running" on port 4152. Free Opus access sitting idle.
- [x] **Retrieved OpenClaw system status** — running on Linux with 86 active sessions, Telegram and WhatsApp channels enabled, default model claude-opus-4-6
- [x] **Retrieved full openclaw.json config** — confirmed `opencode/claude-opus-4-6` was first fallback (aliased "Zen Opus") in both main agent and subagent fallback chains
- [x] **Confirmed OpenCode provider misconfiguration in openclaw.json** — previously no `opencode` provider defined in `models.providers` section, just a dangling model entry
- [x] **Spawned full 20-category Grok social intel scan** — sub-agent running all topics: casino regulation, brand monitoring, affiliate/traffic, payments, player sentiment, new markets, M&A, AI models, agents, GPU inference, crypto, geopolitics, cars, health/biohacking, gaming, luxury, gadgets, audio, Russia/expat, VR/XR
- [x] **MAJOR CORRECTION: OpenCode Black API ACTUALLY WORKS as external endpoint** — Previous investigation tested WRONG URLs (`opencode.ai/api/v1/`, `api.opencode.ai/v1/`). The correct endpoint is `https://opencode.ai/zen/v1/messages` (Anthropic Messages API format). Confirmed working: HTTP 200, valid Opus 4.6 response, cost $0 (flat rate). 33 models available.
- [x] **OpenCode Black rate limits researched**: $200/mo 20X plan provides ~$200+/week worth of Opus usage; users report 6-8hr/day of heavy coding for a full week before hitting weekly cap. Weekly quota reset. **~8-10x more capacity than Antigravity.**
- [x] **Antigravity rate limits confirmed**: ~5 hours of Opus before quota hit, weekly cooldown (users locked out for full weeks). Google tightening limits since Jan 2026.
- [x] **OpenCode provider PROPERLY configured in openclaw.json** — added `opencode` provider definition with `baseUrl: "https://opencode.ai/zen/v1"`, `api: "anthropic-messages"`, API key from env. Model `opencode/claude-opus-4-6` now routes correctly.
- [x] **New pipeline fallback order APPLIED via gateway config**:
  1. Max20 (primary)
  2. OpenCode Black (1st fallback) — $200/mo flat, ~8-10x Antigravity capacity
  3. Antigravity (2nd fallback) — free, ~5hr/week
  4. OpenRouter (3rd fallback) — per-token $15/$75
  5. anthropic-direct (4th fallback) — per-token, last resort
  6. Sonnet 4.6 (5th fallback) — downgrade
- [x] **OpenCode Zen endpoint fully verified**: `opencode.ai/zen/v1/messages` with Black API key, 33 models, Opus 4.6 at ~2,616ms latency, cost $0
- [x] **Fixed Antigravity proxy**: Restarted `google-antigravity-proxy` on port 4152. Confirmed live with HTTP 200 health check and test call.
- [x] **Sent Sasha instructions for apostille of marriage certificate** via WhatsApp.
- [x] **Set reminder for Thursday surgeon appointment**.
- [x] **Pulled Dexcom G7 data via ADB**, analyzed last 7 days.
- [x] **Recommended Mounjaro timing adjustment** to cover lunch spikes.
- [x] **Deployed Grok scanner dedup fix**: Added diff check to `/home/josh/.openclaw/workspace/tools/grok_social_intel.py` to only surface new items.
- [x] Sent SPEC.md to Telegram.

### In Progress
- [ ] **Investigating OpenClaw adaptive thinking translation** — searching OpenClaw 2026.2.15 dist JS files (`image-B1DRN441.js`, `reply-BhWxw1_E.js`, `cron-cli-CeKWtNhW.js`, `gateway-cli-CRiBIFy7.js`) to determine whether `thinkingDefault: "high"` gets translated to new adaptive API or deprecated `budget_tokens`. Josh said "Yeah check" to investigate this.
- [ ] **Manus competitor Phase 0 — write the bible**: Start SPEC.md, CONTRACTS.md, BUILD_STATE.md, shared schemas, task files. ~2-3 hours. Awaiting Josh's final "go."
- [ ] **Star Citizen account evaluation** — Josh confirmed ("Yep") he wants help. Hangar data loaded. Next: determine what Josh wants done.
- [ ] **Week-long pipeline optimization** — monitoring running, daily analysis + morning reports active. Day 1 baseline captured. Runs through Feb 24. OpenCode Black now properly in pipeline as fallback 1. Antigravity now running.
- [ ] **Tai chi for Dad (Lazar) — PINNED** — waiting for Josh to say "Dad's coming home" to pull top 5 Toronto studios + in-home instructors with post-surgical/respiratory rehab experience
- [ ] **ELF email draft awaiting Josh's confirmation to send** — draft complete, Josh reviewing
- [ ] **ВНЖ blue book conversion** — Josh needs migration lawyer (Tarasenko) to convert old-format (2028 expiration) permit to indefinite format. Josh hasn't provided Tarasenko's contact info yet.
- [ ] **Full 20-category Grok scan running** — sub-agent spawned, compiling results + TL;DR executive summary, auto-announce when done
- [ ] Josh needs to forward draft documents to his lawyer (Michelle Shapiro at ArentFox Schiff or Israeli counsel)
- [ ] Rivalry Corp acquisition opportunity — no financials deep-dive done yet
- [ ] Casino market analysis correction — need admin panel access to verify actual player geo/language breakdown
- [ ] Phase 2 server hardening: Docker compose fixes for PostgreSQL 5432, MySQL 3306 → bind to 127.0.0.1
- [ ] Phase 3 server hardening: code-server 3113, OpenCode 9999, Netdata 19999 → bind to Tailscale IP or add iptables rules
- [ ] Tailscale SSH enablement: `sudo tailscale set --ssh` then bind SSH to localhost + Tailscale IP only
- [ ] **Compaction benchmark suite — local models still grinding, cloud results in**
- [ ] **Start "The Cartu Method" website build**
- [ ] **Package the compaction offloader plugin for OpenClaw**

### Blocked
- Casino admin panel access needed — no URLs or credentials stored on Rasputin; Josh needs to provide admin URL + creds or screenshot geo breakdown
- Star Citizen RSI login credentials not in memory — may need Josh to provide if live scrape is needed
- **jarvis-postgres container broken** — `database "jarvis" does not exist` / `role "postgres" does not exist`. Real creds: DB=`jarvis_vault`, user=`jarvis`, password=`***REDACTED***`. Needs fix before ALFIE backend can connect to Postgres. (~30 min fix)
- **Tarasenko contact info unknown** — Josh hasn't provided who Tarasenko is or how to reach them
- **git.shuhari.tools requires SSO auth** — can't audit Ashley's repo code quality without read access

## Key Decisions
- **Dubai over Mexico/Russia for IVF**: Almond Blossoms is confirmed Orchid partner, logistics sorted, only legal letter needed
- **Keep legal disclosure vague**: "Ongoing legal proceedings" only — no Interpol/criminal references
- **Stay on TRT**: 6 banked sperm portions sufficient for ICSI
- **Michelle Shapiro recommended** over Israeli lawyer for the legal letter
- **Don't install SecureClaw**: Manual hardening preferred — behavioral skill conflicts with autonomy-first config
- **Don't change sandbox.mode or elevatedDefault**: Both intentionally set by Josh
- **Security postponed to tomorrow morning**: Phase 1 complete, Phases 2-3 deferred
- **Brazil licensing deprioritized**: Not a primary market. Focus on English-speaking grey markets.
- **josh@cartu.com is the primary email**: Not j@mail99.me — gog configured for cartu.com
- **Manual OAuth token exchange over gog interactive flow**: gog's PTY-based `--manual` auth kept failing. Direct curl token exchange + `gog auth tokens import` worked reliably.
- **Gmail-only initial auth, incremental scope expansion**: `--services all` caused invalid_scope. Started with Gmail, adding incrementally.
- **Google AI Ultra NOT worth investigating**: Consumer subscription for Gemini web UI, does NOT include free API access.
- **Pipeline cost ordering: flat-fee first, free second, per-token last**: Max20 ($200/mo) → OpenCode Black ($200/mo) → Antigravity (free) → OpenRouter (per-token) → anthropic-direct (per-token, absolute last resort).
- **OpenCode is "Black" tier ($200/mo), not free "Zen"**: Josh clarified he has the paid subscription.
- **j@mail99.me for Antigravity, not josh@cartu.com**: j@mail99.me is the account with the Antigravity subscription.
- **Antigravity uses `claude-opus-4-6-thinking` model ID**: The non-thinking `claude-opus-4-6` returns 404 on Antigravity.
- **Manus competitor: build properly from scratch, not hack existing pieces together**: Josh explicitly rejected wiring ALFIE UI + ALFIE backend + Russian Manus orchestrator. Wants clean architecture built for millions, MVP for 5.
- **Manus competitor: architecture for millions, ship for 5**: Day-1 decisions that can't change later: tenant isolation, event protocol schema, API contract, stateless backend, interface-based services. Day-N swaps: Docker→K8s, local disk→S3, Ollama→vLLM, JWT→OAuth/SSO, direct WebSocket→Redis Streams.
- **Manus competitor stack**: Next.js 15 + shadcn/ui + Tailwind + Zustand (frontend), FastAPI (backend), LangGraph (orchestrator), PostgreSQL (event-sourced sessions), Qdrant (per-user vector memory), Redis (cache/pubsub), Docker (sandbox per session), Ollama (Qwen 72B + Coder 30B).
- **Strip enterprise bloat from Russian Manus for MVP**: No Keycloak, Prometheus, Grafana, Loki, OTel, MinIO. Simple JWT auth + file storage on disk.
- **Layered sequential build over parallel waves**: Deep reassessment concluded parallel agents are bad at integration ("the glue IS the product"). 4 sequential stages, each using 3-4 parallel agents with manual integration between stages.
- **Keep Russian Manus backend, rebuild frontend from scratch**: Backend LangGraph orchestrator is solid and will be extended. Frontend rebuilt as clean split-screen Manus UX.
- **Realistic timeline: 5-7 days for working MVP, not 24 hours**: Integration, debugging, frontend polish, and WebSocket streaming reliability are hard problems that can't be parallelized.
- **Filesystem-as-memory for multi-day multi-agent build**: SPEC.md, BUILD_STATE.md, CONTRACTS.md, decisions/, tasks/, shared/, logs/.
- **Local inference for CIS prototype**: Ollama Qwen 72B + Qwen Coder 30B on existing GPUs, $0/mo per-user cost.
- **Per-user Qdrant isolation needed**: Current `second_brain_v2` is one big collection — each prototype user needs own namespace or collection.
- **$20-35 total build cost**: Leveraging OpenCode Black flat, Claude Code ~$5-10, Qwen 72B $0.
- **Use Tarasenko (migration lawyer) for ВНЖ conversion, not ELF**: Administrative document swap at МВД doesn't need extradition rates. ELF is backup if МВД flags the Red Notice.
- **Use Ashley's existing repo, don't rebuild with Tarasenko**: Ashley has the Rasputin Production codebase in a working repo with active commits (Jan 9-10, 2026), battle-tested pg-event-publisher, and designed the architecture.
- **Rasputin Production ≠ Manus competitor**: These are two separate projects.
- **Regulatory intel calibration**: Mention regulatory moves in digests but don't treat them as fire drills.
- **Grok scanner needs dedup logic**: Must diff new scans against last delivered content and only surface genuinely new signals.
- **OpenCode Black IS a valid pipeline fallback**: Previous investigation was WRONG — tested incorrect URLs. The correct endpoint `https://opencode.ai/zen/v1/messages` (Anthropic Messages API) works with the Black API key. HTTP 200, cost $0, 33 models available. Previous conclusion ("CLI-only, no external API") was erroneous.
- **OpenCode Black positioned as 1st fallback (above Antigravity)**: ~8-10x more Opus capacity than Antigravity. Weekly quota vs Antigravity's ~5hr/week. Josh confirmed: "we'll have higher limits with OpenCode Black."
- **Antigravity demoted to 3rd in fallback chain**: Josh said "put that third in line for now" — lower capacity (~5hr/week), Google tightening limits.
- **Hold Star Citizen account**: Don't care about selling it. More curious than anything.
- **Use smaller, faster models for compaction**: A 7-14B model purpose-tuned for summarization could hit 150-200 tok/s.
- **Reduce output size for compaction**: Compress the summary format, 6K tokens instead of 12K = half the time.
- **Two-stage compaction**: Fast local model for immediate compaction, then background Opus sweep for quality.
- **"The Cartu Method"**: A systematic evaluation framework for context compaction in AI agent systems.
- **Compaction Quality Triad**: Speed (time to compact), Fidelity (information retention %), Efficiency (context window utilization).
- **Decoupled Architecture for Compaction**: Compaction is infrastructure, not conversation. It should run on infrastructure-grade models (fast, cheap, reliable) not conversation-grade models (smart, nuanced, expensive).

## Next Steps
1. **Verify Antigravity proxy on port 4152** — free Opus access still idle, probe shows "proxy not running." May need OpenClaw gateway restart or plugin re-auth for the external probe to detect it. Internal OpenClaw plugin IS working.
2. **Fix pipeline probe to also test Max20 primary AND OpenCode Zen** — currently only tests fallbacks, missing the two most important providers.
3. **Complete OpenClaw adaptive thinking investigation** — finish analyzing dist JS files to determine if `thinkingDefault: "high"` maps to new adaptive API or deprecated `budget_tokens`.
4. **Get Tarasenko contact info from Josh** — need to know who they are, how to reach them, draft outreach for ВНЖ conversion
5. **Await Josh's confirmation on ELF email draft** — ready to send to info@extraditionlaw.net when Josh says go
6. **Manus competitor Phase 0 — write the bible**: Start SPEC.md, CONTRACTS.md, BUILD_STATE.md, shared schemas, task files. ~2-3 hours. Awaiting Josh's final "go."
7. **Manus competitor Stages 1-4** (Days 1-7): Multi-user chat → agent mode → split-screen UX → hardening
8. **Get Ashley read access to git.shuhari.tools** — audit actual code quality of Rasputin Production repo
9. **IVF documents next steps**: Josh fills in passport numbers + Sasha's maiden name → notary → apostille → forward to lawyer
10. **Star Citizen**: Clarify with Josh what he wants done
11. **Continue pipeline monitoring (Feb 17-24)**: Daily analysis, morning reports at 08:00 MSK. Focus on Max20 rate limiting patterns, OpenCode Zen capacity under real load, Anthropic overload frequency, OpenRouter latency stability.
12. **Tomorrow morning**: Phase 2+3 server hardening — Docker database binding, code-server/OpenCode binding, Tailscale SSH
13. **Tomorrow morning**: Scrub credential leaks from memory files — `memory/2026-02-07.md` line 242, `memory/god_stack_research.md` line 385
14. Investigate cron lane 403 errors (11:00 and 12:00 today)
15. **When Dad (Lazar) is near release**: Pull top 5 tai chi studios in Toronto + private in-home instructors
16. Josh provides casino admin panel URL + credentials → verify actual player geo/language breakdown
17. Josh forwards draft letters to lawyer → get on letterhead + notarized/apostilled
18. Sasha books appointment with хирург-герниолог for Josh's suspected umbilical hernia
19. Obtain apostille for marriage certificate (Russian ZAGS document → Ministry of Justice)
20. Submit documents to Almond Blossoms (Chloe Meriel B Duran)
21. Coordinate sperm transport from NGC SPb → Almond Blossoms Dubai
22. Sasha baseline bloods (AMH, Day 2-3 scan) if not already done
23. Deep-dive Rivalry Corp financials if Josh wants to pursue acquisition
24. Run full compaction benchmark suite — local and cloud models
25. Start "The Cartu Method" website build
26. Package the compaction offloader plugin for OpenClaw
27. Get Dad's