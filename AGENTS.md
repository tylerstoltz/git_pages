# AGENTS.md file

## Overview
- This repository is a collection of standalone projects, each contained within its own directory.
- Each project has its own README.md file with specific details and instructions.
- This AGENTS.md file provides general guidelines for working with the projects in this repository.
- When in doubt, create a new project directory rather than modifying existing ones!

## Dev environment tips
- You are in a sandboxed, headless virtual environment with internet access.
- You have access to a terminal for running commands.
    - Common commands available: ls, cd, mkdir, rm, cp, mv, cat, echo, touch, git, curl, wget, unzip, tar, sed, awk, grep, make, cmake, etc.
    - Note: Docker is NOT available
- You have the following languages and runtimes available:
    - Python 3.11.14
    - Node.js 22.21.1 (with npm, yarn, pnpm, npx)
    - TypeScript 5.9.3
    - Ruby 3.3.6
    - Rust 1.91.1
    - Go 1.24.7
    - Bun 1.3.2
    - PHP 8.4.14
    - Java 21.0.8
- You can install additional packages using the respective package managers:
    - Python: pip, pip3, or uv
    - Node.js: npm, yarn, or pnpm
    - Ruby: gem
    - Rust: cargo
    - Go: go get/go install
    - Bun: bun install
- Use virtual environments for Python projects to manage dependencies (prefer `uv venv`).


## Testing instructions
- Each project should include its own testing setup and instructions in its README.md
- Run tests from within the project directory
- Common test commands by language:
    - Python: `pytest`, `python -m pytest`, or `uv run pytest`
    - Node.js/TypeScript: `npm test`, `yarn test`, `pnpm test`, or `bun test`
    - Ruby: `bundle exec rspec` or `rake test`
    - Rust: `cargo test`
    - Go: `go test ./...`
- Ensure all tests pass before creating a pull request

## PR instructions
- Title format: [<project_name>] <Title>
- Description: Provide a brief description of the changes made.
- Link to any relevant issues or tickets.
