# 2. Evidence of relevance

**Owner:** B (synthesis). Interviews are conducted by A, B and C.

We use two sources of evidence:

1. **Interviews with potential users** — meme creators and meme page admins. Target: 3–5 for pre-defense 1, more before pre-defense 2.
2. **Analysis of available data** — official monetization rules and documentation of existing platforms, collected for the [existing system comparison](../04-existing-systems.md).

Each finding below is marked **[verified]** when it is supported by evidence we collected, and **[assumption]** when it is still a hypothesis.

## Method

- **Interview guide:** [guide.md](guide.md); **consent text:** [consent.md](consent.md).
- **Format:** call or text chat, 15–20 minutes, in English or Russian.
- **Recruitment:** direct messages to meme creators and meme page admins (purposive sampling: people who already make memes).
- **Privacy:** notes contain no names, handles, page names or links. Participants are coded P1, P2, … Notes are stored in [notes/](notes/).

## Hypotheses

| ID | Hypothesis | Requirements it affects |
|---|---|---|
| H1 | Creators find it hard to earn from memes directly | `FR-MON` |
| H2 | Making a meme about fresh news takes too long | `FR-GEN` |
| H3 | Creators worry that AI-generated memes can distort the facts | `FR-TRUST` |
| H4 | Creators accept identity verification (KYC) to receive payouts | `FR-MON-01` |
| H5 | Creators want to see how their earnings are calculated | `FR-MON-05` |

## Evidence from available data

| ID | Finding | Status | Source | Hypothesis |
|---|---|---|---|---|
| D1 | YouTube pays creators only after 1,000 subscribers plus 4,000 watch hours in 12 months or 10M Shorts views in 90 days | [verified] | [04, YouTube](../04-existing-systems.md) | H1 |
| D2 | X's creator programme requires a paid subscription, 500 verified followers and 500,000 impressions in 90 days, and Kazakhstan is not on its country list | [verified] | [04, X](../04-existing-systems.md) | H1 |
| D3 | On the platforms compared, earnings shown to creators are estimates or set at the platform's discretion; only Zora's on-chain payouts can be checked independently | [verified] | [04, criterion 6](../04-existing-systems.md) | H5 |
| D4 | None of the platforms compared offers meme generation grounded in a news story or a check of generated content against its source before publishing | [verified] | [04, criteria 7–9](../04-existing-systems.md) | H2, H3 |
| D5 | Platforms that pay creators require identity verification before payouts (YouTube, X) | [verified] | [04, criterion 4](../04-existing-systems.md) | H4 |

## Interviews

| ID | Date | Format | Interviewer | Notes |
|---|---|---|---|---|
| P1 | | | | [notes/P1.md](notes/) |
| P2 | | | | |
| P3 | | | | |

## Synthesis

| Hypothesis | Data analysis | Interviews | Status |
|---|---|---|---|
| H1 | supported (D1, D2) | pending | [assumption] until interviews confirm it for meme creators |
| H2 | gap in tools (D4) | pending | [assumption] |
| H3 | gap in tools (D4) | pending | [assumption] |
| H4 | common practice (D5) | pending | [assumption] for our users |
| H5 | supported (D3) | pending | [assumption] for our users |

**What is verified now:** the barriers and gaps in existing platforms (D1–D5).
**What is still an assumption:** how our target creators experience these barriers and whether they would use the proposed solution. Interviews will confirm or revise H1–H5; requirements whose source is an assumption are marked so in [06-requirements.md](../06-requirements.md).

## Limitations

The number of interviews for pre-defense 1 is small and the sample is purposive, so findings show transferable patterns rather than generalizable facts. We will continue interviews before pre-defense 2 and update this synthesis.
