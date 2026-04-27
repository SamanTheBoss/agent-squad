# /agent-integration

Run the integration agent to define contracts
and create the execution plan.

## Usage
/agent-integration

## Prerequisites
- context/project.md must exist
- context/features.md must exist
- context/technical.md must exist

## What this does
1. Reads all spec files
2. Detects conflicts between features
3. Defines all contracts (entities, interfaces, API, DB)
4. Creates execution plan with task ordering
5. Identifies parallelism opportunities

## Output files
- context/contracts.md
- context/execution-plan.md

## Runs in parallel with
/agent-qa phase=1

## Agent file
@agents/integration.md