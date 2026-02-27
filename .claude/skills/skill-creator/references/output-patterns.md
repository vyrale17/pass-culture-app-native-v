# Output Patterns

## Template Pattern

When output structure is critical, provide explicit templates.

### Strict Template (for rigid requirements: APIs, data formats)

```
ALWAYS use this exact structure:

## Title
[One sentence]

## Executive Summary
[2-3 sentences max]

## Key Findings
- [Finding 1]
- [Finding 2]

## Recommendations
1. [Action 1]
2. [Action 2]
```

### Flexible Template (for content that adapts to context)

Provide a sensible default while encouraging adaptation:

```
Default structure (adapt as needed):
- Opening context
- Main body
- Next steps

Adjust section depth based on complexity.
```

---

## Examples Pattern

When output quality depends on style understanding, provide input/output pairs.

### Commit Message Example

**Input:** "Fixed the bug where users couldn't log in"

**Output:**
```
fix(auth): resolve login failure for users with special characters in email

The email validation regex incorrectly rejected valid addresses containing
'+' characters, causing login failures for affected users.

Fixes #234
```

**Key takeaway:** Examples help Claude understand the desired style and level of detail more clearly than descriptions alone.

---

## When to Use Which Pattern

| Situation | Pattern |
|-----------|---------|
| Structured data output (JSON, tables) | Strict template |
| Repeated tasks with consistent format | Template + example |
| Creative or variable content | Flexible template |
| Style-sensitive output | Examples |
| One-off analysis | Minimal guidance |
