# Architecture Diagram (Conceptual)

*(Conceptual Diagram - Textual Representation)*

```mermaid
graph TD
    subgraph Client Applications
        GB[Main Game Board]
        PMI[Player Mobile Interface]
        ADM[Admin Dashboard]
    end

    subgraph Real-time Communication & Backend Logic (PartyKit)
        PKS[PartyKit Server / WebSocket Server & Endpoints]
        PK_STORAGE[PartyKit Storage]
    end

    subgraph External AI Services
        LLM_Q[LLM Service (Question Gen)]
        LLM_A[LLM Service (Answer Eval)]
        VS[Voice Synthesis Service]
        VR[Voice Recognition Service]
    end

    GB -- WebSocket --> PKS
    PMI -- WebSocket --> PKS
    ADM -- WebSocket --> PKS

    PKS -- Reads/Writes --> PK_STORAGE
    PKS -- API Calls --> LLM_Q
    PKS -- API Calls --> LLM_A
    PKS -- API Calls --> VS
    PKS -- API Calls --> VR
```

**Explanation:**

* **Client Applications:** These are the user-facing interfaces.
    * **Main Game Board (GB):** Display-only client, receives real-time updates.
    * **Player Mobile Interface (PMI):** Interactive client for input (buzzer, voice).
    * **Admin Dashboard (ADM):** Control client for game management.
* **Real-time Communication & Backend Logic (PartyKit):** Acts as the central hub for all real-time communication. PartyKit's server-side logic (Endpoints) handles game logic, orchestrates interactions, and uses PartyKit's built-in Storage for persistent data.
* **External AI Services:** Represent various third-party API endpoints for specialized AI functionalities (LLMs, Voice Services). These are consumed by PartyKit Endpoints. 