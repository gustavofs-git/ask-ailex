---
name: setup-tasks
description: Creates initial task breakdown using verified architecture and project specifications. Generates organized, timestamped task files categorized by development type for comprehensive project implementation.
---

This command creates the initial task breakdown for greenfield projects after the architecture has been verified. It transforms project specifications and technical architecture into actionable development tasks organized by category.

## Purpose

The `/setup-tasks` command is the second phase of greenfield project setup. It assumes you have already run `/setup-docs` and verified the architecture output. This command creates comprehensive task breakdowns that developers can execute to build the complete project.

## Prerequisites

**Required files** (created by `/setup-docs`):
- `outputs/architecture.md` - Technical architecture document (must be verified/approved)
- `outputs/project-prd.md` - Product Requirements Document
- `outputs/translated-requirements.md` - Structured requirements

## Command Execution

This command executes the `taskmaster` agent which:

### 1. Input Analysis
- Reads and analyzes the system architecture
- Reviews project requirements and specifications
- Maps features to architectural components
- Identifies technical dependencies

### 2. Task Creation
- Breaks down the project into actionable development tasks
- Organizes tasks by development category
- Creates timestamped task files for version control
- Defines dependencies and sequencing

### 3. File Organization
Creates organized task structure:
```
outputs/tasks/
├── setup/
│   └── [timestamp]_initial-project-setup.md
├── frontend/
│   ├── [timestamp]_ui-components.md
│   └── [timestamp]_user-interface.md
├── backend/
│   ├── [timestamp]_api-development.md
│   └── [timestamp]_database-setup.md
├── testing/
│   └── [timestamp]_test-framework.md
└── deployment/
    └── [timestamp]_deployment-pipeline.md
```

## Usage

```bash
/setup-tasks
```

**Note**: This command doesn't require additional input as it uses the existing project documentation files.

## What This Command Creates

### Task Categories

**Setup Tasks**
- Development environment configuration
- Project initialization and tooling
- Database setup and migrations
- CI/CD pipeline establishment

**Frontend Tasks**
- UI component development
- Page layouts and routing
- Client-side business logic
- Styling and responsive design
- API integration

**Backend Tasks**
- API endpoint development
- Database models and relationships
- Business logic implementation
- Authentication and authorization
- Data processing and validation

**Testing Tasks**
- Test framework configuration
- Unit test development
- Integration test scenarios
- End-to-end testing
- Quality assurance processes

**Deployment Tasks**
- Build process optimization
- Environment configuration
- Hosting and infrastructure
- Monitoring and logging
- Performance optimization

### Task File Structure

Each task file contains:
- Detailed task description
- Clear acceptance criteria
- Implementation guidance
- Dependencies and prerequisites
- Technical requirements aligned with architecture
- Testing strategy
- Definition of done

## Output Files

After execution, you'll have:
- Multiple timestamped task files in `outputs/tasks/[category]/`
- Each file represents specific, actionable development work
- Tasks organized by development discipline
- Clear dependencies and sequencing information

## When to Use This Command

- **After architecture approval**: Once you've reviewed and approved the system architecture
- **Greenfield projects**: For new projects needing complete task breakdown
- **Team planning**: When you need to distribute work across multiple developers
- **Project estimation**: To understand scope and complexity of the full project

## When NOT to Use This Command

- **Before architecture review**: Always verify architecture first
- **Existing projects**: Use `/add-feature` for adding functionality to existing systems
- **Feature additions**: This creates tasks for entire projects, not individual features
- **Architecture changes**: If you modify architecture, you may need to re-run this command

## Integration with Development Workflow

### Immediate Next Steps
1. Review generated task files in each category
2. Prioritize tasks based on dependencies
3. Assign tasks to team members
4. Begin development starting with setup tasks

### Future Integration
- Tasks can be imported into Linear or other project management tools
- Use task files as foundation for sprint planning
- Track progress by updating task status
- Reference task files during code reviews

## Error Handling

The command will fail if:
- Required architecture file doesn't exist
- Project documentation files are missing or corrupted
- Unable to create output directories
- Architecture and requirements are inconsistent

## Tips for Best Results

1. **Verify architecture first**: Always review `outputs/architecture.md` before running this command
2. **Complete documentation**: Ensure your PRD and requirements are comprehensive
3. **Architecture alignment**: Make sure your architecture supports all required features
4. **Review task output**: Check generated tasks for completeness and accuracy

## Example Task Output

A typical backend task might look like:

```markdown
# Backend: User Authentication API

**Created**: 2024-01-15 14:30:00
**Category**: backend
**Priority**: High
**Estimated Effort**: 8 hours

## Description
Implement secure user authentication system with JWT tokens, password hashing, and session management.

## Acceptance Criteria
- [ ] User registration endpoint with validation
- [ ] Login endpoint with secure password verification
- [ ] JWT token generation and validation
- [ ] Password reset functionality
- [ ] Session management and logout

## Dependencies
- Database schema setup
- Security configuration
- Password hashing library integration

[... additional details ...]
```

## Workflow Integration

This command fits into the complete greenfield workflow:

1. **User Input** → `/setup-docs` → **(Review Architecture)** → `/setup-tasks` → **Development**

The tasks created by this command become the roadmap for your development team, ensuring all work aligns with the approved architecture and meets the project requirements.