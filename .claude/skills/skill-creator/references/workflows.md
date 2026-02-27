# Workflow Patterns

## Sequential Workflows

Break complex tasks into ordered steps. Show Claude the complete roadmap upfront.

**Example — PDF Form Processing:**
```
1. Analyze the form (run analyze_form.py)
2. Extract fields and their types
3. Map to database schema
4. Generate pre-filled values
5. Verify output (run verify_output.py)
```

**When to use:** Linear progression where each step depends on the previous one.

---

## Conditional Workflows

Introduce branching logic based on decision points.

**Example — Content workflow:**
```
Start: Understand user's goal

IF goal == "create new content":
  → Ask: topic, audience, format
  → Draft outline
  → Write full content

IF goal == "edit existing content":
  → Ask user to provide current content
  → Identify improvement areas
  → Apply targeted edits

In both cases:
  → Review for quality
  → Present result with rationale
```

**When to use:** When the path forward depends on user input or context.

---

## Best Practices

1. **Name each step explicitly** — avoids ambiguity about what "next" means
2. **Include decision criteria** — what triggers each branch?
3. **Specify outputs** — what does each step produce?
4. **Keep steps atomic** — one action per step
5. **Show the full flow upfront** — Claude performs better with complete context than discovering steps iteratively
