# User Stories

This section outlines the functionalities of "QuizGame" from the perspective of different user roles, describing what each user can do with the system to achieve a specific goal.

## As a Player...

* **US-P-001:** As a player, I want to **easily join a specific game instance from my phone** by visiting a unique web link so that I can participate in the quiz.
* **US-P-002:** As a player, I want to **enter my desired display name** in the lobby so that my identity is shown on the game board.
* **US-P-003:** As a player, I want to **press a buzzer button on my phone** when a question is displayed so that I can be the first to answer.
* **US-P-004:** As a player, I want my **buzzer button to be disabled** if another player presses it first so that only one player can answer at a time.
* **US-P-005:** As a chosen player, I want my **phone's microphone to activate** for 5 seconds so that I can speak my answer.
* **US-P-006:** As a player, I want to **see the countdown timer** on the game board while waiting for the chosen player's answer so that I know when the game will proceed.
* **US-P-007:** As a player, I want to **see my current score** and the overall game progress on the game board so that I can track my performance.
* **US-P-008:** As a player, I want to **see the winner screen** at the end of the game, displaying the final rankings and scores, so that I know the outcome.

## As an Admin (Game Host)...

* **US-A-001:** As an admin, I want to **view a list of all available quiz questions** so that I can manage the game content.
* **US-A-002:** As an admin, I want to **generate new quiz questions using an LLM** so that I have fresh content for games.
* **US-A-003:** As an admin, I want to **specify the difficulty and/or category** when generating questions, or choose random, so that I can customize the game's challenge.
* **US-A-004:** As an admin, I want to **edit existing questions** so that I can correct errors or refine content.
* **US-A-005:** As an admin, I want to **pause and resume the game** so that I can manage interruptions or breaks.
* **US-A-006:** As an admin, I want to **skip the current question** so that I can move past irrelevant or problematic questions.
* **US-A-007:** As an admin, I want to **kick a player out of the game** so that I can manage participant misconduct or disconnections.
* **US-A-008:** As an admin, I want to **manually modify a player's score** so that I can correct errors or apply penalties/bonuses.
* **US-A-009:** As an admin, I want to **reset the game to its lobby state** so that I can start a new game or rectify a major issue.
* **US-A-010:** As an admin, I want to **move to the next or last round/question** so that I can navigate the game flow manually if needed.
* **US-A-011:** As an admin, I want to **undo the last action** so that I can quickly rectify mistakes.
* **US-A-012:** As an admin, I want to **adjust the total number of questions** for a game so that I can control game duration.

## As a Game System...

* **US-GS-001:** As a game system, I want to **manage the overall game state** (lobby, question active, answering phase, round transition, game over) to ensure proper game progression.
* **US-GS-002:** As a game system, I want to **accurately identify the first player to buzz** and immediately disable other buzzers to ensure fairness.
* **US-GS-003:** As a game system, I want to **manage and display the 5-second answer timer** for the chosen player so that everyone knows the time limit.
* **US-GS-004:** As a game system, I want to **use an LLM to evaluate player voice answers** for correctness so that scoring can be automated.
* **US-GS-005:** As a game system, I want to **award points for correct answers and deduct points for incorrect answers or time-outs** to reflect player performance.
* **US-GS-006:** As a game system, I want to **automatically move to the next question** after an answer judgment or time-out, following a brief delay, to maintain game flow.
* **US-GS-007:** As a game system, I want to **end the game** when the configured number of questions has been asked so that a winner can be declared. 