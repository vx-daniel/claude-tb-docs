# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Project Name**: ThingsBoard Platform Documentation & Claude Code Skills

**Purpose**: A dual-purpose repository containing:
1. Technical documentation for the ThingsBoard IoT platform (v4.3.0-RC), prepared for platform rewrite
2. Custom Claude Code skills and specialized agents for documentation, workflow orchestration, development, and research tasks

**Tech Stack (ThingsBoard)**:
| Layer | Technology |
|-------|------------|
| Runtime | Java 17, Spring Boot 3.4.10 |
| Message Queue | Kafka 3.9.1 |
| Databases | PostgreSQL, Cassandra, TimescaleDB |
| Cache | Redis/Valkey, Caffeine |
| Frontend | Angular 18.2.13, NgRx, Material Design |
| Service Discovery | Apache Zookeeper |
| Load Balancer | HAProxy |

## Project Structure

```
.claude/
├── agents/              # 43 specialized agent definitions
├── commands/            # Custom slash commands
│   └── update-docs.md   # /update-docs command
├── skills/              # 21 reusable Claude Code skills
└── settings.local.json  # Local permissions config

01-architecture/         # ThingsBoard system architecture
02-core-concepts/        # Core concepts (data-model, entities, identity)
03-actor-system/         # Actor system documentation
04-rule-engine/          # Rule engine documentation
05-transport-layer/      # Transport layer documentation
06-api-layer/            # API layer documentation
07-data-persistence/     # Data persistence documentation
08-message-queue/        # Message queue documentation
09-security/             # Security documentation
10-frontend/             # Frontend documentation
11-microservices/        # Microservices documentation
diagrams/                # Diagram assets

CLAUDE.md                # This file - project guidance
README.md                # Project overview and quick start
GLOSSARY.md              # ThingsBoard terminology
ROADMAP.md               # Documentation progress tracking
```

## Skills (21 Total)

All skills are in `.claude/skills/`. Each has a `SKILL.md` with YAML frontmatter.

### Workflow Orchestration

| Skill | Triggers | Description |
|-------|----------|-------------|
| **main-workflow-router** | "start project", "what's next", "status" | Routes between BMAD (L2-4) and OpenSpec (L0-1) workflows. Auto-invokes on workflow queries. |
| **workflow-orchestration-patterns** | "temporal", "saga pattern", "distributed workflow" | Design durable workflows with Temporal (sagas, fan-out/fan-in, async callbacks). |
| **compound-engineering** | "plan this feature", "implement this", "compound learnings" | AI-assisted development with Plan → Work → Review → Compound loop. |

### Documentation

| Skill | Triggers | Description |
|-------|----------|-------------|
| **docs-write** | "write documentation", "create docs" | Write docs following Metabase's conversational style. Format with `yarn prettier --write <file-path>`. |
| **docs-review** | "review documentation", "check docs PR" | Review documentation for style compliance. Supports local and GitHub PR review modes. |
| **doc-coauthoring** | "write a doc", "draft a proposal", "create a spec" | Structured workflow: context gathering → refinement → reader testing. |
| **architecture-doc-creator** | "architecture doc creator" | Auto-activating skill for creating architecture documentation. |
| **configuration-reference-generator** | "configuration reference generator" | Auto-activating skill for configuration reference documentation. |
| **architecture-decision-records** | "ADR", "architecture decision", "tech decision" | Document architectural decisions using ADR patterns (MADR, Y-Statement, RFC). |

### Planning & Research

| Skill | Triggers | Description |
|-------|----------|-------------|
| **brainstorming** | vague/complex requests needing design exploration | Refine rough ideas through iterative questioning. ONE QUESTION AT A TIME rule. |
| **prd** | "create a prd", "write prd for", "plan this feature" | Generate Product Requirements Documents. Outputs to `tasks/prd-[feature-name].md`. |
| **ralph** | "convert this prd", "ralph json", "create prd.json" | Convert PRDs to prd.json format for Ralph autonomous agent system. |
| **web-research** | "research this topic", "web research" | Structured web research using subagents. Creates `research_[topic_name]/` folders. |
| **create-plan** | "create a plan", "planning" | Create concise implementation plans with action-item checklists. Read-only mode. |

### Development Patterns

| Skill | Triggers | Description |
|-------|----------|-------------|
| **modern-javascript-patterns** | "ES6+", "async/await", "refactor legacy JavaScript" | Master ES6+ features, async/await, destructuring, functional programming patterns. |
| **bash-defensive-patterns** | "bash script", "shell script", "CI/CD pipeline" | Defensive Bash programming (strict mode, error trapping, idempotency). |

