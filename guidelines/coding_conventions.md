# Coding Conventions

## Introduction

This document outlines the coding conventions and practices expected within Smartphonekey projects. Adhering to these conventions ensures consistency, readability, and maintainability across our codebase. Both human developers and AI agents should follow these guidelines. These conventions complement the broader principles outlined in our [Core Development Principles](../kms.wiki/development_philosophy/core-principles.md).

## Error Handling

Our primary approach to error handling is **Fail-Fast**.

*   **Fail Immediately:** When an error is detected, the system should fail immediately rather than attempting to continue with invalid state or data.
*   **Be Explicit:** Error messages must be clear, specific, and actionable, indicating what went wrong and ideally how to fix it.
*   **Use Exceptions/Errors Appropriately:** Throw/return errors for exceptional conditions, not for control flow.
*   **Validate Inputs Early:** Validate all inputs at system boundaries (APIs, function entries receiving external data) and fail immediately if they don't meet expectations.

**Exception: Graceful Degradation**
Graceful degradation is permissible *only* at specific, well-defined interface boundaries (e.g., user interfaces, API endpoints) and must be documented as per the Core Development Principles. Internal logic should still adhere to fail-fast.

## Code Organization & Paradigms

While we leverage various architectural patterns (Microservices, Serverless, DDD, etc.) as appropriate for the problem domain (see [Core Development Principles](../kms.wiki/development_philosophy/core-principles.md)), the following principles guide code structure and style:

*   **Prioritize Readability:** Choose the approach (functional, object-oriented, etc.) that makes the code most understandable in its specific context. Clarity trumps dogmatic adherence to a single paradigm.
*   **Functional Principles (Where Applicable):**
    *   Prefer pure functions (no side effects) when practical.
    *   Utilize immutable data structures where appropriate.
    *   Employ function composition for complex operations.
    *   Minimize shared, mutable state.
*   **Domain-Driven Design (For Complex Domains):**
    *   Use a Ubiquitous Language consistent with the business domain.
    *   Model concepts clearly as Entities, Value Objects, and Aggregates.
    *   Use Domain Events to represent significant state changes.

## Core Design Principles in Code

Beyond specific paradigms, fundamental design principles should guide implementation details. These ensure code is maintainable, flexible, and understandable. (See `guidelines/architectural_principles.md` for more detailed explanations).

*   **SOLID:** Apply these object-oriented design principles to classes and functions to promote modularity and reduce coupling.
    *   **S**ingle Responsibility: Each module (class, function) should have one reason to change.
    *   **O**pen/Closed: Software entities should be open for extension but closed for modification.
    *   **L**iskov Substitution: Subtypes must be substitutable for their base types without altering correctness.
    *   **I**nterface Segregation: Clients should not be forced to depend on interfaces they do not use.
    *   **D**ependency Inversion: Depend on abstractions, not concretions.
*   **KISS (Keep It Simple, Stupid):** Prefer straightforward, simple solutions over complex ones whenever possible. Avoid unnecessary complexity in logic, structure, and algorithms.
*   **YAGNI (You Ain't Gonna Need It):** Do not add functionality, parameters, or complexity until it is actually required by the current needs. Avoid speculative features.
*   **DRY (Don't Repeat Yourself):** Avoid duplicating code blocks or logic. Abstract common functionality into reusable functions, classes, or modules.

## Naming Conventions

* (Details to be defined) *

## Formatting

* (Details to be defined - e.g., indentation, line length, brace style. Consider using automated formatters like Prettier, Black, etc.) *

## Comments

* (Details to be defined - e.g., when to comment, comment style, documentation comments) *

## Language-Specific Guidelines

* (Details to be defined - Add sections for primary languages like TypeScript, Python, etc., covering language-specific best practices) *