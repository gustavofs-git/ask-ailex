---
name: executor
description: Universal task analysis, implementation and documentation system with anti-over-engineering philosophy. Questions complexity first, implements second.
---

This command provides comprehensive analysis, implementation oversight, and documentation for Linear tasks. It follows the "Question First, Implement Second" philosophy, automatically detecting and challenging over-engineering while ensuring proper documentation and validation at every step.

## Purpose

The `/executor` command is designed for thorough task analysis and execution with built-in safeguards against over-engineering. It provides critical analysis of implementation complexity, intelligent agent selection, mandatory user validation, and comprehensive documentation generation for any Linear task.

## Command Sequence

This command executes an 8-stage workflow with mandatory checkpoints:

### 1. Critical Analysis
**Purpose**: Analyze task and detect over-engineering patterns
**Process**:
- Fetch Linear task via MCP
- Analyze existing implementation (if any)
- Calculate complexity metrics (file count, lines of code, abstraction levels)
- Identify unnecessary complexity and suggest simplifications
**Output**: Critical analysis report with over-engineering detection

### 2. Agent Selection
**Purpose**: Choose the most appropriate specialized agent
**Process**:
- Analyze task type and requirements
- Map to suitable agent (senior-backend-engineer, senior-frontend-engineer, system-architect, etc.)
- Consider complexity level and required expertise
- Provide confidence scoring and alternatives
**Output**: Selected agent with reasoning

### 3. Linear Update (if needed)
**Purpose**: Update Linear task with complexity analysis
**Process**:
- Add comments about detected over-engineering
- Suggest scope simplifications
- Propose alternative approaches
- Flag complexity concerns for review
**Output**: Linear comments with suggested improvements

### 4. User Validation
**Purpose**: Mandatory approval checkpoint before implementation
**Process**:
- **STOPS EXECUTION** and presents analysis to user
- Shows complexity concerns and suggested simplifications
- Asks explicit approval for proposed approach
- Will NOT proceed without user confirmation
**Output**: User approval or rejection with feedback

### 5. Implementation (if approved)
**Purpose**: Execute task with selected agent under oversight
**Process**:
- Use Task tool to execute selected specialized agent
- Monitor implementation for complexity creep
- Apply approved simplifications
- Track file creation and code metrics
**Output**: Implementation results with complexity tracking

### 6. Post-Implementation Analysis
**Purpose**: Validate results and measure final complexity
**Process**:
- Re-analyze implementation complexity
- Execute relevant tests
- Validate expected outputs
- Measure performance and quality metrics
**Output**: Implementation validation report

### 7. Structured Documentation
**Purpose**: Generate comprehensive, organized documentation
**Process**:
- Create `docs/tasks/{TASK_ID}_implementation_summary/` directory
- Generate implementation summary, code explanations, testing guides
- Document agent selection reasoning and complexity decisions
- **Document practical error handling**: List simple validations included (required fields, format checks, basic try-catch)
- **Document over-engineering avoided**: Note redundant solutions rejected, single library chosen
- Create organized test files in `tests/tasks/{TASK_ID}/`
**Output**: Complete documentation suite distinguishing practical validation from defensive complexity

### 8. Final Linear Update
**Purpose**: Mark task complete and link documentation
**Process**:
- Update Linear task status to completed
- Add links to generated documentation
- Summarize complexity decisions and simplifications applied
- Record final metrics and outcomes
**Output**: Updated Linear task with documentation links

## Usage

```bash
/executor GUS-7
```

```bash
/executor DEV-123
```

```bash
/executor TASK-456
```

## What Happens

1. **Automatic Analysis**: The task is fetched from Linear and analyzed for complexity issues, over-engineering patterns, and implementation requirements

2. **Intelligent Agent Matching**: Based on task characteristics, the most suitable specialized agent is selected with confidence scoring

3. **Complexity Challenge**: If over-engineering is detected, the system automatically questions the approach and suggests simplifications

4. **Mandatory Approval**: Execution stops and requires explicit user approval before proceeding with any implementation

5. **Monitored Implementation**: If approved, the selected agent implements the task with ongoing complexity monitoring

6. **Comprehensive Validation**: Results are tested, validated, and measured against quality metrics

7. **Structured Documentation**: Complete documentation is generated in organized directories with detailed explanations

8. **Task Completion**: Linear task is updated with completion status and documentation links

## Output Files Created

After successful execution, you'll have:

### Documentation Directory: `docs/tasks/{TASK_ID}_implementation_summary/`
- `implementation_summary.md` - Executive summary of what was implemented
- `code_explanation.md` - Detailed line-by-line code explanations
- `testing_guide.md` - How to run tests and validate functionality
- `agent_selection.md` - Justification for chosen agent and approach

### Test Directory: `tests/tasks/{TASK_ID}/`
- `test_basic.py` - Basic functionality tests
- `test_integration.py` - Integration and system tests
- `test_performance.py` - Performance and quality tests

### Linear Updates
- Task status updated to completed
- Comments added with complexity analysis
- Documentation links attached
- Implementation decisions recorded

## Anti-Over-Engineering Features

