# 1. Project proposal

| | |
|---|---|
| **Title** | Memechain: Development of a Blockchain-Based Monetization Platform for Content Creators with AI-Driven Meme Generation from News Feeds |
| **Team** | Serik Alikhan (A), Toleukhan Alizhan (B), Kaliyeva Nazerke (C); group SE-2421 |
| **Supervisor** | Kozhakhmet Zhaksylyk Yerdenuly, School of Software Engineering |
| **Owner of this document** | A |

## Problem statement

Memes about current events are one of the most shared forms of online content, but the people who make them face three connected problems.

1. **Speed against accuracy.** A meme about a news story is valuable while the story is fresh. Generative AI can propose meme variants in seconds ([B1](03-literature-review.md#theme-b-ai-meme-generation), [B2](03-literature-review.md#theme-b-ai-meme-generation)), but generated text can contradict its source. Fact-checking research treats consistency with a source document as a separate, measurable task ([C1](03-literature-review.md#theme-c-news-processing-and-fact-checking), [C5](03-literature-review.md#theme-c-news-processing-and-fact-checking)). Our search found no peer-reviewed work that generates memes from news stories and checks them against those stories.
2. **Hard and opaque monetization.** Large platforms pay creators only after audience thresholds (for example, 1,000 subscribers on YouTube), some programmes do not pay creators in Kazakhstan at all, and creators see estimates rather than a calculation they can verify ([existing systems](04-existing-systems.md)). Earnings on creator platforms are also highly unequal ([A2](03-literature-review.md#theme-a-creator-monetization-and-blockchain-payouts)).
3. **No system joins the chain.** Among the systems we compared, none links a news story, the meme made from it, a check of the meme against the story, and payment to the creator. The only dedicated meme generator does not pay creators.

The problem is a working hypothesis supported by documents and literature. Interviews with creators are in progress ([evidence of relevance](02-interviews/README.md)); findings will confirm or revise it.

## Target users

- **Creators:** English-speaking meme creators and page admins who react to news.
- **Viewers:** people who read the feed and may subscribe to creators.
- **Moderators:** platform staff who review flagged memes.

## Aim

To develop and evaluate a web platform where creators generate memes from news stories with AI assistance, each meme is checked against its source story before publishing, and creators earn from a share of ad revenue and paid subscriptions, paid out in a stablecoin on a testnet after identity verification.

## Objectives

1. To identify creators' needs and constraints through interviews, analysis of existing systems and a literature review.
2. To design the requirements, architecture and prototype of the platform.
3. To implement the pipeline from news ingestion to meme generation, fact-check and publication.
4. To implement creator earnings, the KYC gate and stablecoin payouts on a testnet.
5. To evaluate meme quality, fact-check accuracy, and payout cost and speed against baselines.

## Expected outcomes

- A working beta on testnets and sandboxes covering the full chain: news → story → meme variants → fact-check → publication → earnings → payout.
- Three evaluation studies, one per team member ([verification plan](09-verification-plan.md)).
- The diploma thesis.

## Scope

**In scope (MVP)**

- English-language web application.
- News ingestion from open sources (RSS) and grouping of articles into stories.
- AI-generated meme variants for a chosen story, using meme templates and text.
- An automatic check of each meme against its story before publishing, and an "AI-made" label.
- Creator earnings from a share of ad revenue (ads are mocked in the MVP) and from paid subscriptions.
- Identity verification (KYC) in a provider sandbox before monetization is enabled.
- Payouts in test PYUSD on the Arbitrum Sepolia testnet through a payout smart contract.
- A withdrawal flow in the PayPal sandbox.

**Out of scope**

- Real money, mainnet deployment and real advertising.
- Mobile applications, video memes, languages other than English.
- Verifying whether the news itself is true: the platform checks that a meme is consistent with its source story, not the story's truth.

**Constraints:** total cash budget of about 10,000 KZT for the whole project; only free tiers, testnets and sandboxes.

## Engineering complexity

The project combines three technical areas in one system: news processing (ingestion, clustering into stories), generative AI (meme generation and its evaluation) and blockchain payments (a payout smart contract on a Layer-2 testnet). On top of these sit two cross-cutting mechanisms: an identity-verification gate before money moves and an automatic consistency check before content is published. Each team member owns one area and one evaluation study.
