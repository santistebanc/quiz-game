# Functional Requirements

This section details the specific functionalities that "QuizGame" must possess to meet its objectives and provide the intended user experience. These requirements are categorized by the main components of the game.

## Game Board (Main Display)

* **FR-GB-001: Lobby Display:** The game board SHALL display a lobby screen initially, showing the project name "QuizGame" and waiting for players to join.
* **FR-GB-002: Player List Display:** The game board SHALL dynamically update and display the names of all players who have joined the game and are ready to play.
* **FR-GB-003: Question Display:** When a game starts, the game board SHALL display quiz questions one by one.
* **FR-GB-004: Question Audio Playback:** When a question is displayed on the game board, the game board SHALL play an audio rendition of the quiz question using a voice synthesizer. This audio rendition SHALL be immediately interrupted as soon as any player hits the buzzer.
* **FR-GB-005: Answer Timer Display:** The game board SHALL display a 5-second countdown timer when a chosen player is about to answer a question.
* **FR-GB-006: Game Progress Info:** The game board SHALL display overall information on the progress of the game (e.g., current question number out of total questions).
* **FR-GB-007: Score Display:** The game board SHALL display player scores, updating in real-time.
* **FR-GB-008: Winner Announcement:** At the end of the game, the game board SHALL display a winner screen announcing the winner and the second, third, and subsequent places with their respective scores and stats.
* **FR-GB-009: Brief Delay After Answer:** The game board SHALL introduce a brief delay after a player's answer (correct, incorrect, or time-out) before moving to the next question.

## Player Mobile Interface (PMI)

* **FR-PMI-001: Game Joining:** Players SHALL be able to join a specific instance of the game by visiting a unique website URL (with specific query parameters for the game instance) on their phones.
* **FR-PMI-002: Name Input:** In the lobby, players SHALL be presented with a text box to enter their desired display name.
* **FR-PMI-003: Join Button:** Players SHALL have a "Join" button to send their name and signal their intent to join the game.
* **FR-PMI-004: Buzzer Button:** When a question is displayed on the game board, players' phones SHALL display a buzzer button.
* **FR-PMI-005: Buzzer Lockout:** The buzzer button SHALL become disabled for all other players once one player presses it first.
* **FR-PMI-006: Microphone Activation:** When a player is chosen to answer, their phone SHALL activate its microphone to listen for their answer.
* **FR-PMI-007: Answer Submission (Voice):** The chosen player's voice input SHALL be captured. The player SHALL be able to explicitly submit their answer by pressing the microphone icon, which stops listening and sends the recorded audio for evaluation. Otherwise, the microphone SHALL automatically stop listening after 5 seconds, and all recorded audio from that duration SHALL be sent for LLM evaluation.
* **FR-PMI-008: Real-time Feedback:** Players SHALL receive real-time feedback on their buzzer status (e.g., active, locked out).

## Admin Dashboard (ADM)

* **FR-ADM-001: Question List View:** The admin dashboard SHALL display a list of all questions available for the game.
* **FR-ADM-002: Question Generation:** The admin SHALL be able to click a button to generate new quiz questions using an LLM.
* **FR-ADM-003: Question Generation Options:** The admin SHALL be able to specify difficulty and an optional category for question generation, or select random generation.
* **FR-ADM-004: Question Editing:** The admin SHALL be able to edit generated or existing questions.
* **FR-ADM-005: Game Pause/Resume:** The admin SHALL have controls to pause and resume the game.
* **FR-ADM-006: Question Skip:** The admin SHALL have a control to skip the current question.
* **FR-ADM-007: Player Management (Kick):** The admin SHALL be able to kick out a player from the game.
* **FR-ADM-008: Score Modification:** The admin SHALL be able to manually modify players' scores.
* **FR-ADM-009: Game Reset:** The admin SHALL be able to reset the game to its initial state (lobby).
* **FR-ADM-010: Round Navigation:** The admin SHALL have controls to move to the next or last round/question.
* **FR-ADM-011: Undo Last Action:** The admin SHALL have a control to undo the last game action.
* **FR-ADM-012: Adjustable Question Count:** The admin SHALL be able to adjust the total number of questions for a game in settings.

## Core Game Logic

* **FR-CGL-001: Game State Management:** The system SHALL manage the overall game state (lobby, question active, answering phase, round transition, game over).
* **FR-CGL-002: Buzzer Arbitration:** The system SHALL accurately determine the first player to press the buzzer and lock out others.
* **FR-CGL-003: Timer Management:** The system SHALL manage the 5-second answer timer for the chosen player.
* **FR-CGL-004: Answer Evaluation:** The system SHALL use an LLM to read the transcribed player answer and decide if it is correct or not.
* **FR-CGL-005: Scoring Mechanism:** The system SHALL award points for correct answers and deduct points for incorrect answers or time-outs. The exact point values should be configurable.
* **FR-CGL-006: Question Progression:** The system SHALL automatically move to the next question after an answer is judged or time runs out, following a brief delay.
* **FR-CGL-007: Game End Condition:** The game SHALL end when the adjusted number of questions has been asked.
* **FR-CGL-008: Buzzer Time-out Question Skip:** If 10 seconds pass after the question audio begins playing on the game board and no player presses the buzzer, the question SHALL be automatically skipped. In this scenario, no player SHALL gain or lose points, and the game SHALL immediately move to the next question after a brief delay. 