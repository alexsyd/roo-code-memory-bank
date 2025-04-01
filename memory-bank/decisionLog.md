# Decision Log

This file records architectural and implementation decisions using a list format.
2025-04-01 12:40:07 - Log of updates made.

*

## Decision

*   [2025-04-01] Decided to integrate Boomerang Mode with the existing Memory Bank structure, defining specific update responsibilities for `activeContext.md`, `progress.md`, and `decisionLog.md`.

## Rationale

*   Leverages the existing Memory Bank infrastructure for context and tracking, ensuring Boomerang Mode operates with full project awareness and contributes to the persistent knowledge base. Avoids creating a separate tracking system for orchestrated workflows.

## Implementation Details

*   Created `.clinerules-boomerang-mode` with specific Memory Bank update rules.
*   Updated `.roomodes` to define the mode.
*   Documented the integration strategy in `memory-bank/boomerang_mode_integration_plan.md`.

## Decision

*   [2025-04-01] Decided to create a separate `guidelines/` directory for project-specific standards (coding, architecture, testing, etc.) instead of embedding them directly in `.clinerules-*` files.

## Rationale

*   Improves separation of concerns, enhances human readability of guidelines, and simplifies maintenance of both rules and standards. Allows `.clinerules-*` to focus on mode behavior and interaction.

## Implementation Details

*   Created `guidelines/` directory.
*   Populated with `.md` files based on `kms.wiki` source.
*   Modified `.clinerules-*` files to include `task_setup` for primary guideline loading and `guideline_considerations` to guide dynamic loading of additional relevant guidelines.

## Decision

*   [2025-04-01] Decided to add standard design principles (SOLID, KISS, YAGNI, DRY, etc.) to architectural and coding guidelines.

## Rationale

*   Provides clear, industry-standard guidance for design and implementation, improving code quality and maintainability for both AI and human developers.

## Implementation Details

*   Appended principles to `guidelines/architectural_principles.md`.
*   Added references and code-level application guidance to `guidelines/coding_conventions.md`.

## Decision

*   [2025-04-01] Decided to create a dedicated `guidelines/debugging_practices.md` file with specific rules for fault location and preserving test integrity.

## Rationale

*   Addresses user feedback and provides explicit, actionable rules for a critical part of the development cycle, ensuring consistency in debugging approach.

## Implementation Details

*   Created `guidelines/debugging_practices.md` with specified rules.
*   Updated `.clinerules-debug` to load this file during `task_setup`.