# Track 2 — Autonomous ML Research Agent for recommender systems

**Official objective:** build an agent that autonomously performs the ML iteration loop—understand data/metrics, inspect data, engineer features, train/tune, evaluate, reflect, revise—and improves over the organizer's baseline on KuaiRand.

Workshop: **28 August 2026, 2:00–2:45pm SGT**. The supplied brief was last updated **25 August 2026, 9:10pm**.

## What you are actually being asked to make

This is not a standard “make the best recommender model” challenge. You are asked to make an **agent that behaves like a junior ML researcher**. Given the provided recommender dataset and scoring program, it should inspect the data, write or alter experiment code, run it, read the results, decide what to try next, and repeat with little human help.

The final quality of the recommender matters, but so does the evidence that the *agent* drove the improvement cycle. The judges expect a log showing each experiment's hypothesis, code change, metric result, and recovery from errors. A team that manually makes all changes and simply calls it an “agent” does not match the objective.

This is a technically demanding track. At least one teammate should be able to run Python ML training, understand train/validation/test separation, and diagnose failures such as an out-of-memory error. Non-technical teammates can make a major contribution by creating the experiment-log template, checking evidence/claims, researching permitted published methods, documenting intervention count, and explaining the agent's decisions in the video.

### What success looks like

- The system can start with the organizer's baseline and reproduce it.
- It independently proposes and runs several justified improvements, rather than applying a prewritten list manually.
- It records what happened and remains usable when a step fails.
- It submits its chosen best converged result without having used the hidden test data during development.

## Required benchmark and target

KuaiRand-Pure is required and supplies 100% of the primary metric score. KuaiRand-1k and KuaiRand-27k are optional bonus benchmarks. The task uses click as the fixed positive label and NDCG@10 plus Recall@50. The goal is to beat the fixed official baseline on the hidden test set, but falling short is scored continuously rather than disqualifying the submission.

The agent may develop with **train and validation only**. It never sees the hidden test. The brief describes date-based splits: 4/08–4/21 standard for training; first 50% of 4/22–5/08 standard for validation; final 50% for test. Use the organizer kit as the authoritative implementation of split and evaluation rules.

## Official requirements and restrictions

- Reproduce the official baseline end-to-end and confirm its validation score.
- Run the full required pipeline to convergence; a fully autonomous run is ideal, while a well-instrumented semi-automated run with few interventions is acceptable.
- Improve any stage, not only the model: features, training, evaluation, or algorithmic stack are in scope.
- Handle errors/timeouts/unexpected inputs by recovery, retry, or routing around them so long runs do not crash, stall, or diverge.
- Open-source libraries, papers, public solutions, and pretrained weights are allowed.
- **No external training data**, no joining/augmenting with other datasets, and no weights trained on these benchmarks' test labels.
- Hidden test access during development is prohibited.
- The compute budget is marked **TBD** in the supplied brief. Confirm current limits with organizers.

## Convergence and scoring

The final scored checkpoint is the validation-best checkpoint once the run has converged (no validation improvement above organizer threshold ε for N consecutive iterations) or reaches the fixed compute/wall-clock budget, whichever happens first. It is evaluated once on hidden test data.

For each dataset, the score is the mean absolute improvement over official baseline across NDCG@10 and Recall@50. Bonus datasets can add points but cannot reduce the required KuaiRand-Pure score.

| Judging area | Weight | Practical implication |
| --- | ---: | --- |
| Technical Execution | 35% | Final converged metric and robust recovery matter |
| Innovation & Problem Insight | 20% | Explain why the agent selected each experiment, beyond naive tweaks |
| Impact & Relevance | 20% | Autonomy: fewer manual interventions score higher |
| Feasibility & Practicality | 15% | Report/manage total LLM tokens and GPU-hours |
| Presentation & Communication | 10% | Final event pitch and technical understanding |

## Required deliverables

In addition to Devpost, public repository, and public YouTube demo:

- Per-iteration logs: hypothesis and rationale, applied code diff, NDCG@10/Recall@50, and error/recovery events.
- A manual-intervention count and short summary.
- Required benchmark final output/checkpoint in starter-kit schema.
- Results table with validation-best scores and absolute deltas over baseline; include bonus results if attempted.
- Total LLM input/output tokens and total training/evaluation GPU-hours to converged result.

## Recommended agent design

Build the agent as a constrained experiment manager, not an unconstrained coding loop:

1. **Inspect:** schema, split integrity, feature availability, baseline assumptions, resource envelope.
2. **Plan:** generate a small ranked experiment queue with a hypothesis and rollback criteria.
3. **Execute:** make isolated code changes on a branch/worktree or versioned experiment directory.
4. **Evaluate:** use one authoritative evaluator, fixed seeds where possible, and structured metric records.
5. **Reflect:** compare to baseline and prior experiments; retain, revert, or schedule a follow-up.
6. **Recover:** classify failures (syntax, dependency, OOM, timeout, metric regression), take bounded recovery actions, and log each one.

High-value recommender directions supported by the dataset include feature crosses/embeddings, DeepFM-style baselines, multi-task learning over the 12 feedback signals, training/calibration strategy, and counterfactual/OPE analysis. Do not claim a method improves the official metric until the official evaluator confirms it.

## Definition of done

- [ ] Baseline is reproduced and recorded.
- [ ] Required benchmark runs through the agent with little/no manual intervention.
- [ ] Every iteration has structured hypothesis, diff, metrics, and recovery evidence.
- [ ] No test leakage or external-training-data use.
- [ ] Converged best checkpoint, resource totals, results table, README, and video are ready.
