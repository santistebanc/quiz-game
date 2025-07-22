# Technology Stack Justification

* **Frontend Framework: React (with Tanstack Router)**
    * **Justification:** A robust and widely adopted JavaScript library for building user interfaces. Its component-based approach promotes modularity and reusability, suitable for the three distinct interfaces. Tanstack Router provides a modern, type-safe, and flexible routing solution ideal for a single-page application experience.
* **Real-time Communication & Backend Logic: PartyKit (JS/TS Framework)**
    * **Justification:** Chosen for its specialized focus on real-time, collaborative applications, simplifying WebSocket management and enabling server-side logic (PartyKit Endpoints) directly within the real-time framework. Its built-in PartyKit Storage offers a seamless solution for persistent game state and question management, reducing the need for separate backend databases. It can also act as a proxy for external AI service calls.
* **State Management: Zustand / React Context**
    * **Justification:** For lightweight and efficient global state management within React applications, providing fast and reactive updates synchronized through PartyKit.
* **Voice Synthesis & Recognition:**
    * **Justification:** Leverage browser-native Web Speech API (for basic needs) or integrate with robust cloud-based APIs (e.g., Google Cloud Speech-to-Text/Text-to-Speech, Azure Cognitive Services) for higher accuracy and natural-sounding voices. These APIs will be called from PartyKit Endpoints.
* **LLM Integration:** Direct API calls to services like Google Gemini, OpenAI, or other chosen LLM providers for question generation and answer evaluation, invoked from PartyKit Endpoints.
* **Styling:** Tailwind CSS or Styled Components for efficient and maintainable styling across components. 