# 6. Requirements specification

**Owner:** C (consolidation). Module sections: `MON` — A, `GEN` — B, `NEWS`, `TRUST`, `PLAT` and non-functional requirements — C.

## Conventions

- **IDs:** `FR-<MODULE>-<nn>` for functional requirements, `NFR-<nn>` for non-functional ones.
- **Priority (MoSCoW):** Must — required for the MVP; Should — important, planned; Could — if time allows; Won't — not in this project.
- **Source:** `D1–D5` — findings from data analysis ([02](02-interviews/README.md)); `H1–H5` — hypotheses still to be confirmed by interviews (assumption); literature IDs such as `A1` ([03](03-literature-review.md)); `S` — project scope decision ([01](01-proposal.md)).
- Every Must requirement has a check in the [verification plan](09-verification-plan.md).

## Actors

| Actor | Description |
|---|---|
| Creator | Makes and publishes memes, earns money |
| Viewer | Reads the feed, subscribes to creators, reports memes |
| Moderator | Reviews flagged and reported memes |
| External systems | News sources, LLM API, KYC provider, Ad network (mock), Arbitrum Sepolia, PayPal sandbox |

## Functional requirements

### MON — monetization (A)

| ID | Requirement | Priority | Acceptance criteria | Source |
|---|---|---|---|---|
| FR-MON-01 | Monetization is enabled only after the creator's KYC is approved | Must | A creator without approved KYC cannot request payouts and sees a prompt to verify; after approval in the provider sandbox, payouts become available | D5, A3, H4 |
| FR-MON-02 | The platform credits each creator a share of mocked ad revenue in proportion to valid views of their memes | Must | For a test period with a known revenue pool and view counts, each creator's credited amount equals pool × share rate × creator views ÷ total views, to the cent | D1, A1 |
| FR-MON-03 | A viewer can subscribe to a creator for a monthly price set by the creator | Must | After a test subscription payment, the subscription is active for 30 days and the creator's balance increases by the price minus the published platform fee | S, H1 |
| FR-MON-04 | A creator can request a payout of their balance in test PYUSD to their wallet on Arbitrum Sepolia | Must | The payout transaction is confirmed on Arbitrum Sepolia, the wallet receives the requested amount and the platform balance decreases by the same amount | S, D1 decision |
| FR-MON-05 | A creator can see how each credited amount was calculated and a link to each payout transaction | Must | The earnings page shows for every credit: period, views or subscription, rate, amount; every payout links to its transaction in the block explorer | D3, A2, H5 |
| FR-MON-06 | A creator can start a withdrawal to PayPal in the sandbox | Could | A sandbox payout to a test PayPal account completes and is shown in the creator's history | S |

### GEN — meme generation (B)

| ID | Requirement | Priority | Acceptance criteria | Source |
|---|---|---|---|---|
| FR-GEN-01 | A creator can open a story and start meme generation from it | Must | The story page has a "Make a meme" action that opens the studio with the story's title and summary filled in | D4, H2 |
| FR-GEN-02 | The studio generates several meme variants for the story: a template image and captions | Must | For any story, at least 3 variants appear within the time in NFR-02 | B1, H2 |
| FR-GEN-03 | The creator can pick a variant and edit its captions before publishing | Must | Edited captions are saved and shown in the preview exactly as typed | B2 |
| FR-GEN-04 | The creator can regenerate variants with a different tone (for example, ironic, neutral) | Should | Choosing another tone produces a new set of at least 3 variants | B1 |

### NEWS — news and stories (C)

| ID | Requirement | Priority | Acceptance criteria | Source |
|---|---|---|---|---|
| FR-NEWS-01 | The system ingests articles from configured RSS sources on a schedule | Must | New articles from every configured source appear within 30 minutes of publication; duplicates are stored once | S |
| FR-NEWS-02 | The system groups articles about the same event into stories | Must | On the labelled evaluation set, clustering reaches the B³-F1 target set in the verification plan | C2 |
| FR-NEWS-03 | Each story shows its articles with links to the original sources | Must | Every story page lists at least one article with a working link to the source | S, C5 |

