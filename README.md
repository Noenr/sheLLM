# sheLLM
An operating shell for LLMs. A protocol that transforms conversational interaction into a stateful, programmable command-line session for advanced persona management.

<p align="center">
  <img src="./assets/sheLLM.png" alt="sheLLM Logo" width="700"/>
</p>

<p align="center">
  <a href="https://github.com/VOTRE-NOM/sheLLM/blob/main/LICENSE">
    <img src="https://img.shields.io/badge/License-MIT-white.svg" alt="License: MIT">
  </a>
  <img src="https://img.shields.io/badge/Contributions-Welcome-brightgreen.svg" alt="Contributions Welcome">
  <img src="https://img.shields.io/github/stars/Noenr/sheLLM?style=social" alt="GitHub stars">
</p>

<h1 align="center">sheLLM</h1>
<p align="center"><i>sheLLM: The Protocol for a Programmable AI.</i></p>

---

**sheLLM** is a protocol that transforms conversational interaction with Large Language Models (LLMs) into a stateful and programmable command session. It equips LLMs with a conversational shell for advanced persona management, output control, and memory persistence.

## Core Features

-   **Persistent Persona Management:** Create (`/uCR`), load (`/uX`), and delete (`/uDEL`) user profiles with their own memorized configuration.
-   **Intuitive Command Interface:** Drive the style (`/Sp`), format (`/Fo`), and structure (`/Me`) of the LLM's responses with a simple and powerful syntax.
-   **Stateful Session Interaction:** Initialize a persona at the start of a chat and interact with it contextually. The LLM remembers the agent's state for the entire duration of the chat.
-   **Strict & Validated Protocol:** A clear syntax and a zero-tolerance policy for errors, ensuring reliable and predictable interactions.

## How It Works

`sheLLM` works as a command interpretation layer that executes before the LLM processes the prompt.

1.  **Creation:** A user is created via `/uCR` with a configuration file defining their `USER_ID` and rules.
2.  **Initialization:** The user is loaded into memory for the chat session via `/u0`, `/u1`, etc.
3.  **Execution:** Subsequent commands (`/SpC`, `/MeLi`...) are intercepted to modify the AI's behavior without needing to be re-explained.

### Usage Example

```bash
# 1. Create a new user "u1" from a configuration file
/uCR "u1" + [Content of the configuration file with USER_ID = "u1"]

# 2. Initialize a session with this new user
/u1 /SpC /Fo -m /MeLi Hello, introduce yourself.

# 3. The configuration is now active. Subsequent commands are shorter.
# The LLM remembers to use standard language, Markdown, and lists.
Give me a list of the planets in the solar system.