### Automatic Detection
- **File Count Analysis**: Flags implementations with excessive number of files
- **Code Complexity Metrics**: Measures lines of code, abstraction levels, interface usage
- **Pattern Recognition**: Identifies common over-engineering patterns (unnecessary interfaces, excessive abstractions)
- **Dependency Analysis**: Reviews external dependencies and integration complexity
- **Redundant Library Detection**: Flags multiple libraries for same purpose (e.g., 2 PDF readers)
- **Premature Fallback Detection**: Identifies fallback strategies added before encountering actual problems

### Simplification Suggestions
- **Consolidation Opportunities**: Suggests combining related functionality
- **Abstraction Reduction**: Recommends removing unnecessary interfaces and abstractions
- **Single Library Approach**: Pick ONE library/approach, use until it fails
- **Core Focus**: Helps identify and prioritize essential functionality
- **Practical Error Handling**: Document simple validation (required fields, format checks) as part of normal implementation
- **Remove Defensive Complexity**: Strip out retry mechanisms, fallback strategies, edge case handling added "just in case"

### Validation Checkpoints
- **Mandatory User Review**: Cannot proceed without explicit approval
- **Complexity Justification**: Requires explanation for any high-complexity implementations
- **Alternative Evaluation**: Presents simpler alternatives before implementation
- **Scope Verification**: Confirms implementation matches actual requirements

## Example Scenarios

### Over-Engineering Detection
```bash
/executor GUS-7
# Output: "COMPLEXITY ALERT: 21 files detected for basic PDF processing.
# Suggested approach: 3-4 files maximum focusing on core functionality.
# Proceed with simplification? [Y/N]"
```

### Agent Selection
```bash
/executor API-456
# Output: "Task analysis: REST API endpoints
# Recommended agent: senior-backend-engineer (confidence: 0.9)
# Alternative: system-architect (if architecture changes needed)
# Proceed with backend specialist? [Y/N]"
```

### Implementation Monitoring
```bash
/executor UI-789
# Output: "Implementation started with senior-frontend-engineer
# Monitoring: 3 components created (within expected range)
# No complexity concerns detected
# Testing: All UI tests passing"
```

## When to Use This Command

- **Critical Tasks**: Important features that need thorough analysis and documentation
- **Complex Implementations**: Tasks that might be prone to over-engineering
- **Team Projects**: When multiple people need to understand implementation decisions
- **Quality Assurance**: Tasks requiring comprehensive testing and validation
- **Learning Opportunities**: When you want to understand why certain approaches were chosen
- **Process Compliance**: Projects requiring detailed documentation and approval workflows

## When NOT to Use This Command

- **Simple Tasks**: Minor bug fixes or trivial changes that don't need analysis
- **Urgent Hotfixes**: Time-critical fixes where analysis overhead isn't justified
- **Experimental Code**: Proof-of-concepts or prototypes where over-engineering isn't a concern
- **Well-Defined Tasks**: Tasks where implementation approach is already clear and agreed upon

## Prerequisites

- **Linear Integration**: MCP Linear must be configured and accessible
- **Project Structure**: Basic project directory structure should exist
- **Agent Access**: Specialized agents (senior-backend-engineer, etc.) must be available
- **Write Permissions**: Must be able to create documentation and test directories

## Error Handling

The command will fail if:
- **Linear Task Not Found**: Invalid task ID or inaccessible task
- **MCP Connection Issues**: Cannot connect to Linear via MCP
- **Permission Problems**: Cannot create required directories or files
- **Agent Unavailable**: Selected specialized agent is not accessible
- **User Rejection**: User explicitly rejects the proposed implementation approach

## Best Practices for Success

### Provide Context
- Ensure Linear tasks have clear descriptions and acceptance criteria
- Include technical constraints or preferences in task descriptions
- Specify expected complexity level and quality requirements

### Review Analysis Carefully
- Take time to understand complexity concerns raised
- Consider suggested simplifications seriously
- Ask questions if analysis seems incorrect

### Trust the Process
- Don't skip the validation checkpoint
- Allow the system to challenge over-engineering
- Use generated documentation as learning material

### Maintain Standards
- Keep task descriptions updated based on analysis feedback
- Use consistent naming and structure across tasks
- Review and improve based on post-implementation analysis

## Integration with Other Commands

### Workflow Integration
- Use after `/setup-tasks` for implementing planned tasks
- Combine with `/add-feature` for new functionality implementation
- Complement `/process-task` with additional analysis and documentation

### Documentation Chain
- Builds upon architecture from `/setup-docs`
- Creates task-specific documentation that references system architecture
- Feeds implementation lessons back into project knowledge base

## Success Metrics

A successful `/executor` run produces:
- ✅ **Critical Analysis Complete**: Over-engineering detected and addressed
- ✅ **Appropriate Agent Selected**: Right specialist for the task type
- ✅ **User Validation Passed**: Explicit approval obtained before implementation
- ✅ **Implementation Successful**: Task completed within complexity guidelines
- ✅ **Tests Passing**: All validation and quality checks successful
- ✅ **Documentation Generated**: Complete documentation suite created
- ✅ **Linear Task Updated**: Task marked complete with proper documentation

Remember: The `/executor` command prioritizes quality and maintainability over speed. Its primary goal is to ensure thoughtful, well-documented implementations that avoid unnecessary complexity.