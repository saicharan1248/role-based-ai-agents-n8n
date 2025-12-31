Role-Based AI Agent Orchestration in n8n
Overview

This repository documents the design and incremental build of a role-based AI agent system implemented in n8n, using a supervisor → worker architecture.

The goal is to explore production-grade patterns for AI agents that prioritize:

determinism

explicit role control

strict boundaries

operational reliability

This is a design-first project. Code and workflows will be added incrementally.

Problem Statement

Many AI agent implementations fail in real environments due to:

unbounded loops

unclear agent responsibilities

uncontrolled tool access

lack of observability and guardrails

This project explores how n8n can be used as a state machine and job orchestrator, rather than an AutoGPT-style loop.

Core Design Principles

Explicit roles (no implicit behavior)

Supervisor agent handles only:

task decomposition

role selection

workflow routing

Worker agents are:

pre-templated n8n sub-workflows

strictly validated via JSON schemas

limited to allowlisted tools

No recursion

No self-spawning workflows

Planned MVP Scope

Manual role selection (e.g. Chief, Financial Advisor, Ops)

Supervisor workflow for routing and orchestration

Predefined worker workflows with strict inputs/outputs

Agent registry (role, capabilities, permissions, versions)

Hybrid LLM setup:

API-based model for supervision

Local models for workers

Guardrails:

schema validation

timeouts

approval gates for high-impact actions

What This Project Is NOT

Not an AutoGPT clone

Not a self-replicating agent system

Not a fully autonomous AI platform

All automation is explicit and bounded by design.

Current Status

🚧 Design phase

Initial architecture, schemas, and workflow templates will be added step by step.

Roadmap

 Agent registry schema

 Supervisor workflow design

 First worker agent (Financial Advisor)

 Role-switching demo

 Evaluation and guardrails

Why This Exists

The intention is to learn, validate, and share practical agent orchestration patterns that actually hold up under real operational constraints.

Contributions / Feedback

This is an exploratory project.
Architectural feedback and real-world lessons are welcome.

License

MIT
