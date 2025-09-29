# Claude Configuration

We are using Linux Mint to develop this project.

# Be extremely concise!
# When asked to develop a task from linear, make sure all the acceptance criteria are fulfilled.

## Development Philosophy (CRITICAL)

### Simple Error Handling (DO THIS)
✅ Check required fields aren't empty
✅ Validate user input format (email, phone, etc.)
✅ Handle obvious failure cases (file not found, network timeout)
✅ Return clear error messages to users
✅ Basic try-catch for expected errors

### Over-Engineering (DON'T DO THIS)
❌ Multiple libraries for same task (2 PDF readers "just in case")
❌ Fallback strategies before encountering actual problems
❌ Complex abstraction layers for simple operations
❌ Retry mechanisms with exponential backoff before seeing failures
❌ Defensive code for edge cases that don't exist yet

### The Rule
- **Simple validation**: Always include
- **Redundant solutions**: Only after proven necessary
- **Pick ONE approach**: Use it until it fails
- **When it fails**: THEN add alternatives/complexity

## Proactive Agent Usage

### Intelligent Code Searcher

Use the `intelligent-code-searcher` agent automatically when:

- **Multiple search operations** would be needed with Read, Grep, or Glob
- **Code exploration** is required to understand implementation details
- **Specific functionality** needs to be located across multiple files
- **Complex queries** about how code works or where it's implemented
- **Cross-referencing** between different parts of the codebase is needed

Instead of using Read/Grep/Glob tools directly for code searches, delegate to the `intelligent-code-searcher` agent to:
- Save context by filtering out irrelevant information
- Provide comprehensive analysis of relevant findings
- Strategically combine multiple search tools
- Deliver focused results for the specific task at hand

**Examples of when to use:**
- "Find authentication implementation"
- "Locate API route definitions"
- "Understand how user validation works"
- "Find all test files for feature X"
- "Show me configuration for database connections"

The agent will handle the search strategy and return complete, relevant information without context pollution from irrelevant files or code sections.

### Workflow Agents

Use these agents for structured project development:

#### tradutor
- **Purpose**: Translates user input into structured, LLM-friendly requirements
- **Usage**: First step for both greenfield and brownfield projects
- **Output**: `outputs/translated-requirements.md`

#### docmaster
- **Purpose**: Creates comprehensive Product Requirements Document (PRD)
- **Usage**: Greenfield projects only, after tradutor
- **Input**: `outputs/translated-requirements.md`
- **Output**: `outputs/project-prd.md`

#### system-architect
- **Purpose**: Transform product requirements into comprehensive technical architecture blueprints
- **Usage**: Greenfield projects only, after docmaster
- **Input**: `outputs/project-prd.md`
- **Output**: `outputs/architecture.md`

#### taskmaster
- **Purpose**: Breaks down requirements into organized, timestamped development tasks
- **Usage**: Both greenfield (after architecture) and brownfield workflows
- **Requirements**: Always needs `outputs/architecture.md`
- **Output**: Timestamped files in `outputs/tasks/[category]/`

#### senior-frontend-engineer
- **Purpose**: Systematic frontend implementation from technical specifications
- **Usage**: Transform design systems and API contracts into production-ready UIs
- **Output**: Modular, performant, accessible web applications

#### senior-backend-engineer
- **Purpose**: Implement robust, scalable server-side systems from technical specifications
- **Usage**: Build APIs, business logic, and data persistence layers
- **Output**: Production-quality backend systems with database migrations

#### ux-ui-designer
- **Purpose**: Design user experiences and visual interfaces for applications
- **Usage**: Translate product manager feature stories into comprehensive design systems
- **Output**: Style guides, user flows, implementation-ready specifications

#### task-to-linear
- **Purpose**: Convert project tasks from docs/tasks/ into Linear tickets
- **Usage**: Following team workflow and project conventions
- **Output**: Actionable development tickets with proper dependencies and labels

### Workflow Commands

#### /setup-docs
- **Purpose**: Greenfield project documentation setup
- **Sequence**: tradutor → docmaster → system-architect
- **Stops**: After architecture creation for user verification
- **Use when**: Starting new projects, need complete documentation

#### /setup-tasks
- **Purpose**: Create initial task breakdown after architecture approval
- **Requirements**: Verified `outputs/architecture.md` and project docs
- **Agent**: taskmaster
- **Use when**: Architecture approved, ready to plan development

#### /add-feature
- **Purpose**: Add feature tasks to existing projects
- **Sequence**: tradutor → taskmaster (uses existing architecture)
- **Use when**: Brownfield development, extending existing systems

#### /process-task
- **Purpose**: Automated end-to-end task processing from Linear ticket to completion
- **Usage**: Project workflow management with automated task execution
- **Use when**: Processing existing Linear tickets through development workflow

### Usage Examples

**Greenfield**: `/setup-docs "build e-commerce platform"` → verify architecture → `/setup-tasks`
**Brownfield**: `/add-feature "add dark mode toggle"`

## Acceptance Criteria Compliance (CRITICAL)
- **NEVER assume** user's environment, OS, setup, or preferences
- **ALWAYS ask** when encountering environment issues or technical blockers
- **STOP implementation** immediately when any acceptance criteria cannot be met
- **ASK USER** for guidance before proceeding with workarounds or alternatives
- **DO NOT mark task complete** until ALL acceptance criteria are 100% met and verified
- **DO NOT continue** to subsequent tasks if prerequisites are not fully satisfied
- **VERIFY explicitly** each acceptance criterion before claiming completion