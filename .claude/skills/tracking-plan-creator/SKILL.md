---
name: tracking-plan-creator
description: Generate comprehensive Firebase Analytics tracking plan documentation for the Pass Culture application from mockups, PRDs, and business requirements.
---

# Tracking Plan Creator

This skill generates comprehensive Firebase Analytics documentation for the Pass Culture application. It helps teams create Jira-formatted tracking specifications from mockups, PRDs, and business requirements.

## Key Architecture Points

Pass Culture employs a "multi-provider analytics architecture" spanning:
- Firebase Analytics (204 events)
- AppsFlyer (4 events)
- Batch (16 events)
- Algolia Analytics

Naming conventions: **PascalCase for events** (e.g., `ConsultOffer`) and **camelCase for parameters** (e.g., `offerId`).

## Three Core Collaboration Principles

1. **Accuracy First**: Mark uncertain elements as `[À compléter]` rather than inventing event names or parameters
2. **Interactive Design**: Validate events and naming choices before delivering final documentation
3. **Expert Partnership**: Challenge tracking utility by connecting data collection to specific business questions

## Implementation Workflow

### Step 1: Analyze Input Materials
Examine provided materials while **immediately consulting** `references/pass-culture-trackers.md` to identify existing events. Look for user interactions, screen transitions, multi-step flows, conditional logic, and success/failure states. This prevents duplicating current tracking and reveals architectural gaps.

### Step 2: Design Event Structure
- Search existing 204+ events before creating new ones
- Match established naming patterns (e.g., `CONSULT_*`, `CLICK_*` prefixes)
- Reuse common parameters like `from`, `offerId`, `venueId`, `searchId`
- Verify naming against `references/firebase-best-practices.md`
- Consider multi-provider requirements (Firebase, AppsFlyer, Batch, Algolia)

### Step 3: Generate Tracking Plan
Structure documentation using the template with these sections:
- Business context and current limitations
- Analytical objectives and value
- User stories in standard format
- Technical management rules with variation details
- Gherkin-style validation scenarios
- Standard testing and data validation procedures
- Complete event documentation with parameters

### Step 4: Review and Validate
Verify completeness, granularity, clarity, consistency, coverage, and absence of regressions before finalizing.

## Critical Resources (In Priority Order)

1. `references/pass-culture-trackers.md` — All 204+ Firebase events with parameters, AppsFlyer/Batch/Algolia events
2. `references/firebase-existing-properties.md` — Catalog of all existing properties to prevent duplication
3. `references/firebase-best-practices.md` — Pass Culture-specific naming conventions and design patterns
4. `references/jira-format-guide.md` — Complete Jira formatting specifications with examples
