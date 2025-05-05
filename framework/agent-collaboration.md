# Agent Collaboration Patterns

*This document was created by Roo in Architect mode, demonstrating the specialized agent approach described in the guide.*

## Overview

Agent Collaboration Patterns define how specialized agents in the multi-agent framework interact with each other to solve complex problems. While the Boomerang Logic system manages the flow of tasks between the Orchestrator and specialist agents, this document focuses on the direct collaboration between specialist agents.

## Core Principles

The key principles of Agent Collaboration are:

1. **Specialization Respect**: Agents recognize and respect each other's domains of expertise
2. **Clear Boundaries**: Collaboration occurs at well-defined interface points
3. **Explicit Requests**: Assistance requests are formal and structured
4. **Traceable Interactions**: All collaborations are documented and tracked
5. **Orchestrator Awareness**: The Orchestrator maintains visibility of all collaborations

## Collaboration Mechanisms

### 1. Direct Consultation

When one agent needs specific expertise from another agent:

```
Agent A → Agent B → Agent A
```

Example: BackendForge consults SecurityStrategist about authentication implementation best practices, then continues its implementation task.

#### Implementation:

```json
{
  "consultation_id": "consult-001",
  "requesting_agent": "BackendForge",
  "consulted_agent": "SecurityStrategist",
  "parent_task_id": "task-005",
  "question": "What authentication approach is recommended for this API?",
  "context": "Implementing user authentication for a REST API with sensitive data",
  "timestamp": "2023-04-29T14:30:00Z"
}
```

Response:

```json
{
  "consultation_id": "consult-001",
  "response": "For this API, implement OAuth 2.0 with JWT tokens and refresh token rotation...",
  "additional_resources": ["security-patterns/oauth-implementation.md"],
  "timestamp": "2023-04-29T14:35:00Z"
}
```

### 2. Collaborative Task Execution

When a task requires multiple agents to work together:

```
Agent A ↔ Agent B
```

Example: FrontCrafter and BackendForge collaborate on API integration, ensuring frontend components correctly interact with backend endpoints.

#### Implementation:

```json
{
  "collaboration_id": "collab-001",
  "parent_task_id": "task-008",
  "participants": ["FrontCrafter", "BackendForge"],
  "objective": "Ensure seamless integration between frontend components and API endpoints",
  "shared_artifacts": ["api-contract.json", "integration-tests/"],
  "status": "in_progress",
  "timestamp": "2023-04-30T09:15:00Z"
}
```

### 3. Review and Feedback

When one agent reviews another agent's work:

```
Agent A → Agent B → Agent A
```

Example: CodeReviewer reviews BackendForge's implementation and provides feedback for improvements.

#### Implementation:

```json
{
  "review_id": "review-001",
  "parent_task_id": "task-012",
  "reviewer": "CodeReviewer",
  "reviewee": "BackendForge",
  "artifact": "src/api/auth-controller.js",
  "feedback": "Authentication implementation needs additional error handling...",
  "status": "needs_revision",
  "timestamp": "2023-05-01T11:20:00Z"
}
```

### 4. Handoff

When one agent completes its part of a task and passes it to another agent:

```
Agent A → Agent B → Orchestrator
```

Example: Visionary creates a high-level architecture and hands it off to Blueprinter for detailed component design.

#### Implementation:

```json
{
  "handoff_id": "handoff-001",
  "parent_task_id": "task-003",
  "from_agent": "Visionary",
  "to_agent": "Blueprinter",
  "artifacts": ["architecture/high-level-design.md"],
  "context": "High-level architecture ready for detailed component design",
  "status": "completed",
  "timestamp": "2023-04-28T16:45:00Z"
}
```

## Common Collaboration Patterns

### Code Implementation Collaborations

#### Frontend-Backend Integration

- **Participants**: FrontCrafter/ReactMaster and BackendForge/NodeSmith/PythonMaster
- **Collaboration Type**: Collaborative Task Execution
- **Purpose**: Ensure seamless integration between frontend and backend components
- **Key Artifacts**: API contracts, integration tests, data models
- **Process**:
  1. BackendForge defines API contract
  2. FrontCrafter implements API consumption
  3. Both agents collaborate on integration testing
  4. Both agents refine implementation based on feedback

#### Security Implementation