### Agent & Learning Systems

| Skill | Triggers | Description |
|-------|----------|-------------|
| **reasoningbank-intelligence** | "adaptive learning", "self-learning agent" | Implement adaptive learning with ReasoningBank for pattern recognition. |
| **agent-memory** | "remember this", "save this", "recall", "check notes" | Persistent memory space in `.claude/skills/agent-memory/memories/`. |

### Content Creation

| Skill | Triggers | Description |
|-------|----------|-------------|
| **concept-workflow** | "create concept page", "JavaScript concept" | End-to-end workflow for JavaScript concept documentation. |
| **internal-comms** | "3P update", "status report", "newsletter", "FAQ" | Write internal communications in company formats. |

### Skill Development

| Skill | Triggers | Description |
|-------|----------|-------------|
| **skill-writer** | "create skill", "write skill", "new skill" | Guide for creating new Claude Code skills with proper frontmatter and structure. |

## Specialized Agents (43 Total)

Located in `.claude/agents/`. Agents are available via the Task tool's `subagent_type` parameter.

### Development
| Agent | Focus |
|-------|-------|
| backend-developer | Node.js/Python/Go, APIs, microservices, 80%+ test coverage |
| frontend-developer | React/Vue/Angular, TypeScript, accessibility, 85%+ coverage |
| fullstack-developer | End-to-end feature delivery, database to UI |
| typescript-pro | Advanced type system, full-stack TypeScript |
| javascript-pro | ES2023+, async programming, Node.js ecosystem |

### Architecture
| Agent | Focus |
|-------|-------|
| cloud-architect | AWS/Azure/GCP, multi-cloud, scalable architectures |
| microservices-architect | Service boundaries, communication patterns, distributed systems |
| java-architect | Spring ecosystem, enterprise Java, reactive programming |
| angular-architect | Angular 15+, RxJS, NgRx, micro-frontends |
| angular-expert | Modern Angular features, component architecture |
| spring-boot-engineer | Spring Boot 3+, cloud-native patterns, microservices |
| architect-reviewer | System design validation, technology stack evaluation |

### Infrastructure
| Agent | Focus |
|-------|-------|
| devops-engineer | CI/CD, containerization, automation, monitoring |
| kubernetes-specialist | Container orchestration, cluster management, security |
| platform-engineer | Internal developer platforms, GitOps, golden path templates |
| network-engineer | Cloud/hybrid networks, security, zero-trust |
| iot-engineer | Connected devices, edge computing, IoT protocols |
| embedded-systems | Microcontroller programming, RTOS, hardware optimization |

### Database & Data
| Agent | Focus |
|-------|-------|
| database-administrator | PostgreSQL/MySQL/MongoDB/Redis, high availability, disaster recovery |
| postgres-expert | Advanced SQL, indexing, performance tuning, replication |
| prisma-expert | Type-safe queries, schema modeling, migrations |

### Protocol Specialists
| Agent | Focus |
|-------|-------|
| mqtt-expert | MQTT protocol, QoS levels, IoT communication, broker optimization |
| websocket-engineer | Real-time communication, WebSocket architectures, low-latency messaging |

### Management
| Agent | Focus |
|-------|-------|
| project-manager | Project planning, resource management, stakeholder communication |
| scrum-master | Agile transformation, team facilitation, impediment removal |
| product-manager | Product strategy, roadmap planning, user-centric development |
| task-distributor | Work allocation, load balancing, priority scheduling |

### Documentation
| Agent | Focus |
|-------|-------|
| technical-writer | Clear documentation, API guides, making complex info accessible |
| documentation-engineer | Documentation-as-code, automated generation, maintainable docs |
| api-documenter | OpenAPI/Swagger, interactive documentation portals |

### Engineering Specialties
| Agent | Focus |
|-------|-------|
| performance-monitor | Metrics collection, anomaly detection, system-wide optimization |
| security-engineer | DevSecOps, vulnerability management, zero-trust architecture |
| error-coordinator | Distributed error handling, failure recovery, cascade prevention |
| tooling-engineer | Developer tools, CLI development, productivity enhancement |
| dx-optimizer | Build performance, tooling efficiency, developer experience |

