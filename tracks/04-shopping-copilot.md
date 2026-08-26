# Track 4 — Shopping Copilot: conversational search and recommendations

**Official objective:** build a headless shopping agent over the supplied frozen Amazon catalog. It must distinguish high-intent buying from exploratory browsing, retrieve/rank accurately, maintain multi-turn state, and guide the user to the target purchase in few turns.

Workshop: **28 August 2026, 4:00–4:45pm SGT**. Kit: <https://github.com/TechJam2026/techjam-conversational-search> and its [participant release](https://github.com/TechJam2026/techjam-conversational-search/releases/tag/participant-kit).

## Track summary and example products

You are building the **brain behind a shopping conversation**, using a fixed catalog of 50,000 clothing/shoes/jewellery products. The evaluator simulates a shopper talking to your system. Your system must decide whether the person wants a precise purchase or is still browsing, remember/update their preferences across turns, search the catalog, and return/rank useful candidates.

The key distinction is:

- A **buying** request has hard requirements—e.g. a specific item/category/price/size—and should use precise filters.
- A **browsing** request is exploratory—e.g. a vague situation or style—and should return diverse relevant possibilities or ask a useful clarifying question.

The evaluator has a hidden target product for each conversation. You score well by including it, ranking it highly, and reaching it in few turns. You do not make a webpage; the organizer tests the backend agent interface directly. A friendly chat response is not enough if the retrieval and ranked product output are wrong.

Example product directions: an intent router that selects buying versus browsing retrieval; a hybrid lexical/category/vector search-and-reranking Agent; or a dialogue-state engine that handles preference changes and asks focused clarification questions. The team needs to implement and run the supplied Python Agent interface and evaluator.

### What success looks like

- The supplied evaluator can call your Agent and receive valid results.
- The Agent reacts differently to precise buying vs exploratory browsing requests.
- It correctly changes its “memory” when a shopper changes their mind.
- It avoids wasting turns: it recommends when enough information exists and asks targeted questions when it does not.

## Core pillars expected by the brief

1. **Intent routing and hybrid retrieval:** route buying requests to high-precision hard-constraint filtering; route browsing requests to diverse dense retrieval. Use in-memory multi-route retrieval across keyword, category, and vector similarity, then semantic ranking.
2. **Multi-turn dialogue evolution:** accumulate slots; on an intent override, erase/rewrite obsolete state; when the request is too general, cut off retrieval and ask structured clarification questions.
3. **Dynamic context programming:** distil history into short-term session state and long-term user profile, then adapt runtime workflow and guidance logic.
4. **Product and efficiency measurement:** optimise retrieval coverage (Hit Rate@K), exact-item ranking (MRR/Top-K hit), and Mean Turns to Conversion (MTTC).

## Official constraints

- Evaluation is backend API/headless only; UI/UX is out of scope.
- Catalog, pricing, category tree, and sessions are static. The 50,000-product catalog is read-only: no structural mutations or mock ASIN injection.
- Text-only catalog/metadata/dialogue; multimodal processing is out of scope.
- Run entirely in memory; do not deploy a heavy external industrial vector database cluster.
- Do not train or full-parameter fine-tune a foundational LLM.
- Hard maximum: **10 turns per session**. Exceeding it forces termination and yields **zero score**.
- Inputs are pre-cleaned; sessions are isolated single-user simulations.

## Data and evaluator

The kit provides a weak Python BM25 starter Agent, published Python Agent interface/API contract, deterministic local evaluator (Hit Rate@10, MRR, MTTC, Efficiency, combined TechnicalScore), baseline results, data docs, submission rules, and SHA256 checksum. There are 200 labelled development sessions and 800 separate private sessions; users and targets are disjoint between public/private evaluation.

No hosted model, API key, token, or third-party credit is provided. Paid LLMs are optional; teams bear cost and must not publish credentials. The starter agent may be replaced as long as the official evaluator remains usable.

## Recommended implementation priorities

1. Get a contract-compliant BM25 baseline to score locally; verify the catalog checksum.
2. Implement deterministic intent classifier + slot/state reducer before adding an LLM. Make overwrite semantics explicit (e.g., a new category/budget can invalidate old slots).
3. Add a cheap in-memory hybrid candidate layer: lexical + category/attribute filters + embedding similarity, with intent-specific weights and candidate limits.
4. Add a lightweight reranker and a retrieval-cutoff clarification policy. Optimise expected conversion within 10 turns, not chat fluency.
5. Create tests for intent override, overspecific/overgeneral query, constraint conflict, and termination at turn 10.

Avoid tuning solely to the 200 public sessions. Use deterministic runs and held-out slices within development for diagnosis, then rely on the official public evaluator for comparable claims.

## Deliverables and completion criteria

Submit Devpost description, public repository/README, and public YouTube demo. The repository must explain setup, reproduction, limitations, and contributions. A functional headless/API walkthrough is an appropriate demo.

- [ ] Official local evaluator runs against your agent.
- [ ] Agent obeys the API contract and all sessions terminate by turn 10.
- [ ] Catalog remains unmodified and in-memory constraint is met.
- [ ] Results include Hit Rate@10, MRR, MTTC, Efficiency, and TechnicalScore where the kit reports them.
- [ ] Demo shows an intent route, evolving state/override, retrieval or clarification choice, and conversion-oriented result.
