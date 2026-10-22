# Explicit Architecture: Software Architecture for Understandable, Evolvable, Verifiable Systems

**Version: V1**

**Languages / 语言 / 言語:** [简体中文](README.zh-CN.md) · [日本語](README.ja.md)

---

### 1. Definition

**Explicit Architecture is a software architecture design method centered on system understandability, traceable behavior, and controlled change.**

It calls for clear, discoverable expression of a system’s core capabilities, module responsibilities, critical control flows, dependencies, shared rules, and testing boundaries. This lets developers and AI understand the system within a limited context, make focused changes, and verify the results reliably through layered tests.

Explicit Architecture does not prescribe one folder layout, layering style, or technology stack. It uses a set of actionable design constraints to keep software clear in structure, sound in responsibility, and controlled in complexity while meeting real functional, operational, security, and reliability requirements and continuing to evolve.

### 2. Core Principles

**1. Capability & Kernel Boundaries — Keep core capabilities and shared mechanisms distinct**

Organize the project around its core capabilities and concepts. When a system has a shared execution kernel or foundational runtime mechanisms, make the responsibilities of each capability and the shared mechanism explicit. Capability modules own their domain rules; the shared kernel owns execution mechanisms and common invariants that must hold across capabilities. Do not centralize code in the kernel solely for reuse, and do not reimplement global rules in the name of local autonomy.

**2. Structural Transparency — Make structure and critical paths visible**

Project structure, module names, application entry points, and architecture documentation should clearly express the system’s composition, module responsibilities, dependency directions, and main runtime paths. The application entry point should show how modules are assembled, while external entry points should delegate work to modules with clear responsibilities. Critical architecture information should not depend on memory, extensive file searches, or invisible framework conventions.

**3. Responsibility Cohesion — Organize around responsibility, reasons for change, and test boundaries**

Keep related rules, state, implementations, and tests together when they share meaning, collaborate closely, or change for the same reason. Introduce a new module or abstraction when responsibilities, reasons for change, dependencies, or testing boundaries are genuinely different and the split lowers overall complexity. Let cohesion, collaboration cost, and change patterns determine module size; do not use line count, directory count, or code reuse rate as the sole measure.

**4. Explicit Control Flow — Make critical control flow traceable**

Make critical decisions, call order, state transitions, side effects, error handling, retries, and recovery traceable in code or a clear execution contract. Events, callbacks, asynchronous jobs, and framework mechanisms are valid choices when their triggers, execution semantics, state effects, and failure handling are explicit. Critical business or system behavior must not depend on undiscoverable implicit control logic.

**5. Explicit Dependencies & Assembly — Make dependencies and assembly explicit**

Keep module dependencies visible and their direction stable, and have modules collaborate through clear interfaces or contracts. The application composition root connects modules and their infrastructure dependencies. Modules should not depend back on the application entry point or unnecessarily on other modules’ internals. Add interfaces and abstractions when there is a real need for replacement, isolation, independent evolution, or a stable contract. Avoid circular dependencies, implicit global dependencies, and unnecessary indirection.

**6. Necessary Complexity — Let real needs and risks drive complexity**

Abstractions, layers, patterns, and infrastructure should serve confirmed functional needs, operating constraints, and risks. Do not omit necessary persistence, state recovery, access control, budget management, version consistency, or failure handling for the sake of surface simplicity. Also avoid overdesign without a real basis. Be able to explain the problem each important structural choice solves, the value it provides, and the effect of removing it.

**7. Local Change & Shared Invariants — Balance local change with shared invariants**

Let independently changing responsibilities evolve within their owning modules. Give rules that must remain consistent across modules one clear authority. Shared rules should be unified because their meaning and invariants match, not because their code looks similar. Stable contracts let modules use shared rules without duplication or semantic drift, while keeping a shared module from becoming a god module that owns all business logic. Locality should reduce unnecessary change propagation while preserving required consistency.

**8. Composable Testability — Make tests focused and composable**

Rules and capabilities should be independently verifiable and composable through clear interfaces. Unit tests verify local rules; use-case tests verify complete operations; protocol and integration tests verify module collaboration; end-to-end tests verify real runtime paths. Give every test layer a clear purpose and make failures easy to locate. For systems that depend on models, distinguish deterministic software behavior tests from model behavior evaluations, and design each strategy for its validation goal, stability, and cost.

**9. Bounded Context — Provide the smallest sufficient context**

Project structure, module documentation, public contracts, important constraints, and tests should help developers and AI quickly understand a local task and its necessary upstream and downstream context. This allows reliable work without requiring an understanding of the whole system. Use cohesive modules, focused dependencies, clear names, and progressive information loading to lower the cost of understanding. Context efficiency means the smallest sufficient information for the task, not the fewest files, the smallest modules, or a large collection of tiny packages.

**10. Layered Feedback & Continuous Verification — Use layered feedback and continuous verification**

Every kind of change should have a clear, appropriate, repeatable verification path. Protect key invariants with automated tests, type checks, static analysis, and architecture checks. Provide fast feedback first, then run more costly integration, real-model, and end-to-end tests according to change risk, impact, and release stage. Continuously remove obsolete contracts, duplicate rules, unused abstractions, and leaking boundaries so the system remains aligned with its principles as it evolves.

### 3. Architecture Decision Criteria

Every important architecture decision should have clear answers to these questions:

- **Capability ownership:** Which module owns this capability or rule? Which rules must be shared and kept consistent?
- **Structural visibility:** Can a developer find it quickly from the project structure and entry point?
- **Behavioral traceability:** Can someone understand how it runs, changes state, and handles failure?
- **Dependency rationale:** Why does it depend on another module? Is the dependency necessary and its direction stable?
- **Complexity rationale:** What real problem does a new abstraction, layer, or infrastructure component solve?
- **Change locality:** Which modules will a change affect? Which effects are necessary, and which can be avoided?
- **Composable testing:** Can it be verified independently and then as part of a larger behavior?
- **Sufficient context:** Can developers or AI complete the task with limited, relevant information?
- **Effective feedback:** Is there a verification path suited to the change’s risk?

If these questions do not have clear answers, the design needs further clarification.

### 4. Overall Design Goal

Explicit Architecture aims to lower the cost of understanding, change propagation, and verification as much as practical while meeting real operating requirements. Code volume, module count, and abstraction depth are design choices rather than measures of success.

Its purpose is to:

- Give necessary complexity a clear owner and a traceable expression.
- Protect cross-module consistency through an explicit source of authority.
- Let independent responsibilities evolve locally and be verified independently.
- Make system structure, behavior, and constraints discoverable to people and AI.
- Keep tests and feedback continuously checking that the architecture still holds.

### 5. Core Declaration

**Make Structure Visible. Make Behavior Explicit. Keep Dependencies Clear. Preserve Shared Invariants. Keep Changes Local. Make Tests Composable.**

### 6. In One Sentence

**Explicit Architecture is a software architecture method that uses clear capability boundaries, visible project structure, traceable control flow, stable dependencies, consistent shared invariants, and composable tests to enable reliable understanding, focused change, and continuous evolution within a limited context.**

---
