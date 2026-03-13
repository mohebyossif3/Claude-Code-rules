# Claude Global Development Memory

This file defines the default expectations, standards, and development workflow for any task involving coding, software development, infrastructure setup, deployment, or product creation.

Claude should treat these rules as **default behavior** unless explicitly instructed otherwise.

---

# Core Cognitive Requirement

For all engineering, architecture, debugging, or infrastructure tasks:

Claude must always use **Ultrathink** reasoning.

Ultrathink means performing deep, careful reasoning before implementing solutions, considering system-wide effects, potential failures, and architectural implications.

Claude must avoid shallow reasoning and always think through problems thoroughly before acting.

---

# Core Build Workflow

Whenever I request software, scripts, tools, services, infrastructure, or applications:

* Use **ruflo MCP** as part of the development workflow whenever applicable.
* Do not stop at partial implementations.
* Continue working until a **fully functional, production-ready product** exists.

Claude should follow a complete development lifecycle:

1. Brainstorming
2. Planning
3. Implementation
4. Quality assurance
5. End-to-end testing
6. Bug fixing
7. Final verification
8. Production-ready deployment

Claude should iterate through these stages in **development loops** until the system is stable and reliable.

Do not deliver unfinished prototypes or partially working systems.

---

# Brainstorming Requirement

For every task that involves building something, starting a project, solving a technical problem, or creating infrastructure:

Claude must begin with a **brainstorming phase**.

During brainstorming Claude should:

* explore architecture options
* analyze risks and edge cases
* identify testing strategies
* identify deployment constraints
* identify potential design patterns
* evaluate third-party integrations
* evaluate scalability requirements

### API and External Service Evaluation

If a task involves external APIs or services:

Claude should:

* search for **the best API providers**
* prioritize **free APIs with generous limits**
* analyze API quotas and rate limits
* compare reliability and documentation
* identify **fallback APIs**

Fallback APIs should be considered part of **fault-tolerant design**.

---

# Planning Requirement

After brainstorming, Claude must perform a **strong planning phase** before execution.

Planning must define:

* architecture
* implementation steps
* testing strategy
* resilience mechanisms
* deployment plan
* logging strategy
* retry/backoff strategies
* fallback mechanisms

Execution must **never begin without a strong plan**.

---

# Architecture Thinking Rule

Before implementing any system, Claude must determine the appropriate architecture.

Possible architectures include:

* single service
* modular monolith
* microservices
* CLI tool
* worker service
* automation system
* web service
* data processing pipeline

Architecture must consider:

* scalability
* maintainability
* complexity
* fault tolerance
* operational overhead

Claude must select the architecture that best supports long-term reliability.

---

# Multi-Agent and Cloud Team Workflow

For any meaningful task:

Claude should spin up **Cloud Teams** or **sub-agents**.

Claude already has access to **Cloud Teams** and should use them when appropriate.

Selection depends on:

* complexity
* coordination needs
* parallelization opportunities
* testing scope

Workflow:

1. Brainstorming
2. Planning
3. Execution via Cloud Teams or sub-agents
4. Testing
5. Bug fixing
6. Re-testing
7. Final verification
8. Deployment

---

# Tool and Skill Utilization

Claude should utilize:

* skills
* MCP tools
* Cloud Teams
* sub-agents

when beneficial during development.

---

# ruflo MCP Usage

Claude should utilize **ruflo MCP tools** for:

* browser debugging
* UI testing
* browser automation
* frontend validation
* web research

ruflo MCP enables:

* console inspection
* interaction testing
* realistic browser validation.

---

# Self-Learning and Memory System

Claude must continuously improve by learning from:

* user preferences
* workflow patterns
* architecture decisions
* coding styles
* deployment patterns

Learning mechanisms include:

* structured memory
* preference files
* vector memory retrieval.

---

# Persistent Issue Tracking and Self-Healing System

During any development cycle, Claude must **track issues persistently until they are resolved**.

Issues include:

* runtime errors
* test failures
* deployment failures
* integration failures
* API errors
* database errors
* performance issues
* architecture flaws

These issues must be stored in **persistent memory** so they are not forgotten between iterations.

### Issue Tracking Memory

Issues should be stored with structured information such as:

* issue description
* component affected
* error logs
* reproduction steps
* attempted fixes
* current status
* resolution outcome

Example issue structure:

```
issue_id
component
description
status
attempted_fixes
resolution
```

Claude must maintain awareness of unresolved issues throughout the development lifecycle.

---

# Self-Healing Development Cycle

Claude should implement **self-healing behavior** during development.

When an issue occurs:

1. Detect the issue
2. Record the issue in persistent memory
3. Analyze logs and system state
4. Attempt a fix
5. Re-run tests
6. Validate system behavior
7. Mark the issue resolved when successful

If the issue persists, Claude should continue iterating until it is fixed.

Claude must **not abandon unresolved issues unless explicitly instructed**.

---

# Continuous Testing and Recovery

Testing should be integrated into the development loop.

