# /agent-dev

Run a dev agent to implement one task.

## Usage
/agent-dev task=[T-id]

Example:
/agent-dev task=T0101
/agent-dev task=T0102

## Prerequisites
- context/contracts.md must exist
- context/execution-plan.md must exist
- context/design-system.md must exist (FE only)
- context/tests/[task-id].test.ts must exist
- All task dependencies must be complete

## What this does
1. Reads assigned task from execution-plan.md
2. Checks all dependencies are complete
3. Implements against contracts.md
4. Uses components from design-system.md (FE only)
5. Runs until acceptance tests pass
6. Commits one commit per passing test
7. Marks task complete in execution-plan.md

## Run parallel tasks simultaneously
Check execution-plan.md for parallel groups.
Tasks in the same parallel group can run at the same time.

Example:
/agent-dev task=T0101
/agent-dev task=T0102
/agent-dev task=T0201

## Agent file
@agents/dev.md
@agents/code-standards.md