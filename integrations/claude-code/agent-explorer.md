# /agent-explorer

Run the explorer agent to scan the codebase
before dev starts.

## Usage
/agent-explorer

## Prerequisites
- context/project.md must exist
- context/features.md must exist
- context/technical.md must exist

## What this does
1. Scans existing codebase architecture and patterns
2. Identifies integration points
3. Maps test infrastructure
4. Detects spec conflicts
5. Flags merge conflict risks
6. Checks design system overlap (FE only)
7. Flags tech debt in affected files
8. Notes security observations in affected files

## Runs in parallel with
/agent-integration

## Output files
- context/explorer-report.md

## Agent file
@agents/explorer.md