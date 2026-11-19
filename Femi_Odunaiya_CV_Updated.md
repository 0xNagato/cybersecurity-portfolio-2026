# Femi Odunaiya

**Backend and Systems Engineer (Rust)**

Lagos, Nigeria · Open to remote roles and relocation · [0xnagato.github.io](https://0xnagato.github.io) · [github.com/0xNagato](https://github.com/0xNagato) · [linkedin.com/in/femi-odunaiya-3b1307a8](https://linkedin.com/in/femi-odunaiya-3b1307a8)

## Summary

Backend engineer who builds Rust services that take in live data, model it and act on it. I designed and run a 9-crate Rust trading system for Polymarket (1,756 tests, live orders behind two separate safety gates) and wrote a 63,000-line Rust ingestion pipeline that feeds a Laravel and React product. I also run a self-hosted multi-agent AI assistant and build open-source tools that keep AI agents honest. Before engineering I spent five years in banking, as a legal officer and then a credit analyst at Access Bank, and a credit analyst at Wema Bank. That shaped how I work: clear writing, evidence before claims, and systems built to be audited.

## Skills

- **Languages:** Rust (main), TypeScript, Python, PHP, SQL, Solidity
- **Rust:** Tokio, Actix Web, SQLx, reqwest, tokio-tungstenite, ethers-rs, alloy, serde, thiserror, clap
- **Web and APIs:** Laravel 12, Filament, Inertia.js, React 19, Next.js, Hono, REST and WebSocket clients, MCP servers
- **Data:** PostgreSQL (partitioned tables, materialized views, 200+ SQL migrations), Redis, SQLite, Supabase, Qdrant, graph databases
- **Delivery:** GitHub Actions, Linux servers on AWS EC2, pm2, Foundry
- **Testing:** cargo test, Pest, PHPStan, Node test runner, shadow (no-money) runs against live data
- **Security:** Linux, SQL, SIEM and intrusion detection tools, Wireshark and tcpdump packet analysis, incident documentation
- **AI agents:** multi-agent systems on OpenClaw, Claude Code, MCP tool design, agent skills, failover across model providers

## Selected projects

### polymarket-printer: automated trading system for Polymarket
*Rust, Tokio, WebSockets, Polygon · Jul 2026 to present · private repo, walkthrough on request*

- Trades short-term crypto Up/Down markets (1 to 15 minutes), including five-minute Bitcoin markets. Built as a 9-crate Rust workspace: core types, Polymarket API client, strategies, backtester, research runner, live runner, probability models, a model bridge and a terminal UI. About 286,000 lines of Rust and 118 binaries.
- Real orders need both a compile-time feature flag and a runtime `--arm` flag. Without both, every binary runs in detection-only mode.
- Shadow harnesses run strategies against live order books with realistic fill and queue modelling, with no money at risk.
- Settles against Chainlink price feeds. Complete-set arbitrage (split, merge, redeem) runs through Polymarket's gas-free relayer. Position size is quarter-Kelly under hard per-order caps.
- Built with AI coding agents under a written operating contract: hooks block unsafe actions, models are tested on data they have not seen, paper trading runs beside live trading, and every result goes to an append-only log.
- 1,756 Rust tests; GitHub Actions for build checks and AI-assisted code review.

### game-compare-ingest and game-compare: game price comparison platform
*Rust (Tokio, Actix Web, SQLx), PostgreSQL, Laravel 12, React 19 · Dec 2025 to Feb 2026 · public*

- Rust ingestion backend: about 63,000 lines and 76 CLI binaries. Syncs catalogues, prices and media from 12 providers, including PlayStation Store, Steam, Xbox, IGDB and IsThereAnyDeal, and converts currencies.
- Every write is idempotent (`ON CONFLICT` upserts), so any job can be re-run safely. Price history lives in monthly partitioned tables, and materialized views serve the read side.
- Schema managed through 200+ SQL migrations, with GitHub Actions workflows for schema dumps and spec checks.
- Laravel 12 and React 19 (Inertia.js) front end over the same PostgreSQL database, with Horizon queues, Pest tests and PHPStan.

### Multi-agent AI assistant on OpenClaw
*Self-hosted · private, retry plugin public*

- A multi-agent assistant my family talks to on WhatsApp, iMessage and Telegram: 8 agents, each with its own workspace and memory, plus a four-agent research team (coordinator, researcher, reviewer and writer).
- Runs on Anthropic, xAI and NVIDIA-hosted open models with automatic failover. When a provider rate-limits, my openclaw-message-queue plugin queues the reply and retries it so no message is lost.

### Tools for AI coding agents
*Rust, Python, TypeScript · Aug to Oct 2026 · public, MIT licensed*

- **ctxgrep** (Rust): code search for agents that ranks matches, returns only what fits a token budget and reports exactly how many it left out. Runs as a CLI or an MCP server.
- **skill-lint** (Python, no dependencies): lints agent `SKILL.md` files and MCP tool schemas for problems such as tools a model can't tell apart, destructive tools without a confirmation step and broken file links. Runs as a CLI or an MCP server.
- **logdex** (Python): indexes very large logs into greppable manifests, with optional vector search in Qdrant. A 127 MB JSONL file became a 1.1 MB manifest in 4.4 seconds.
- **confound-check**: a review procedure for agents. Before a claim that one thing caused another is accepted, every rival explanation gets a check that can be run.
- **openclaw-message-queue** (TypeScript): idempotent message queue for an agent gateway. Uses optimistic locking and a strict state machine so retries never send twice.
- **polymarket-complete-set-checker-lite** (Python, standard library only): read-only Polymarket fee and complete-set checker, packaged as an agent skill. No wallet, no API key, never trades.

### More projects

- **architecture-studio** (Python): turns a one-line brief such as "3-bed bungalow at Lekki" into floor plans, site sheets, location maps, 3D renders and a BIM model, with no paid services.
- **qvac-doc-qa** (JavaScript): question answering over your own documents with a model that runs entirely on your machine.
- **inhouse-ai-php** (TypeScript, Laravel): an AI agent for hospitality bookings that calls a reservation system's functions directly.

## Open source

### OpenClaw: WhatsApp messages lost during gateway downtime
*TypeScript · Aug to Oct 2026 · openclaw/openclaw (open-source AI agent platform, about 395,000 GitHub stars)*

- Found why WhatsApp messages that arrived while the gateway was offline were marked read but never answered: a 60-second startup cutoff treated them as old history and dropped them.
- Fixed it in [PR #132260](https://github.com/openclaw/openclaw/pull/132260): long-linked accounts now answer messages up to 20 minutes old, while newly linked accounts stay filtered. Added regression tests that fail on the old code and a live outage trace from a paired device.
- The maintainers merged a reworked version of the fix in October 2026 ([#188882](https://github.com/openclaw/openclaw/pull/188882)) and credited me as co-author.

### mevericks/solana-mev-projects: Kamino integration
*Rust · merged May 2025*

- [PR #4](https://github.com/mevericks/solana-mev-projects/pull/4): Kamino flash loans and address lookup tables for Solana transactions.

## Experience

### Independent Software Engineer
*Remote, Lagos · 2022 to present*

- Design, build and run my own systems in Rust, TypeScript, Python and PHP, from data ingestion and trading engines to tooling for AI agents (see projects above).
- Own the full cycle: requirements, design, implementation, testing, deployment on Linux servers and day-to-day operation of live systems.

### Full-Stack Developer (contract)
*PrimaVIP, remote · Jul to Sep 2025*

- Worked on PRIMA, a dining concierge platform, as part of the engineering team.
- Back-end features on the platform's Laravel 11 and Filament code.
- The concierge booking flow in React and TypeScript, built from Figma designs.
- WhatsApp and messaging integrations, and the itinerary tracker.

### Blockchain Developer, with Solidquant
*Solidquant (Seoul), remote · Mar 2023 to Nov 2024*

- Co-programmer with Solidquant on MEV bots: wrote much of the code for arbitrage and sandwich bots on EVM layer 1 and layer 2 chains (Ethereum, Base, Blast, BSC, Arbitrum, Polygon), including pool discovery across V2 and V3 pools, 3-hop and 4-hop paths, and bundle submission through Flashbots.
- Worked out Uniswap V3 trade calculations and estimated the price impact of trades mathematically. Researched new protocols such as Blast before launch and designed bots for them.
- Set up nodes and servers for Base, Ethereum, BNB Smart Chain and Blast, plus subgraphs on SQL databases and Substreams, to route trades across exchanges. Advised newcomers on MEV and designed bots and contracts for Web3 applications.

### Credit Analyst
*Wema Bank Plc, Lagos · Dec 2021 to Feb 2023*

- Credit recovery: led and assisted recovery negotiations with defaulting customers.
- Advised the team on the law of credit recovery, including notice periods and methods of recovery, and drafted letters to defaulting customers.

### Credit Analyst, Credit Administration
*Access Bank Nigeria, Lagos · Nov 2020 to Jun 2021*

- Reviewed drawdown documents against the facility approval memo, the bank's credit guide and Central Bank of Nigeria rules.
- Maintained customer credit lines on Flexcube, the bank's core banking system, and the collateral register, including insurance and valuation records. Generated CRMS codes so facilities were registered with the Central Bank.

### Legal Officer, Corporate Counsel
*Access Bank Nigeria, Lagos · Sep 2017 to Nov 2020*

- Issued contingent liability instruments for the bank's units, including guarantees, indemnities and letters of credit, and drafted and reviewed legal documents across the bank.
- Litigation team: kept the litigation schedule and briefed external lawyers on new cases. Perfection team: made sure pledged property was registered so the bank could enforce its security.

### Legal Associate
*Abraham & Co (Barristers and Solicitors), Lagos · Nov 2015 to Apr 2017*

- Drafted the Digital Broadcasting Agreement for the operation and maintenance of Nigeria's digital terrestrial (DTT) and digital satellite (DSAT) television platforms for the 2017 digital switch-over, plus content aggregation, transmission and set-top box distribution agreements, working with both parties to each agreement.
- Researched and drafted legal opinions.

### Trainee Solicitor (NYSC)
*Anu Eso & Co, Lagos · Nov 2014 to Oct 2015*

- Appeared in court as co-counsel, attended mediation sessions and filed terms of settlement for consent judgments. Drafted legal opinions, including on wrongful termination of employment.
- Company secretarial work (board and annual general meetings, minutes, annual returns) and perfection of clients' titles at the Lands Registry, Alausa.

## Education

- **LLB (Hons) Law**, Durham University, United Kingdom, Second Class Upper (2:1) · 2010 to 2013
- **Barrister at Law (BL)**, Nigerian Law School, a one-year postgraduate professional qualification for call to the Nigerian Bar · 2013 to 2014
- **Access Bank School of Banking Excellence**, entry-level banking programme · May to Aug 2017
- **International Baccalaureate Diploma**, Ardingly College, West Sussex, 38 points · 2008 to 2010

## Certifications

- **Google Cybersecurity Professional Certificate**, Google on Coursera, September 2026 ([verify](https://coursera.org/verify/professional-cert/8VZBLE82IWMO)). Nine courses: networks, Linux and SQL, threats and vulnerabilities, detection and response with SIEM and IDS tools, and Python automation. Coursework included an incident handler's journal from Wireshark and tcpdump packet analysis, and a full incident report on a forced-browsing breach of customer data.
- **Claude Certified Associate: Foundations**, Anthropic, July 2026 ([verify](https://www.credly.com/badges/3d0b2b57-186b-4f68-9f04-2349f63b48a3/public_url))
- **Rust Programming Specialization**, including Rust for Large Language Model Operations, Duke University on Coursera, April 2024
- **LFEL1002: Getting Started with Rust**, The Linux Foundation, April 2024
