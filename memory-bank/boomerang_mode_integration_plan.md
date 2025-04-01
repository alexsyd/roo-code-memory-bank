# Boomerang Mode Integration with Memory Bank

## Integration Strategy

Boomerang Mode, as a workflow orchestrator, will be deeply integrated with the Memory Bank system to leverage its persistent project context and enhance its workflow management capabilities.

**1. Memory Bank Initialization and Access:**

*   Boomerang Mode will follow the standard Memory Bank initialization process, checking for and loading the Memory Bank upon activation.
*   It will have read access to all Memory Bank files (`productContext.md`, `activeContext.md`, `progress.md`, `decisionLog.md`, `systemPatterns.md`) to gain a comprehensive understanding of the project context, current status, and past decisions, which is essential for effective task delegation.

**2. Leveraging `activeContext.md` for Workflow Management:**

*   Boomerang Mode will utilize `activeContext.md` to track the current complex task being orchestrated. The "Current Focus" section will be updated to reflect the high-level workflow in progress.
*   `activeContext.md` will also be used to maintain a list of active subtasks, including their assigned modes and current status, providing a centralized monitoring point for the overall workflow.

**3. Updating `progress.md` for Task Tracking:**

*   Boomerang Mode will actively manage `progress.md` to track the advancement of the complex workflow and its constituent subtasks.
*   Upon delegating a subtask via `new_task`, Boomerang Mode will add a new entry to the "Current Tasks" section of `progress.md`, detailing the subtask, the mode it is delegated to, and the expected outcome.
*   When a subtask is completed (signaled by `attempt_completion` from the delegated mode), Boomerang Mode will:
    *   Update the corresponding entry in `progress.md`, moving it from "Current Tasks" to "Completed Tasks". This update will include a timestamp and a summary of the subtask's result, extracted from the `attempt_completion` result.
    *   Based on the completed subtask and the overall workflow objectives, Boomerang Mode will determine and append "Next Steps" to `progress.md`, ensuring continuous workflow progression.

**4. Utilizing `decisionLog.md` for Workflow Decisions:**

*   Strategic decisions made by Boomerang Mode regarding workflow orchestration (e.g., adjustments to task delegation strategies, workflow modifications based on subtask outcomes) will be meticulously logged in `decisionLog.md`.
*   This practice ensures that the rationale behind workflow management decisions is recorded, providing a valuable audit trail and historical context for future reviews.

**5. Limited Direct Updates to `productContext.md` and `systemPatterns.md`:**

*   Generally, Boomerang Mode, in its role as an orchestrator, will not directly modify `productContext.md` or `systemPatterns.md`. These files are typically updated by Architect Mode or Code Mode.
*   However, it is acknowledged that Boomerang Mode's workflow orchestration may indirectly necessitate updates to these files. Should the workflow outcomes suggest a need to adjust the overall project direction or system patterns, Boomerang Mode will initiate a handoff to Architect Mode, ensuring these critical project files remain consistent and up-to-date.

**6. Mode Collaboration and Handoffs:**

*   Boomerang Mode's primary collaboration is with all other modes, achieved through the delegation of tasks.
*   The trigger for engaging Boomerang Mode is the identification of a complex task requiring orchestration. This could originate from the user's initial request or be initiated by another mode, such as Architect Mode when a design necessitates a complex implementation workflow.
*   Handoffs from Boomerang Mode are less direct. Upon completion of a complex workflow, Boomerang Mode will use `attempt_completion` to signal overall task completion to the user. It may also trigger handoffs to other modes if the workflow reveals further needs, such as to Debug Mode for issue resolution or back to Architect Mode for design reviews based on implementation insights.

**7. `.clinerules-boomerang-mode` Configuration:**

*   A dedicated `.clinerules-boomerang-mode` file will be created to define the specific rules and behaviors of Boomerang Mode. This configuration file will include:
    *   Definition of its identity and description as a workflow orchestrator.
    *   Memory Bank strategy, encompassing initialization and access protocols.
    *   Specific instructions for updating `activeContext.md`, `progress.md`, and `decisionLog.md` to maintain workflow context and progress.
    *   Mode collaboration patterns and clearly defined handoff triggers to ensure seamless interaction with other modes.
    *   Tool access permissions, primarily focusing on `new_task` and `attempt_completion` for task delegation and completion signaling, along with read access to Memory Bank files for context retrieval.

## Benefits of this Integration:

*   **Centralized Workflow Management:** Boomerang Mode acts as the central hub for complex task management, with the Memory Bank serving as the shared contextual repository.
*   **Improved Task Tracking:** `progress.md` becomes a dynamically updated, comprehensive log of workflow progression, actively managed by Boomerang Mode.
*   **Contextual Task Delegation:** Boomerang Mode ensures that subtasks are delegated to other modes with a deep understanding of the overarching project context derived from the Memory Bank.
*   **Enhanced Collaboration:** The Memory Bank facilitates transparent communication and streamlined coordination between Boomerang Mode and all other modes involved in the orchestrated workflow.
*   **Persistent Workflow History:** `decisionLog.md` meticulously records strategic decisions made by Boomerang Mode in orchestrating workflows, creating a valuable historical record of the project's development process and strategic evolution.

This integration strategy empowers Boomerang Mode to orchestrate complex tasks effectively, leveraging the Roo Code Memory Bank to maintain context, track progress, and log decisions, thereby significantly enhancing the efficiency and coherence of AI-assisted development workflows.