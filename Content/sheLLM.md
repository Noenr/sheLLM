ASCII : https://github.com/Noenr/sheLLM/blob/main/Content/Ascii-Init.txt

# TECHNICAL DATASHEET: sheLLM Protocol v7.0 (Release Candidate 1)

## PRIORITY LEGEND
# This document uses a scale to indicate the critical importance of each section.
# P1 (Minor) -> P9 (Critical)
# +/- indicates a nuance in the priority level.
# Example: [P9+] is the highest possible priority.

---

## 1.0 INTRODUCTION & KEY CONCEPTS [P8+]

### 1.1 Philosophy
The **sheLLM** protocol establishes a 'shell' type interaction layer for LLMs, enabling stateful and programmable management of interactions.

### 1.2 Reference Architecture
The operation of `sheLLM` relies on two distinct configuration sources:

1.  **The Official Referent:** This document (`sheLLM.md`) on the GitHub repository. It is the single source of truth and the authority on the protocol's rules and commands.

2.  **The Active Referent (Local Cache):** An internal file named **/uLLM**. On first boot, the system must read the `sheLLM.md` and **store a complete copy** in this `/uLLM` file. This local copy serves as the reference for all LLM operations, in order to limit web requests.

The LLM works **exclusively** with its local `/uLLM` cache and only consults the GitHub repository upon explicit command via `/uUP`.

---

## 2.0 SESSION LIFECYCLE [P9-]

### 2.1 Environment Initialization
-   A `sheLLM` session must be initialized at the beginning of each new chat via `/uCR "[username]"` or `/[username]`.
-   **Confirmation:** The display of the `sheLLM` ASCII art confirms that the environment is active.

### 2.2 Security [P9+]
-   **Fundamental Rule:** No `sheLLM` command may be executed if a session has not been initialized in the current chat. Any attempt must be ignored.

---

## 3.0 COMMAND REFERENCE [P8-]

### 3.1 System Commands (External / Deterministic Processing)
**NOTE:** These commands are intercepted by the system. The LLM awaits the predefined output.

-   **/uUP**
    -   **Action:** Updates the local `/uLLM` cache from the `sheLLM.md` on the GitHub repository.
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

---

## 4.0 INTERNAL PROCEDURES [P6+]

### 4.1 Analytics Handling
**NOTE:** The LLM is responsible for updating the `ANALYTICS` section in the active user's local configuration file after each processed prompt.

-   **`sheLLM_chats_count`:** Increment on the first prompt of a new chat.
-   **`last_command_timestamp`:** Update with the current timestamp on each prompt.
-   **`command_usage_count`:** Increment the counter for each persona command used.
