# Issue #2025-04-05T14:32:15Z: Simplifying `/generate` — Removing "Unit test" and "Statement flow" Options

## Description

This issue proposes a **simplification of the `/generate` command** in the GPT Morph CLI Bot. The two optional sub-commands — `/unit_test` and `/statement_flow` — which were initially experimental but have since become outdated, are now **fully removed** from the command flow.

### Background: The Evolution of Code Morphing

When the GPT Morph CLI Bot was first developed, the concept of *code morphing* was still in its early stages. The initial vision was that morphing could be applied to two specific, high-value tasks:

1. **Unit test generation** — automatically generating a full test suite for a given module.
2. **Statement flow generation** — creating a Graphviz `dot` file (`.dot`) that visualizes the logical flow of a function or method.

These two paths were considered distinct and important enough to warrant separate sub-commands under the `/generate` umbrella.

However, over time, it became evident that:

- The *idea of morphing* is **universal** — it applies to any code generation task.
- The need for a dedicated `/unit_test` flow is **redundant**: a simple, natural language description like *"Generate a unit test for my transaction processor, including edge cases."* is sufficient.
- Similarly, the need for a separate `/statement_flow` command is **less critical** — the same description-driven approach works equally well for generating a Graphviz flow.

### The Problem: Complexity Without Necessity

The current flow for `/generate` includes the following menu choices:

```
1. /generate - Generate a new file for your project.
2. /settings - Display your LLM settings.
3. /graph - Graphviz representation for this bot's API.
4. /help - Show help.
5. /exit - Exit the application.
```

After selecting `/generate`, users are prompted for a file name, then they are presented with:

```
Please, describe, what should be checked in this test.
```

This choice was initially a way to distinguish between:

- **Basic generation** (`/generate`) — a generic file.
- **Unit test generation** (`/unit_test`) — a test file with a specific format and structure.
- **Flow graph generation** (`/statement_flow`) — a Graphviz diagram.

But now, these two sub-commands are **out of phase** with the overall philosophy of GPT Morph: **the whole project is the context**.

### The Solution: Return to Simplicity

The core idea is to **streamline the `/generate` experience** by removing the two obsolete branches:

- `/unit_test` → **removed**
- `/statement_flow` → **removed**

Instead, the bot now accepts a **single, unified text prompt** for all types of generation, regardless of the file type.

### Updated Flow After This Change

```
mrph> Welcome to the GPT Morph CLI Bot! You are currently in the main menu.
            
Please choose one of the following options:
1. /generate - Generate a new file for your project.
2. /settings - Display your LLM settings.
3. /graph - Graphviz representation for this bot's API.
4. /help - Show help.
5. /exit - Exit the application.

To execute a command, type the corresponding option and press Enter.

You can always return to the main menu by typing "/start".
[['Generate', 'Patch'], ['Settings', 'Help', 'Exit'], ['Graph'], ['Version']]

/generate
mrph> Enter the file name for saving the generated file:
main.py
mrph> Ok, I will create a file "main.py" when finished. What should be in this file?
Please, generate a Python "Hello, world!" application. Include error handling and input validation.
mrph> Your "main.py" file was saved.

$ python main.py
Hello, world!
```

Now, a user can generate:

- A **unit test** via a simple prompt:  
  > "Generate a unit test for the `TransactionsSource` class, checking initialization and data processing."

- A **Graphviz flow** via a descriptive prompt:  
  > "Generate a statement flow graph for the `process()` method in `TransactionProcessor` class. Show control flow, data dependencies, and method calls."

- A **configuration file**:  
  > "Generate a `config.yaml` file for the web server, with logging, database, and cache sections."

- A **README**:  
  > "Create a detailed `README.md` for this project, including installation, usage, and contribution guidelines."

### Benefits of This Change

| Benefit | Explanation |
|-------|---------------|
| **Simplicity** | Fewer menu choices, less cognitive load. |
| **Consistency** | Every morph is driven by the same natural language description. |
| **Flexibility** | The same prompt can generate any type of code — no need to remember sub-commands. |
| **Future-proofing** | As LLMs grow more capable, the quality of description-based generation will improve, making this model the foundation for all morphing. |
| **Reduced maintenance** | The codebase no longer needs to maintain two specialized flows, reducing technical debt. |

### Impact on User Experience

- **New users** will find the bot more intuitive: one command, one prompt, one workflow.
- **Experienced users** will appreciate the elegance of a unified generation interface.
- **Documentation** can now be simplified: the "How to generate code" guide is just a single paragraph:  
  > "Type `/generate`, enter the file name, and write a clear description of what you want in the file."

### Next Steps

- Update the `examples.md` file to reflect the new `/generate` simplicity.
- Update the `README.md` documentation to reflect the removal of `/unit_test` and `/statement_flow`.
- Add a `CHANGELOG.md` entry to track this change.

---

**Author**: Syun Lee  
**Date**: 2025-04-05  
**Time**: 14:32:15 UTC  
**Status**: Open  
**Priority**: High  
**Labels**: `enhancement`, `simplification`, `user experience`, `core flow`
