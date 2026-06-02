# steno-main reviewer notes

## Architecture
The StenoAI repository is organized into a front-end built with React and Vite, and a back-end powered by Python. The front-end resides in the `app` directory while the backend code is located in `src`, with a CLI interface provided by `simple_recorder.py`. The application is designed to be an Electron desktop app that facilitates recording, transcribing, and summarizing confidential conversations.

## Conventions
- **File Structure**: The repository follows a clear hierarchical structure where front-end code is in `app/` and back-end code is in `src/`. The `app/` directory contains `main.js` for the Electron process, a `preload.js`, and `renderer/` for React components.
- **TypeScript and JSX**: All React components are written in TypeScript with JSX syntax. Type definitions are managed in the `tsconfig.json` found in `app/renderer/`.
- **Inline Documentation**: Functions and modules leverage JSDoc-style comments for better understanding (e.g., `app/preload.js`).
- **Style Guides**: Python code adheres to PEP 8 standards with type hints and docstrings, while JavaScript uses semicolons and prefers `const/let` over `var` as per the guidelines outlined in `CONTRIBUTING.md`.
- **Dependency Management**: JavaScript dependencies are defined in `package.json`, while Python dependencies are managed via `requirements.txt`.

## Intentional non-standard choices
- **Single Instance Mode**: The application requests a single instance lock via `app.requestSingleInstanceLock()` in `app/main.js`, an approach designed for a better user experience ensuring only one instance runs at a time.
- **Environment Configuration with .env**: The project practices a flexible configuration loading system from local `.env` files, which are not tracked in source control. This choice is crucial to securing sensitive information (as mentioned in `app/main.js`).
- **Manual Semantic Versioning**: The project employs a manual approach to semantic versioning as per the guidelines in `CONTRIBUTING.md`, which may seem archaic compared to automated systems.

## Watch out for
- **Back-end Communication**: Ensure all communication with the Electron main code and Python services via IPC is properly documented in `app/docs/ipc-contract.md`.
- **Incomplete .env Setup**: Issues may arise if the `.env` file is not set up correctly; ensure to provide a template or documentation for required variables.
- **Missing Cleanup in `ensureMainWindow`**: The function lacks cleanup on errors, which could lead to resource leaks or locked resources.
- **Error Handling**: There is room to strengthen error handling, particularly in functions interacting with the filesystem, network, or external services, to ensure resilience and proper debugging information is available.
- **Rigid Testing Guidelines**: The testing guidelines in `CONTRIBUTING.md` may need to be enforced more strictly, especially under the sections mentioning manual testing processes which could lead to gaps in automated testing coverage.