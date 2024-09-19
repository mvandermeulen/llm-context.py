# LLM Context

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![PyPI version](https://badge.fury.io/py/llm-context.svg)](https://badge.fury.io/py/llm-context)

LLM Context is a tool designed to help developers efficiently copy and paste relevant context from code / text repositories into Large Language Model (LLM) chats. It leverages `.gitignore` patterns for smart file selection and uses the clipboard for seamless integration with LLM interfaces.

> **Note**: This project was developed in collaboration with Claude-3.5-Sonnet, using LLM Context itself to share code context during development. All code in the repository is human-curated (by me 😇, @restlessronin).
  
## Current Usage Patterns

- **LLM Integration**: Primarily used with Claude (Project Knowledge) and GPT (Knowledge), but adaptable to various chat interfaces.
- **Project Types**: Suitable for code repositories and collections of text/markdown/html documents.
- **Project Size**: Optimized for projects that fit within an LLM's context window. Large project support is in development.

## Installation

Use [pipx](https://pypa.github.io/pipx/) to install LLM Context:

```
pipx install llm-context
```

## Usage

### Quick Start and Typical Workflow

1. Navigate to your project's root directory.
2. (Optional) Edit `.llm-context/config.toml` to [add custom ignore patterns](#customizing-ignore-patterns).
3. Run `lc-sel-full` to select files for full content inclusion.
4. (Optional) [Review the selected file](#reviewing-and-editing-selected-files) list in `.llm-context/curr_ctx.toml`.
5. Run `lc-context` to generate and copy the context to your clipboard.
6. Paste the generated context into your Claude Project Knowledge or GPT Knowledge.
7. Start your conversation with the LLM about your project.

### Handling LLM File Requests

When the LLM asks for a file that isn't in the current context:

1. Copy the LLM's file request (typically in a markdown block) to your clipboard.
2. Run `lc-clipfiles` to generate the content of the requested files.
3. Paste the generated file contents back into your chat with the LLM.

### Configuration

#### Customizing Ignore Patterns

Add custom ignore patterns in `.llm-context/config.toml` to exclude specific files or directories not covered by your project's `.gitignore`. This is useful for versioned files that don't contribute to code context, such as media files, large generated files, detailed changelogs, or environment-specific configurations.

Example:

```toml
# /.llm-context/config.toml
[gitignores]
full_files = [
  "*.svg",
  "*.png",
  "CHANGELOG.md",
  ".env",
  # Add more patterns here
]
```

#### Reviewing Selected Files

Review the list of selected files in `.llm-context/curr_ctx.toml` to check what's included in the context. This is particularly useful when trying to minimize context size.

```toml
# /.llm-context/curr_ctx.toml
[context]
full = [
  "/llm-context.py/pyproject.toml",
  # more files ...
]
```

## Command Reference

- `lc-sel-full`: Select files for full content inclusion
- `lc-sel-outline`: Select files for outline inclusion (experimental)
- `lc-context`: Generate and copy context to clipboard
- `lc-clipfiles`: Generate content for LLM-requested files

## Experimental: Handling Larger Repositories

For larger projects, we're exploring a combined approach of full file content and file outlines. Use `lc-sel-outline` after `lc-sel-full` to experiment with this feature.

**Note:** The outlining feature currently supports the following programming languages:
C, C++, C#, Elisp, Elixir, Elm, Go, Java, JavaScript, OCaml, PHP, Python, QL, Ruby, Rust, and TypeScript. Files in unsupported languages will not be outlined and will be excluded from the outline selection.

### Feedback and Contributions

We welcome feedback, issue reports, and pull requests on our [GitHub repository](https://github.com/cyberchitta/llm-context.py).

## Acknowledgments

LLM Context has evolved from several projects and influences:

- This project is a successor to [LLM Code Highlighter](https://github.com/restlessronin/llm-code-highlighter), a TypeScript library developed for use in IDEs like VS Code.
- LLM Code Highlighter was inspired by [Aider Chat](https://github.com/paul-gauthier/aider), particularly its [RepoMap](https://aider.chat/docs/repomap.html) functionality.
- The original concept grew out of a project for [RubberDuck](https://github.com/rubberduck-ai/rubberduck-vscode) and was later used for [Continue](https://github.com/continuedev/continuedev).
- LLM Code Highlighter included functionality for ranking and highlighting tags, based on a translation of Aider Chat's Python code to TypeScript (with the help of Chat-GPT-4). This functionality is not yet implemented in LLM Context.
- The outlining functionality, independently developed in LLM Code Highlighter, has been reimplemented in this project.
- Parts of the code in LLM Context were translated from TypeScript to Python with Claude-3.5-Sonnet's help, bringing the project full circle (Python -> TypeScript -> Python).
- This project currently uses the tree-sitter [tag query files](src/llm_context/highlighter/tag-qry/) from Aider Chat.

We are grateful for the open-source community and the innovations that have influenced this project's development.

I am grateful for the help of Claude-3.5-Sonnet in the development of this project.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the Apache License, Version 2.0. See the [LICENSE](LICENSE) file for details.