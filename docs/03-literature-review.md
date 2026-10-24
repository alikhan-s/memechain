# 3. Literature review

**Owner:** B (consolidation). Theme A — A, theme B — B, theme C — C.
**Structured table:** [03-literature-table.csv](03-literature-table.csv). **Citation style:** APA 7.

## Search method

- **Databases:** Google Scholar, ACL Anthology, ACM Digital Library, publisher sites (ScienceDirect, INFORMS, Nature, Oxford Academic), arXiv for open versions of published papers.
- **Inclusion criteria:** peer-reviewed journal articles or full papers at reputable conferences; published 2021–2026; directly relevant to one of the three themes.
- **Exclusion criteria:** preprints without a published version, blogs, white papers, predatory venues.
- **Quality checks:** identity via DOI; venue via SJR (journals) and the venue record (conferences); retraction status on the publisher's page.
- **Search log:** queries, filters and result counts are recorded in the table below, section [Search log](#search-log).

The review is organised by theme. Official standards and documentation are used only for technical facts and are listed separately as grey literature.

## Theme A: creator monetization and blockchain payouts

**How platforms share revenue with creators.** Bhargava (2022) [A1] models a platform that shares advertising revenue with creators and shows that the sharing rate affects both how much content is supplied and how concentrated earnings become. The work is an analytical model without empirical data, so it explains mechanisms rather than measuring them. Empirical data point in the same direction: on Twitch, income from subscriptions and donations is highly unequal across streamers (Houssard et al., 2023) [A2]. Together they suggest that a revenue-share model needs transparent rules and an inequality measure among its evaluation metrics.

**Identity verification before payouts.** Schlatt et al. (2022) [A3] design and evaluate a digital KYC process built on self-sovereign identity, in which verified credentials stay with the user rather than on a blockchain. Their context is banking; applying the idea to a creator platform is our design decision, and their discussion of the tension between data protection and anti-money-laundering record keeping is a limitation we take into account.

**Layer-2 networks for low-cost payouts.** Gangwal et al. (2023) [A4] survey Layer-2 protocols and compare payment channels with rollups on cost, finality and withdrawal delay. Their comparison supports choosing a rollup network for many small payouts. The literature we found does not include peer-reviewed measurements of payout cost on Arbitrum specifically; we will measure this ourselves (study 3 in the [verification plan](09-verification-plan.md)).

**What the project takes into account:** earnings concentration (A1, A2) → transparent earnings calculation and an inequality metric; privacy of identity data (A3) → KYC through a provider, only verification status stored; payout cost depends on the network (A4) → measured, not assumed.

## Theme B: AI meme generation

**Generating memes with language and vision models.** Wang and Lee (2024) [B1] generate memes by describing a template image with a vision-language model, writing captions with a language model and filtering hateful outputs, and evaluate the results with human ratings. Wu et al. (2025) [B2] compare memes created by people alone, by people with a language model and by the model alone, rating humour, creativity and shareability. Both show that model-generated captions can be competitive, and both rely on human evaluation.

**Evaluating generated content.** Human rating is costly, so language models are often used as judges. Bavaresco et al. (2025) [B3] compare model judges with human annotations across 20 evaluation tasks and find that agreement varies widely by task, which means a model judge must be checked against humans before it is trusted.

**Harmful memes.** Sharma et al. (2022) [B5] survey the types of harmful memes and the datasets and methods for detecting them. Harmful content is a known risk of meme generation, so a filter before publishing is required.

**What the project takes into account:** human ratings as the reference for quality (B1, B2); a model judge only after measuring its agreement with humans (B3); a harmful-content filter before publishing (B1, B5). **Gap:** we found no peer-reviewed work that generates memes from news stories and checks them against the stories.

## Theme C: news processing and fact-checking

**From news streams to stories.** Yoon et al. (2023) [C2] discover stories in a continuous news stream without labelled data, by clustering article embeddings online, and evaluate clusters with standard metrics (B³-F1, AMI, ARI). This matches our step of grouping news into stories and gives us metrics for it.

**Checking generated text against a source.** Guo et al. (2022) [C5] define the stages of automated fact-checking and separate checking a claim's truth from checking its consistency with evidence. Tang et al. (2024) [C1] show that a small model can check whether a claim is supported by a grounding document at a fraction of the cost of large models. This is the check Memechain needs: whether a meme is consistent with its source story, not whether the story is true. Neither work was evaluated on humorous text such as memes, which is a limitation for us.

**Labelling AI-generated content.** Altay and Gilardi (2024) [C3] find in online experiments that people trust headlines labelled as AI-generated less, even when they are true or written by people, because they assume full automation. A label therefore needs careful wording.

**What the project takes into account:** consistency with the source rather than truth (C5); a small grounding-based checker as the starting point (C1), evaluated on memes because the original benchmarks do not include them; story clustering metrics (C2); label wording that explains how the meme was made (C3).

## Summary of limitations the project takes into account

| Limitation in the literature | How Memechain responds |
|---|---|
| Revenue-share effects are modelled, not measured (A1) | Earnings rules are public; an inequality metric is part of the evaluation |
| KYC research is from banking (A3) | KYC through a provider sandbox; only status is stored |
| No measured payout costs on Arbitrum (A4) | Study 3 measures cost and speed |
| Meme generation is evaluated without news grounding (B1, B2) | Memes are generated from a story and checked against it |
| Model judges disagree with humans on some tasks (B3) | Judge agreement is measured on a human-rated subset |
| Fact-checkers are not evaluated on memes (C1) | Study 2 evaluates the check on labelled meme–story pairs |

## Grey literature (technical facts only)

- Paxos. *PYUSD testnet addresses* (Paxos sandbox documentation). https://docs.sandbox.paxos.com/guides/stablecoin/pyusd/testnet
- Offchain Labs. *Gas and fees* (Arbitrum documentation). https://docs.arbitrum.io/how-arbitrum-works/deep-dives/gas-and-fees
- FATF. (2021). *Updated guidance for a risk-based approach to virtual assets and virtual asset service providers*. https://www.fatf-gafi.org/en/publications/Fatfrecommendations/Guidance-rba-virtual-assets-2021.html
- C2PA. *C2PA technical specification*. https://spec.c2pa.org/

## References

Altay, S., & Gilardi, F. (2024). People are skeptical of headlines labeled as AI-generated, even if true or human-made, because they assume full AI automation. *PNAS Nexus, 3*(10), pgae403. https://doi.org/10.1093/pnasnexus/pgae403

Bavaresco, A., Bernardi, R., Bertolazzi, L., Elliott, D., Fernández, R., Gatt, A., Ghaleb, E., Giulianelli, M., Hanna, M., Koller, A., Martins, A., Mondorf, P., Neplenbroek, V., Pezzelle, S., Plank, B., Schlangen, D., Suglia, A., Surikuchi, A. K., Takmaz, E., & Testoni, A. (2025). LLMs instead of human judges? A large scale empirical study across 20 NLP evaluation tasks. In *Proceedings of the 63rd Annual Meeting of the Association for Computational Linguistics (Volume 2: Short Papers)* (pp. 238–255). https://doi.org/10.18653/v1/2025.acl-short.20

Bhargava, H. K. (2022). The creator economy: Managing ecosystem supply, revenue sharing, and platform design. *Management Science, 68*(7), 5233–5251. https://doi.org/10.1287/mnsc.2021.4126

Gangwal, A., Gangavalli, H. R., & Thirupathi, A. (2023). A survey of Layer-two blockchain protocols. *Journal of Network and Computer Applications, 209*, 103539. https://doi.org/10.1016/j.jnca.2022.103539

Guo, Z., Schlichtkrull, M., & Vlachos, A. (2022). A survey on automated fact-checking. *Transactions of the Association for Computational Linguistics, 10*, 178–206. https://doi.org/10.1162/tacl_a_00454

Houssard, A., Pilati, F., Tartari, M., Sacco, P. L., & Gallotti, R. (2023). Monetization in online streaming platforms: An exploration of inequalities in Twitch.tv. *Scientific Reports, 13*, 1103. https://doi.org/10.1038/s41598-022-26727-5

Schlatt, V., Sedlmeir, J., Feulner, S., & Urbach, N. (2022). Designing a framework for digital KYC processes built on blockchain-based self-sovereign identity. *Information & Management, 59*(7), 103553. https://doi.org/10.1016/j.im.2021.103553

Sharma, S., Alam, F., Akhtar, M. S., Dimitrov, D., Da San Martino, G., Firooz, H., Halevy, A., Silvestri, F., Nakov, P., & Chakraborty, T. (2022). Detecting and understanding harmful memes: A survey. In *Proceedings of the Thirty-First International Joint Conference on Artificial Intelligence (IJCAI-22)* (pp. 5597–5606). https://doi.org/10.24963/ijcai.2022/781

Tang, L., Laban, P., & Durrett, G. (2024). MiniCheck: Efficient fact-checking of LLMs on grounding documents. In *Proceedings of the 2024 Conference on Empirical Methods in Natural Language Processing* (pp. 8818–8847). https://doi.org/10.18653/v1/2024.emnlp-main.499

Wang, H., & Lee, R. K.-W. (2024). MemeCraft: Contextual and stance-driven multimodal meme generation. In *Proceedings of the ACM Web Conference 2024*. https://doi.org/10.1145/3589334.3648151

Wu, Z., Weber, T., & Müller, F. (2025). One does not simply meme alone: Evaluating co-creativity between LLMs and humans in the generation of humor. In *Proceedings of the 30th International Conference on Intelligent User Interfaces* (pp. 1082–1092). https://doi.org/10.1145/3708359.3712094

Yoon, S., Lee, D., Zhang, Y., & Han, J. (2023). Unsupervised story discovery from continuous news streams via scalable thematic embedding. In *Proceedings of the 46th International ACM SIGIR Conference on Research and Development in Information Retrieval* (pp. 802–811). https://doi.org/10.1145/3539618.3591782

## Search log

| # | Who | Database | Query | Filters | Results | Kept |
|---|---|---|---|---|---|---|
| 1 | A | Google Scholar | `"creator economy" "revenue sharing" OR "Layer-2" blockchain` | 2021–2026 | 1,420 | 4 (A1–A4) |
| 2 | B | Google Scholar | `"meme generation" "large language model" OR "harmful memes"` | 2021–2026 | 1,180 | 4 (B1–B3, B5) |
| 3 | C | Google Scholar | `"automated fact-checking" "grounding" OR "news stream" story discovery` | 2021–2026 | 1,650 | 4 (C1–C3, C5) |
