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

### First: what are we actually submitting?

You choose **one** track and build a small, working proof of concept for its problem. You do not need to build a company or a polished commercial product. The important thing is that the project does the central thing the track asks for, can be demonstrated, and has evidence that it works. In most tracks, this means a code repository, a short video, a written Devpost explanation, and track-specific results.

If most of the team is not technical, that is still useful. A strong entry needs more than code: clear interpretation of user problems, evaluation design, test cases, documentation, a coherent demo story, research, and honest analysis of limitations. However, every track ultimately requires some functional code. Do not choose a track whose required technical core nobody on the team can build or learn with available time.

### Official track names and plain-English summaries

| Track | Official name | Summary | Example product directions (optional inspiration) |
| --- | --- | --- |
| 1 | Agent Launchpad: Design and Build Lightweight Agent Middleware | Add a functional safety, control, or observability layer to the supplied Agent platform. | Permission and approval gateway; Run audit timeline; budget guardrail; multi-Agent coordinator |
| 2 | Autonomous Machine Learning Research Agent for Recommender Systems | Create an agent that runs, evaluates, and improves recommender-system experiments with minimal human intervention. | Experiment-planning agent; self-repairing training agent; feature-engineering and tuning agent |
| 3 | Implement a GPU Kernel for a Transformer Layer | Replace part of a Transformer layer with a numerically correct, faster GPU implementation. | Shape-aware attention kernel; fused softmax/attention operation; performance profiler plus optimized kernel |
| 4 | Shopping Copilot: AI Conversational Search and Recommendations | Create a backend shopping agent that understands intent, manages changing preferences, retrieves products, and ranks them efficiently. | Intent router; hybrid retrieval/reranking agent; conversational preference-state engine |
| 5 | Robust Detection of AI-Generated Images Under Real-World Transformations | Create an image detector that remains useful after compression, blur, cropping, resize, and similar transformations. | Robust AIGC classifier; detector with confidence calibration; transformation-aware forensic ensemble |

### How to choose based on team setup

Start with the technical constraint, then use interest to break ties:

- **Avoid Track 3** unless at least one person is comfortable with GPU programming/performance profiling and has usable GPU access. It is the most specialised option and the least suitable for learning from zero during a hackathon.
- **Track 1** works when you have at least one web/backend developer.
- **Track 2** needs the deepest ML engineering. It is attractive if someone can run and modify Python ML experiments, but it is not simply “use an AI coding tool to make a recommender.” The autonomous iteration/logging requirement is central.
- **Track 4** is often easier to explain as a product problem, but still needs someone who can work with Python APIs, search/ranking, and the supplied evaluator. UI skills do not directly earn points here.
- **Track 5** can be approachable for a Python/CV learner because the task has a clear input/output and public data, but it still requires model training/inference and rigorous evaluation under transformations.

For a team with limited technical experience, a narrow, reliable project on Track 1, 4, or 5 is usually easier to explain and validate than Tracks 2 or 3—**provided** the team has at least one person who can own the required code. This is a planning recommendation, not an organizer rule.

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

## Keep in mind — engineering hygiene (recommended, not organizer-mandated)

These practices make a hackathon project more credible and easier to demo. Apply them proportionately; a focused prototype does not need enterprise-scale infrastructure.

| Area | Practical standard to aim for |
| --- | --- |
| Tests | Cover the core logic and all required failure/edge cases. A useful target is **70%+ coverage** for code you own, with higher confidence in critical paths; coverage is a signal, not a substitute for meaningful tests. |
| Test layers | Use fast unit tests for business logic, integration tests for API/model/data boundaries, and at least one end-to-end happy path that mirrors the demo/evaluator. |
| Inputs and errors | Validate inputs at system boundaries; return useful errors; set timeouts; avoid unbounded retries; handle missing files, bad data, model/API failures, and resource exhaustion. |
| Authentication and authorization | If users, protected data, or external actions are in scope, authenticate identities and enforce authorization on the backend—not only in the UI. Use least privilege and a clear ownership model. |
| Secrets | Put keys in environment variables or a secret manager; commit an `.env.example`, never real `.env` values; redact secrets from logs, screenshots, traces, and demo recordings. |
| Data and privacy | Record data source/licence, keep train/validation/test separation, minimise sensitive data, and document retention/deletion behaviour if you store user or image data. |
| Reproducibility | Pin dependencies, document environment/hardware, provide one command or short sequence to run, version datasets/models, record seeds/configuration, and state expected output. |
| Observability | Use structured logs with request/run IDs, meaningful status/error messages, and basic timing/resource metrics. Never log raw sensitive data by default. |
| Performance | Measure before optimising; report latency/throughput and memory/compute where relevant; use a baseline and repeatable methodology rather than one best-case run. |
| Reliability | Make operations idempotent where practical, clean up temporary resources, define retry/backoff/cancel behaviour, and test a realistic failure or recovery path. |
| Code quality | Keep modules small, name things clearly, format/lint/type-check where the stack supports it, remove dead code, and explain non-obvious decisions close to the code. |
| API design | Define request/response schemas, version or stabilise public interfaces, validate contracts, and return predictable status codes/output shapes. |
| Accessibility and UX | If a UI is in scope, use keyboard-accessible controls, readable contrast, loading/error states, and clear language. Do not spend time polishing UI where the track evaluates a headless backend. |
| Documentation | README should cover purpose, architecture, prerequisites, setup, test/run commands, demo steps, metrics, limitations, licences, and team contributions. |
| Delivery | Run the full test/evaluation path from a clean clone before recording the video; tag or note the exact commit demonstrated. |

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
