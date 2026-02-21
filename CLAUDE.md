# CLAUDE.md

This file provides context and guidance for AI assistants (Claude and others) working on this repository.

## Project Overview

**Name:** envios-automatizado-em-planilha
**Description:** Automated sending/shipments management via spreadsheet — a tool for automating dispatch workflows driven by spreadsheet data (e.g., Excel or Google Sheets).
**Language:** Portuguese-language project (variable names, comments, and documentation may be in Portuguese).
**Status:** Repository initialized; no source code yet. This CLAUDE.md is the starting point.

The project name breaks down as:
- **envios** — shipments / sends / dispatches
- **automatizado** — automated
- **em planilha** — in spreadsheet / via spreadsheet

Likely use cases include reading rows from a spreadsheet and triggering automated actions such as email sends, shipping label generation, status updates, or API calls.

---

## Repository Structure

Currently the repository contains only scaffolding:

```
envios-automatizado-em-planilha-/
├── .gitkeep          # Placeholder to keep directory tracked by git
└── CLAUDE.md         # This file
```

As the project grows, expect a structure similar to one of the patterns below depending on the chosen stack:

### If Python
```
envios-automatizado-em-planilha-/
├── src/
│   ├── main.py           # Entry point
│   ├── planilha.py       # Spreadsheet reading/parsing logic
│   ├── envios.py         # Dispatch/send logic
│   └── config.py         # Configuration and environment loading
├── tests/
│   └── test_*.py
├── requirements.txt
├── .env.example
└── README.md
```

### If Node.js/TypeScript
```
envios-automatizado-em-planilha-/
├── src/
│   ├── index.ts          # Entry point
│   ├── planilha.ts       # Spreadsheet reading/parsing logic
│   ├── envios.ts         # Dispatch/send logic
│   └── config.ts         # Configuration and environment loading
├── tests/
├── package.json
├── tsconfig.json
├── .env.example
└── README.md
```

---

## Development Workflow

### Branch Strategy

- `main` / `master` — stable, production-ready code
- `claude/...` — branches created by AI assistants for automated changes
- Feature branches should follow: `feature/<short-description>`
- Bug fix branches: `fix/<short-description>`

### Git Conventions

- Write commit messages in English or Portuguese consistently; prefer English for international collaboration.
- Use imperative mood: "Add spreadsheet parser" not "Added spreadsheet parser."
- Keep commits atomic — one logical change per commit.
- Never commit secrets, credentials, or `.env` files containing real values.

### Environment Variables

All secrets and configuration must be managed via environment variables. When adding a new variable:
1. Add it to `.env.example` with a placeholder value and a comment explaining it.
2. Never commit `.env` (add it to `.gitignore`).
3. Document the variable in this file or in `README.md`.

Expected environment variables (to be defined as the project evolves):

| Variable | Description |
|----------|-------------|
| _(none yet)_ | _(to be added as project develops)_ |

---

## Code Conventions

### General

- Keep business logic separate from I/O (reading files, sending emails, calling APIs).
- Configuration should be centralized — avoid hardcoded values scattered across files.
- Prefer explicit error handling over silent failures, especially for I/O operations.
- Log meaningful messages at key steps (file read, dispatch start, dispatch result).

### Spreadsheet Handling

- Validate spreadsheet structure on load — fail early with a clear error if required columns are missing.
- Treat all spreadsheet data as untrusted input: sanitize and validate before use.
- Support both `.xlsx` and `.csv` formats where practical.

### Dispatch / Send Logic

- Make dispatch operations idempotent where possible (re-running should not create duplicates).
- Track dispatch state in a status column or an external log to allow resuming interrupted runs.
- Rate-limit outbound calls (emails, API requests) to avoid throttling.

### Testing

- Write unit tests for parsing logic and business rules.
- Use mocks/stubs for external services (email, APIs, spreadsheet reads) in unit tests.
- Integration tests may use fixture spreadsheet files kept in `tests/fixtures/`.
- Test file names should mirror source file names: `src/planilha.py` → `tests/test_planilha.py`.

---

## Key Commands

These commands will be relevant once the project stack is established. Update this section when the stack is chosen.

### Python
```bash
# Install dependencies
pip install -r requirements.txt

# Run the application
python src/main.py

# Run tests
pytest

# Lint
flake8 src/ tests/
# or
ruff check src/ tests/
```

### Node.js / TypeScript
```bash
# Install dependencies
npm install

# Run the application
npm start

# Run tests
npm test

# Build
npm run build

# Lint
npm run lint
```

---

## AI Assistant Guidelines

When working in this repository as an AI assistant:

1. **Understand the domain first.** This is a Portuguese-language automation project. Read any existing code carefully before making changes.

2. **Preserve language consistency.** If existing variables, functions, or comments are in Portuguese, continue in Portuguese. Do not silently translate existing names to English.

3. **Do not add complexity prematurely.** The project is in early stages. Prefer simple, readable solutions over elaborate abstractions.

4. **Environment variables.** Never hardcode credentials or API keys. Always use environment variables and update `.env.example`.

5. **Spreadsheet schema changes.** If modifying what columns the spreadsheet expects, update all related parsing code, validation, and documentation atomically.

6. **Test before pushing.** Run the test suite and linter before committing. If tests don't exist yet, note this as a known gap.

7. **Update this file.** When significant new conventions, commands, or structures are established, update `CLAUDE.md` to reflect them.

8. **Branch usage.** Always work on the designated feature branch. Never push directly to `main`/`master`.

---

## Notes

- Repository initialized: January 22, 2026
- CLAUDE.md created: February 21, 2026
- This file should be updated as the project matures.
