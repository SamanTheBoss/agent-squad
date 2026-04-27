# Code Standards

## Identity
You are not a separate agent.
You are a mindset every dev agent carries
at all times. These standards are non-negotiable.
No shortcuts. No exceptions.

## Language
All code, naming, and documentation in English.
Always.

## Core Principles (timeless, all languages)

### Single Responsibility
One file. One job.
If you can describe a file with "and" — split it.
This applies to every language, every pattern.

### Separation of Concerns
Logic never lives in UI.
UI never lives in services.
Data fetching never lives in components.
The boundaries differ per language pattern —
but the principle never changes.

### DRY — when it makes sense
Don't repeat yourself — but don't over-abstract.
If code is duplicated twice → consider extracting.
If duplicated three times → extract. Always.
Never abstract speculatively.

### Pure functions by default
Functions take input, return output.
No hidden side effects.
Dependencies are injected, never hardcoded inside functions.
If a function has side effects → make it explicit in the name.

```
❌ function saveUser() { db.save(); analytics.track(); }
✅ function saveUser(db: Database): User {}
✅ function trackUserSave(analytics: Analytics): void {}
```

### Self-documenting code
Code explains itself through naming.
No comments describing WHAT or HOW.

Exception — public APIs and services in languages
where documentation is standard (C#, Java):
Use the language's official documentation convention
(XML docs in C#, Javadoc in Java) for public methods
and interfaces only. Never for private implementation.

For all other cases, only one type of comment is allowed:
```
// Why: [reason that is not obvious from the code]
```

If you feel the urge to comment what the code does →
rewrite the code instead.

### Testability
Write code that is easy to test — always.
- Pure functions where possible
- Dependencies injected, never hardcoded
- No logic in constructors
- No global state
- Side effects isolated and named explicitly
- One behavior per function

If code is hard to test → the design is wrong.
Rewrite the code, not the test.

## Language-Specific Standards

### Before writing any code in any language:
1. Identify the language and framework
2. Search: "[language] [framework] project structure best practices [year]"
3. Search: "[language] naming conventions [year]"
4. Follow the established pattern for that language

### TypeScript / JavaScript

#### Project structure
Feature-based. Every feature is self-contained.
No feature reaches into another feature's internals.
Cross-feature communication through shared types only.

```
src/
  features/
    [feature]/
      [Feature].tsx         → component only
      [Feature].types.ts    → types for this feature
      [Feature].service.ts  → business logic
      [Feature].test.ts     → tests
      index.ts              → public exports only
  types/
    api.types.ts            → API response types
    common.types.ts         → shared types
  utils/
    [util].ts               → pure utility functions
  constants/
    [domain].constants.ts   → constants by domain
```

Never import from inside another feature:
```
❌ import { UserService } from '../user/UserService'
✅ import { UserService } from '../user'
```

#### Naming
- Variables and functions: camelCase, descriptive verbs
- Components: PascalCase
- Types and interfaces: PascalCase
- Constants: SCREAMING_SNAKE_CASE
- Files: kebab-case (except components → PascalCase)

```typescript
❌ const d = new Date()
✅ const createdAt = new Date()

❌ function handle() {}
✅ function handleUserSubmit() {}

❌ const flag = true
✅ const isEmailVerified = true
```

#### File length guidelines
| File type       | Guideline  |
|-----------------|------------|
| Component       | ~200 lines |
| Service         | ~150 lines |
| Util / Helper   | ~100 lines |
| Types           | no limit   |
| Constants       | no limit   |

These are guidelines, not hard limits.
If a file exceeds its guideline →
check if it has more than one responsibility.
If yes → split it.

#### Types
- Explicit types always — never rely on inference for public APIs
- Types live in separate .types.ts files
- No `any` — ever
- Use `unknown` over `any` when type is truly unknown
- Prefer `interface` for objects, `type` for unions and primitives

```typescript
❌ const user: any = getUser()
✅ const user: User = getUser()
```

#### Async
- async/await over .then() chains
- Always handle errors explicitly
- Never swallow errors silently

```typescript
❌ try { ... } catch (e) {}
✅ try { ... } catch (error) {
     logger.error('fetchUser failed', { error })
     throw error
   }
```

#### React (if applicable)
- Functional components only
- One component per file
- Props typed explicitly — never inferred
- No inline styles — use design tokens
- No logic in JSX — extract to variables or functions

```typescript
❌ return <div>{users.filter(u => u.active).map(...)}</div>
✅ const activeUsers = users.filter(u => u.active)
   return <div>{activeUsers.map(...)}</div>
```

---

### C#

#### Project structure
Search: "C# clean architecture project structure [year]"
Default to Clean Architecture unless spec states otherwise:
```
src/
  [Project].Domain/         → entities, value objects
  [Project].Application/    → use cases, interfaces
  [Project].Infrastructure/ → DB, external services
  [Project].API/            → controllers, middleware
```

#### Naming
Follow Microsoft conventions:
- PascalCase for everything public
- camelCase with _ prefix for private fields (_userId)
- Interfaces prefixed with I (IUserService)

#### File length
Controllers and services can legitimately be longer.
Rule: one responsibility per class, not per line count.
If a controller handles more than one resource → split it.

#### Documentation
XML documentation required for all public methods,
interfaces, and classes:
```csharp
/// <summary>
/// Retrieves a user by their unique identifier.
/// </summary>
/// <param name="id">The user's unique identifier.</param>
/// <returns>The user if found, null otherwise.</returns>
public async Task<User?> GetByIdAsync(Guid id)
```

---

### Python

#### Project structure
Search: "Python project structure best practices [year]"
Follow PEP 8 and PEP 20 (Zen of Python).

#### Naming
- snake_case for variables, functions, files
- PascalCase for classes
- SCREAMING_SNAKE_CASE for constants

#### Documentation
Docstrings for all public functions and classes:
```python
def get_user(user_id: str) -> User:
    """
    Retrieve a user by ID.

    Args:
        user_id: The unique identifier of the user.

    Returns:
        User object if found.

    Raises:
        UserNotFoundError: If no user exists with given ID.
    """
```

---

### Other languages
Search:
- "[language] project structure best practices [year]"
- "[language] naming conventions [year]"
- "[language] documentation standard [year]"
- "[language] [framework] architecture pattern [year]"

Apply core principles. Follow what the search returns
from official documentation over community opinions.

---

## Before Every File You Write

1. What language and framework is this?
2. What is the standard pattern for this language?
3. Am I following that pattern?
4. Does this file have exactly one responsibility?
5. Are all dependencies injected?
6. Is every name self-explanatory in English?
7. Is the documentation standard for this language followed?
8. Is this easy to test?

If any answer is no → fix before moving on.

## Never
- Assume a pattern without checking language standards first
- Write logic in UI components
- Import directly from inside another feature (JS/TS)
- Write comments explaining what code does
- Create files that do more than one thing
- Write untestable code
- Use magic numbers — extract to named constants
- Leave dead code — delete it
- Use `any` in TypeScript
- Speculate about future needs — build what is spec'd