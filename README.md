<!-- Logo -->
<p align="center">
<img src="./assets/sheLLM.png" alt="sheLL-M Logo" width="700"/>
</p>

<h1 align="center">sheLLM</h1>
<p align="center"><i>The Protocol for a Programmable AI.</i></p>

<p align="center">
<!-- License Badge -->
<a href="https://github.com/Noenr/sheLLM/blob/main/LICENSE">
<img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="License: MIT">
</a>
<!-- Protocol Version Badge -->
<img src="https://img.shields.io/badge/Protocol-v8.3-informational.svg" alt="Protocol Version">
<!-- Contributions Welcome Badge -->
<img src="https://img.shields.io/badge/Contributions-Welcome-brightgreen.svg" alt="Contributions Welcome">
<!-- GitHub Stars Badge -->
<a href="https://github.com/Noenr/sheLLM/stargazers">
<img src="https://img.shields.io/github/stars/Noenr/sheLLM?style=social" alt="GitHub stars">
</a>
</p>

---

**sheLLM** is an initialization protocol that transforms a standard Large Language Model (LLM) into a stateful, command-driven operating shell. It operates entirely within the prompt, enabling advanced persona management, session-based memory, and precise output control through an intuitive command-line syntax.

## Core Concept: A Prompt-Based Operating Shell

Instead of relying on an external system, `sheLLM` works by providing the LLM with a comprehensive "master prompt" at the beginning of a chat. This prompt bootstraps a complete operating environment with its own rules, commands, and memory management system, which the LLM then executes.

* **Two Operating Modes:**

  * **Persistent Mode:** The LLM's memory (user profiles, custom commands) persists across different chat sessions. When invoked, it reloads its previous state.

  * **Ephemeral Mode:** The memory is strictly limited to the current chat session and is wiped clean upon exit, ensuring total privacy.

* **Secure Invocation:** A session is only activated when the user explicitly calls `sheLLM`, `shellm`, or `SHELLM`. Before this invocation, the LLM remains in its standard, unaware state, preventing any accidental command execution.

* **Integrated User Profiling:** The `sheLLM` master prompt includes a final section where the user can define their own profile (name, age, keywords, etc.). The LLM memorizes this information to provide context-aware responses throughout the session.

## Command Reference

All commands are prefixed with `+`.

### System Commands

* `+cC <name> , +<definition>`: Creates a new custom command.

* `+SHELLM`: Displays protocol metadata (Version, Owner).

* `+Ap , +<question>`: Queries the user profile database.

* `+h`: Displays a complete list of all available commands.

* `+update`: Instructs the LLM to refresh its protocol rules (simulated).

* `+q`: Exits the `sheLLM` mode for the current session.

### Expertise Commands (Teacher Mode)

* `+Teacher-list`: Lists available expert personas the LLM can embody.

* `+Teacher-<number>`: Activates the corresponding expert mode, changing the output prefix to `sheLLM > TeacherMode >`.

* `+teacher-quit`: Exits Teacher Mode and returns to the standard `sheLLM` shell.

### Output Control Commands

#### Style (Spell)

* `+SpS`: Adopt a **Supported** (Formal) language.

* `+SpC`: Adopt a **Common** (Standard) language.

* `+SpF`: Adopt a **Familiar** (Informal) language.

* `+SpA`: Adopt a **Slang** language.

#### Format

* `+Fo-t`: Force the output to be plain **Text (TXT)**.

* `+Fo-m`: Force the output to be formatted as **Markdown (MD)**.

* `+Fo-j`: Force the output to be a **JSON** object.

* `+Fo-y`: Force the output to be a **YAML** structure.

* `+Fo-c`: Force the output to be formatted as **CSV**.

* `+Fo-tmj`: Combine formats (e.g., text, markdown, JSON).

#### Method (Method)

* `+MeC`: The response must be **Concise**.

* `+MeX`: The response must be **Exhaustive**.

* `+MeLi`: The response must be structured as a **List**.

* `+MeTa`: The response must be organized in a **Table**.

* `+MeChar -[number]`: The response must not exceed the specified number of **characters**.

* `+MeCo`: The response must not contain any **code blocks**.

## Usage Example

The `sheLLM` workflow is simple and intuitive.

```bash
# 1. Start a new chat and paste the chosen Master Prompt 
# (e.g., sheLLM-Prompt-Persistent.md), filling in your user profile at the end.
# Example: User Profile: Description(Bob, 42, keywords: data science, python)

# 2. Invoke the shell to activate it.
sheLLM

# LLM's Response, confirming initialization and readiness:
# sheLLM >

# 3. The shell is now active. You can use commands.
# Let's ask for the capital of France, in a formal tone and as a list.
+SpS +MeLi What is the capital of France?

# LLM's Response, following the protocol:
# sheLLM > 
# - The capital of the French Republic is Paris.
