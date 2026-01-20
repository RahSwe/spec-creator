---
name: Spec Writing
description: This skill should be used when the user asks to "write a specification", "create a PRD", "document a feature", "write a user story", "write a bug report", "improve spec quality", "make spec more testable", or needs guidance on specification structure, acceptance criteria, or spec writing best practices.
version: 0.1.0
---

# Specification Writing Best Practices

This skill provides guidance for writing high-quality product specifications that are clear, complete, and actionable for development teams.

## Core Principles

**Clarity**: Every requirement should be unambiguous. Avoid words like "should", "may", "might", "could", "approximately", "user-friendly", "fast", "intuitive".

**Completeness**: Address the full scope including happy paths, error cases, edge conditions, and out-of-scope items.

**Testability**: Every acceptance criterion should be verifiable. Include specific, measurable conditions.

**Audience Awareness**: Specifications are for developers and QA. Include technical details they need, not business justifications they don't.

## Specification Types

### Bug Report

Document a defect with enough detail to reproduce and fix.

**Required Sections:**
- Title (specific, searchable)
- Environment (versions, OS, browser, etc.)
- Steps to Reproduce (numbered, specific)
- Expected Behavior
- Actual Behavior
- Severity/Priority
- Screenshots/Logs (if applicable)

**Quality Checklist:**
- Can a developer reproduce this from the steps alone?
- Is the expected behavior clearly defined?
- Is severity justified?

### Feature Spec

Define a new capability with requirements and boundaries.

**Required Sections:**
- Problem Statement (what problem this solves)
- User Impact (who benefits and how)
- Proposed Solution (high-level approach)
- Requirements (functional, non-functional)
- Acceptance Criteria (testable conditions)
- Scope Boundaries (what's NOT included)
- Dependencies (what this relies on)

**Quality Checklist:**
- Does this solve a real user problem?
- Are requirements specific enough to implement?
- Are acceptance criteria testable?
- Is scope clearly bounded?

### User Story

Capture a user need in standard format with acceptance criteria.

**Format:**
```
As a [persona],
I want [goal/action],
So that [benefit/value].
```

**Acceptance Criteria Format (Given-When-Then):**
```
Given [precondition],
When [action],
Then [expected result].
```

**Quality Checklist:**
- Is the persona specific and realistic?
- Is the goal achievable in one sprint?
- Is the benefit clear and valuable?
- Are acceptance criteria comprehensive?

### PRD (Product Requirements Document)

Comprehensive document for significant features or products.

**Required Sections:**
- Executive Summary
- Problem Statement
- Goals and Success Metrics
- User Personas
- User Journey/Flow
- Functional Requirements
- Non-Functional Requirements
- Constraints and Assumptions
- Dependencies
- Risks and Mitigations
- Timeline/Milestones
- Out of Scope

**Quality Checklist:**
- Are success metrics measurable?
- Are personas based on research?
- Are requirements prioritized (Must/Should/Could)?
- Are risks identified with mitigations?

## Writing Acceptance Criteria

### Good Acceptance Criteria

**Specific and Measurable:**
```
✅ "Search results load within 2 seconds for queries under 100 characters"
❌ "Search should be fast"
```

**Testable:**
```
✅ "Given a user with admin role, when they access /admin, then they see the dashboard"
❌ "Admins can access admin features"
```

**Complete:**
```
✅ "When upload fails, display error message with reason and retry option"
❌ "Handle upload errors appropriately"
```

### Common Mistakes

**Vague Language:**
- "User-friendly" → Specify what makes it friendly
- "Fast" → Specify maximum response time
- "Secure" → Specify security requirements
- "Scalable" → Specify scale targets

**Missing Edge Cases:**
- Empty states
- Maximum limits
- Error conditions
- Concurrent access
- Timeout scenarios

**Untestable Conditions:**
- "Intuitive navigation" → How do you test intuitive?
- "Good performance" → What's good?
- "Appropriate error handling" → Specify the handling

## Specification Templates

### Bug Report Template

```markdown
## Bug Report: [Brief Description]

### Environment
- Application Version:
- Operating System:
- Browser/Device:
- User Role:

### Steps to Reproduce
1. [First step]
2. [Second step]
3. [Continue with numbered steps]

### Expected Behavior
[What should happen]

### Actual Behavior
[What actually happens]

### Severity
[Critical / High / Medium / Low]

### Additional Context
[Screenshots, logs, related issues]
```

### Feature Spec Template

```markdown
## Feature: [Feature Name]

### Problem Statement
[What problem does this solve? For whom?]

### Proposed Solution
[High-level description of the solution]

### Requirements

#### Functional Requirements
1. [FR-1] [Requirement description]
2. [FR-2] [Requirement description]

#### Non-Functional Requirements
1. [NFR-1] [Performance/security/etc. requirement]

### Acceptance Criteria
- [ ] [Criterion 1]
- [ ] [Criterion 2]

### Out of Scope
- [What this feature does NOT include]

### Dependencies
- [Systems, services, or features this depends on]
```

### User Story Template

```markdown
## User Story: [Short Title]

### Story
As a [persona],
I want [goal],
So that [benefit].

### Acceptance Criteria

**Scenario 1: [Description]**
- Given [precondition]
- When [action]
- Then [expected result]

**Scenario 2: [Description]**
- Given [precondition]
- When [action]
- Then [expected result]

### Notes
[Additional context, edge cases, or constraints]
```

## Review Perspectives

When reviewing specifications, consider these perspectives:

**Developer Perspective:**
- Can I implement this without asking questions?
- Are edge cases defined?
- Are technical constraints clear?

**QA Perspective:**
- Can I write tests from these criteria?
- Are expected behaviors specific?
- Are error scenarios covered?

**Product Perspective:**
- Does this solve the stated problem?
- Is scope appropriate?
- Are success metrics defined?

**Security Perspective:**
- Are data handling requirements clear?
- Are authentication/authorization needs specified?
- Are compliance requirements addressed?

## Additional Resources

### Reference Files

For detailed guidance and examples:
- **`references/acceptance-criteria-patterns.md`** - Comprehensive acceptance criteria examples
- **`references/common-spec-problems.md`** - Frequent issues and how to fix them

### Example Files

Working templates in `examples/`:
- **`bug-report-example.md`** - Complete bug report
- **`feature-spec-example.md`** - Complete feature specification
- **`user-story-example.md`** - Complete user story with acceptance criteria
- **`prd-example.md`** - PRD outline structure
