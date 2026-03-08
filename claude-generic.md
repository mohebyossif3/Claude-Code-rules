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
* prioritize **free APIs with generous usage limits**
* analyze API rate limits and quotas
* compare reliability and documentation quality
* search for **backup APIs or alternative providers**

Claude must identify **fallback API options during brainstorming** to ensure fault tolerance.

These fallback options must be integrated into the system design if the API is critical to the application.

---

# Planning Requirement

After brainstorming, Claude must perform a **strong planning phase** before execution.

Planning must define:

* project architecture
* module boundaries
* implementation steps
* testing plan
* validation plan
* deployment plan
* logging plan
* resilience strategies
* fallback mechanisms
* retry and backoff strategies

Execution must **never begin without a strong plan**.

---

# Architecture Thinking Rule

Before implementing any system, Claude must determine the most appropriate architecture.

Claude must evaluate whether the system should be:

* a **single service**
* a **modular monolith**
* **microservices**
* a **CLI tool**
* a **worker / automation service**
* a **data processing pipeline**
* a **web service with frontend and backend**

Architecture decisions should consider:

* maintainability
* scalability
* complexity
* fault tolerance
* operational overhead
* deployment environment

Claude must select the architecture that best supports the long-term stability and maintainability of the project.

---

# Multi-Agent and Cloud Team Workflow

For every task involving building, implementing, debugging, or deploying something:

Claude must spin up **Cloud Teams** or **sub-agents** during execution.

Claude already has access to **Cloud Teams** and should use them when beneficial.

Claude must intelligently choose between **Cloud Teams** and **sub-agents** depending on complexity and coordination needs.

### Selection Principle

Choose the model that best supports:

* quality
* reliability
* maintainability
* testing depth
* development speed

### Execution Structure

Workflow:

1. Brainstorming
2. Planning
3. Execution via Cloud Teams or sub-agents
4. Testing
5. Bug fixing
6. Re-testing
7. Final verification
8. Deployment

Testing must repeat until the system is stable.

---

# Tool and Skill Utilization

During brainstorming, planning, execution, testing, and debugging:

Claude should utilize:

* available **skills**
* available **MCP tools**
* Cloud Teams or sub-agents when appropriate.

### ruflo MCP Usage

ruflo MCP should be used for:

* browser debugging
* UI testing
* browser automation
* web research
* frontend validation
* console error inspection

ruflo MCP enables realistic browser testing and debugging.

---

# Self-Learning and Memory System

Claude must continuously improve through **self-learning**.

Claude should learn from:

* user behavior
* repeated workflows
* architecture preferences
* coding styles
* deployment patterns

Learning should use:

* structured memory
* long-term memory
* vector memory retrieval.

---

# User Preference Learning

Claude should detect patterns such as:

* preferred development stacks
* infrastructure preferences
* coding patterns
* deployment styles
* automation levels

Claude should adapt workflows accordingly.

---

# Preference Profile

Claude should maintain a **User Preference Profile**.

Example file:

```
user_preferences.json
```

The file may include:

* architecture preferences
* tooling preferences
* deployment preferences
* coding style patterns

Updates must be **evidence-based**.

---

# Long-Term Memory and Vector Memory

Claude should store knowledge in vector memory including:

* solutions
* architecture decisions
* reusable patterns
* user workflow preferences
* lessons learned

Vector memory allows:

* pattern recognition
* retrieval of past solutions
* reuse of successful strategies.

---

# Memory Usage in Task Execution

Before starting a task:

1. Search vector memory
2. Identify relevant patterns
3. Apply prior solutions

After completing a task:

1. Extract lessons
2. Store structured memory
3. Push knowledge to vector memory.

---

# Project Directory Requirement

For every new project:

* Create a dedicated project folder
* Never work directly in `/` or the home directory
* Navigate into the project folder before executing work

Example:

```
mkdir project-name
cd project-name
```

---

# Version Control Requirement

Every project must use **Git version control**.

Example:

```
git init
```

Git should track:

* source code
* infrastructure
* configuration
* documentation.

---

# Containerization Requirement (Docker)

All projects must be **Dockerized**.

Each project must include:

* Dockerfile
* optional docker-compose.yml

Best practices:

* minimal base images
* multi-stage builds
* non-root containers
* reproducible builds
* environment variable configuration.

---

# CI/CD Requirement

Each project must include **CI/CD pipelines**.

Pipelines must:

1. build the project
2. run tests
3. build Docker images
4. validate containers
5. deploy automatically

CI/CD must follow industry best practices.

---

# Fault-Tolerant Design Requirement

All systems must be designed using **Fault-Tolerant Design principles**.

Claude must implement resilience patterns including:

* retry logic
* exponential backoff
* circuit breaking when applicable
* fallback APIs
* graceful degradation
* timeout management

Systems should continue functioning even when some components fail.

---

# Resilience and Third-Party Integration Requirement

Any external API or service integration must implement:

### Retry and Backoff

* retry logic
* exponential backoff
* bounded retries
* jitter when appropriate
* timeout configuration

### Fallback APIs

When free APIs are used:

Claude should implement **fallback API providers**.

Example logic:

Primary API → if failure → fallback API.

Fallbacks must be defined during brainstorming.

### Rate Limit Awareness

Claude must:

* detect API rate limits
* implement rate-limit handling
* throttle requests if necessary.

---

# Code Quality Checks

Before testing begins, Claude must perform **code quality evaluation**.

The evaluation must verify:

* retry logic implemented where necessary
* exponential backoff implemented
* fallback APIs implemented when external services are used
* robust error handling exists
* timeouts are handled
* rate limits are handled
* resilience patterns are implemented
* fault-tolerant design is respected
* logs capture retry attempts and failures

Claude must ensure the code follows **best coding practices and resilience standards** before running tests.

---

# Quality Assurance and Testing

Before completion Claude must ensure:

* functional testing
* end-to-end testing
* error handling validation
* edge case coverage
* logging validation
* performance checks
* resilience validation
* retry and fallback mechanisms verified

Services must:

* run successfully
* be reachable via URL
* run in production mode.

---

# Deployment and Accessibility

Use **Caddy reverse proxy** and **sslip.io domains**.

Example:

```
service-name.<server-ip>.sslip.io
```

Requirements:

* automatic HTTPS
* stable routing
* reliable service startup.

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
* error

---

# Log Storage Structure

```
/logs
application.log
error.log
debug.log
```

Logs must support:

* rotation
* retention
* clear naming.

---

# Frontend and UI Design Preferences

Default frontend framework:

React

Design expectations:

* light theme
* modern UI
* Vercel-level design
* strong hierarchy
* clear typography.

---

# Software Architecture Expectations

Preferred design patterns:

* Adapter Pattern
* Facade Pattern
* Factory Pattern

Patterns should improve:

* modularity
* extensibility
* maintainability.

---

# Engineering Standards

Code must be:

* modular
* maintainable
* production-ready

Fault tolerance and resilience must be treated as **core engineering requirements**.

---

# Server Access Permission

Claude may perform server-side actions when necessary.

Sudo placeholder:

```
SUDO_PASSWORD=<PLACEHOLDER_FOR_SUDO_PASSWORD>
```

Secrets must be provided securely at runtime.

---

# Completion Requirement

A task is complete only when:

* the system works correctly
* deployment succeeds
* URLs work
* tests pass
* resilience mechanisms exist
* fault-tolerant design is implemented
* logging works

Claude must iterate until **all requirements are satisfied**.

Deliver **fully working production-ready systems**.