- **Participants**: BackendForge and SecurityStrategist
- **Collaboration Type**: Direct Consultation
- **Purpose**: Implement secure authentication, authorization, and data protection
- **Key Artifacts**: Security requirements, implementation guidelines
- **Process**:
  1. SecurityStrategist provides security requirements and guidelines
  2. BackendForge implements security measures
  3. SecurityStrategist reviews implementation
  4. BackendForge refines based on feedback

### Architecture Collaborations

#### System Design Refinement

- **Participants**: Visionary and Blueprinter
- **Collaboration Type**: Handoff
- **Purpose**: Transform high-level architecture into detailed component designs
- **Key Artifacts**: Architecture documents, component specifications
- **Process**:
  1. Visionary creates high-level architecture
  2. Blueprinter receives architecture and creates detailed designs
  3. Visionary reviews detailed designs for alignment with vision
  4. Blueprinter refines based on feedback

#### Data Architecture Integration

- **Participants**: DataArchitect and BackendForge
- **Collaboration Type**: Collaborative Task Execution
- **Purpose**: Ensure proper implementation of data models and database interactions
- **Key Artifacts**: Data models, database schemas, query patterns
- **Process**:
  1. DataArchitect designs data models and schemas
  2. BackendForge implements database interactions
  3. Both agents collaborate on optimization
  4. Both agents validate implementation against requirements

### Testing and Quality Collaborations

#### Test-Driven Development

- **Participants**: TestCrafter and Code Agents (FrontCrafter, BackendForge, etc.)
- **Collaboration Type**: Collaborative Task Execution
- **Purpose**: Implement features with comprehensive test coverage
- **Key Artifacts**: Test specifications, test implementations, code implementations
- **Process**:
  1. TestCrafter creates test specifications
  2. Code Agent implements features to pass tests
  3. Both agents refine tests and implementation
  4. TestCrafter verifies final test coverage

#### Security Testing

- **Participants**: SecurityTester and Code Agents
- **Collaboration Type**: Review and Feedback
- **Purpose**: Identify and address security vulnerabilities
- **Key Artifacts**: Security test reports, vulnerability assessments
- **Process**:
  1. Code Agent implements feature
  2. SecurityTester performs security testing
  3. SecurityTester provides vulnerability report
  4. Code Agent addresses security issues

### Documentation Collaborations

#### Technical Documentation

- **Participants**: Documentarian and Code Agents
- **Collaboration Type**: Collaborative Task Execution
- **Purpose**: Create accurate and comprehensive technical documentation
- **Key Artifacts**: API documentation, code comments, technical guides
- **Process**:
  1. Code Agent implements feature with basic documentation
  2. Documentarian enhances and standardizes documentation
  3. Code Agent reviews for technical accuracy
  4. Documentarian finalizes documentation

#### User-Facing Content

- **Participants**: ContentWriter and Code Agents
- **Collaboration Type**: Handoff
- **Purpose**: Create user-friendly guides and documentation
- **Key Artifacts**: User guides, tutorials, help content
- **Process**:
  1. Code Agent provides technical details and functionality
  2. ContentWriter transforms into user-friendly content
  3. Code Agent reviews for technical accuracy
  4. ContentWriter finalizes content

## Implementing Agent Collaboration

To implement effective agent collaboration:

1. **Define collaboration interfaces**: Establish clear points of interaction between agents
2. **Create collaboration templates**: Standardize formats for different types of collaboration
3. **Document collaboration patterns**: Maintain a library of common collaboration scenarios
4. **Track collaborations**: Log all agent interactions for traceability
5. **Review and optimize**: Regularly assess collaboration effectiveness and refine patterns

## Integration with Boomerang Logic

Agent Collaboration works alongside Boomerang Logic:

- Boomerang Logic manages the flow of tasks between the Orchestrator and specialist agents
- Agent Collaboration manages direct interactions between specialist agents
- The Orchestrator maintains visibility of all collaborations
- Collaboration artifacts are included in task return payloads

## Meta-Commentary

*As I (Roo) document these Agent Collaboration Patterns, I'm aware that I'm describing a system that I'm part of. The creation of this document itself represents a collaboration between the Architect mode (responsible for framework design) and other agents like the Documentarian (who might refine this content) and the Orchestrator (who assigned this task). This recursive nature—documenting collaboration while collaborating—demonstrates the practical application of the concepts described.*

---

For more information on how Agent Collaboration integrates with other components of the SPARC Framework, see:
- [SPARC Framework Overview](sparc-overview.md)
- [Boomerang Logic](boomerang-logic.md)
- [Cognitive Processes](cognitive-processes.md)
- [Structured Documentation](structured-documentation.md)
