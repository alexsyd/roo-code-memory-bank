# System Patterns *Optional*

This file documents recurring patterns and standards used in the project.
It is optional, but recommended to be updated as the project evolves.
2025-04-01 12:40:37 - Log of updates made.

*

## Coding Patterns

*   Use of YAML for `.clinerules-*` configuration files.
*   Use of JSON for `.roomodes` configuration file.
*   Use of Markdown for Memory Bank files and documentation.
*   Emphasis on clear, descriptive naming for modes and files.

## Architectural Patterns

*   Mode-based architecture: Separating concerns into specialized AI agents (modes).
*   Persistent context via Memory Bank: Using structured markdown files for storing and retrieving project state and knowledge.
*   Rule-driven behavior: Defining mode capabilities, restrictions, and interactions via `.clinerules` files.
*   Workflow Orchestration: Utilizing a dedicated mode (Boomerang) for managing complex, multi-step tasks involving multiple modes.

## Testing Patterns

*   (Not yet defined for this project, as the focus is on building the system itself).