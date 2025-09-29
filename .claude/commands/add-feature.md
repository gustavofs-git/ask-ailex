---
name: add-feature
description: Adds new feature tasks to existing projects by translating feature requests and creating timestamped tasks using current architecture context. Designed for brownfield development workflows.
---

This command adds new functionality to existing projects without regenerating all project documentation. It's designed for brownfield development where you have an established codebase and architecture but need to add new features or capabilities.

## Purpose

The `/add-feature` command handles the brownfield workflow for extending existing projects. It translates your feature request into structured requirements and creates appropriate development tasks that integrate with your existing system architecture.

## Prerequisites

**Required files** (from previous greenfield setup):
- `outputs/architecture.md` - Existing system architecture
- Either `outputs/project-prd.md` OR previous project documentation

**Project Context**: This command assumes you have an established project with existing architecture and documentation.

## Command Sequence

This command executes the following agents in order:

### 1. Feature Requirements Translation
**Agent**: `tradutor`
**Purpose**: Convert your feature request into structured requirements
**Output**: `outputs/translated-requirements.md` (overwrites previous)

### 2. Feature Task Creation
**Agent**: `taskmaster`
**Purpose**: Create development tasks for the new feature
**Input**:
- `outputs/translated-requirements.md` (new feature requirements)
- `outputs/architecture.md` (existing system architecture)
- Existing project context
**Output**: New timestamped task files in `outputs/tasks/[category]/`

## Usage

```bash
/add-feature "Add dark mode toggle to the application with user preference persistence and system theme detection"
```

```bash
/add-feature "Implement two-factor authentication using SMS and authenticator apps for enhanced security"
```

## What Happens

1. **Feature Analysis**: Your feature request is analyzed and converted into structured requirements that consider integration with the existing system

2. **Architecture Integration**: The taskmaster reviews your existing architecture to understand how the new feature should integrate with current systems

3. **Task Creation**: New timestamped task files are created in appropriate categories, ensuring no duplication with existing tasks

4. **Dependency Mapping**: Tasks are created with awareness of existing system components and dependencies

## Output Files Created

New timestamped files added to existing structure:
```
outputs/tasks/
├── setup/
│   ├── [existing files...]
│   └── 2024-01-17_09-15-00_feature-environment-setup.md  # New
├── frontend/
│   ├── [existing files...]
│   └── 2024-01-17_09-20-00_feature-ui-components.md      # New
├── backend/
│   ├── [existing files...]
│   └── 2024-01-17_09-25-00_feature-api-endpoints.md      # New
└── testing/
    ├── [existing files...]
    └── 2024-01-17_09-30-00_feature-test-cases.md          # New
```

## Task Integration Strategy

### Existing System Awareness
- **Architecture Alignment**: Tasks align with existing technology stack and patterns
- **Component Reuse**: Leverages existing components and services where possible
- **Consistency**: Maintains coding standards and architectural patterns
- **Dependencies**: Considers existing system dependencies and constraints

### Incremental Development
- **Non-Breaking**: Tasks designed to add functionality without breaking existing features
- **Backward Compatibility**: Ensures new features don't disrupt current user experience
- **Gradual Rollout**: Tasks can be implemented incrementally
- **Testing Integration**: Tests work with existing test suites

## When to Use This Command

- **Existing projects**: When you have an established codebase and architecture
- **Feature additions**: Adding new functionality to existing systems
- **Enhancement requests**: Improving or extending current capabilities
- **User feedback**: Implementing requested features from users
- **Business requirements**: Adding new business functionality
- **Technical improvements**: Adding performance, security, or maintenance features

## When NOT to Use This Command

- **New projects**: Use `/setup-docs` and `/setup-tasks` for greenfield projects
- **Major architectural changes**: Significant system redesigns may need full replanning
- **Complete rewrites**: When replacing entire system components
- **Missing architecture**: If you don't have existing architecture documentation

## Example Feature Scenarios

### User Interface Enhancement
```bash
/add-feature "Add drag-and-drop functionality to the task management board with real-time updates and conflict resolution"
```

### Integration Feature
```bash
/add-feature "Integrate with Slack to send notifications for project updates and allow task creation from Slack commands"
```

### Security Feature
```bash
/add-feature "Implement role-based access control with admin, manager, and user roles, including permission management UI"
```

### Performance Feature
```bash
/add-feature "Add caching layer with Redis for frequently accessed data and implement cache invalidation strategies"
```

### Analytics Feature
```bash
/add-feature "Create analytics dashboard showing user activity, project progress, and performance metrics with exportable reports"
```

## Task Output Characteristics

### Feature-Specific Tasks
- **Focused scope**: Tasks specifically for the new feature
- **Integration points**: Clear interfaces with existing system
- **Isolated changes**: Minimal impact on existing functionality
- **Feature flags**: Support for gradual rollout if needed

### Architecture Consistency
- **Technology alignment**: Uses existing tech stack and frameworks
- **Pattern consistency**: Follows established coding and design patterns
- **Data integration**: Works with existing database schema and models
- **API consistency**: Maintains existing API design principles

## Error Handling

The command will fail if:
- No existing architecture file found
- Feature request is too vague or conflicts with existing architecture
- Unable to create new task files
- Existing project context is incomplete or corrupted

## Tips for Best Results

1. **Be specific**: Provide detailed information about the feature you want to add
2. **Consider integration**: Think about how the feature should work with existing functionality
3. **Mention constraints**: Include any technical or business constraints
4. **User experience**: Describe how users should interact with the new feature
5. **Review existing system**: Understand your current architecture before adding features

## Workflow Integration

This command fits into the brownfield development workflow:

**Existing Project** → `/add-feature` → **Review Tasks** → **Implementation** → **Testing** → **Deployment**

The tasks created will integrate seamlessly with your existing development process and can be imported into your project management tools alongside existing project tasks.

## Follow-up Actions

After running `/add-feature`:
1. Review generated task files for accuracy and completeness
2. Prioritize new tasks against existing development work
3. Consider feature flag implementation for gradual rollout
4. Update project timelines and resource allocation
5. Coordinate with team members on implementation approach
6. Plan testing strategy that includes existing functionality regression testing