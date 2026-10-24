# AI CLI — Gemini-powered command-line assistant

AI CLI is an experimental Python project that turns natural-language requests into shell commands using Google's Gemini API. It includes separate starter scripts for Windows, Linux, and macOS.

> **Important safety warning:** this repository is a prototype, not a hardened agent. The inspected scripts pass model-generated commands to `subprocess.run(..., shell=True)` and use a simple blocklist that cannot reliably prevent dangerous commands. They execute generated commands automatically without the interactive approval described in some earlier documentation. **Do not run this on a machine or account containing important data.** Review and manually run commands yourself until execution is redesigned around explicit approval and a strict allowlist.

## Current capabilities

- Sends a natural-language request to the Gemini API.
- Prints the generated command.
- Runs the command and prints its output.
- Loads `GEMINI_API_KEY` from the process environment or a local `.env` file.
- Provides OS-specific starter scripts:
  - `Gemini_Agent_Windows.py`
  - `Gemini_Agent_Linux.py`
  - `Gemini_Agent_MacOS.py`

This project is an educational starting point. The current implementation does **not** provide a robust permission system, a reliable sandbox, or dependable command safety guarantees.

## Requirements

- Python 3
- A Gemini API key
- Packages listed in `requirements.txt`

The scripts currently use the legacy `google.generativeai` Python package and request the `gemini-pro` model. API/package compatibility may have changed, so verify the currently supported SDK and model name if requests fail.

## Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/pkrRepo00/Ai-CLI.git
   cd Ai-CLI
   ```
2. Install the dependencies:
   ```bash
   python -m pip install -r requirements.txt
   ```
3. Create a local `.env` file in the project root:
   ```env
   GEMINI_API_KEY=your_gemini_api_key
   ```
   Keep this key private. Never commit your `.env` file.
4. Choose the script for your operating system:
   ```bash
   python Gemini_Agent_Windows.py
   ```
   Or use `Gemini_Agent_Linux.py` on Linux and `Gemini_Agent_MacOS.py` on macOS.

## Example request

You can enter a request such as:

```text
User: Show files in the current directory
```

The model returns a command. **Inspect the command instead of trusting it automatically.** Model output can be incorrect, destructive, or manipulated by untrusted input.

## Known limitations and recommended next steps

- Replace the legacy SDK/model configuration with a currently supported Gemini SDK and model.
- Remove automatic shell execution; show the proposed command and require explicit user approval.
- Prefer structured, OS-specific command generation and an allowlist over substring blocklists.
- Add timeouts, clearer error handling, and tests for command validation.
- Add a dry-run mode and isolate file operations to a user-selected working directory.

## License

Released under the MIT License. See [LICENSE](LICENSE).
