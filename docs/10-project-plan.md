# 10. Project plan

**Owner:** B. **Repository:** https://github.com/alikhan-s/memechain.git · **YouTrack project (DIP):** DIP

## Responsibilities

| Member | Module | Owns documents | Evaluation study |
|---|---|---|---|
| A — Serik Alikhan | `MON` | 01 proposal, 04 existing systems, 07 architecture, 10 risk register | Study 3: payout cost and speed |
| B — Toleukhan Alizhan | `GEN` | 02 evidence, 03 literature review, 10 project plan, 11 supervisor feedback | Study 1: meme quality |
| C — Kaliyeva Nazerke | `NEWS`, `TRUST`, `PLAT` | README, 06 requirements, 09 verification plan, submission | Study 2: fact-check accuracy |

Each member also writes the parts of shared documents for their own module. Pull requests are reviewed in a ring: A reviews B, B reviews C, C reviews A.

## Milestones

| Milestone | What is ready | Date |
|---|---|---|
| PD-1 | Analysis and design package, tag `pre-defense-1` | 24 Oct 2026 |
| M1 | End-to-end scenario on testnet: news → story → meme → check → publish → earning → payout | per university schedule |
| PD-2 | Pre-defense 2, tag `pre-defense-2` | per university schedule |
| M2 | All Must requirements implemented | per university schedule |
| M3 | Three evaluation studies completed | per university schedule |
| M4 | Thesis text | per university schedule |
| Final | Final pre-defense and defense | per university schedule |

Dates after 24 Oct 2026 will be aligned with the official academic calendar.

## Dependencies

| Work | Depends on |
|---|---|
| Technology decisions (05) | Requirements (06) |
| Diagrams (07), wireframes (08) | Glossary and requirements (06, 07) |
| Verification plan (09) | Requirements (06) |
| Payout implementation | D1 decision; test PYUSD or mock token (risk R3) |
| Monetization gate | KYC sandbox test (D2) |
| Study 2 | Labelled story–meme pairs |
| Study 1 | Generation service working end to end |

## Next steps after pre-defense 1

1. Complete interviews (target 5+) and update the evidence synthesis (B, with A and C).
2. Test the KYC sandbox and confirm D2; re-check prices and limits in 05 (A, B, C).
3. Build the Figma prototype for the key scenarios (A, B, C).
4. Implement the M1 end-to-end scenario on testnet (all).
5. Prepare labelled sets for studies 1 and 2 (B, C).
