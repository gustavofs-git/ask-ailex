---
name: setup-docs
description: Orchestrates initial project documentation setup by translating user requirements, creating comprehensive PRD, and designing system architecture. Stops after architecture creation for user verification.
---

This command orchestrates the initial documentation phase of greenfield projects. It executes a sequence of specialized agents to transform user input into comprehensive project specifications and technical architecture.

## Purpose

The `/setup-docs` command is designed for greenfield projects where you need to establish the foundational documentation before proceeding to task breakdown. It handles the complete requirements → specifications → architecture workflow while allowing for verification checkpoints.

## Command Sequence

This command executes the following agents in order:

### 1. Requirements Translation
**Agent**: `tradutor`
**Purpose**: Convert user's natural language input into structured requirements
**Output**: `outputs/translated-requirements.md`

### 2. Product Documentation
**Agent**: `docmaster`
**Purpose**: Create comprehensive Product Requirements Document (PRD)
**Input**: `outputs/translated-requirements.md`
**Output**: `outputs/project-prd.md`

### 3. System Architecture
**Agent**: `system-architect`
**Purpose**: Design technical architecture based on requirements and PRD
**Input**: `outputs/translated-requirements.md` and `outputs/project-prd.md`
**Output**: `outputs/architecture.md`

## Usage

```bash
/setup-docs "I want to build a task management application with user authentication, project creation, task assignment, and real-time collaboration features. It should support teams of up to 100 users and integrate with Slack and email notifications."
```

## What Happens

1. **Requirements Processing**: Your input is analyzed and converted into structured, clear requirements that other agents can process effectively

2. **Product Specification**: A comprehensive PRD is created that includes user personas, feature specifications, success criteria, and business context

3. **Architecture Design**: Technical architecture is designed including technology stack, system components, data models, and integration patterns

4. **Verification Point**: Command stops here to allow you to review the architecture before proceeding to task breakdown

## Output Files Created

After successful execution, you'll have:
- `outputs/translated-requirements.md` - Structured requirements
- `outputs/project-prd.md` - Complete product specification
- `outputs/architecture.md` - Technical architecture document

## Next Steps

After reviewing the architecture output:
1. If architecture looks good: Run `/setup-tasks` to create the initial task breakdown
2. If architecture needs changes: Manually edit `outputs/architecture.md` or re-run `/setup-docs` with clarifications

## When to Use This Command

- **New projects (greenfield)**: Starting from scratch with a project idea
- **Complete documentation needed**: When you need full specifications and architecture
- **Team collaboration**: When multiple people need to understand the project scope and technical approach
- **Complex projects**: Projects requiring careful planning and architectural consideration

## When NOT to Use This Command

- **Existing projects**: Use `/add-feature` instead for adding functionality to existing systems
- **Simple tasks**: For minor changes or simple features, direct agent calls might be more efficient
- **Architecture already exists**: Skip to `/setup-tasks` if you already have project documentation and architecture

## Error Handling

The command will fail if:
- User input is too vague or incomplete
- Required output directories cannot be created
- Previous command outputs are corrupted

## Tips for Best Results

1. **Be specific**: Provide detailed information about what you want to build
2. **Include context**: Mention target users, scale, and key constraints
3. **Technical preferences**: If you have technology preferences, mention them
4. **Business goals**: Explain what problem you're solving and success criteria

## Example Scenarios

### E-commerce Platform
```bash
/setup-docs "Build an e-commerce platform for small businesses to sell products online. Need inventory management, payment processing, customer accounts, order tracking, and admin dashboard. Should handle 1000+ products and integrate with Stripe for payments."
```

### SaaS Application
```bash
/setup-docs "Create a project management SaaS for development teams. Features include kanban boards, time tracking, team collaboration, reporting, and integrations with GitHub and Jira. Targeting teams of 5-50 people with subscription billing."
```

### Internal Tool
```bash
/setup-docs "Build an internal employee onboarding system for HR. New employees should complete forms, watch training videos, get task assignments, and track progress. Integrate with existing AD and Slack. Support 500+ employees."
```

Remember: This command creates the foundation for your project. Take time to review the architecture output carefully, as it will guide all subsequent development work.