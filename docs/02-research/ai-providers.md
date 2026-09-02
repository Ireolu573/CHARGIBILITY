# AI Provider Research

> Living research document for the CHARGIBILITY project.
>
> Last reviewed: 2026-09-02

## Purpose

CHARGIBILITY is intended to route software-development tasks to the most suitable AI capability instead of hard-coding one model to one task. This document records provider capabilities, integration requirements, costs, limits, and trade-offs that will influence the routing architecture.

## Initial Findings

### OpenAI

- OpenAI provides API access through the Responses API and official SDKs.
- API access requires an API key.
- The API supports streaming, tool use, file/image inputs, and agent-oriented workflows.
- OpenAI has dedicated coding models in its current model catalog, including Codex-optimized models.
- For CHARGIBILITY, OpenAI is a strong candidate for coding, reasoning, tool use, and agent orchestration.

Source: OpenAI API documentation.

### Anthropic / Claude

- Anthropic provides the Claude API and SDKs for application integration.
- Claude is positioned for reasoning, analysis, coding, text, and visual inputs.
- Claude models are available through Anthropic's platform and also through cloud providers such as Amazon Bedrock.
- Current Claude offerings include models aimed at high-end reasoning/coding and faster, lower-cost workloads.
- For CHARGIBILITY, Anthropic is a candidate provider for coding, code review, planning, and complex reasoning.

Source: Anthropic developer documentation.

### Google Gemini

- Gemini provides a developer API with free and paid usage tiers.
- Current Gemini documentation lists models suitable for coding, reasoning, and agentic workloads.
- Gemini 2.5 Pro is explicitly described as strong for coding and complex reasoning.
- Gemini 2.5 Flash provides a large context window and a lower-cost/faster option.
- The free tier provides free input and output tokens for eligible models, subject to rate limits.
- For CHARGIBILITY, Gemini is a strong candidate for coding, reasoning, large-context project analysis, and lower-cost workloads.

Source: Google AI for Developers documentation.

### Ollama

- Ollama runs open models locally.
- Local execution can keep prompts and project data on the user's machine.
- Ollama can serve models to coding agents and allows models to be switched without changing the surrounding workflow.
- Local models avoid per-token cloud API charges, but performance depends on available hardware.
- For CHARGIBILITY, Ollama is important because it can provide a local/free provider option and a fallback when cloud APIs are unavailable or too expensive.

Source: Ollama official website.

## Early Architectural Observation

CHARGIBILITY should not define routing as:

```text
Frontend -> Claude
Backend -> Codex
Database -> Gemini
```

Instead, routing should be capability-based:

```text
Task
  -> required capabilities
  -> available providers/models
  -> constraints (cost, latency, privacy, context, availability)
  -> selected provider/model
```

This allows providers and models to change without rewriting the application's core routing logic.

## Questions Still To Research

- Exact API authentication and account requirements for each provider
- Current free-tier limits and restrictions
- Current model IDs and lifecycle/deprecation policies
- Tool/function calling differences
- Streaming differences
- Context-window differences
- Structured output support
- File and repository analysis capabilities
- Coding-agent capabilities versus raw model APIs
- Local model hardware requirements on the CHARGIBILITY development machine
- Additional providers worth supporting
- How to measure provider quality for different task types
- How CHARGIBILITY should handle provider failures, rate limits, and unavailable models

## Current Position

No provider is permanently assigned to a task category yet. The project will make provider selection a replaceable architectural concern and use research plus real experiments to determine routing rules.