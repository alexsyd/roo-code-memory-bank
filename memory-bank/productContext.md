# Product Context

This file provides a high-level overview of the project and the expected product that will be created. Initially it is based upon projectBrief.md (if provided) and all other available project-related information in the working directory. This file is intended to be updated as the project evolves, and should be used to inform all other modes of the project's goals and context.
2025-04-01 12:30:10 - Log of updates made will be appended as footnotes to the end of this file.

*

## Project Goal

*   Define and implement a robust Memory Bank system and task coordination framework (including Boomerang Mode) for Roo Code, enabling persistent context and efficient workflow management in AI-assisted development.

## Key Features

*   Persistent Memory Bank storage (`memory-bank/` directory with core markdown files: `activeContext.md`, `productContext.md`, `progress.md`, `decisionLog.md`, `systemPatterns.md`).
*   Specialized modes (Architect, Code, Ask, Debug, Test, Boomerang) with defined roles and rules (`.clinerules-*`, `.roomodes`).
*   Intelligent mode switching based on intent and context.
*   Real-time Memory Bank updates and synchronization (conceptual).
*   Workflow orchestration via Boomerang Mode using the `new_task` tool.
*   Clear documentation (`README.md`, `developer-primer.md`) explaining the system.

## Overall Architecture

*   A system designed for integration with a VS Code extension (Roo Code), utilizing a set of project-level configuration files (`.clinerules-*`, `.roomodes`) and a project-specific `memory-bank/` directory. This enables different operational modes, each with specific capabilities and access rules, all sharing persistent context managed through the Memory Bank files.