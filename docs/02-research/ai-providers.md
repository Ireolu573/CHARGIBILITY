# AI Provider Research

> Living research document for the CHARGIBILITY project.
>
> Last reviewed: 2026-09-03

## Purpose

CHARGIBILITY is intended to route software-development tasks to specialized AI providers. The project will begin with a deliberate provider assignment while keeping the provider layer replaceable so models can change later without rewriting the application.

## Initial Routing Strategy

For the first version of CHARGIBILITY, the working assignment is:

```text
Frontend -> Claude
Backend  -> Codex
Database -> Gemini
Ollama   -> Local AI option
```

This is an initial product decision, not a permanent claim that these providers are always the best at these tasks.

Ollama remains part of the equation because it gives CHARGIBILITY a local model path for development, experimentation, fallback use, and potentially specialized tasks.

## Current Provider Findings

### OpenAI / Codex

OpenAI provides API access through its developer platform. Current OpenAI documentation lists dedicated Codex models optimized for agentic coding. GPT-5.3-Codex is described as an agentic coding model and supports configurable reasoning effort, a 400K context window, and up to 128K output tokens.

For CHARGIBILITY:

- Primary role: Backend
- Strong fit: software implementation, debugging, reasoning, repository-oriented coding workflows
- Research priority: API authentication, Codex-specific agent capabilities, tool execution, project context, cost, and rate limits

Source: OpenAI developer documentation.

### Anthropic / Claude

Anthropic provides the Claude API and current Claude models for coding, reasoning, analysis, and agentic workloads. Anthropic's current documentation also provides guidance specifically for coding and frontend tasks and supports tool use for agentic workflows.

For CHARGIBILITY:

- Primary role: Frontend
- Strong fit: frontend implementation, UI work, code review, reasoning, and design-oriented coding workflows
- Research priority: API access, model selection, tool use, context limits, coding performance, cost, and rate limits

Source: Anthropic developer documentation.

### Google Gemini

Google provides the Gemini API with current models for coding, reasoning, multimodal work, and agentic workflows. Gemini 2.5 Pro is explicitly described as a model for complex tasks with deep reasoning and coding capabilities. Google's current documentation also lists newer Gemini models for long-horizon software engineering and agentic workflows.

Google identifies the Interactions API as the default interface for new Gemini projects. Gemini 2.5 and newer models also support implicit context caching.

For CHARGIBILITY:

- Primary role: Database
- Strong fit: SQL generation, schema reasoning, database analysis, migrations, and large-context technical analysis
- Research priority: API authentication, free-tier limits, structured output, tool use, context limits, caching, cost, and rate limits

Source: Google AI for Developers documentation.

### Ollama

Ollama runs open models locally and exposes a local API. Its chat API supports streaming, structured JSON/JSON Schema output, and tool calling. Ollama also provides OpenAI-compatible endpoints, which is useful for CHARGIBILITY because a common provider interface can potentially support both cloud providers and local models.

For CHARGIBILITY:

- Role: Local AI provider
- Strong fit: private/local work, experimentation, fallback use, low-cost development, and tasks that do not require the strongest cloud model
- Research priority: suitable coding models, RAM/CPU requirements, model size, context limits, tool calling, latency, and performance on the development machine

Source: Ollama official documentation.

## Architectural Principle

The initial routing strategy is intentionally simple, but the implementation should still use a provider abstraction.

Conceptually:

```text
User request
    -> task classification
    -> initial task route
    -> provider adapter
    -> model
    -> result
```

The provider adapter prevents the rest of CHARGIBILITY from depending directly on one vendor's API format.

Later, routing can evolve toward:

```text
Task
  -> required capabilities
  -> initial preferred provider
  -> available providers/models
  -> constraints
  -> selected provider/model
```

Possible constraints include cost, latency, privacy, context size, availability, and model capability.

## Research Questions

- What account and API-key requirements apply to each provider?
- Which models should CHARGIBILITY use initially?
- Which providers have meaningful free usage?
- What are the current rate limits?
- How do streaming implementations differ?
- How do tool/function calling implementations differ?
- How should project files be supplied to each provider?
- How should CHARGIBILITY protect API keys?
- What can Ollama realistically run on the development machine?
- How should provider failures and rate limits be handled?
- How should we evaluate the three primary providers against real CHARGIBILITY tasks?

## Current Position

The working assignment is:

```text
Frontend -> Claude
Backend  -> Codex
Database -> Gemini
Ollama   -> Local AI option
```

This assignment will guide the first research and prototype experiments. It can be revised later based on measured results, cost, availability, and user experience.
