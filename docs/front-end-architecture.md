---
id: fullstack-architecture
title: Frontend Architecture
---

### 1. Overview

This document outlines the proposed frontend architecture for the "QuizGame" application. It defines the structural design, key components, data flow, technology stack, and deployment strategy for the three primary user interfaces: the Main Game Board (TV/Large Display), the Player Mobile Interface, and the Admin Dashboard. The architecture aims to ensure real-time responsiveness, scalability for concurrent players, maintainability, and a robust foundation for future enhancements, adhering to the requirements set forth in the PRD and UI/UX Specification.

---

### 2. Architecture Diagram (Conceptual)

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

---

### 3. Core Components

The frontend will be composed of several distinct components, each responsible for specific functionalities.

#### 3.1. Main Game Board (GB)

* **Lobby Component:** Displays game ID, joined players, "waiting" message.
* **Question Display Component:** Renders question text, current question number, background visuals.
* **Timer Component:** Displays countdown for buzzer timeout and answer time.
* **Scoreboard Component:** Dynamically updates and displays player names and scores.
* **Winner Screen Component:** Presents game-over summary, winner, and rankings.
* **Audio Playback Module:** Integrates with voice synthesis service for question audio (initiated via PartyKit).

#### 3.2. Player Mobile Interface (PMI)

* **Join/Lobby Component:** Input field for name, "Join" button, displays lobby status.
* **Buzzer Component:** Large, responsive button for buzzing in, visual feedback for active/locked state.
* **Microphone/Answer Input Component:** Activates microphone, displays "listening" status, visual/haptic feedback on activation/deactivation, explicit submit option, 5-second auto-stop.
* **Real-time Status Indicator:** Small UI elements to show connection status, game phase.

#### 3.3. Admin Dashboard (ADM)

* **Game Control Panel:** Buttons for Start/Pause/Resume, Skip Question, Reset Game, Undo Last Action, Round Navigation.
* **Player Management Table:** List of active players with scores, "Kick" button.
* **Question Editor/Generator:** UI for generating new questions (difficulty/category inputs), editing existing questions (text fields), and saving.
* **Score Adjustment Tool:** Input fields to manually change player scores.
* **Game State Display:** Real-time overview of current question, active player, timers.

#### 3.4. Shared Components/Utilities

* **Real-time Client (PartyKit):** Manages WebSocket connections and message handling.
* **State Management:** Centralized store for game state, player data, and UI state (e.g., Zustand, React Context), synchronized via PartyKit.
* **Utility Functions:** Timer logic, score calculation, data formatting.

---

### 4. Data Flow

1.  **Player Join:**
    * PMI sends "join game" event with player name to PartyKit Server.
    * PartyKit Server updates game state in PartyKit Storage, broadcasts "player joined" event to GB and ADM.
    * GB and ADM update their player lists.
2.  **Question Display:**
    * ADM sends "next question" command to PartyKit Server.
    * PartyKit Server fetches question from PartyKit Storage/generates via LLM (by calling LLM_Q service), sends to GB.
    * GB displays question, sends text to Voice Synthesis Service (via PartyKit proxy if needed), plays audio.
    * PartyKit Server broadcasts "question active" to PMIs (activating buzzers).
3.  **Buzzer Interaction:**
    * PMI sends "buzzer pressed" event to PartyKit Server.
    * PartyKit Server determines first buzzer, broadcasts "player X buzzed, others locked" to all clients.
    * GB highlights player X, starts 5-second answer timer.
    * PMI of player X activates microphone; other PMIs disable buzzer.
4.  **Player Answering:**
    * Chosen PMI captures audio, sends to Voice Recognition Service.
    * STT transcript sent to PartyKit Server.
    * PartyKit Server sends transcript and question context to LLM Answer Evaluation Service.
    * LLM result (correct/incorrect) sent back to PartyKit Server.
    * PartyKit Server updates game state (score) in PartyKit Storage, broadcasts result to all clients.
    * GB updates score, briefly delays, moves to next question.
