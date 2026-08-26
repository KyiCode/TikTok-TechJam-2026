# TikTok TechJam 2026: team guide

This guide is a practical reading of the official early-bird brief in [`Documents/Full documentation`](Documents/Full%20documentation). It separates **official requirements** from **team recommendations** so that planning choices are not mistaken for rules. Where the brief leaves something unresolved, this guide says so rather than filling the gap with an assumption.

## Event at a glance

Five technical tracks are available. The technical workshops are on **Friday, 28 August 2026 (SGT / GMT+8)**:

| Time | Track | Best fit |
| --- | --- | --- |
| 1:00–1:45pm | [1. Agent Launchpad](tracks/01-agent-launchpad.md) | Full-stack / backend engineers interested in agent infrastructure and safety |
| 2:00–2:45pm | [2. Autonomous ML Research Agent](tracks/02-autonomous-ml-research-agent.md) | ML, recommender-systems, and agent-automation teams |
| 3:00–3:45pm | [3. GPU Kernel](tracks/03-transformer-gpu-kernel.md) | CUDA/Triton, profiling, and performance engineering teams with a GPU |
| 4:00–4:45pm | [4. Shopping Copilot](tracks/04-shopping-copilot.md) | Search/retrieval, ranking, and dialogue-state teams |
| 5:00–5:45pm | [5. Robust AIGC Image Detection](tracks/05-robust-aigc-image-detection.md) | Computer-vision teams focused on robust evaluation |

The workshop link in the supplied brief is <https://vc-my.larkoffice.com/j/484622806>. The brief says the specific links are to be shared after public release; verify access before relying on it.

## What the five tracks have in common

Tracks 2–5 use the same high-level judging split: Technical Execution 35%, Innovation & Problem Insight 20%, Impact & Relevance 20%, Feasibility & Practicality 15%, and Final Event Presentation & Communication 10%. Track 1 has its own, more implementation-specific rubric.

For tracks 2–5, expect to submit through Devpost:

- a project description explaining the approach, tools/APIs, libraries, and data/assets;
- a public, reproducible code repository with setup, reproduction steps, limitations, and team contributions; and
- a public YouTube demo linked from Devpost, without unlicensed third-party trademarks or copyrighted content.

Each track adds its own required artifacts. Do not treat a polished front end as a universal requirement: it is explicitly out of scope for Track 4, and a backend/API walkthrough is accepted where a UI is not relevant.

## Choosing a track

| Track | Main technical risk | Main judging risk | A strong team profile |
| --- | --- | --- | --- |
| 1 | Integrating a real middleware capability without breaking the starter platform | Building static UI rather than trusted-path behavior | Full-stack team able to test backend/runtime behavior |
| 2 | Reliable autonomous experimentation and ranking improvement | Manual intervention, weak logs, or test-data leakage | ML + agent orchestration + disciplined experiment tracking |
| 3 | Correctness and performance across all supplied shapes | Optimising one shape or reporting only speed without correctness | GPU available; CUDA/Triton/profile expertise |
| 4 | Meeting quality *and* low-turn efficiency within a headless contract | Exceeding 10 turns, dataset mutation, external vector DB dependency | IR/recsys + dialogue-state engineering |
| 5 | Generalising through transformations without train/validation leakage | Reporting clean accuracy only or training on the demo validation set | CV/forensics team with rigorous augmentation and error analysis |

Choose the track where the team can prove the core metric or behaviour early. A focused, reproducible solution with a clear failure analysis is generally safer than an ambitious system with an incomplete evaluation story.

## Cross-track execution recommendations

1. **Make the official evaluator or acceptance flow run before building features.** Capture the baseline score/output and commit a small reproducibility note.
2. **Freeze a thin end-to-end vertical slice on day 1.** It should exercise the official contract, return a valid result, and be demonstrable.
3. **Treat experiments as evidence.** Record configuration, data split/version, seed, hardware, runtime, metrics, and failures. This is mandatory evidence in Track 2 and compelling proof everywhere.
4. **Protect the final day.** Reserve it for reproducibility, packaging, metrics tables, README, video rehearsal, and a clean-clone run.
5. **Keep a claim/evidence map.** For every pitch claim, have a metric, automated test, output sample, trace, or demo step that proves it.
6. **Document limitations plainly.** Be explicit about data scope, compute cost, known failure modes, and what would be needed for production. This supports feasibility rather than weakening the project.

## Submission-ready checklist

Use the selected track file as the authoritative detailed checklist. Before submission, verify:

- [ ] The repository is public, structured, commented, and can be run from its README.
- [ ] A fresh environment can reproduce the key output, metric, or live behaviour.
- [ ] Required artifacts (logs, reports, output schema, robustness table, diagram, etc.) are included for the chosen track.
- [ ] The video shows the actual working system and matches the submitted revision.
- [ ] No API key, token, password, sensitive payload, or private data appears in Git history, logs, screenshots, README, or the demo.
- [ ] The project description names all tools, models/APIs, libraries, datasets, and team contributions accurately.

## Official sources in this repository

- [`Documents/Full documentation`](Documents/Full%20documentation): supplied problem-statement brief.
- Track 1 starter kit: <https://github.com/RrankPyramid/CodeJam>.
- Track 4 participant repository: <https://github.com/TechJam2026/techjam-conversational-search>.

The official brief is the source of truth. Recheck organizer channels for later revisions, especially Track 2's compute budget, which is marked **TBD** in the supplied version.
