# Ollama Research

> Living research document for the CHARGIBILITY project.
>
> Last reviewed: 2026-09-03

## What Is Ollama?

Ollama is a local AI runtime that lets applications run supported open models on the user's own computer. It is available on Linux, macOS, and Windows.

For CHARGIBILITY, Ollama matters because it can provide a local AI provider without requiring every request to go to a cloud API.

## API

Ollama exposes a local HTTP API. Its chat endpoint can receive conversation messages and supports optional tools, structured output, streaming, thinking controls, and other generation options.

The default local API is available at:

```text
http://localhost:11434
```

This means CHARGIBILITY can communicate with Ollama as a normal backend service rather than treating it as a separate desktop application.

## Tool Calling

Ollama supports function/tool calling. A model can request a tool, CHARGIBILITY can execute that tool, and the result can be returned to the model for continued reasoning.

This is important for the eventual CHARGIBILITY agent architecture because tools could include operations such as:

- Read a project file
- Search the project
- Write a file
- Run a command
- Run tests
- Inspect Git status
- Inspect database information

The actual tool permissions will need to be designed carefully before implementation.

## OpenAI Compatibility

Ollama provides compatibility with parts of the OpenAI API. Its documentation lists support for chat completions, streaming, JSON mode, vision, tools, and reasoning controls. Ollama also supports the OpenAI Responses API in a non-stateful form.

This is particularly valuable for CHARGIBILITY. It suggests that our provider abstraction can normalize different providers while Ollama can often be accessed using familiar OpenAI-style client patterns.

## Local AI Role in CHARGIBILITY

Our current position is not to assign Ollama permanently to frontend, backend, or database work.

Instead:

```text
Claude  -> Frontend
Codex   -> Backend
Gemini  -> Database
Ollama  -> Local AI option
```

Ollama can later be used for:

- Local development and experimentation
- Private project analysis
- Offline or limited-connectivity work
- Lower-cost tasks
- Fallback when a cloud provider is unavailable
- Specialized local agents

## Important Trade-off

Ollama avoids cloud API token charges, but the user pays in local computing resources. Model quality, speed, context size, and practical usability depend heavily on the hardware and the selected model.

Therefore, we need to benchmark candidate models on the actual CHARGIBILITY development machine instead of choosing a model only from online benchmarks.

## Research To Do

- Identify coding-focused models that can run locally.
- Compare 3B, 7B, 14B, and larger model sizes where practical.
- Measure RAM usage.
- Measure generation speed.
- Measure context handling.
- Test tool calling.
- Test structured output.
- Test code editing workflows.
- Determine whether the development machine can run a useful model alongside the CHARGIBILITY development stack.
- Determine which local tasks should use Ollama first.

## Current Evidence

Ollama's official documentation confirms local API access, streaming, tool calling, and OpenAI-compatible interfaces. The next stage is an actual hardware/model experiment.

Source: Ollama official documentation.
