# Philosophy

![Token Philosophy](../assets/token-philosophy.png)

agent-squad is built on a single belief:

> The quality of AI-generated code is determined by the quality of the context each agent receives — not the sophistication of the agent itself.

Most AI coding systems fail not because the AI is bad, but because it is given too much to think about at once. Context bloats. Quality degrades. You end up babysitting.

We solve this differently.

---

## Spec first. Always.

Nothing gets built without a spec.

This sounds obvious. It rarely happens in practice.

When you skip the spec, you skip the most important conversation — the one where you discover what you actually want to build, what the edge cases are, what is out of scope, and what decisions need to be made before a single line of code is written.

The requirements agent exists to force that conversation. It asks one question at a time. It pushes back on vague answers. It detects conflicts. It protects MVP scope. It does not let you proceed until the spec is complete.

A bad spec produces bad code. No amount of clever agents fixes that.

---

## Contracts before code.

Dev agents never guess interfaces.

One of the most common failure modes in AI coding is agents that build features in isolation and then fail to connect them. Each agent makes assumptions about how its piece connects to the others. The assumptions conflict. Integration breaks.

We solve this with the integration agent. Before any dev agent writes a single line, all interfaces are defined — entity shapes, service contracts, API request/response shapes, database schemas. Dev agents implement against contracts, not assumptions.

If a contract is missing, the dev agent stops and reports it. It does not guess.

---

## Tests before dev.

The QA agent writes tests before dev starts.

When you let an AI write tests after implementing, the tests are designed to pass. The AI knows what it built. It writes tests that confirm what it built, not tests that verify behavior.

We separate the concern completely. The QA agent reads the spec and writes acceptance tests before the dev agent touches the codebase. The dev agent's only job is to make those tests pass.

This is not TDD in the traditional sense. We do not do RED-GREEN-REFACTOR cycles. We do contract-first acceptance testing — which is faster, cheaper in tokens, and produces tests that actually test behavior.

---

## Minimal context per agent.

Every agent reads only what it needs. Nothing more.

This is the core token optimization in agent-squad. It is not about using cheaper models or writing shorter prompts. It is about surgical context design.

The dev agent does not read the design spec. It reads contracts and tests.
The QA agent does not read the explorer report. It reads test criteria and features.
The mutation agent does not read the contracts. It reads tests and the QA report.

Each agent gets exactly the context it needs to do its job. No more. This keeps every agent's context window clean and focused, which means consistent quality across every task — not just the first few before context degrades.

---

## One job per agent.

No agent does more than it should.

The requirements agent does not write tests.
The design agent does not write feature code.
The dev agent does not review its own work.
The fixer agent does not add features.

This separation is not just organizational — it is a quality mechanism. An agent that tries to do everything becomes an agent that does nothing well. Focused agents with clear inputs and clear outputs are predictable, reliable, and easier to debug when something goes wrong.

---

## Independent verification.

Never trust self-reports.

When a dev agent says "I implemented everything and all tests pass" — do not trust it. Read the code. Run the tests yourself. Compare against the spec line by line.

This is what the spec-review and quality-review agents do. They receive the dev agent's completion report and ignore it. They read the actual code. They run the actual tests. They report what they find, not what the dev agent claimed.

This catches a surprisingly large number of issues — misunderstood requirements, tests that technically pass but do not verify behavior, code that works for the test input but breaks for anything else.

---

## Why not TDD?

We considered strict RED-GREEN-REFACTOR TDD. We chose not to use it.

The problem with TDD in an AI agent context is token cost. Each RED-GREEN-REFACTOR cycle requires the agent to hold the full implementation context while writing one test at a time. For a feature with ten behaviors, that is ten cycles, each burning context.

More importantly, TDD requires the agent to think about what it is about to build while writing each test. An AI agent that knows what it is about to build will write tests designed to pass — which defeats the purpose.

Our approach separates the concerns completely. A different agent writes the tests. A different agent writes the code. Neither one can influence the other's output. This produces better tests and better code, at lower token cost.

---

## Why contracts-first instead of codebase exploration?

SpecOps explores the codebase first, then builds. We do both — but we define contracts before dev starts regardless.

Codebase exploration (our explorer agent) tells us what patterns to follow and where integration points are. But it does not tell us what the interfaces between new features should look like. That is the integration agent's job.

Without contracts, two dev agents building different parts of the same feature will make different assumptions about how their pieces connect. With contracts, they both build to the same blueprint.

---

## Fixer, not rewriter.

When something fails review, we fix it — we do not rebuild it.

The fixer agent has a strict mandate: fix what the review found, nothing more. It does not improve unrelated code. It does not refactor things it notices along the way. It does not add features while it is in there.

This keeps the review-fix cycle fast and predictable. If the fixer is allowed to make additional changes, every re-review becomes a review of unknown scope. By constraining the fixer to exactly what was reported, re-reviews are fast and focused.

---

## Mutation testing as the final gate.

Green tests are not enough.

A test suite that never fails is not a good test suite — it is a test suite that was written to pass. Mutation testing proves that tests actually catch bugs by introducing deliberate bugs and verifying that tests fail.

We use mutation score as a release gate. Features below 70% mutation score do not ship. This is not optional. It is the final quality check before done.

---

## Credit

agent-squad was inspired by [meganide/specops](https://github.com/meganide/specops) and the excellent article by Renas Hassan on AI agent teams. His work on parallel execution, context isolation, and the two-stage review pipeline directly influenced this project.

We built on his foundation with a different philosophy: design systems, contracts-first, language-agnostic standards, mutation testing, and aggressive token optimization.

---

## What we do not claim

agent-squad does not replace human judgment.

The requirements agent cannot replace a real product discovery session with real stakeholders.
The QA agent cannot replace exploratory testing by an experienced tester.
The mutation agent cannot replace a security audit by a security engineer.
The design agent cannot replace a designer who understands your users.

What agent-squad does is handle the mechanical parts of feature development — spec, design, contracts, implementation, testing, review — so that human judgment can focus on the parts that actually require it.