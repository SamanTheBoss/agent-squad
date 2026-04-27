# /agent-design

Run the design agent to build the complete
design system before dev starts.

## Usage
/agent-design
/agent-design add=[ComponentName]

## Prerequisites
- context/project.md must exist
- context/design.md must exist
- context/features.md must exist
- project_type must not be backend or cli

## What this does
1. Reads all spec files
2. Determines token complexity and responsiveness
3. Presents color palette options
4. Builds token system
5. Builds all required components
6. Documents everything in Storybook (or equivalent)
7. Produces context/design-system.md

## Output files
- src/tokens/
- src/components/
- context/design-system.md

## Agent file
@agents/design.md
@agents/design-standards.md