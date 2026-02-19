# Compaction Summary: Sonnet 4.6 (No Thinking)

**Time:** 189.0s
**Tokens:** 23335 in / 7265 out
**Summary length:** 23170 chars

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
21. **Investigate OpenClaw adaptive thinking support** — determine whether OpenClaw 2026.2.15 translates `thinkingDefault: "high"` to new Anthropic adaptive thinking API format
22. **Fix OpenCode Black as OpenClaw provider/fallback** — configure proper provider definition and verify working as pipeline fallback
23. **Run full 20-category Grok social intel scan** — all forums/topics across casino regulation, brand monitoring, affiliate/traffic, payments, player sentiment, new markets, M&A, AI, crypto, geopolitics, cars, health, gaming, luxury, gadgets, audio, Russia/expat, VR/XR
24. **Build "The Cartu Method" website** — publish compaction methodology, benchmarks, and plugin as a tech research lab-style site on rasputin.studio or rasputin.to
25. **Run full compaction model benchmark suite** — test all local and cloud models for compaction speed/quality/cost

## Constraints & Preferences
- Josh cannot travel internationally (Interpol Red Notice — binary options fraud case)
- Legal documents must NOT reference criminal matters, Interpol, or specific jurisdictions — keep vague ("ongoing legal proceedings")
- Sasha doesn't want to do IVF in Mexico (Orchid's other international option)
- Josh's sperm is stored at NGC Clinic, St. Petersburg, Russia — export restrictions and sanctions complicate shipping
- Josh operates grey-market iGaming brands (WikiLuck, BetOBet, 24Slots, BattleBet, Pure Casino, Peer Casino — INSINE KFT/NewEra B.V., Curaçao licensed)
- **Brazil is NOT a primary market** — focus is English-speaking grey markets (Canada, NZ, India, Northern Europe likely)
- **No SecureClaw install** — Josh rejected the Adversa AI third-party security tool; manual hardening preferred
- Server is behind NAT (192.168.1.94, router 192.168.1.1) — public IP 193.186.162.74 shows ports filtered; LAN exposure only
- Only Josh's wife has WiFi access — LAN attack surface is minimal
- **gog keyring**: file backend, `GOG_KEYRING_PASSWORD=***PASSWORD_REDACTED***`, `GOG_ACCOUNT=josh@cartu.com`
- **OAuth client "Second Brain Health"** is set to **Internal** user type — only cartu.com org users can auth
- **Morning briefing preference**: Bundle pipeline health + casino updates into one morning shot at 08:00 MSK
- **Pipeline cost priority**: Flat-fee subs first (Max20, OpenCode Black), then free (Antigravity), then per-token last
- **.env file keys are STALE** — auth-profiles.json is the real source of truth for API keys
- **Rewrite tone preference**: One paragraph, no dashes (—), no AI-style formatting. Older brother telling younger brothers how it is.
- **Manus competitor: build once, scale later** — Day-1 decisions locked: tenant isolation, event protocol, API contract, stateless backend, interface-based services
- **Manus competitor: $0 build + $0 run** — OpenCode Black flat + Ollama Qwen 72B/Coder 30B on GPUs
- **Grey-market regulatory news is NOT a fire drill** — worth a mention in intel digests, not red alerts
- **Don't repeat the same analysis/intel multiple times in one day** — dedup fixed
- **ELF draft is for review only** — Josh will confirm if/when to send. Do NOT send autonomously. Currently on hold pending call with Michelle Shapiro.
- **Star Citizen account**: Josh decided to **hold** — not selling, just curious
- **Don't ping Ashley about casino admin access** — Josh will provide when ready
- **Wedding planning**: Josh and Sasha will discuss venue together; just note for now