5.  **Admin Actions:**
    * ADM sends commands (pause, skip, modify score, generate question) to PartyKit Server.
    * PartyKit Server executes command (e.g., calls LLM_Q, updates PartyKit Storage), updates game state, broadcasts relevant changes to all clients.

---

### 5. Technology Stack Justification

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

---

### 6. Deployment Strategy

* **PartyKit Deployment:** Deploy the PartyKit server-side logic and storage to the PartyKit platform/CDN.
* **Frontend Clients (GB, PMI, ADM):**
    * Serve as static assets (pure React application) deployed to a modern CDN or static hosting provider (e.g., Vercel, Netlify, AWS S3/CloudFront, Google Cloud Storage/CDN).
    * Each client (Game Board, Player Interface, Admin Dashboard) will likely have its own dedicated URL.

---

### 7. Scalability Considerations

* **PartyKit Scalability:** PartyKit is specifically designed for high concurrency and real-time messaging, supporting horizontal scaling for simultaneous players and game instances. Its built-in storage scales with the application.
* **Stateless Frontend Clients:** All frontend clients (GB, PMI, ADM) remain stateless, relying on the PartyKit server for real-time state updates, ensuring they are easily scalable.
* **External AI Service Scalability:** Ensure chosen LLM and voice services can handle anticipated request volumes initiated by PartyKit Endpoints.
* **CDN for Assets:** Utilize Content Delivery Networks for serving frontend assets to minimize latency and improve global accessibility.

---

### 8. Security Considerations

* **Admin Dashboard Access:** As per user's request, no authentication will be implemented for the Admin Dashboard. Access relies on the inherent trust within the social gathering environment.
* **Secure Real-time Communication:** PartyKit inherently uses WebSockets over TLS (WSS) for encrypted communication between clients and the server.
* **API Key Management:** Securely manage API keys for LLM and voice services within PartyKit Endpoints (using environment variables/secrets management provided by PartyKit or the hosting platform) to prevent client-side exposure.
* **Input Validation:** Validate all user inputs (player names, admin commands) on both client and PartyKit server-side to prevent injection attacks or malformed data.
* **Rate Limiting:** Implement rate limiting within PartyKit Endpoints on sensitive operations (e.g., question generation) to prevent abuse of external AI services.
* **Sanitization of LLM Outputs:** Sanitize any LLM-generated content before displaying it on client interfaces to prevent XSS attacks.

---

### 9. Performance Considerations

* **Optimized Real-time Updates:** Minimize the size of real-time messages and optimize the frequency of state updates managed by PartyKit to reduce network traffic.
* **Efficient Component Rendering:** Utilize React's reconciliation and optimize component re-renders to ensure smooth UI performance, especially on the Game Board.
* **Asynchronous API Calls:** Ensure all calls from PartyKit Endpoints to external LLM and voice services are asynchronous to prevent blocking.
* **Asset Optimization:** Optimize image assets, CSS, and JavaScript bundles to ensure fast loading times for all client applications, especially the Player Mobile Interface.
* **Caching:** Implement caching mechanisms within PartyKit for frequently accessed static content (questions) or LLM responses where appropriate to reduce redundant external API calls.

---

### 10. Open Issues (Architecture)

* **AI Service Provider Selection:** Finalize the specific LLM (e.g., Gemini Pro, GPT-4) and voice synthesis/recognition (e.g., Google Cloud, Azure) providers, considering their performance, cost, and API capabilities.
* **Error Handling and Retry Logic:** Comprehensive strategy for handling network errors, API failures from external services, and other exceptions across all components, including retry mechanisms within PartyKit Endpoints.
* **Monitoring and Logging:** Define the monitoring and logging strategy for the entire application (clients and PartyKit Endpoints) to track performance, errors, and user activity.
* **Deployment Environment Specifics (PartyKit details):** Pin down any specific configurations or environment variables needed for optimized PartyKit deployment.