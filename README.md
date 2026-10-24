# Memechain

A web platform where meme creators turn fresh news into memes with AI assistance, every meme is checked against its source story before publishing, and creators earn from a share of ad revenue and paid subscriptions, paid out in a dollar-pegged stablecoin.

Diploma project, Astana IT University, School of Software Engineering, group SE-2421.

## Problem, users and expected outcomes

**Problem.** Meme creators who react to news face three problems at once:

- making a good meme about a fresh story takes time, and AI tools that speed this up can distort the facts of the story;
- existing platforms pay creators only after high audience thresholds, often not in every country, and creators cannot verify how their earnings are calculated;
- none of the systems we compared links a news story, the meme made from it, a check of the meme against the story, and payment to the creator.

Details and evidence: [project proposal](docs/01-proposal.md), [evidence of relevance](docs/02-interviews/README.md), [existing systems](docs/04-existing-systems.md).

**Target users.** English-speaking meme creators and their audience; platform moderators.

**Expected outcomes.**

- A working beta of the web platform on testnets and sandboxes: news → story → AI meme variants → fact-check → publication → earnings → payout.
- Three evaluation studies: meme quality, fact-check accuracy, payout cost and speed.
- The diploma thesis.

## Team and supervisor

| Member | Role | Responsibilities |
|---|---|---|
| Serik Alikhan (A) | Web3 and monetization | Module `MON`: ad revenue share, subscriptions, KYC gate, stablecoin payouts, payout contract; risk register; YouTrack |
| Toleukhan Alizhan (B) | AI meme generation | Module `GEN`: creator studio, meme variant generation, generation quality; interviews; literature review; project plan; supervisor feedback log |
| Kaliyeva Nazerke (C) | News, trust and platform | Modules `NEWS`, `TRUST`, `PLAT`: news ingestion and stories, fact-check and moderation, backend and feed, DevOps; requirements; verification plan |

**Supervisor:** Kozhakhmet Zhaksylyk Yerdenuly, School of Software Engineering.

## Scope

**In scope (MVP):** English-language web app; news ingestion from open sources and grouping into stories; AI meme variants from a story; a check of each meme against its story before publishing; an "AI-made" label; creator earnings from a share of mocked ad revenue and from paid subscriptions; KYC in a provider sandbox before monetization; payouts in test PYUSD on Arbitrum Sepolia; a withdrawal flow in the PayPal sandbox.

**Out of scope:** real money and mainnet deployment, mobile apps, video memes, languages other than English.

Full scope: [docs/01-proposal.md](docs/01-proposal.md).

## Current status

| Stage | Date | Status |
|---|---|---|
| Pre-defense 1: analysis and design | 24 Oct 2026 | Submitted, tag `pre-defense-1` |
| M1: end-to-end scenario on testnet | per university schedule | Planned |
| Pre-defense 2 | per university schedule | Planned |
| M2: all MVP features | per university schedule | Planned |
| M3: evaluation studies | per university schedule | Planned |
| Final pre-defense and defense | per university schedule | Planned |

There is no runnable code yet. Plan and next steps: [docs/10-project-plan.md](docs/10-project-plan.md).

## Selected technologies (preliminary)

| Layer | Choice | Justification |
|---|---|---|
| Payouts | Arbitrum Sepolia testnet, test PYUSD, Solidity smart contract | [D1](docs/05-technology-comparison.md#d1-payout-network-and-method) |
| Identity verification | Didit sandbox (preliminary), Veriff as backup | [D2](docs/05-technology-comparison.md#d2-kyc-provider) |
| AI generation | gpt-oss-20b via a free API, same model locally as fallback | [D3](docs/05-technology-comparison.md#d3-meme-generation-approach) |
| Meme images | Meme templates and text, self-hosted memegen | [D4](docs/05-technology-comparison.md#d4-how-the-meme-image-is-made) |
| Backend | Python, FastAPI | [D5](docs/05-technology-comparison.md#d5-server-platform) |
| Data | PostgreSQL with pgvector | [D6](docs/05-technology-comparison.md#d6-data-storage) |
| Service interaction | REST plus Celery task queue with Redis | [D7](docs/05-technology-comparison.md#d7-component-interaction) |
| Infrastructure | Docker Compose, GitHub Actions | |

## Links

- **YouTrack project:** `<add YouTrack link>`
- **Documentation:** [docs/](docs/) — files are numbered like the pre-defense components (01–11)
- **Diagrams:** [diagrams/](diagrams/) — Mermaid and PlantUML sources in `src/`, PNG exports in `export/`
- **Prototype:** [docs/08-prototype/](docs/08-prototype/README.md)
- **Pre-defense 1 submission summary:** [docs/submissions/pre-defense-1.md](docs/submissions/pre-defense-1.md)

## Repository structure

```text
docs/            proposal, evidence, literature, comparisons, requirements,
                 architecture, prototype, verification plan, plan, risks,
                 supervisor feedback, submission summaries
diagrams/src/    editable diagram sources (Mermaid, PlantUML)
diagrams/export/ readable exports (PNG)
src/             application code by component (from M1)
tests/           automated tests and test materials (from M1)
config/          dependency definitions and configuration examples
```

## How we work

1. Every meaningful work item is a YouTrack task with an assignee, priority, due date, expected outcome and acceptance criteria.
2. One branch per task: `DIP-<id>-short-name`. Commit messages start with the task ID: `DIP-20: Add use case diagram`.
3. Changes reach `main` only through a pull request that names the task, explains the change and says how it was checked.
4. Another team member reviews every pull request: A reviews B, B reviews C, C reviews A.
5. A task is closed only when its acceptance criteria are met.
6. Each pre-defense submission is tagged: `pre-defense-1`, `pre-defense-2`, `final-pre-defense`. Tags are never moved.

## Setup, run and test

No runnable code yet. Instructions will be added with the first runnable component.

## Security

Never commit passwords, API keys, wallet private keys or seed phrases, or personal data of interview participants. Copy [.env.example](.env.example) to `.env` and fill in local values; `.env` is ignored by Git.
