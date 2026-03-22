# AGENTS.md

## Guideline

- follow TDD, follow t-wada method
- read the latest code when starting a new task, because it might be updated independently of your work

### Styling Rules

- Use Tailwind CSS utility classes as the primary styling method. Avoid inline `style=""` attributes.
- Only use `style=""` for values that Tailwind cannot express (e.g., `width` percentages for chart bars, `conic-gradient`, specific `clip-path` values).
- For opacity variants, use `bg-primary opacity-70` instead of `bg-primary/70` (CSS variable colors do not support the `/opacity` modifier).
- Never use `!important` in CSS. Solve specificity issues with more specific selectors.
- Never use `shadow-*` classes (e.g., `shadow-sm`, `shadow-md`, `shadow-lg`). PDF変換時に不自然な影が表示される原因になる。立体感が必要な場合は `border` で代替する。

---

## Workflow

### 1. Plan Mode Default

- Enter plan mode for ANY non-trivial task (3+ steps or architectural decisions)
- If something goes sideways, STOP and re-plan immediately – don't keep pushing
- Use plan mode for verification steps, not just building
- Write detailed specs upfront to reduce ambiguity

### 2. Subagent Strategy

- Use subagents liberally to keep main context window clean
  fad research, exploration, and parallel analysis to subagents
- For complex problems, throw more compute at it via subagents
- One task per subagent for focused execution

### 3. Self-Improvement Loop

- After ANY correction from the user: update `tasks/lessons.md` with the pattern
- Write rules for yourself that prevent the same mistake
- Ruthlessly iterate on these lessons until mistake rate drops
- Review lessons at session start forelevant project

### 4. Verification Before Done

- Never mark a task complete without proving it works
- Diff behavior between main and your changes when relevant
- Ask yourself: "Would a staff engineer approve this?"
- Run tests, check logs, demonstrate correctness

### 5. Demand Elegance

- For non-trivial changes: pause and ask "is there a more elegant way?"
- If a fix feels hacky: "Knowing everything I know now, implement the elegant solution"
- Skip this for simple, obvious fixes – don't over-engineer
- Challenge your o work before presenting it

### 6. Autonomo Bug Fing

- When given a bug report: just fix it. Don't ask for hand-holding
- Point at logs, errors, failing tests – then resolve them
- Zero context switching required from the user
- Go fix failing CI tests without being told how

---

## Task Management

1. Plan First: Write plan to `tasks/todo.md` with checkable items
2. Verify Plan: Check in before starting implementation
3. Track Progress: Mark items complete as you go
4. ExplChanges: High-level summary at each step
5. Document Results: Add review section to `tasks/todo.md`
6. Capture Lessons: Update `tasks/lessons.md` after corrections

---

## Core Principles

- Simplicity First: Make every change as simple as possible. Impact minimal code.
- No Laziness: Find root causes. No temporary fixes. Senior developer standards.
- Minimal Impact: Changes should only touch what's necessary. Avoid introducing bugs.

---
