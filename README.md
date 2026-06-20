 ContextOS

```markdown
Agent Context OS

Agent Context OS is a local-first Python SDK for turning documents and text into semantic graphs, retrieving graph-aware context, optimizing token usage, and sending compact prompts to OpenAI, FastRouter, or a local mock model.

It is built for developers creating AI agents that need structured memory, transparent context selection, and replayable prompt decisions.

 Why Agent Context OS?

Most agent systems pass large chunks of raw text into prompts. That gets expensive, noisy, and hard to debug.

Then, when a user asks a question, it retrieves only the most relevant graph facts and document chunks, compiles an optimized prompt, and records exactly what context was kept or ignored.

## Features

- Local semantic graph builder
- Entity-relation triple extraction
- NetworkX graph storage
- OpenAI extraction and completion support
- FastRouter support through OpenAI-compatible API style
- Offline mock mode with no API keys required
- Graph-aware context retrieval
- Token budget optimization
- Duplicate sentence removal
- Structured prompt compiler
- Agent replay and context diff
- CLI command: `contextos`
- JSON export for graph, memory, and replay data
- GitHub-ready package structure

## Installation

Clone the project and install it locally:

```bash
git clone https://github.com/your-username/agent-context-os.git
cd agent-context-os
pip install -e .
```

For development and tests:

```bash
pip install -e ".[dev]"
pytest tests
```

## Quickstart

```python
from agent_context_os import ContextOS

ctx = ContextOS(provider="mock")

ctx.add_text(
    "OrbitGuard uses CelesTrak and LSTM for satellite collision prediction."
)

result = ctx.ask("Explain OrbitGuard architecture")

print(result.answer)
print(result.semantic_graph)
print(result.tokens_saved_percent)
```

Example output includes:

```text
OrbitGuard -> uses -> CelesTrak
OrbitGuard -> uses -> LSTM
```

## Using OpenAI

Set your API key:

```bash
export OPENAI_API_KEY="your-key"
```

Windows PowerShell:

```powershell
$env:OPENAI_API_KEY="your-key"
```

Then:

```python
from agent_context_os import ContextOS

ctx = ContextOS(provider="openai")
ctx.add_text("Agent Context OS converts documents into semantic graphs.")
result = ctx.ask("What does Agent Context OS do?")

print(result.answer)
```

The SDK uses the official `openai` Python package.

## Using FastRouter

Set your FastRouter environment variables:

```bash
export FASTROUTER_API_KEY="your-key"
export FASTROUTER_BASE_URL="https://api.fastrouter.ai/v1"
```

Windows PowerShell:

```powershell
$env:FASTROUTER_API_KEY="your-key"
$env:FASTROUTER_BASE_URL="https://api.fastrouter.ai/v1"
```

Then:

```python
from agent_context_os import ContextOS

ctx = ContextOS(provider="fastrouter")
ctx.add_text("OrbitGuard uses CelesTrak and LSTM.")
result = ctx.ask("Explain the architecture")

print(result.answer)
```

## Local Mock Mode

Mock mode works without API keys:

```python
ctx = ContextOS(provider="mock")
```

Use mock mode for:

- Local development
- Tests
- Demos
- Offline prototyping
- CI pipelines

## CLI Usage

After installation, use the `contextos` CLI:

```bash
contextos add path/to/file.txt
contextos ask "What is this project about?"
contextos graph
contextos replay
contextos export
```

You can select a provider:

```bash
contextos ask "Explain this project" --provider mock
contextos ask "Explain this project" --provider openai
contextos ask "Explain this project" --provider fastrouter
```

## Exporting Data

Export graph, memory, and replay data:

```python
ctx.export("contextos_export")
```

This creates:

```text
contextos_export/
├── semantic_graph.json
├── memory.json
└── replay.json
```

## Agent Replay

Every `ctx.ask()` creates a replay object with:

- Query ID
- Original token count
- Optimized token count
- Tokens saved percent
- Semantic facts retained
- Chunks retained
- Removed or ignored context summary
- Final prompt sent to the model
- Provider and model selected
- Timestamp
- Step-by-step timeline

Example:

```python
result = ctx.ask("Explain OrbitGuard architecture")

replay = ctx.get_replay(result.query_id)
print(replay.final_prompt)
print(replay.timeline)

all_replays = ctx.list_replays()
```

## Architecture

```text
Documents / Text
      |
      v
SemanticExtractor
      |
      |-- OpenAI extraction when OPENAI_API_KEY exists
      |-- FastRouter extraction when FASTROUTER_API_KEY exists
      |-- Mock extraction fallback
      v
GraphStore
NetworkX MultiDiGraph
      |
      +-------------------+
      |                   |
      v                   v
Semantic Facts       Document Chunks
      |                   |
      +---------+---------+
                |
                v
        ContextOptimizer
                |
                v
        PromptCompiler
                |
                v
        ModelRouter
      /     |       \
 OpenAI FastRouter Mock
                |
                v
        AskResult + Replay
```

## Token Optimization

Agent Context OS compares the full local memory against the optimized context used for the final model call.

Each result includes:

```python
result.original_tokens
result.optimized_tokens
result.tokens_saved_percent
```

The optimizer:

- Searches graph facts
- Searches document chunks
- Keeps relevant context
- Removes duplicate sentences
- Respects a token budget
- Summarizes ignored context in replay metadata

## Examples

Run examples from the project root:

```bash
python examples/quickstart.py
python examples/openai_example.py
python examples/fastrouter_example.py
```

## Package Structure

```text
agent-context-os/
├── agent_context_os/
│   ├── core.py
│   ├── models.py
│   ├── extractor.py
│   ├── graph_store.py
│   ├── context_optimizer.py
│   ├── prompt_compiler.py
│   ├── router.py
│   ├── replay.py
│   ├── tokenizer.py
│   ├── cli.py
│   └── llms/
├── examples/
├── tests/
├── README.md
├── pyproject.toml
├── .env.example
├── LICENSE
└── .gitignore
```

## Environment Variables

```env
OPENAI_API_KEY=
OPENAI_MODEL=gpt-4o-mini

FASTROUTER_API_KEY=
FASTROUTER_BASE_URL=https://api.fastrouter.ai/v1
FASTROUTER_MODEL=openai/gpt-4o-mini
```

## Testing

```bash
pytest tests
```

## License

MIT License

## Author

Created by **D Varsha** **Hemanth A N**.
```
