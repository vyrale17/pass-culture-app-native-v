---
name: skill-creator
description: Create new Claude skills — modular packages that extend Claude's capabilities with specialized knowledge, workflows, and tool integrations.
---

# Skill Creator Guide

This skill teaches how to create **Skills**—modular packages that extend Claude's capabilities with specialized knowledge, workflows, and tool integrations.

## Core Principles

**Concise is Key**: "The context window is a public good." Only include information Claude doesn't already possess. Challenge each detail's necessity to avoid wasting tokens.

**Appropriate Degrees of Freedom**: Match specificity to task fragility. Open-ended tasks use text instructions; complex operations need tighter constraints with specific scripts.

**Progressive Disclosure**: Load information in three levels—metadata (always), SKILL.md body (when triggered), and bundled resources (as needed).

## Skill Structure

Every skill requires a `SKILL.md` file with YAML frontmatter (`name`, `description`) and markdown instructions. Optional bundled resources include:

- **Scripts** (`scripts/`): Deterministic code for repeated tasks
- **References** (`references/`): Documentation loaded contextually
- **Assets** (`assets/`): Output files like templates or boilerplate

## Creation Process

1. **Understand** concrete usage examples
2. **Plan** reusable contents (scripts, references, assets)
3. **Initialize** using `init_skill.py`
4. **Edit** the skill and resources
5. **Package** with `package_skill.py`
6. **Iterate** based on real-world usage

## Collaboration Principles

- Avoid fabrication — mark unknowns explicitly
- Work interactively — validate before producing
- Think strategically — don't just produce output

## Reference Files

- `references/output-patterns.md` — Template and examples patterns for consistent outputs
- `references/workflows.md` — Sequential and conditional workflow patterns
