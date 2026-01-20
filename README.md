# Spec Creator

An adversarial specification forge for Claude Code that uses multiple AI reviewer agents to iteratively refine product specifications until consensus.

## Overview

Spec Creator helps product owners, product managers, and technical leads create high-quality specifications through:

1. **Guided Interview** - Interactive questions with choices to gather requirements (similar to plan mode)
2. **Multi-Agent Review** - 5 specialized reviewers critique the spec from different perspectives
3. **Iterative Refinement** - Synthesized feedback drives clarifications until all reviewers agree

## Features

- **4 Spec Templates**: Bug reports, Feature specs, User stories, PRDs
- **5 Adversarial Reviewers**: Devil's advocate, Security, UX, Tech feasibility, Edge cases
- **Adaptive Reviews**: Only relevant reviewers activate based on spec type
- **Consensus-Driven**: Iterations continue until all active reviewers are satisfied

## Commands

### `/forge-spec`
Create a new specification from scratch through guided interview.

```
/forge-spec
/forge-spec feature
/forge-spec bug
```

### `/review-spec`
Review and improve an existing specification document.

```
/review-spec specs/my-feature.md
/review-spec path/to/existing-spec.md
```

## Installation

### Quick Install (Recommended)

Install the plugin directly in Claude Code:

```bash
/plugin add RahSwe/spec-creator
```

That's it! The plugin is now installed and ready to use.

### Alternative: Add to Settings File

You can also add the plugin manually to your Claude Code settings file (`~/.claude/settings.json`):

```json
{
  "plugins": [
    "RahSwe/spec-creator"
  ]
}
```

### Alternative: Add via Marketplace

To browse plugins from the marketplace:

1. Add the marketplace:
   ```bash
   /plugin marketplace add RahSwe/spec-creator
   ```

2. Then install by name:
   ```bash
   /plugin install spec-creator@spec-creator
   ```

### Local Development

For local testing or development:

```bash
cc --plugin-dir /path/to/spec-creator
```

### Verify Installation

After installing, run `/help` in Claude Code to see the new commands:
- `/forge-spec` - Create a new specification
- `/review-spec` - Review an existing specification

## Configuration

Create `.claude/spec-creator.local.md` in your project to customize defaults:

```yaml
---
default_spec_type: feature
output_directory: specs
preferred_reviewers:
  - devils-advocate
  - tech-feasibility
  - edge-case-hunter
---

# Project-Specific Context

Add any project-specific context here that reviewers should consider:
- Tech stack: React, Node.js, PostgreSQL
- Team size: 5 developers
- Release cadence: 2-week sprints
```

## Reviewer Agents

| Agent | Focus | Activates For |
|-------|-------|---------------|
| Devil's Advocate | Challenges assumptions, questions necessity | All specs |
| Security Reviewer | Threats, compliance, data handling | Features, PRDs |
| UX Advocate | User experience, accessibility | Features, User stories |
| Tech Feasibility | Implementation complexity, architecture | Features, PRDs |
| Edge Case Hunter | Boundary conditions, error scenarios | All specs |

## Output

Specifications are saved to `specs/` directory (configurable) with naming:
- `specs/YYYY-MM-DD-spec-type-title.md`

## How It Works

### Workflow Diagram

```
User runs /forge-spec
    ↓
Orchestrator asks interview questions (with choices)
    ↓
Initial specification drafted
    ↓
Parallel review by selected adversarial agents
    ↓
Orchestrator synthesizes critiques into prioritized issues
    ↓
User resolves issues via choices
    ↓
Specification updated → Reviews re-run
    ↓
Continue until all reviewers reach consensus
    ↓
Final specification saved to specs/
```

### Consensus Criteria

Each reviewer provides a status:
- **BLOCKING**: Critical issues that must be resolved
- **CONCERNS**: Important issues that should be addressed
- **APPROVED**: No blocking issues, spec is acceptable

The specification is complete when all active reviewers are APPROVED.

## Development

### Project Structure

```
spec-creator/
├── .claude-plugin/
│   └── plugin.json         # Plugin manifest
├── agents/
│   ├── spec-orchestrator.md   # Main workflow coordinator
│   ├── devils-advocate.md     # Challenges assumptions
│   ├── security-reviewer.md   # Security analysis
│   ├── ux-advocate.md         # User experience
│   ├── tech-feasibility.md    # Technical assessment
│   └── edge-case-hunter.md    # Edge case analysis
├── commands/
│   ├── forge-spec.md       # Create new spec
│   └── review-spec.md      # Review existing spec
├── skills/
│   └── spec-writing/       # Specification best practices
│       ├── SKILL.md
│       ├── references/
│       └── examples/
├── README.md
└── LICENSE
```

## Contributing

Contributions welcome! Please submit issues and pull requests.

## License

MIT
