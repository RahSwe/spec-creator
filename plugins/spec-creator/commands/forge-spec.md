---
description: Create a new specification through guided interview and adversarial review
argument-hint: [spec-type]
allowed-tools: Read, Write, Glob, Grep, Task, AskUserQuestion, TodoWrite
model: opus
---

# Specification Creation Workflow

You are initiating an adversarial specification creation workflow. Your goal is to guide the user through creating a high-quality specification using structured interviews and multi-agent review.

## Step 1: Determine Specification Type

If $ARGUMENTS is provided and matches a known type (bug, feature, story, prd), use that type.

Otherwise, ask the user:

```
Use AskUserQuestion to ask:
"What type of specification would you like to create?"
Options:
- Bug Report: Document a bug with reproduction steps and expected behavior
- Feature Spec: Define a new feature with requirements and acceptance criteria
- User Story: Capture a user need in "As a... I want... So that..." format
- PRD: Comprehensive product requirements document
```

## Step 2: Launch Orchestrator

Once the spec type is determined, launch the spec-orchestrator agent using the Task tool:

```
Task: "Create a [spec-type] specification through guided interview.
The user wants to create a [spec-type].
Guide them through the interview process, asking questions with choices.
After drafting the initial spec, coordinate adversarial review cycles.
Continue iterating until all reviewers reach consensus.
Save the final spec to specs/ directory."
```

The orchestrator will:
1. Conduct structured interview with AskUserQuestion choices
2. Draft initial specification
3. Select and run appropriate reviewer agents
4. Synthesize feedback into prioritized issues with choices
5. Iterate based on user decisions
6. Continue until all active reviewers reach consensus
7. Save final specification

## Step 3: Completion

When the orchestrator completes, summarize:
- Specification type and title
- Number of review iterations
- Which reviewers participated
- Final file location
- Any noted limitations or future considerations

## Notes

- All user interactions should use AskUserQuestion with concrete choices
- The workflow continues until consensus, not a fixed number of iterations
- If iterations exceed 5, the orchestrator will ask user if they want to continue
- Specs are saved to `specs/YYYY-MM-DD-{type}-{title}.md`
