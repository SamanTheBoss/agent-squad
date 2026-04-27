# /agent-qa

Run the QA agent to write tests and verify quality.

## Usage
/agent-qa phase=1
/agent-qa phase=2

## Prerequisites
Phase 1:
- context/test-criteria.md must exist
- context/features.md must exist

Phase 2:
- Dev agent must be complete
- All tests must be committed

## What phase 1 does
1. Reads test-criteria.md
2. Identifies gaps in coverage
3. Writes automated tests per feature
4. Creates manual test files in context/manual-tests/

## What phase 2 does
1. Runs all automated tests independently
2. Reviews test quality
3. Flags weak tests
4. Produces context/qa-report.md

## Output files
Phase 1:
- context/tests/[task-id].test.ts
- context/manual-tests/visual.md (if applicable)
- context/manual-tests/ux-flows.md (if applicable)
- context/manual-tests/accessibility.md (if applicable)
- context/manual-tests/devices.md (if applicable)
- context/manual-tests/performance.md (if applicable)
- context/manual-tests/security.md (if applicable)
- context/manual-tests/exploratory.md (always)

Phase 2:
- context/qa-report.md

## Runs in parallel with
/agent-integration (phase 1 only)

## Agent file
@agents/qa.md