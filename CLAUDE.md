# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a Claude Code skills repository containing custom skills and specialized agents that extend Claude's capabilities for documentation, workflow orchestration, development, and research tasks. The repository also contains ThingsBoard technical documentation organized in numbered directories.

## Directory Structure

```
.claude/
├── agents/          # 37 specialized agent definitions
├── skills/          # 21 reusable Claude Code skills
└── settings.local.json

01-architecture/     # ThingsBoard system architecture
02-core-concepts/    # Core concepts (data-model, entities, identity)
03-actor-system/     # Actor system documentation
04-rule-engine/      # Rule engine documentation
05-transport-layer/  # Transport layer documentation
06-api-layer/        # API layer documentation
07-data-persistence/ # Data persistence documentation
08-message-queue/    # Message queue documentation
09-security/         # Security documentation
10-frontend/         # Frontend documentation
11-microservices/    # Microservices documentation
diagrams/            # Diagram assets
```

## Skills (21 Total)

All skills are in `.claude/skills/`. Each has a `SKILL.md` with YAML frontmatter:
- `name`: Lowercase, hyphens only (must match directory name)
- `description`: What it does and when to use it
- `allowed-tools`: Optional tool restrictions

### Workflow Orchestration
- **main-workflow-router**: Routes between BMAD (Level 2-4) and OpenSpec (Level 0-1) workflows. Auto-invokes on "start project", "what's next", "status".
- **workflow-orchestration-patterns**: Design durable workflows with Temporal for distributed systems (sagas, fan-out/fan-in, async callbacks).
- **compound-engineering**: AI-assisted development with Plan → Work → Review → Compound loop.

### Documentation
- **docs-write**: Write documentation following Metabase's conversational style. Format with `yarn prettier --write <file-path>`.
- **docs-review**: Review documentation for style compliance. Supports local and GitHub PR review modes.
- **doc-coauthoring**: Structured workflow for collaborative documentation (context gathering → refinement → reader testing).
- **architecture-doc-creator**: Auto-activating skill for creating architecture documentation.
- **configuration-reference-generator**: Auto-activating skill for configuration reference documentation.
- **architecture-decision-records**: Document architectural decisions using ADR patterns (MADR, Y-Statement, RFC).

### Planning & Research
- **brainstorming**: Refine rough ideas through iterative questioning (ONE QUESTION AT A TIME rule).
- **prd**: Generate Product Requirements Documents. Outputs to `tasks/prd-[feature-name].md`.
- **ralph**: Convert PRDs to prd.json format for Ralph autonomous agent system.
- **web-research**: Structured web research using subagents. Creates `research_[topic_name]/` folders.
- **create-plan**: Create concise, actionable implementation plans with action-item checklists.

### Development Patterns
- **modern-javascript-patterns**: Master ES6+ features, async/await, destructuring, functional programming.
- **bash-defensive-patterns**: Defensive Bash programming for production-grade scripts (strict mode, error trapping, CI/CD).

### Agent & Learning Systems
- **reasoningbank-intelligence**: Adaptive learning with ReasoningBank for self-improving agents.
- **agent-memory**: Persistent memory space for storing knowledge across conversations.

### Content Creation
- **concept-workflow**: End-to-end workflow for creating JavaScript concept documentation.
- **internal-comms**: Write internal communications (status reports, newsletters, FAQs, incident reports).

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

## Specialized Agents (37 Total)

Located in `.claude/agents/`. Each agent is a markdown file defining a specialized role.

### By Category
- **Development**: backend-developer, frontend-developer, fullstack-developer, typescript-pro, javascript-pro
- **Architecture**: cloud-architect, microservices-architect, java-architect, angular-architect, spring-boot-engineer, architect-reviewer
- **Infrastructure**: devops-engineer, kubernetes-specialist, platform-engineer, network-engineer, iot-engineer, embedded-systems
- **Database**: database-administrator
- **Management**: project-manager, scrum-master, product-manager, task-distributor
- **Documentation**: technical-writer, documentation-engineer, api-documenter
- **Engineering**: performance-monitor, security-engineer, error-coordinator, tooling-engineer, websocket-engineer, dx-optimizer
- **Coordination**: workflow-orchestrator, multi-agent-coordinator, agent-organizer, knowledge-synthesizer, context-manager, research-analyst

## Adding New Skills

1. Create directory: `.claude/skills/[skill-name]/`
2. Add `SKILL.md` with YAML frontmatter
3. Include specific trigger words in description for discovery
4. Optional: Add `reference.md`, `examples.md`, `scripts/`

## Adding New Agents

1. Create file: `.claude/agents/[agent-name].md`
2. Define the agent's role, expertise, and focus areas
3. Agents are available for use via the Task tool's `subagent_type` parameter
