# Analyze Code and Dependencies

## Context

Analyze the provided codebase thoroughly and generate a comprehensive development guide including the following aspects:

1. Development Environment:
- Identify and describe the development environment used (e.g., programming languages, IDEs, compilers, SDKs).

2. Dependencies:
- List all dependencies used in the project, including libraries, frameworks, package managers, and tools.
- Provide clear instructions on how to install each dependency.

3. Development Setup on Ubuntu with VS Code:
- Provide step-by-step instructions for setting up the project development environment on an Ubuntu system using Visual Studio Code.
- Include how to install necessary software, configure VS Code, and any environment variables or settings required.

Support the guide with reasoning detailing how you identified dependencies and environment requirements from the codebase.

# Steps
- Analyze files such as package managers (e.g., package.json, requirements.txt, Pipfile), configuration files, and documentation.
- Extract relevant details about programming languages, frameworks, and tools.
- Compile the findings into a clear, easy-to-follow guide tailored for Ubuntu and VS Code.
- Add the guide inside a file called "Installation.md" inside markdown folder which is located in the root of the project folder

# Output Format
Provide the output as a structured markdown document with titled sections:

# Development Environment

# Dependencies and Installation

# Development Setup on Ubuntu with VS Code

Include code blocks for installation commands and configuration snippets where applicable.

# Notes
Ensure the guide assumes the reader has a fresh Ubuntu installation and no prior setup. Be explicit and precise to avoid ambiguity.

# Response Formats

## prompt

{"prompt":"[full prompt text]","name":"Codebase Development Guide","short_description":"Generates a detailed development environment and setup guide for a codebase on Ubuntu with VS Code.","icon":"CodeBracketIcon","category":"technical","tags":["Development","Setup","Ubuntu","VS Code"],"should_index":true}