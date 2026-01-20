---
description: Review and improve an existing specification through adversarial analysis
argument-hint: [spec-file-path]
allowed-tools: Read, Write, Glob, Grep, Task, AskUserQuestion, TodoWrite
model: opus
---

# Specification Review Workflow

You are initiating an adversarial review of an existing specification. Your goal is to analyze the specification using multiple reviewer agents and provide consolidated, actionable feedback.

## Step 1: Load Specification

If $ARGUMENTS is provided, read that file.

Otherwise, ask the user:

```
Use AskUserQuestion to ask:
"Which specification would you like to review?"
Options:
- From specs/ directory: I'll help you find it
- Provide file path: I'll specify the exact path
- Paste content: I'll paste the spec content directly
```

If user chooses "From specs/ directory", use Glob to find .md files in specs/ and present them as choices.

## Step 2: Analyze Specification Type

After loading the spec, determine its type by analyzing the content:
- Bug Report: Contains reproduction steps, expected/actual behavior
- Feature Spec: Contains requirements, acceptance criteria, scope
- User Story: Contains "As a...", "I want...", "So that..."
- PRD: Comprehensive document with personas, goals, metrics

If unclear, ask the user to confirm the spec type.

## Step 3: Launch Orchestrator for Review

Launch the spec-orchestrator agent in review mode:

```
Task: "Review the following specification through adversarial analysis.

Spec Type: [detected-type]
Spec Content:
---
[spec content]
---

Select appropriate reviewers based on spec type.
Run all selected reviewers in parallel.
Synthesize their critiques into:
- Critical Issues (must address)
- Important Concerns (should address)
- Suggestions (nice to have)

Present synthesized feedback to user with choices for resolution.
If user wants to make changes, update the spec and re-run reviewers.
Continue until consensus or user accepts current state."
```

## Step 4: Review Options

After presenting feedback, offer user choices:
- Address critical issues: Make changes to resolve blocking problems
- Address all issues: Comprehensive update addressing all feedback
- Accept as-is: Document known issues and accept current state
- Export feedback: Save review findings without modifying spec

## Step 5: Iteration

If user chooses to address issues:
1. Orchestrator guides user through changes with choices
2. Updated spec is re-reviewed by relevant agents
3. Process continues until consensus or user accepts

## Step 6: Completion

When review is complete, summarize:
- Original vs. final consensus status per reviewer
- Number of iterations performed
- Key changes made (if any)
- Outstanding issues acknowledged
- Updated file location (if modified)

## Notes

- Review can be run on any markdown specification file
- Reviewers are selected adaptively based on spec type
- User always has option to accept current state
- Original file is preserved; updates create new version if requested
