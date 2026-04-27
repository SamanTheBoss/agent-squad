# Contributing to agent-squad

agent-squad is a community project. Contributions are welcome — but quality over quantity. Every change must have a clear reason.

## How to contribute

### 1. Open an issue first

Before writing any code or markdown, open an issue.
Describe:
- **What** you want to change
- **Why** it is needed — be specific
- **What problem it solves** — not just "improvement" or "enhancement"

Issues without a clear why will be closed.

### 2. Wait for feedback

A maintainer will respond with one of:
- Approved — go ahead
- Needs more context — explain further
- Out of scope — not aligned with project philosophy

Do not open a pull request before your issue is approved.

### 3. Make the change

Keep changes focused. One issue = one pull request.
Do not bundle unrelated changes.

### 4. Open a pull request

Reference the issue number.
Describe what changed and why.
Keep the diff small and readable.

---

## What we want

- **New language standards** in `agents/code-standards.md`
  Must include: naming conventions, file structure, documentation standard, example.
  Must follow the same format as existing languages.

- **Integrations for other AI coding tools**
  Cursor, Windsurf, Copilot Workspace etc.
  Must follow the same command structure as `integrations/claude-code/`.

- **Bug fixes in existing agents**
  Agent produces wrong output, misses an edge case, or contradicts another agent.
  Must include: exact reproduction steps and why current behavior is wrong.

- **Real-world usage reports**
  Ran agent-squad on a real project and found gaps?
  Open an issue describing what broke and what the agent should have done instead.

---

## What we do not want

- Changes without a clear why
- Adding features "just in case"
- Rewriting agents because you prefer a different style
- Lowering standards to make agents "more flexible"
- Anything that increases token usage without a proportional quality benefit

---

## Philosophy alignment

Before contributing, read `docs/PHILOSOPHY.md`.
Every change must align with:
- Spec first
- Minimal context per agent
- One job per agent
- Independent verification
- No shortcuts

If your change conflicts with any of these — it will not be merged.

---

## License

By contributing, you agree your work is licensed under MIT.