# Financial Research Agent

A LangChain agent that answers personal finance questions with structured, multi-scenario solutions. For each question, it returns a topic, a summary covering worst, average, and best cases, sources, and the tools used.

## Features

- Answers financial questions with a tool-calling LangChain agent.
- Covers worst, average, and best-case scenarios for each problem.
- Returns output in a fixed structure defined by a Pydantic model (`ResearchResponse`).
- Supports three LLM providers: Google Gemini, OpenAI, and Anthropic Claude.

## Project Structure

| File | Purpose |
| --- | --- |
| `main.py` | Builds the prompt, agent, and parser, then runs an example query |
| `ResearchResponse.py` | Pydantic model for the structured output (`topic`, `summary`, `sources`, `usedTools`) |
| `tools.py` | Reserved for agent tools (currently empty) |
| `Requirements.txt` | Python dependencies |
| `.env` | API keys (not committed; listed in `.gitignore`) |

## Requirements

- Python 3.9 or higher
- Packages listed in `Requirements.txt`: langchain, wikipedia, langchain-community, langchain-openai, langchain-anthropic, python-dotenv, pydantic, duckduckgo-search

You also need the `langchain-google-genai` package, which is imported by `main.py` but is not listed in `Requirements.txt`.

## Installation

```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
pip install -r Requirements.txt langchain-google-genai
```

## Configuration

Create a `.env` file in the project folder with your keys:

```
OPENAI_API_KEY=your_openai_key
ANTHROPIC_API_KEY=your_anthropic_key
GOOGLE_API_KEY=your_google_key
```

Never commit this file. Keep `.env` in `.gitignore`.

## Running

```bash
python main.py
```

The script runs a sample query about buying a car in Egypt on a 3,500 EGP salary and prints the raw and structured responses.

## Known Issues

- `main.py` calls `parser.paarse(...)`. It should be `parser.parse(...)`.
- `claude-3-5-sonnet-2024022` is not a valid model name. Check the Anthropic model list for the correct ID.
- `rawResponse.get("output")[0]["text"]` assumes a specific output format. This may fail depending on the provider and version.
- `llm2` and `llm3` are created but never used. The agent runs only on `llm` (Gemini).
- `tools=[]` means the agent has no tools yet, even though the prompt tells it to use tools.