### Coordination
| Agent | Focus |
|-------|-------|
| workflow-orchestrator | Complex process design, state machines, business process automation |
| multi-agent-coordinator | Inter-agent communication, parallel execution, fault tolerance |
| agent-organizer | Multi-agent orchestration, team assembly, task decomposition |
| knowledge-synthesizer | Cross-agent learning, best practice extraction, collective intelligence |
| context-manager | Information storage/retrieval, state management across agents |
| research-analyst | Information gathering, synthesis, insight generation, actionable intelligence |

### Mobile
| Agent | Focus |
|-------|-------|
| android-expert | Modern Android practices, performance optimization, architecture |

## Commands

### Custom Slash Commands

| Command | Description |
|---------|-------------|
| `/update-docs` | Scan project and update CLAUDE.md with current structure, skills, agents |

### No package.json Scripts

This is a documentation repository without build tooling. No npm/yarn/pnpm scripts are available.

### Git Commands (Pre-authorized)

The following commands are pre-approved in `.claude/settings.local.json`:
- `git add`, `git commit`, `git push`
- `ls`, `xargs`, `find`, `grep`

## Workflow Patterns

### BMAD Workflow (Level 2-4 Complex Projects)

For new products, complex features, or architectural changes:

1. **Analysis** (bmad-discovery-research) - Optional for L2, recommended L3-4
2. **Planning** (bmad-product-planning, bmad-ux-design)
3. **Solutioning** (bmad-architecture-design, bmad-test-strategy)
4. **Implementation** (bmad-story-planning, bmad-development-execution)

State tracked in: `docs/bmad-workflow-status.md`, `docs/sprint-status.yaml`

### OpenSpec Workflow (Level 0-1 Small Changes)

For bug fixes, small changes, simple features:

1. openspec-change-proposal
2. openspec-change-implementation
3. openspec-change-closure

State tracked in: `openspec/changes/<change-id>/`

## Code Conventions

### Documentation Style (Metabase Guide)

- Lead with what to do, then explain why
- Use headings that state your point: "Set SAML before adding users" not "SAML configuration"
- Backticks for code/variables, **bold** for UI elements
- Use "people" or "companies" instead of "users"
- Contractions are fine (can't, don't)
- Never link the word "here" - use descriptive text
- American spelling, serial commas

### Technology-Agnostic Language

Documentation describes behaviors and contracts, not implementation details:
- "message handler" not "Spring Bean"
- "persistent storage" not "JPA Repository"
- "scheduled task" not "Quartz Job"

### Diagrams

All architecture and flow diagrams use [Mermaid](https://mermaid.js.org/) syntax for version control compatibility.

### Skill File Structure

```
.claude/skills/[skill-name]/
├── SKILL.md           # Required - YAML frontmatter + instructions
├── reference.md       # Optional - detailed reference
├── examples.md        # Optional - usage examples
├── scripts/           # Optional - helper scripts
└── templates/         # Optional - file templates
```

### Agent File Structure

```yaml
---
name: agent-name
description: Brief description of specialization
tools: Read, Write, Edit, Bash, Glob, Grep  # Optional tool restrictions
model: claude-sonnet-4-20250514              # Optional model override
---

# Agent content with focus areas, approach, and checklists
```

## Adding New Skills

1. Create directory: `.claude/skills/[skill-name]/`
2. Add `SKILL.md` with YAML frontmatter:
   ```yaml
   ---
   name: skill-name          # Lowercase, hyphens only, max 64 chars
   description: "What it does and when to use it. Include trigger phrases."
   allowed-tools: Read, Grep  # Optional tool restrictions
   ---
   ```
3. Include specific trigger words in description for discovery
4. Optional: Add `reference.md`, `examples.md`, `scripts/`

## Adding New Agents

1. Create file: `.claude/agents/[agent-name].md`
2. Add YAML frontmatter with name, description, and optional tool/model settings
3. Define the agent's role, expertise, focus areas, and quality checklists
4. Agents are available via the Task tool's `subagent_type` parameter

## Quick Start for ThingsBoard Documentation

If you're new to the ThingsBoard documentation, read these in order:

1. [Glossary](./GLOSSARY.md) - Learn the terminology
2. [System Overview](./01-architecture/system-overview.md) - Understand the big picture
3. [Device Entity](./02-core-concepts/entities/device.md) - The central IoT concept
4. [Actor System](./03-actor-system/README.md) - How the runtime works
5. [Telemetry](./02-core-concepts/data-model/telemetry.md) - Primary data type

See [ROADMAP.md](./ROADMAP.md) for documentation status and next steps.

## Source Reference

ThingsBoard documentation derived from source code at:
```
~/work/viaanix/thingsboard/
```

Version: 4.3.0-RC
