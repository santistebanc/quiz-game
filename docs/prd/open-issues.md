# Open Issues

This section outlines any outstanding questions, unresolved decisions, or potential challenges that need to be addressed as the "QuizGame" project progresses. These are areas that require further investigation, discussion, or a definitive decision.

* **OI-001: Specific LLM Integration Details:** The exact LLM provider and specific APIs for question generation and answer evaluation need to be finalized. This includes details on prompt engineering strategies for optimal performance and and cost.
* **OI-002: Voice Recognition Library Selection & Tuning:** The precise voice recognition library or service (e.g., Web Speech API, a third-party service) for player answers needs to be selected, and its accuracy tuned for various accents and potential background noise.
* **OI-003: Voice Synthesis Tool Selection:** The specific online tool for voice synthesis (text-to-speech) needs to be chosen, considering voice quality, naturalness, and API accessibility.
* **OI-004: Scoring Algorithm Details:** While points will be awarded/deducted, the exact scoring algorithm (e.g., points per correct answer, deduction for wrong/timeout, bonus points) needs to be defined.
* **OI-005: Detailed UI/UX Flows:** While functional requirements outline what each interface does, the detailed wireframes, mockups, and user flow diagrams for the Game Board, Player Mobile Interface, and Admin Dashboard still need to be designed.
* **OI-006: Concurrent Player Limit for Performance:** The specific target number for "up to [Number] concurrent players" in the Non-Functional Requirements needs to be defined, which will impact architectural decisions and performance testing.
* **OI-007: Error Handling and User Guidance:** Detailed plans for how the system will handle and provide feedback for various errors (e.g., network disconnects, invalid buzzer presses, LLM errors) need to be established. 