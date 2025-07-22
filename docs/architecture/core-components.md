# Core Components

The frontend will be composed of several distinct components, each responsible for specific functionalities.

## Main Game Board (GB)

* **Lobby Component:** Displays game ID, joined players, "waiting" message.
* **Question Display Component:** Renders question text, current question number, background visuals.
* **Timer Component:** Displays countdown for buzzer timeout and answer time.
* **Scoreboard Component:** Dynamically updates and displays player names and scores.
* **Winner Screen Component:** Presents game-over summary, winner, and rankings.
* **Audio Playback Module:** Integrates with voice synthesis service for question audio (initiated via PartyKit).

## Player Mobile Interface (PMI)

* **Join/Lobby Component:** Input field for name, "Join" button, displays lobby status.
* **Buzzer Component:** Large, responsive button for buzzing in, visual feedback for active/locked state.
* **Microphone/Answer Input Component:** Activates microphone, displays "listening" status, visual/haptic feedback on activation/deactivation, explicit submit option, 5-second auto-stop.
* **Real-time Status Indicator:** Small UI elements to show connection status, game phase.

## Admin Dashboard (ADM)

* **Game Control Panel:** Buttons for Start/Pause/Resume, Skip Question, Reset Game, Undo Last Action, Round Navigation.
* **Player Management Table:** List of active players with scores, "Kick" button.
* **Question Editor/Generator:** UI for generating new questions (difficulty/category inputs), editing existing questions (text fields), and saving.
* **Score Adjustment Tool:** Input fields to manually change player scores.
* **Game State Display:** Real-time overview of current question, active player, timers.

## Shared Components/Utilities

* **Real-time Client (PartyKit):** Manages WebSocket connections and message handling.
* **State Management:** Centralized store for game state, player data, and UI state (e.g., Zustand, React Context), synchronized via PartyKit.
* **Utility Functions:** Timer logic, score calculation, data formatting. 