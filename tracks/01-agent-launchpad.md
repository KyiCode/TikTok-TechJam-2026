# Track 1 — Agent Launchpad: lightweight agent middleware

**Official objective:** extend the provided agent platform with a coherent, functional, testable middleware story. Build the missing middleware, not a replacement platform. The platform baseline and Playground must continue working.

Workshop: **28 August 2026, 1:00–1:45pm SGT**. Starter kit: <https://github.com/RrankPyramid/CodeJam>.

## Track summary and example products

You receive a mostly working website where a user can create an AI coding Agent and ask it to work in a workspace. Your project is an **improvement behind or alongside that existing experience**: something that helps a person control, inspect, protect, or recover the Agent's actions.

Think of middleware as the rules and records between a user clicking “run” and an Agent doing work. A valid project could make the platform answer questions such as: “May this Agent access this file?”, “Why did this Run fail?”, “Who approved this action?”, “How do we stop an expensive Run?”, or “Which Agent acted next?”

Example product directions: a permission-and-approval gateway for Agent tools; a Run audit/trace explorer with redaction; a budget and rate-limit controller; or a coordinator that controls multiple Agents sharing a task. The essential proof is that the rule/record is enforced by backend or Runtime code, not just shown on a screen.

### What a valid project must visibly do

1. Start from the supplied platform without breaking its basic Agent workflow.
2. Let someone invoke a real Agent task from the frontend.
3. Make a meaningful middleware decision/event during that path.
4. Show evidence of it (for example a policy decision, audit record, trace, budget event, or recovery record).
5. Show an adverse case: denied, failed, unsafe, degraded, or recovered.

That is the core story. You do **not** need to implement every example in the problem statement.

## What is already supplied

The starter kit includes React UI, Agent CRUD and lifecycle controls, Playground chat and asynchronous Run status, Fastify control plane and JSON persistence, persistent per-Agent workspaces, Codex CLI Runtime, local disposable containers, BytePlus ModelArk integration, and optional ECS deployment. The intended development/judging path is local Docker, Colima, or rootless Podman; ECS is optional and does not affect score.

Baseline prerequisites are macOS or Linux, Node 22+, npm 10+, a container engine, and a ModelArk API key plus Responses-compatible endpoint ID. Before middleware work, prove: create an Agent; run a task; receive a response; resume its session; and stop/restart it while preserving the workspace. Run `npm run check` before submission.

## Official requirements and completion criteria

- Preserve Agent CRUD, lifecycle actions, Playground chat, persistence, and model execution.
- Implement actual middleware behaviour in a backend, Runtime, data, or infrastructure path. A UI-only screen or hard-coded success result is insufficient.
- State the ownership boundary, data crossing it, and failure behaviour.
- Demonstrate normal behaviour **and** a suitable failure, denial, degraded, abuse, or recovery case.
- Add automated verification of core middleware behaviour.
- Keep secrets and unredacted sensitive payloads out of source, browser state, logs, traces, screenshots, and demo output.
- Supply a 3-minute live demo, a one-page architecture diagram (middleware, data flow, trust boundary, enforcement/instrumentation/recovery point), and a repository with setup, rationale, design, tests, demo steps, limitations, and no secrets.

A reviewer must be able to clone/start the platform, create or test an Agent in the frontend, observe meaningful middleware executing outside the UI, understand/reproduce the POC, and pass `npm run check`.

## Evaluation

| Criterion | Weight | What to prove |
| --- | ---: | --- |
| End-to-end middleware behaviour | 40% | Real frontend-to-backend/Runtime/data/infrastructure path and evidence |
| Technical design and integration | 25% | Clear rationale, good boundary, focused extensible changes |
| Verification and robustness | 20% | Tests, error handling, cleanup/recovery, redaction, bypass resistance |
| Demo and reproducibility | 15% | Concise demo, one-command startup, limitations, no hidden setup |

## Strong scope options

The brief's examples are optional. Pick one narrow narrative, for example:

- **Delegated tool access:** a human grants an Agent a narrowly scoped, revocable permission; backend enforcement permits one mock resource and denies another; the audit trail shows actor, scope, decision, target, and result.
- **Run trace plus safe recovery:** propagate a trace ID through API, model/tool/workspace actions; redact payloads; surface a failed controlled action; retry or reconcile it in a visible, testable way.
- **Budget gate:** enforce per-Run tool/step/cost limits in the trusted execution path; demonstrate a normal Run, a blocked limit breach, and an operator action to resume or adjust policy.
- **Small multi-Agent coordinator:** shared topic/state with turn routing, duplicate prevention, timeout/retry, and visible history. The supplied countdown example must reach 10 to 1 without duplicates or gaps.

Recommendation: combine only closely related capabilities. For example, authorization + audit is coherent; a separate identity system, tracing system, and new scheduler is likely too broad for three days.

## Suggested implementation path

1. Run the starter acceptance flow unchanged. Identify the smallest seam (Fastify boundary, `AgentService`, `AgentRunner`, or execution model).
2. Write a one-page contract: event/request, trusted enforcer, persisted evidence, expected deny/failure/recovery result, and one negative test.
3. Implement the backend/Runtime decision first and test it using a controlled fixture.
4. Persist just enough evidence for a Run-specific view; add minimal UI only after the behaviour works.
5. Rehearse one uninterrupted 3-minute scenario: select/create Agent → real task/action → evidence → controlled adverse case → clear final controllable state.

## Common pitfalls

- A login page without server-side authorization does not prove identity/authorization.
- Existing container CPU/memory/default hardening is not itself a new safety feature.
- A trace that stores secrets or cannot identify the failed step weakens the design.
- Cloud deployment, production OAuth, microVMs, schedulers, and multi-region design are not required.

## Definition of done

- [ ] Baseline acceptance flow and `npm run check` pass.
- [ ] A new trusted-path middleware decision/event is automated-tested.
- [ ] A real Playground Run produces inspectable evidence.
- [ ] A controlled adverse case proves enforcement/recovery rather than UI messaging.
- [ ] Diagram, README, demo script, and secret scan are complete.
