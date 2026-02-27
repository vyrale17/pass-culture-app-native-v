# Jira Ticket Writing Best Practices

## Core Principles

**Clarity Over Completeness:** Prioritize value in every sentence, eliminate filler, use bullets for readability, and cap paragraphs at 2-4 sentences.

**Action-Oriented Language:** Employ active voice with verb-first structures like "Enable" or "Fix," avoiding passive constructions and vague terminology.

**Measurable Outcomes:** Ensure acceptance criteria are verifiable through concrete conditions rather than subjective assessments.

## Key Section Guidelines

**Title Format:**
- Prefix with scope: [Front], [Back], [Tracking]
- 5-8 words maximum
- Start with action verb
- Example: "[Front] Add CSV export for transaction history"

**Context:**
- 2-3 sentences maximum
- Lead with user/business impact
- Include metrics when available
- Avoid generic "improving experience" statements

**User Story:**
- Specific persona (not generic "user")
- Single focused capability
- Concrete measurable benefit
- Format: "As a [role], I want to [action], so that [benefit]"

**Business Rules:**
- One rule per bullet
- Include specific values, times, or roles
- Focus on constraints and validations
- Omit obvious requirements

**Technical Strategy:**
- 2-4 sentences naming specific components
- Highlight key architectural decisions
- Optional for trivial implementations

**Acceptance Criteria:**
- Use Given/When/Then/And structure
- Name scenarios explicitly
- Ensure each criterion is independently testable

## Critical Mistakes to Avoid

Avoid verbosity, vague criteria, developer-focused user stories, and combining multiple features. Keep tickets focused, concise, and measurable.