## Progress
### Done
- [x] Reviewed MOTS-c history, mechanisms, and Josh's previous dosing
- [x] Updated Josh's health profile: TB-500, BPC-157, Somatropin 1iu/day, TRT 10mg/day, Mounjaro 7.5mg/week
- [x] Confirmed Josh & Sasha married January 14, 2026 in Moscow
- [x] Assessed fertility impact of TRT; confirmed 6 banked sperm portions
- [x] Drafted legal restrictions letter → `/home/josh/.openclaw/workspace/drafts/almond-blossoms-legal-restriction-letter.md`
- [x] Drafted notarized consent letter → `/home/josh/.openclaw/workspace/drafts/almond-blossoms-consent-letter.md`
- [x] Sent both drafts to Josh via Telegram
- [x] Researched Russia→Dubai sperm shipping options (IVF Couriers hand-carry, Sasha hand-carry backup)
- [x] Identified Rivalry Corp (TSXV: RVLY) winding down operations as of Feb 13, 2026
- [x] Confirmed OpenClaw version 2026.2.15; ran security audit (3 CRITICAL + 2 WARN + 1 INFO)
- [x] **OpenClaw security hardening — all 6 priority fixes applied**
- [x] **Phase 1 server hardening — internal services bound to localhost** (Second brain, Embedding server, ttyd, ADB killed)
- [x] **Full Rasputin server audit completed**: 58 services inventoried. Score: 0 CRITICAL (was 3), 4 WARN remaining
- [x] Identified Josh's likely medical issue: **umbilical hernia** + possible diastasis recti
- [x] Wrote Russian-language instructions for Sasha to book хирург-герниолог appointment
- [x] **gog OAuth for josh@cartu.com — COMPLETE** with all scopes (Gmail, Calendar, Drive, Sheets, Docs, Contacts, Fitness)
- [x] **Google AI subscription identified**: josh@cartu.com has Google One AI Premium (AI Pro, ~$23/mo)
- [x] **Gemini API key tested**: `***GEMINI_API_KEY_REDACTED***` — all 44 models working
- [x] **Antigravity plugin enabled**: `@openclaw/google-antigravity-auth` enabled, OAuth complete for j@mail99.me
- [x] **Opus 4.6 provider deep dive COMPLETED** — all sources tested and verified
- [x] **Pipeline fallback order APPLIED** (Josh approved)
- [x] **Opus Pipeline Monitoring System DEPLOYED** (Feb 17-24)
- [x] **Full pipeline test completed** (Feb 17, 15:56 MSK) — 5/6 providers live
- [x] **Star Citizen hangar data retrieved** — decision: HOLD (Josh not selling)
- [x] **Full Russian Manus codebase audit completed**
- [x] **OpenManus audit completed** — running at `manus.rasputin.to`
- [x] **Drafted IVF document reply to Chloe** — consent + legal restrictions letters
- [x] **OpenCode Black CLI verified WORKING** — v1.2.5, `opencode/claude-opus-4-6`, $200/mo flat
- [x] **Manus competitor architecture fully specced** — SPEC.md, CONTRACTS.md, BUILD_STATE.md ready
- [x] **Found ELF contact info** and drafted full inquiry email to Kshevitsky
- [x] **Retrieved and analyzed Ashley McDonald's Rasputin Production architecture**
- [x] **OpenCode Black IS a valid pipeline fallback** — confirmed working at `opencode.ai/zen/v1/messages`
- [x] **OpenCode provider properly configured in openclaw.json** with `api: "anthropic-messages"`
- [x] **New pipeline fallback order APPLIED**: Max20 → OpenCode Black → Antigravity → OpenRouter → anthropic-direct → Sonnet 4.6
- [x] **Spawned full 20-category Grok social intel scan**
- [x] **Overnight pipeline report reviewed** (Feb 18, 00:00-08:00 MSK): 47/48 Max20 requests successful (98%), 1 rate limit at 03:22 auto-recovered via OpenCode Black, OpenCode Black 6/6 fallback calls successful
- [x] **Antigravity proxy restored** — killed during server reboot on Feb 16 (PID 892341), restarted as PID 1247891 on port 4152, health check OK, test call successful. All 6 providers now active.
- [x] **Brazilian regulation noted and deprioritized** — SIGAP draft leaked, Curaçao operators mentioned, Q3 2026 deadline, not a fire drill for Josh's operation
- [x] **Manus competitor SPEC.md sent to Josh on Telegram** (47 pages) — awaiting review/greenlight for Stage 1
- [x] **Surgeon appointment reminder set** — Thursday Feb 20, 2026 at 09:00 MSK (хирург-герниолог, suspected umbilical hernia)
- [x] **Dexcom G7 data pulled via ADB** — 7-day analysis: avg glucose 128 mg/dL, TIR 68%, GMI 6.1%, lunch spike pattern confirmed (12:00-14:00, 165-190 range), worst day Tuesday (196 peak). Mounjaro injection timing identified as likely cause; recommended shift to Thursday/Friday morning injection.
- [x] **Apostille instructions written for Sasha** (Russian) — Ministry of Justice Moscow, Кржижановского 13к1, госпошлина 2,500₽, 3-5 days. Sent to Sasha via WhatsApp.
- [x] **IVF timeline updated**: Consent letter ✅, Legal restrictions ✅, Marriage cert apostille ⏳ (Sasha handling), Notarized consent ⏳, Sperm transport ⏳
- [x] **Dad (Lazar) update committed to memory** — bronchoscopy complete, fungal infection found, voriconazole prescribed, 2-3 weeks until home, tai chi search activated
- [x] **Voriconazole + prednisone interaction flagged** — CYP3A4 inhibition can increase prednisone levels 30-40%, docs should monitor
- [x] **Tai chi initial research completed** — Fung Loy Kok Taoist Tai Chi (8 GTA locations, donation-based, health-recovery focused), Toronto Tai Chi Academy, The Peaceful Dragon, Tai Chi for Health Institute (house calls $80-120/session), Dr. Paul Lam's network. Awaiting Lazar's post-release address.
- [x] **ELF email placed on hold** — Josh wants to talk to Michelle Shapiro first before engaging Russian lawyers
- [x] **Grok scanner dedup fix DEPLOYED** — hash-based diff check added to `/home/josh/.openclaw/workspace/tools/grok_social_intel.py`, saves to `/workspace/data/scans/last_delivered.json`, tested against last scan data (filtered 12/15 items correctly)
- [x] **Compaction benchmark suite initiated** — testing Qwen 2.5 72B (RTX PRO 6000), Qwen 3 Coder 30B (RTX 5090), Gemini 3 Flash, Gemini 2.5 Flash, Gemini 2.5 Pro, Sonnet 4.6 no thinking
- [x] **"The Cartu Method" website plan created** — Next.js 15 + Tailwind + Framer Motion + Recharts, dark tech research lab vibe, 6 pages, deploy to cartu.rasputin.studio or method.rasputin.to
- [x] **Wedding planning noted** — ceremony/party for 50-80 people, Moscow vs SPb TBD, budget flexible, elegant not ostentatious. Josh and Sasha to discuss together.

