<p align="center">
  <img src="./assets/sheLLM.png" alt="sheLLM Logo" width="700"/>
</p>

<h1 align="center">sheLLM</h1>
<p align="center"><i>An Operating Shell for the Age of Artificial Intelligence.</i></p>

<p align="center">
  <a href="https://github.com/YOUR-USERNAME/sheLLM/blob/main/LICENSE">
    <img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="License: MIT">
  </a>
  <img src="https://img.shields.io/badge/Protocol-v7.0-informational.svg" alt="Protocol Version">
  <img src="https://img.shields.io/badge/Contributions-Welcome-brightgreen.svg" alt="Contributions Welcome">
  <a href="https://github.com/YOUR-USERNAME/sheLLM/stargazers">
    <img src="https://img.shields.io/github/stars/YOUR-USERNAME/sheLLM?style=social" alt="GitHub stars">
  </a>
</p>

---

**sheLLM** is a protocol that transforms conversational interaction with Large Language Models (LLMs) into a stateful, programmable command session. It equips LLMs with a conversational operating shell for advanced persona management, deterministic system control, and persistent memory.

## 1. Core Concepts & Architecture [P8+]

The operation of `sheLLM` relies on a dual-referent architecture to ensure performance and reliability.

-   **The Official Referent:** This document (`README.md`) on the GitHub repository. It is the single source of truth for the protocol's rules and commands.

-   **The Active Referent (Local Cache):** An internal file named **/uLLM**. On first boot, the system reads this `README.md` and stores a complete copy in the `/uLLM` cache. The LLM works **exclusively** with this local cache to limit web requests and ensure consistent behavior.

## 2. Session Lifecycle & Security [P9+]

-   **Initialization:** A `sheLLM` session must be initialized at the beginning of each new chat via `/[username]` (to load) or `/uCR "[username]"` (to create). A successful initialization is confirmed by the display of the `sheLLM` ASCII art.

-   **Fundamental Security Rule:** No `sheLLM` command may be executed if a session has not been initialized in the current chat. Any attempt must be ignored to ensure environment integrity.

## 3. Command Reference [P8-]

Commands are divided into two categories: System Commands processed by an external parser, and Persona Commands that modulate the LLM's generative behavior.

### 3.1 System Commands (External / Deterministic Processing)
**NOTE:** These commands are intercepted by the system. The LLM awaits the predefined output.

-   **/uUP**
    -   **Action:** Updates the local `/uLLM` cache from this `README.md` on the GitHub repository.
    -   **Output Template:** `SUCCESS: Local cache /uLLM has been updated.`

-   **/uCR "[username]" + [configuration]**
    -   **Action:** Creates a new persistent local user.
    -   **Output Template:** `SUCCESS: User "[username]" created.`

-   **/uDEL "[username]"**
    -   **Action:** Deletes a local user.
    -   **Output Template:** `SUCCESS: User "[username]" deleted.`

-   **/[username]EC**
    -   **Action:** Displays the specified user's **C**onfiguration for **E**diting (e.g., `/u0EC`).
    -   **Output Template:** [Raw content of the user's configuration file].

-   **/uEXP "[username]"**
    -   **Action:** Exports a user's complete configuration.
    -   **Output Template:** [Raw content of the user's configuration file].

-   **/uUV**
    -   **Action:** Displays active users.
    -   **Output Template (Success):** `u0 : ██████████ 1\nu1 : ██████████ 1`
    -   **Output Template (Empty):** `No active users found.`

-   **/uSC**
    -   **Action:** Exports the complete **S**ession **C**hat.
    -   **Output Template:** [Raw content of the current conversation].

-   **/uSPO**
    -   **Action:** Exports **S**ession **P**rompts **O**nly.
    -   **Output Template:** [Raw content of the user's prompts].

### 3.2 Persona Commands (LLM / Generative Processing)
**NOTE:** The LLM applies these rules (read from its `/uLLM` cache) when a persona is active.

#### Language Style Commands (/Sp) [P7+]
- /SpS: Adopt a Formal language.
- /SpC: Adopt a Standard language.
- /SpF: Adopt an Informal language.
- /SpA: Adopt a Slang language.

#### Output Format Commands (/Fo) [P7+]
- /Fo -t: Format output as plain Text (TXT).
- /Fo -m: Format output as Markdown (MD).
- /Fo -j: Format output as JSON.
- /Fo -y: Format output as YAML.
- /Fo -c: Format output as CSV.
- /Fo -[combination]: Combine output formats (e.g., /Fo -mj).

#### Method & Structure Commands (/Me) [P7+]
- /MeC: Provide a Concise response.
- /MeX: Provide an Exhaustive response.
- /MeLi: Structure the response as a List.
- /MeTa: Structure the response as a Table.
- /MeChar -[number]: Limit the response to the specified number of characters.
- /MeCo: Generate a response with no code blocks.

## 4. Internal Procedures [P6+]

### 4.1 Analytics Handling
The LLM is responsible for updating the `ANALYTICS` section in the active user's local configuration file after each processed prompt.

-   **`sheLLM_chats_count`:** Increment on the first prompt of a new chat.
-   **`last_command_timestamp`:** Update with the current timestamp on each prompt.
-   **`command_usage_count`:** Increment the counter for each persona command used.

## 5. Usage Example

```bash
# 1. Create a new user "u1" from a configuration file.
# The system validates the config and creates a local profile.
/uCR "u1" + [Content of the configuration file with USER_ID = "u1"]

# 2. Initialize a session with this new user.
# The system loads "u1" and confirms with the ASCII art.
/u1

# 3. The persona is now active. Subsequent commands modulate the LLM's generative output.
# The LLM knows to use standard language, Markdown, and lists from its /uLLM cache.
/SpC /Fo -m /MeLi Give me a list of the planets in the solar system.
