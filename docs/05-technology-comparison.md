# 5. Technology comparison

Each decision lists the requirements that drive it, 2–4 alternatives, the comparison and the choice. Requirement IDs refer to [06-requirements.md](06-requirements.md). All facts accessed on 24 Oct 2026; prices and limits change, so they are stated "as of" that date.

| Decision | Owner | Choice |
|---|---|---|
| [D1 Payout network and method](#d1-payout-network-and-method) | A | Arbitrum Sepolia, test PYUSD |
| [D2 KYC provider](#d2-kyc-provider) | A | Didit (preliminary), Veriff as backup |
| [D3 Meme generation approach](#d3-meme-generation-approach) | B | Hybrid: free API and the same open-weight model locally |
| [D4 How the meme image is made](#d4-how-the-meme-image-is-made) | B | Template plus text, self-hosted |
| [D5 Server platform](#d5-server-platform) | C | FastAPI |
| [D6 Data storage](#d6-data-storage) | C | PostgreSQL with pgvector |
| [D7 Component interaction](#d7-component-interaction) | C | REST plus a task queue (Celery, Redis) |

## D1. Payout network and method

**Owner:** A. **Driven by:** FR-MON-04 (payouts in a dollar-pegged stablecoin), FR-MON-05 (creators can verify payouts), NFR-01 (no real money), NFR-06 (payout cost).

| Criterion | Arbitrum Sepolia | Base Sepolia | No blockchain: PayPal Payouts only |
|---|---|---|---|
| Test PYUSD | ✓ Paxos lists a test PYUSD contract on Arbitrum Sepolia [1]; tokens from the Paxos faucet [2] | ✗ not in Paxos's testnet list [1]; only a mock token | not needed |
| Test ETH for gas | faucet, 0.1 ETH per 24 h [3] | faucet, up to 0.1 ETH per 24 h [4] | not needed |
| PYUSD on mainnet (real product) | ✓ listed by Paxos [5] | ✗ not listed [5] | n/a |
| Creator can verify payouts (FR-MON-05) | ✓ public on-chain records | ✓ public on-chain records | ✗ private records |
| Average mainnet fee | about $0.004 per transaction [6] | about $0.002 [6] | Payouts fees not compared |
| Payouts in Kazakhstan | wallet payouts | wallet payouts | PayPal Payouts lists Kazakhstan as "send, receive and withdraw" [7] |

**Decision:** Arbitrum Sepolia with test PYUSD through our payout contract. It is the only network with official test and mainnet PYUSD, and it keeps payouts verifiable on-chain, which the PayPal-only option cannot do (FR-MON-05). Fees on both networks are fractions of a cent according to one source; we measure gas ourselves in study 3. Unit tests use a mock ERC-20; the integration run uses real test PYUSD (risk R3). The PayPal sandbox stays as the withdrawal step.

Sources: [1] Paxos, PYUSD on test networks — https://docs.paxos.com/guides/stablecoin/pyusd/testnet · [2] Paxos faucet — https://faucet.paxos.com/ · [3] Alchemy, Arbitrum Sepolia faucet — https://www.alchemy.com/faucets/arbitrum-sepolia · [4] Base docs, network faucets — https://docs.base.org/base-chain/tools/network-faucets · [5] Paxos, PYUSD on main networks — https://docs.paxos.com/guides/stablecoin/pyusd/mainnet · [6] ethereum.org, Layer 2 networks (updated 22 Oct 2026) — https://ethereum.org/en/layer-2/networks/ · [7] PayPal Developer, Payouts countries and features — https://developer.paypal.com/payouts/supported-features

## D2. KYC provider

**Owner:** A. **Driven by:** FR-MON-01 (KYC before monetization), NFR-01 (no real money, budget), NFR-04 (store only KYC status).

| Criterion | Sumsub | Didit | Veriff | Persona |
|---|---|---|---|---|
| Sandbox | integration testing only, up to 500 profiles per 24 h [1] | free sandbox [2]; sources disagree, to be checked | unlimited test checks during a 15-day trial [3] | sandbox without real checks [4] |
| Kazakhstan documents | not confirmed in public docs [1] | ✓ ID card, passport, driving licence [5] | ✓ passport, ID card, driving licence, residence permit [6] | not checked |
| Web integration | Web SDK, webhooks [1] | Web SDK, hosted flow [2] | Web SDK, hosted page [3] | hosted flow [4] |
| Price after sandbox | from $1.35 per check, min. $149/month [7] | $0.33 per full KYC, no minimum; new pricing from 1 Nov 2026 [2] | from $0.80 per check, min. $49/month [3] | from $250/month [8] |
| Certifications | SOC 2 Type 2, ISO/IEC 27001 [9] | SOC 2, ISO/IEC 27001 [2] | SOC 2 Type II, ISO/IEC 27001:2022 [3] | SOC 2 Type 2 [8] |

**Decision (preliminary):** Didit. It confirms Kazakhstan documents, has a free sandbox and the lowest price with no monthly minimum, which fits the budget. Its sandbox terms are contradictory in its own pages, so A confirms them in a test account before M1; Veriff is the backup. Only test documents are used; no real identity documents of participants (risk R12).

Sources: [1] Sumsub, sandbox — https://docs.sumsub.com/docs/sandbox-mode · [2] Didit, pricing — https://didit.me/pricing · [3] Veriff, pricing — https://www.veriff.com/pricing · [4] Persona Help, key concepts — https://help.withpersona.com/articles/14hgKH7lZo9b6ja7tRJobW · [5] Didit, Kazakhstan — https://didit.me/solutions/countries/kazakhstan/ · [6] Veriff, supported countries — https://www.veriff.com/supported-countries · [7] Sumsub, pricing — https://sumsub.com/pricing/ · [8] Persona, pricing — https://withpersona.com/pricing · [9] Sumsub, Trust Center — https://sumsub.com/sumsub-trust-center

## D3. Meme generation approach

**Owner:** B. **Driven by:** FR-GEN-02 (meme variants for a story), NFR-02 (generation ≤ 20 s), NFR-01 (free tiers only), NFR-04 (no personal data to third parties).

| Criterion | API only (Gemini free tier) | Open-weight model only (gpt-oss-20b locally) | Hybrid: gpt-oss-20b via Groq free API, local fallback |
|---|---|---|---|
| Cost | free tier [1] | free; needs about 16 GB of memory [3] | free [2] |
| Limits | not guaranteed, shown only in the console [1] | our hardware | 30 requests/min, 1,000/day for this model [2] |
| Data on the free tier | prompts may be used to improve products and read by people [4] | stays with us | inference data not retained by default [5] |
| Licence of the model | provider terms | Apache 2.0 [3] | Apache 2.0, same weights [2][3] |
| Same model for evaluation runs | ✗ hosted model may change | ✓ | ✓ API and local runs use the same weights |

**Decision:** hybrid with gpt-oss-20b: the free Groq API for normal use, the same weights locally when limits run out (risk R2). The same model in both modes keeps study 1 reproducible. Only news text goes to the API, never personal data. Captions are text, so templates are chosen by our code (D4).

Sources: [1] Gemini API, rate limits — https://ai.google.dev/gemini-api/docs/rate-limits · [2] Groq, rate limits — https://console.groq.com/docs/rate-limits · [3] Azure AI Foundry, gpt-oss-20b — https://ai.azure.com/catalog/models/gpt-oss-20b · [4] Gemini API, additional terms — https://ai.google.dev/gemini-api/terms · [5] Groq, your data — https://console.groq.com/docs/your-data

## D4. How the meme image is made

**Owner:** B. **Driven by:** FR-GEN-02, FR-TRUST-01 (check the meme against its story), FR-TRUST-03 (nothing public before moderation), NFR-01 (budget).

| Criterion | Template plus text | Image generation | Hybrid: generated background plus text |
|---|---|---|---|
| Tools | memegen (MIT code, stateless API, self-hostable) [1]; Imgflip API [2] | FLUX.1 [schnell], Apache 2.0 [3] | both |
| Cost | free | own GPU, or about $0.034 per image on paid APIs [4] | sum of both |
| Privacy before moderation | self-hosted memegen keeps drafts private; Imgflip makes every created meme public by URL [2] | local generation stays with us | depends |
| Fact-check | caption is a separate text, checked text-to-text against the story | text inside the image is harder to check | text added by code |
| Licensing risk | template images: licence not stated → risk R7 | model output; legal status of AI images to be checked | both |

**Decision:** template plus text with a self-hosted memegen. Captions stay a separate text, so the fact-check (FR-TRUST-01) works text-to-text, and nothing becomes public before moderation. We keep a register of templates with source and licence. Image generation is a Could for later.

Sources: [1] memegen — https://github.com/jacebrowning/memegen · [2] Imgflip API — https://imgflip.com/api · [3] FLUX.1 [schnell] model card — https://huggingface.co/black-forest-labs/FLUX.1-schnell · [4] Gemini API, pricing — https://ai.google.dev/gemini-api/docs/pricing