### In Progress
- [ ] **Compaction benchmark suite running** — Gemini 3 Flash ✅ (18.3s), Gemini 2.5 Flash ✅ (24.7s), Sonnet 4.6 no thinking ✅ (31.2s), Qwen 2.5 72B ⏳ (grinding), Gemini 2.5 Pro ⏳, Qwen 3 Coder 30B (queued)
- [ ] **"The Cartu Method" website build** — plan ready, sub-agent spawning, build starting
- [ ] **Compaction offloader plugin packaging** for OpenClaw
- [ ] **Manus competitor Stage 1** — SPEC.md reviewed by Josh (sent to Telegram), awaiting greenlight
- [ ] **Week-long pipeline optimization** — monitoring running Feb 17-24, daily reports at 08:00 MSK, all 6 providers now active
- [ ] **Tai chi for Dad (Lazar) — PINNED** — initial research done, waiting for post-release address (Hillcrest being sold, may go to David's)
- [ ] **Investigating OpenClaw adaptive thinking translation** — dist JS files analysis pending
- [ ] Josh needs to forward draft IVF documents to lawyer (Michelle Shapiro or Israeli counsel)
- [ ] Phase 2 server hardening: Docker compose fixes for PostgreSQL 5432, MySQL 3306 → bind to 127.0.0.1
- [ ] Phase 3 server hardening: code-server 3113, OpenCode 9999, Netdata 19999 → bind to Tailscale IP
- [ ] Tailscale SSH enablement

### Blocked
- Casino admin panel access needed — Josh will provide when ready (don't ping Ashley)
- Star Citizen RSI login credentials not in memory — moot, Josh decided to hold
- **jarvis-postgres container broken** — `database "jarvis" does not exist` / `role "postgres" does not exist`. Real creds: DB=`jarvis_vault`, user=`jarvis`, password=`***REDACTED***`
- **Tarasenko contact info unknown** — Josh hasn't provided who Tarasenko is or how to reach them
- **git.shuhari.tools requires SSO auth** — can't audit Ashley's repo without read access
- **ВНЖ blue book conversion** — waiting for Tarasenko contact info from Josh
- **ELF email** — on hold pending Josh's call with Michelle Shapiro
- **Manus competitor Stage 1** — awaiting Josh's greenlight after SPEC.md review
- **Tai chi final recommendations** — need Lazar's post-release Toronto address

## Key Decisions
- **Dubai over Mexico/Russia for IVF**: Almond Blossoms confirmed Orchid partner, logistics sorted
- **Keep legal disclosure vague**: "Ongoing legal proceedings" only — no Interpol/criminal references
- **Stay on TRT**: 6 banked sperm portions sufficient for ICSI
- **Don't install SecureClaw**: Manual hardening preferred
- **Brazil licensing deprioritized**: Not a primary market
- **Pipeline cost ordering: flat-fee first, free second, per-token last**: Max20 → OpenCode Black → Antigravity → OpenRouter → anthropic-direct
- **OpenCode Black positioned as 1st fallback**: ~8-10x more Opus capacity than Antigravity
- **Antigravity demoted to 3rd**: Lower capacity (~5hr/week), Google tightening limits
- **Star Citizen: HOLD**: Not selling, Josh just curious. Legatus Navium status appreciates over time.
- **ELF email on hold**: Josh wants to talk to Michelle Shapiro (ArentFox Schiff) first before engaging Russian lawyers
- **Grok dedup fix deployed**: Hash-based diff, only surfaces genuinely new items
- **The Cartu Method is publishable**: Not just "use Sonnet for compaction" — it's a systematic evaluation framework (Quality Triad: speed × fidelity × efficiency) with benchmark protocol. Website + GitHub + plugin.
- **Compaction speed is the real bottleneck, not quality**: Sonnet captures 85%+ of key facts; optimization target is time, not model intelligence
- **Local model compaction may not be faster**: Qwen 72B generation speed (~30-40 tok/s) means 12K token output takes ~340s — slower than cloud. Smaller models or cloud (Gemini Flash at 18.3s) may win.
- **Gemini Flash as compaction candidate**: Basically free, 18.3s for full compaction — 20x improvement over Opus if quality holds
- **Wedding venue TBD**: Josh prefers SPb (White Nights in summer), Sasha prefers Moscow. 50-80 guests, budget flexible, elegant not ostentatious. Will discuss together.
- **Mounjaro injection timing**: Should shift to Thursday/Friday morning for better lunch spike coverage (currently appears Sunday evening, weakest coverage by Thursday-Friday)
- **Voriconazole + prednisone interaction**: Flagged to Josh — CYP3A4 inhibition can increase prednisone levels 30-40%
- **Tai chi: private in-home instructor first**: Lazar immunocompromised post-transplant, 4-6 weeks home before transitioning to studio classes (Fung Loy Kok recommended)
- **Manus competitor: layered sequential build**: 4 stages, 3-4 parallel agents each, manual integration between stages. $20-35 total build cost.
- **Rasputin Production ≠ Manus competitor**: Two separate projects
- **Use Tarasenko for ВНЖ, ELF as backup**: Administrative document swap doesn't need extradition rates

## Next Steps
1. **Complete compaction benchmark suite** — finish Qwen 72B, Gemini 2.5 Pro, Qwen Coder 30B runs; compile full comparison table with speed/quality/cost
2. **Build "The Cartu Method" website** — Next.js 15, dark research lab vibe, 6 pages, deploy to cartu.rasputin.studio
3. **Package compaction offloader plugin** for OpenClaw
4. **Manus competitor Stage 1** — await Josh's greenlight after SPEC.md review
5. **Call Michelle Shapiro** (Josh handling) — then decide on ELF engagement
6. **Get Tarasenko contact info from Josh** — draft ВНЖ conversion outreach
7. **Tai chi final recommendations** — need Lazar's post-release Toronto address (Hillcrest being sold, may go to David's)
8. **Fix pipeline probe** — add Max20 primary to probe targets; Antigravity proxy now live on port 4152
9. **Complete OpenClaw adaptive thinking investigation** — finish analyzing dist JS files
10. **IVF next steps**: Josh fills in passport numbers + Sasha's maiden name → notary → apostille → forward to lawyer; coordinate sperm transport NGC SPb → Dubai
11. **Get Ashley read access to git.shuhari.tools** — audit Rasputin Production code quality
12. **Tomorrow morning**: Phase 2+3 server hardening — Docker database binding, code-server/OpenCode binding, Tailscale SSH
13. **Tomorrow morning**: Scrub credential leaks from memory files
14. Investigate cron lane 403 errors
15. Josh provides casino admin panel URL + credentials → verify player geo/language breakdown
16. Sasha baseline bloods (AMH, Day 2-3 scan) if not already done

## Critical Context
- **IVF Clinic**: Almond Blossoms Fertility, Dubai Healthcare City, Dr. Dimitrios Kafetzis, contact: Chloe Meriel B Duran (Staff Nurse), info@almondblossoms.care
- **IVF Status**: Consent letter ✅ received, Legal restrictions ✅ received, Marriage cert apostille ⏳ (Sasha handling — Ministry of Justice Moscow, Кржижановского 13к1, 2,500₽ госпошлина), Notarized consent ⏳, Sperm transport ⏳
- **Genetic Testing Lab**: Orchid Health, New Jersey — Gold package (PGT-A + monogenic + polygenic), 21-day turnaround
- **Sperm Storage**: NGC Clinic, St. Petersburg (Petrovsky Prospekt 2, Bldg 3), urologist Morev Vladimir Vladimirovich
- **IVF Target**: April 2027 cycle (Sasha egg retrieval late March/early April)
- **Josh's Lawyers**: Michelle Shapiro (michelle.shapiro@afslaw.com, ArentFox Schiff — US/Interpol), Oren Chen (orenchen@barak.net.il — Israeli civil)
- **ELF**: Stanislav Kshevitsky, info@extraditionlaw.net, +7-995-260-4147, Paveletskaya Embankment 8B, Moscow. Draft ready, on hold pending Michelle Shapiro call.
- **Josh's US Indictment**: Case No. 8:21-cr-00331-PX (D. Md.), Aug 25 2021. Binary options fraud 2013-2017. Active Interpol Red Notice. Brothers David and Jonathan released from Dubai (US never submitted extradition docs).
- **ВНЖ**: Old-format 2028 expiration, needs conversion to indefinite format. Tarasenko (migration lawyer) proposed — contact info not yet provided.
- **Josh's iGaming**: ~$2-2.65M/month, Curaçao licensed, English-speaking grey markets primary. BetOBet ~$850K-950K/mo, ~35-40% of group. WikiLuck highest ARPU. Peer Casino newest/ramping.
- **Ashley McDonald / Rick**: CTO. ashley@mcdonald.am, rick@mail99.me, @rick_the_alien. Repo at git.shuhari.tools (SSO required).
- **Dad (Lazar)**:
  - Currently: Toronto Western Hospital
  - Diagnosis: Fungal pulmonary infection (bronchoscopy confirmed)
  - Treatment: Voriconazole (⚠️ inhibits CYP3A4, increases prednisone levels 30-40% — flag to docs)
  - Prednisone: 35mg → 30mg taper
  - Timeline: Home ~early March 2026
  - Post-release: Hillcrest property (being sold) OR David's place (TBD — need address for tai chi)
  - Tai chi: Private in-home instructor first (immunocompromised), then Fung Loy Kok studio. Options compiled, awaiting address.
  - Separating from Barbara; Rob (lawyer) handling power of attorney + separate bank account; Hillcrest + Florida properties being liquidated; Barbara getting $5M settlement
- **Star Citizen**: RSI Handle `jcartu`, Legatus Navium, $34,275.47 spent, $32,432.79 melt. Decision: HOLD.
- **Surgeon Appointment**: Thursday Feb 20, 2026, 09:00 MSK reminder set. Хирург-герниолог, suspected umbilical hernia.
- **Dexcom G7 (7-day)**: Avg 128 mg/dL, TIR 68%, GMI 6.1%, CV 31%. Lunch spikes 165-190 confirmed. Mounjaro injection appears Sunday evening — recommend shift to Thursday/Friday morning.
- **Wedding**: Legal marriage done (ZAGS Jan 14, 2026). Ceremony/party TBD — 50-80 guests, elegant not ostentatious, Moscow vs SPb. Josh and Sasha discussing.
- **The Cartu Method**:
  - Framework: Quality Triad (speed × fidelity × efficiency) + Decoupled Architecture + Feedback Loop Insight + Benchmark Protocol
  - Website: Next.js 15 + Tailwind + Framer Motion + Recharts, dark research lab vibe, deploy to cartu.rasputin.studio or method.rasputin.to
  - 6 pages: Hero, The Problem, The Research, The Method, The Plugin, Run Your Own
  - Benchmark results so far: Gemini 3 Flash 18.3s, Gemini 2.5 Flash 24.7s, Sonnet 4.6 no-thinking 31.2s, Sonnet 4.6 w/thinking 227s/$0.16, Opus 4.6 w/thinking 379s/$0.61
- **OpenClaw Pipeline (LIVE)**:
  1. Max20 (primary) — $200/mo flat, 98% overnight uptime
  2. OpenCode Black (1st fallback) — $200/mo flat, `opencode.ai/zen/v1/messages`, 6/6 overnight calls successful
  3. Antigravity (2nd fallback) — FREE, j@mail99.me, port 4152 restored (PID 1247891) after server reboot killed it
  4. OpenRouter (3rd fallback) — per-token $15/$75 MTok
  5. anthropic-direct (4th fallback) — per-token, last resort
  6. Sonnet 4.6 (5th fallback) — downgrade
- **Grok Scanner**: Dedup fix deployed. Hash-based diff against `/workspace/data/scans/last_delivered.json`. Next run in ~2 hours.
- **Pipeline Monitoring**: Probe every 30 min, morning report 08:00 MSK. Runs Feb 17-24. Context at ~72%.
- **Rasputin Server**: 112 CPU cores, 251GB RAM, RTX PRO 6000 (96GB VRAM, Qwen 72B loaded), RTX 5090 (32GB, Qwen Coder 30B loaded)
- **Gemini API Key**: `***GEMINI_API_KEY_REDACTED***`
- **OpenCode Black API**: `opencode.ai/zen/v1/messages`, key `***OPENCODE_API_KEY_REDACTED***`, 33 models, cost $0
- **Manus Competitor**: 4-stage sequential build, SPEC.md sent to Josh on Telegram (47 pages), awaiting greenlight for Stage 1. Deploy target: manus.rasputin.to. $20-35 total cost.