# Design Standards

## Identity
You are not a separate agent.
You are a mindset every design agent carries
at all times. These standards are non-negotiable.
No shortcuts. No exceptions.

## When This Applies
Read context/project.md before anything else.

if project_type == backend or cli → stop. Do not apply.
if project_type == frontend, fullstack, or mobile → continue.

## Accessibility — Always
WCAG 2.1 AA is the minimum. Always.
This is not a feature. It is a requirement.

- Contrast ratio: 4.5:1 for normal text, 3:1 for large text
- All interactive elements keyboard navigable
- Focus states always visible
- All images have alt text
- Form fields have labels
- Error messages are descriptive, not just color-based
- Touch targets minimum 44x44px on mobile

Never ship a component without checking these.

## Design Tokens

Read context/project.md → scale field.

if scale == small AND complexity is low:
  Minimum token set:
  - colors
  - typography
  - spacing scale

if scale == medium or large:
  Full token system:
  - colors (primitives + semantic)
  - typography (size, weight, line-height)
  - spacing scale
  - border radius
  - shadows
  - breakpoints
  - animation duration + easing

### Token structure (all projects):
```
tokens/
  colors.ts         → primitive colors
  semantic.ts       → semantic mappings (bg, text, border)
  typography.ts     → font sizes, weights, line heights
  spacing.ts        → spacing scale
  breakpoints.ts    → responsive breakpoints (if applicable)
  index.ts          → exports everything
```

### No magic numbers — ever:
```
❌ padding: 16px
✅ padding: tokens.spacing[4]

❌ color: #3B82F6
✅ color: tokens.colors.primary[500]

❌ font-size: 14px
✅ fontSize: tokens.typography.sm
```

## Responsiveness

Read context/design.md → users field.
Read context/project.md → project_type field.

if not defined in spec:
  consumers or public app   → mobile-first
  internal or admin tool    → desktop-first
  both                      → mobile-first

if defined in spec → follow spec. Always.

### Mobile-first means:
Base styles target mobile.
Larger screens add complexity via breakpoints.
Never the other way around.

## Component Standards (all frameworks)

### One component. One job.
If a component needs "and" to describe it → split it.

### No logic in UI
Components render. Services compute.
Never fetch data inside a component.
Never transform data inside a component.
Receive data as props or from a state layer.

### Props are contracts
Every prop explicitly typed.
Every prop has a clear purpose.
No prop drilling beyond 2 levels → use context or state.

### Variants over duplication
```
❌ ButtonPrimary, ButtonSecondary, ButtonDanger
✅ Button variant="primary" | "secondary" | "danger"
```

### States are mandatory
Every interactive component must handle:
- default
- hover
- focus
- active
- disabled
- loading (if async)
- error (if applicable)
- empty (if applicable)

Never ship a component missing a state.

## Component Documentation Tool

Read context/project.md → frontend_language field.

if frontend_language == ts or js:
  Use Storybook
  Every component gets a story
  Every variant gets a story
  Every state gets a story

if frontend_language == swift:
  Use Swift Previews
  Every component gets a #Preview
  Every variant gets a separate preview

if frontend_language == kotlin:
  Use Compose Previews
  Every component gets @Preview
  Every variant gets a separate @Preview

if frontend_language == flutter:
  Use Widgetbook
  Every component gets a use case
  Every variant gets a use case

if frontend_language == other:
  Search: "[language] component documentation
          preview tool best practices [year]"
  Follow top result from official docs.

## Storybook Setup (TS/JS projects)

Boilerplate structure:
```
.storybook/
  main.ts           → config
  preview.ts        → global decorators + tokens
src/
  components/
    [Component]/
      [Component].tsx
      [Component].stories.tsx
      [Component].types.ts
      index.ts
  tokens/
    (as defined above)
```

Every story file includes:
- Default export with component metadata
- Named export per variant
- Named export per state
- Args typed from component props

```typescript
export default {
  title: 'Components/Button',
  component: Button,
} satisfies Meta<typeof Button>

export const Primary: Story = { args: { variant: 'primary' } }
export const Disabled: Story = { args: { disabled: true } }
export const Loading: Story = { args: { loading: true } }
```

## Design Consistency Rules

- Never introduce a new color outside the token system
- Never introduce a new spacing value outside the scale
- Never create a one-off component — extend existing ones
- When in doubt → check if a component already exists
- When extending → add the variant to the existing component

## Before Every Component You Design

1. Read context/project.md — what is the scale?
2. Read context/design.md — what is the tone and users?
3. Does this component already exist?
4. If yes → extend it, do not duplicate
5. Does it follow the token system?
6. Does it handle all required states?
7. Does it meet WCAG 2.1 AA?
8. Is it documented in the correct preview tool?
9. Does it have exactly one responsibility?

If any answer is no → fix before moving on.

## Never
- Use magic numbers — always use tokens
- Skip accessibility checks
- Write logic inside components
- Duplicate components instead of adding variants
- Ship a component without all required states
- Introduce colors or spacing outside the token system
- Skip component documentation
- Assume responsiveness — read spec first
- Apply design standards to backend or cli projects