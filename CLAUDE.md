# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a Claude Code skills repository containing custom skills that extend Claude's capabilities for documentation, workflow orchestration, and research tasks. The repository name references ThingsBoard but currently contains generic skills applicable to any project.

## Directory Structure

All skills are located in `.claude/skills/`. Each skill has a `SKILL.md` file with YAML frontmatter defining:
- `name`: Lowercase, hyphens only (must match directory name)
- `description`: What it does and when to use it
- `allowed-tools`: Optional tool restrictions

## Key Skills

### Workflow Orchestration
- **main-workflow-router**: Routes between BMAD (complex projects, Level 2-4) and OpenSpec (simple changes, Level 0-1) workflows. Auto-invokes on "start project", "what's next", "status" triggers.

### Documentation
- **docs-write**: Write documentation following Metabase's conversational style. Format with `yarn prettier --write <file-path>`.
- **docs-review**: Review documentation for style compliance. Supports both local and GitHub PR review modes.

### Planning & Research
- **brainstorming**: Refine rough ideas through iterative questioning (ONE QUESTION AT A TIME rule).
- **prd**: Generate Product Requirements Documents. Outputs to `tasks/prd-[feature-name].md`.
- **web-research**: Structured web research using subagents. Creates `research_[topic_name]/` folders.

### Skill Development
- **skill-writer**: Guide for creating new Claude Code skills.

## Workflow Patterns

### BMAD Workflow (Level 2-4 projects)
1. Analysis (bmad-discovery-research) - optional for L2, recommended L3-4
2. Planning (bmad-product-planning, bmad-ux-design)
3. Solutioning (bmad-architecture-design, bmad-test-strategy)
4. Implementation (bmad-story-planning, bmad-development-execution)

State tracked in: `docs/bmad-workflow-status.md`, `docs/sprint-status.yaml`

### OpenSpec Workflow (Level 0-1 changes)
1. openspec-change-proposal
2. openspec-change-implementation
3. openspec-change-closure

State tracked in: `openspec/changes/<change-id>/`

## Documentation Style (Metabase Guide)

- Lead with what to do, then explain why
- Use headings that state your point: "Set SAML before adding users" not "SAML configuration"
- Backticks for code/variables, **bold** for UI elements
- Use "people" or "companies" instead of "users"
- Contractions are fine (can't, don't)
- Never link the word "here" - use descriptive text
- American spelling, serial commas

## Adding New Skills

1. Create directory: `.claude/skills/[skill-name]/`
2. Add `SKILL.md` with YAML frontmatter
3. Include specific trigger words in description for discovery
4. Optional: Add `reference.md`, `examples.md`, `scripts/`
