# Data Flow

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