## Changes in my fork
- Fixed bug when pre-defined prompts file is empty
- Changed default open behaviour from CopilotChat commad to open in full screen (I use TMUX for window management and I prefer vim to be single full screen per pane)
- Changed function name from SubmitChatMessage to CopilotSubmit
- Added function CopilotAdd: takes a file path as argument, import full content of this file to send it along with user input as context for GitHub Copilot call

User flow is:
1. Type command `:CopilotChat` to open it
2. Add your input below break line
3. OPTIONAL: Type command `:CopilotAdd <filename>` to add file content for context
4. Type `:CopilotSubmit` and wait answer

<div align="center">

# Copilot Chat for Vim
Copilot Chat functionality without having to leave vim.

Nvim folks will be able to use [CopilotChat.nvim](https://github.com/CopilotC-Nvim/CopilotChat.nvim) for a similar experience.

![copilotChat](https://github.com/user-attachments/assets/0cd1119d-89c8-4633-972e-641718e6b24b)

</div>

## Requirements

- [Vim][] (9.0.0185 or newer).

- [NerdFonts][]. (optional for pretty icons)

## Commands
| Command | Description |
| ------- | ----------- |
| `:CopilotChat` | Opens a new copilot window (default vsplit right) |
| `:CopilotConfig` | Open `config.json` for default settings when opening a new CopilotChat window |
| `:CopilotModels` | View available modes / select active model |

## Key Mappings
| Location | Insert | Normal | Visual | Action |
| ---- | ---- | ---- | ---- | ---- |
| `global` | - | `<Leader>cc` | - | Opens a new chat window `:CopilotChat` |
| `<buffer>` | - | `<CR>` | - | Submit current prompt |
| `:CopilotModels` `<buffer>` | - | `<CR>` | - | Select the model on the current line for future chat use |
| `global` | - | - | `<Leader>a` | Add the current selection to the active chat window inside a code block |

## Installation

Using vim-plug, Vundle, or any other plugin manager. 

## Setup
1. Run `:CopilotChat` to open a chat window. You will be prompted to setup your device on first use.
2. Write your prompt under the line separator and press `<Enter>` in normal mode / `:SubmitChatMessage`
3. You should see a `Waiting for response..` in the buffer to indicate work is being done in the background
4. 🎉!

## Features
### Model selection
Using `:CopilotModels` will bring up a buffer of all the available models for you to choose from. Simply press `<Enter>` in normal mode on the model you would like to use. New chats will use the active model

### Add Selection to chat
By default this is configured to `<Leader>a` when in visual mode
- Adds the selection to the active chat window inside of a `&filetype` named codeblock
![](https://private-user-images.githubusercontent.com/2555073/423367966-e1aac0e2-0e95-4fdb-81d1-b92bb4b7cbf7.gif?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDIxOTg4MTIsIm5iZiI6MTc0MjE5ODUxMiwicGF0aCI6Ii8yNTU1MDczLzQyMzM2Nzk2Ni1lMWFhYzBlMi0wZTk1LTRmZGItODFkMS1iOTJiYjRiN2NiZjcuZ2lmP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQVZDT0RZTFNBNTNQUUs0WkElMkYyMDI1MDMxNyUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyNTAzMTdUMDgwMTUyWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9MjUyMTlmNDAxMjYyNzc5MjcwNmVlNTUwMDY2N2Q0NGVlMzY5OGUyM2U1MjgxMmQzOGI5ZTEwZDg2OGMzNzJkYiZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.hckZ7Swx9wszWWgdduqTRnwtrqvUPMVhqSyoSdwTny4)

### Prompt Templates
Copilot Chat supports custom prompt templates that can be quickly accessed during chat sessions. Templates allow you to save frequently used prompts and invoke them with a simple syntax.

#### Using Prompts
- In the chat window, start a line with `> PROMPT_NAME` 
- The `PROMPT_NAME` will be automatically replaced with the template content before sending to Copilot
- Example: `> explain` would expand to the full explanation template

#### Managing Prompts
1. Open the config with `:CopilotConfig`
2. Add prompts to the `prompts` object in `config.json`:
```json
{
  "model": "gpt-4",
  "prompts": {
    "explain": "Explain how this code works in detail:",
    "refactor": "Suggest improvements and refactoring for this code:",
    "docs": "Generate documentation for this code:"
  }
}
```

#### Example Usage
```
> explain

function validateUser() {
  // code to validate
}
```
This will send the full template text + your code to Copilot.


[Neovim]: https://github.com/neovim/neovim/releases/latest
[Vim]: https://github.com/vim/vim
[NerdFonts]: https://www.nerdfonts.com
