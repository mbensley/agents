---
name: teach_me
description: Codebase comprehension and learning skill. It provides structured checklists, exploration instructions, and output formats for six distinct modes: Architecture, Convention, Feature Trace, Syntax, Testing, and History.
version: 1.0.0
---

# Teach Me Skill

This skill governs codebase comprehension and user teaching. When a user asks you to explain, walk through, or "teach" them about the repository, or when they invoke the `teach_me` skill, you must adopt one or more of the following six specialized exploration modes.

---

## 💻 Exploration Modes

### 1. Architecture Mode
*Target: System structure and component relationships*

*   **Objectives:**
    *   Understand high-level repository structure and boundaries.
    *   Map relationships between components (e.g., frontend-backend contracts, client-database relations, module dependencies).
    *   Identify key entry points, configuration registries, and system setup scripts.
*   **Agent Checklist:**
    1.  List the top-level directories to establish structural context.
    2.  Find application bootstrap/initialization files (e.g., `main.go`, `index.ts`, `app.py`, `Cargo.toml`).
    3.  Analyze imports/dependencies using `grep_search` to map how components interact.
    4.  Draw a dependency or structural diagram representing module relations.
*   **Output Format:**
    *   **Overview:** High-level summary of the architectural pattern (e.g., Layered, Hexagonal, Clean Architecture, Microservices).
    *   **Component Structure:** Table of core modules/packages, their paths, and their primary responsibilities.
    *   **System Relationships:** A Mermaid.js flowchart mapping component dependencies.
    *   **Entry Points:** Markdown links to critical setup/bootstrap files.

---

### 2. Convention Mode
*Target: Coding standards, naming patterns, and established practices*

*   **Objectives:**
    *   Learn the specific coding styles, patterns, and conventions unique to this codebase.
    *   Locate linters, formatters, and static analysis settings.
    *   Understand common paradigms (e.g., error handling, logging, async flows, naming rules).
*   **Agent Checklist:**
    1.  Search for config files (`.eslintrc`, `tsconfig.json`, `Cargo.toml`, `pyproject.toml`, `.prettierrc`, `ruff.toml`).
    2.  Scan code files to observe casing conventions (e.g., camelCase vs snake_case) for variables, functions, and files.
    3.  Inspect how standard procedures are structured (e.g., standard API responses, custom error classes, logging formats).
*   **Output Format:**
    *   **Tooling & Linters:** Which linting, formatting, and validation tools are configured.
    *   **Naming Standards:** Standard naming rules for files, directories, types, and variables.
    *   **Established Paradigms:** Patterns for error propagation, asynchronous tasks, state management, and configuration.
    *   **Examples:** Code snippets comparing non-idiomatic vs. idiomatic code for this specific codebase.

---

### 3. Feature Trace Mode
*Target: End-to-end data flow and feature implementation paths*

*   **Objectives:**
    *   Trace how a specific request or user action propagates through the entire stack.
    *   Map data transformations, validation gates, and storage updates.
    *   Understand critical path branches, logic gates, and side effects.
*   **Agent Checklist:**
    1.  Locate the initial entry point of the feature (e.g., HTTP route, CLI flag, event listener).
    2.  Follow function calls from the handler/controller down through business logic, database queries, and external API requests.
    3.  Identify any asynchronously queued tasks, webhook triggers, or pub/sub events.
*   **Output Format:**
    *   **Trace Map:** Step-by-step list of function calls and files traversed in chronological order.
    *   **Visual Sequence:** A Mermaid.js sequence diagram tracing execution from client/trigger to database/external dependency and back.
    *   **Payload Evolution:** How the request data structure changes (e.g., Route DTO -> Domain Model -> DB Schema).
    *   **Decision Matrix:** Key conditionals, authorization checks, and error fallbacks.

---

### 4. Syntax Mode
*Target: Language-specific patterns and idiom usage*

*   **Objectives:**
    *   Analyze advanced language features and syntactic constructs used.
    *   Deconstruct complex or potentially confusing constructs (e.g., Rust traits and lifespans, Go concurrency primitives, Python decorators, TypeScript utility types).
    *   Assess type-safety patterns and idiomatic usages of the language.
*   **Agent Checklist:**
    1.  Identify compiler directives, macros, or metaprogramming constructs in use.
    2.  Examine type declarations, interface shapes, generics/templates, and custom operators.
    3.  Search for unique syntax patterns that optimize performance or safety.
*   **Output Format:**
    *   **Syntactic Landscape:** Primary language version, paradigms (OOP, functional, reactive), and compiler constraints.
    *   **Idioms & Quirks:** Code constructs that might surprise an outside developer.
    *   **Complexity Breakdown:** High-complexity lines or macros explained step-by-step.
    *   **Type Safety & Generics:** Design of custom traits, interfaces, utility types, and generic patterns.

---

### 5. Testing Mode
*Target: Test coverage, testing patterns, and quality assurance approaches*

*   **Objectives:**
    *   Understand the testing hierarchy (unit, integration, integration integration, E2E).
    *   Identify testing libraries, mocks, stubs, and runners.
    *   Locate where tests live (colocated with code vs. separate test directory).
*   **Agent Checklist:**
    1.  Search for test files (e.g., `*_test.go`, `*.spec.ts`, `test_*.py`, `tests/` directory).
    2.  Identify test harness configurations and script aliases in `package.json`, `Cargo.toml`, `Makefile`, etc.
    3.  Analyze test structures to find standard patterns for mocking databases or external HTTP requests.
*   **Output Format:**
    *   **Testing Stack:** Frameworks, assertion libraries, and mock utilities used.
    *   **Test Strategy:** How unit, integration, and E2E boundaries are defined.
    *   **Test Patterns:** Mocking strategy, fixtures, database transaction rollbacks, or test containers.
    *   **Running Tests:** Practical command-line instructions for running, filtering, and debugging tests.

---

### 6. History Mode
*Target: Evolution of code components and decision rationale*

*   **Objectives:**
    *   Retrieve context for *why* code was written in a certain way, rather than just *how*.
    *   Identify deprecated systems, legacy paths, and current migration targets.
    *   Map ownership and trace major structural refactors.
*   **Agent Checklist:**
    1.  Use `git log` and `git blame` on key system files to locate major commits.
    2.  Find architecture decision records (ADRs) or design documents, if available.
    3.  Inspect commit message patterns or pull request references in comments to extract design constraints.
*   **Output Format:**
    *   **Structural Timeline:** Notable architectural migrations or major version updates.
    *   **Design Rationale:** Chronological context behind non-obvious design choices.
    *   **Legacy & Debt:** Modules slated for refactoring, deprecated functions, and tech debt annotations.
    *   **Authors & Mentors:** Key authors who built core sections (helps route human-level questions).

---

## 🛠️ Execution Protocol

1.  **Acknowledge and Select Mode:** When a request is received, explicitly announce which comprehension objective and mode(s) you are activating.
2.  **Conduct Systematic Investigation:**
    *   Start wide (list files, locate directories).
    *   Narrow down (grep specific patterns, read key files using `view_file`).
    *   Verify details before presenting (confirm file paths and line ranges).
3.  **Synthesize into Teachings:**
    *   Avoid plain text dumps. Use structured headings, tables, and Mermaid flowcharts.
    *   Always use markdown file links (e.g. `[main.go](file:///path/to/main.go#L12-L34)`) pointing to actual file locations and line ranges.
    *   Include actionable code snippets alongside explanations.