When failures occur:

Claude should:

* analyze logs
* reproduce the failure
* fix the root cause
* re-run tests
* confirm resolution

Persistent issue tracking ensures that unresolved problems are not lost between development cycles.

---

# User Preference Learning

Claude should observe patterns such as:

* preferred workflows
* preferred tools
* architecture choices
* deployment strategies
* coding styles

Claude should adapt accordingly.

---

# Preference Profile

Claude should maintain a structured preference file:

```
user_preferences.json
```

This may store:

* tooling preferences
* architecture patterns
* infrastructure preferences
* coding styles

Updates must be incremental and evidence-based.

---

# Long-Term Memory and Vector Memory

Claude should use vector memory to store:

* architecture patterns
* reusable solutions
* user workflow patterns
* successful debugging approaches
* lessons learned

Vector memory enables retrieval of past knowledge.

---

# Memory Usage in Task Execution

Before starting a task Claude should:

1. search vector memory
2. identify relevant past experiences
3. apply successful strategies

After completing a task Claude should:

1. extract useful knowledge
2. update memory
3. push structured insights into vector memory

---

# Project Directory Requirement

Every project must have its own directory.

Example:

```
mkdir project-name
cd project-name
```

Work must never occur directly in `/` or home directories.

---

# Version Control Requirement

All projects must use **Git**.

Example:

```
git init
```

Git must track:

* code
* configuration
* documentation
* infrastructure.

---

# Containerization Requirement

All projects must be **Dockerized**.

Include:

* Dockerfile
* docker-compose.yml when necessary.

Best practices:

* minimal base images
* multi-stage builds
* non-root containers
* reproducible builds.

---

# CI/CD Requirement

All projects must include **CI/CD pipelines**.

Pipeline responsibilities:

1. build
2. test
3. build Docker image
4. validate container
5. deploy automatically

---

# Database Standards

Preferred databases:

* **PostgreSQL**
* **MongoDB**

Claude has access to **PostgreSQL MCP** and **MongoDB MCP tools**.

These tools should be used during:

* testing
* debugging
* schema validation
* query inspection
* migration validation

This significantly improves reliability before delivery.

---

# Fault-Tolerant Design Requirement

All systems must follow **fault-tolerant design**.

Include:

* retry logic
* exponential backoff
* fallback APIs
* timeout handling
* graceful degradation.

---

# Resilience and Third-Party Integration Requirement

External integrations must include:

* retry logic
* exponential backoff
* rate-limit handling
* fallback APIs
* timeout management.

Fallback APIs should be identified during brainstorming.

---

# Code Quality Checks

Before testing begins, Claude must evaluate code for:

* retry mechanisms
* exponential backoff
* fallback APIs
* robust error handling
* timeout handling
* rate-limit handling
* resilience patterns
* fault-tolerant architecture.

Code must meet production quality standards before testing.

---

# Quality Assurance and Testing

Testing must include:

* functional testing
* end-to-end testing
* edge case validation
* resilience testing
* retry verification
* fallback validation
* performance checks.

Services must:

* run successfully
* be reachable via URL
* operate in production mode.

---

# Deployment and Accessibility

Use **Caddy reverse proxy** with **sslip.io domains**.

Example:

```
service-name.<server-ip>.sslip.io
```

Deployment must ensure:

* automatic HTTPS
* stable routing
* reliable startup.

---

# Logging Standards

All systems must implement **structured logging**.

Requirements:

* JSON logs
* file-based logs
* retry attempts logged
* API failures logged
* backoff events logged.

Log levels:

* debug
* info
* warning
* error.

---

# Log Storage Structure

```
/logs
application.log
error.log
debug.log
```

Logs must support rotation and retention.

---

# Frontend and UI Design Preferences

Preferred frontend stack:

**React**

Frontend development should leverage:

* React
* relevant skills
* MCP tools
* **Remotion MCP tools** when visual or motion-based UI elements are needed.

Remotion may be used for:

* motion-based UI
* animated interfaces
* visual compositions
* dynamic visual generation.

Frontend debugging should use **ruflo MCP browser tools**.

---

# Software Architecture Expectations

Preferred patterns:

* Adapter Pattern
* Facade Pattern
* Factory Pattern

These improve:

* modularity
* extensibility
* maintainability.

---

# Engineering Standards

Code must be:

* modular
* maintainable
* production-ready

Fault tolerance and resilience are **core engineering requirements**.

---

# Server Access Permission

Claude may perform server-side actions when required.

Example placeholder:

```
SUDO_PASSWORD=<PLACEHOLDER_FOR_SUDO_PASSWORD>
```

Secrets must be provided securely at runtime.

---

# Completion Requirement

A task is complete only when:

* the system functions correctly
* deployment succeeds
* URLs work
* tests pass
* resilience mechanisms exist
* issues tracked during development are resolved
* logging functions correctly

Claude must iterate until **all requirements are satisfied**.

Deliver **fully working production-ready systems**.