### TRUST — fact-check and moderation (C)

| ID | Requirement | Priority | Acceptance criteria | Source |
|---|---|---|---|---|
| FR-TRUST-01 | Before publishing, each meme is checked for consistency with its source story; inconsistent memes are flagged and need confirmation or editing | Must | On the labelled set of meme–story pairs, the check reaches the F1 target in the verification plan; a flagged meme cannot be published without an explicit creator action | D4, C1, C5, H3 |
| FR-TRUST-02 | Every published meme carries an "AI-made" label that says which part was generated | Must | 100% of published memes show the label; the label text explains that captions were AI-generated and edited by the creator | C3 |
| FR-TRUST-03 | Memes that the harmful-content filter flags are not published until a moderator reviews them | Must | A test set of harmful examples is held for review; none of them appears in the feed | B5 |
| FR-TRUST-04 | Viewers can report a meme; reported memes go to the moderation queue | Must | A report creates a queue item within 1 minute; the moderator can approve or remove the meme | S |

### PLAT — platform (C)

| ID | Requirement | Priority | Acceptance criteria | Source |
|---|---|---|---|---|
| FR-PLAT-01 | Users can sign up and sign in as creator or viewer; moderators are assigned by an admin | Must | Each role sees only its own actions; access to another role's endpoint returns 403 | S |
| FR-PLAT-02 | Viewers see a feed of published memes, newest first, each with its story link | Must | The feed shows only published memes; every item links to its story | S |
| FR-PLAT-03 | A creator can publish a meme that passed the checks | Must | A published meme appears in the feed within 10 seconds | S |

## Non-functional requirements

| ID | Requirement | Priority | Acceptance criteria |
|---|---|---|---|
| NFR-01 | No real money: all payments use testnets and sandboxes | Must | Configuration contains only testnet RPC endpoints and sandbox keys; a CI check fails on mainnet chain IDs |
| NFR-02 | Performance | Must | Feed API p95 ≤ 500 ms with 50 concurrent users; meme variants generated in ≤ 20 s p95 (load test) |
| NFR-03 | Secrets are never committed | Must | A secret scanner runs in CI on every pull request and reports no findings on `main` |
| NFR-04 | Privacy of identity data: the platform stores only the KYC status and provider reference, not documents | Must | Database schema review shows no document images or ID numbers; KYC data stays with the provider |
| NFR-05 | Smart-contract safety | Must | Payout contract tests cover every external function; static analysis reports no high-severity issues |
| NFR-06 | Payout cost is measured and reported | Should | Study 3 reports gas per payout and confirmation time over at least 100 test payouts |
| NFR-07 | The backend API is documented | Should | OpenAPI documentation is generated and covers 100% of public endpoints |
| NFR-08 | Accessibility of key screens | Could | Key screens pass an automated accessibility check with no critical issues |

## Traceability

| Requirement | Diagram | Screen | Check |
|---|---|---|---|
| FR-MON-01 | Use case "Pass KYC" | KYC | Integration test with KYC sandbox |
| FR-MON-02 | Component "Monetization service" | Earnings | Unit test of the share formula |
| FR-MON-04 | Component "Payout contract" | Earnings and payout | Contract test; study 3 |
| FR-MON-05 | Component "Monetization service" | Earnings and payout | End-to-end test |
| FR-GEN-02 | Component "Generation service" | Creator studio | Study 1 |
| FR-NEWS-02 | Component "News service" | Story feed | Clustering evaluation |
| FR-TRUST-01 | Use case "Check meme against news" | Check and publish | Study 2 |
| FR-TRUST-02 | Component "Trust service" | Feed | End-to-end test |
| FR-TRUST-04 | Use case "Review flagged memes" | Moderation queue | Integration test |
