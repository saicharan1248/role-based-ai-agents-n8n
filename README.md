# Role-Based AI Agent Orchestration in n8n

## Overview

This repository documents the design and incremental build of a role-based AI agent system implemented using n8n. The system follows a supervisor to worker architecture and focuses on reliability, explicit control, and production-ready patterns rather than autonomous or self-replicating agent loops.

The project is intentionally design-first. Code, workflows, and diagrams will be added gradually as the architecture is validated.

---

## Problem Statement

Many AI agent implementations work well in demos but fail in real environments due to uncontrolled loops, unclear agent responsibilities, unrestricted tool usage, and lack of guardrails.

This project explores how n8n can be used as a deterministic orchestration engine, behaving like a state machine and job queue, instead of an AutoGPT-style autonomous loop.

---

## Design Goals

The primary goals of this project are:

* Explicit and user-selected agent roles
* Clear separation of responsibilities between agents
* Deterministic and inspectable execution
* Strong validation and safety boundaries
* Maintainability and observability over autonomy

---

## Core Architecture

The system is designed around the following components:

### Supervisor Agent

The supervisor agent is responsible only for orchestration logic. Its responsibilities include:

* Interpreting user input and selected role
* Selecting the appropriate agent specification
* Routing tasks to the correct worker workflow
* Enforcing permissions and execution boundaries

The supervisor does not execute business logic or tools directly.

---

### Worker Agents

Worker agents are implemented as pre-templated n8n sub-workflows. Each worker:

* Has a single, well-defined responsibility
* Accepts strictly validated inputs
* Produces structured outputs
* Uses only allowlisted tools

Worker agents do not call other agents or modify system state outside their scope.

---

## Role-Based Execution

Agent behavior is driven by explicit role selection. The same system can act in different roles, such as Chief, Financial Advisor, or Operations Agent, based on user input.

Role selection controls:

* The prompt and reasoning context
* The tools and workflows available
* Permission levels and approval requirements

Role switching is handled through configuration and state management, not autonomous reasoning.

---

## Planned MVP Scope

The initial MVP will include:

* Manual role selection through input or UI
* A supervisor workflow for task routing
* Three predefined worker agent workflows
* An agent registry storing role definitions, capabilities, and versions
* A hybrid model setup using API-based LLMs for supervision and local models for workers
* Basic guardrails including schema validation, timeouts, and approval gates

---

## Guardrails and Constraints

To ensure reliability and safety, the following constraints are enforced:

* No recursive agent calls
* No self-spawning workflows
* Strict JSON schema validation for all inputs and outputs
* Tool access restricted per agent role
* Human approval required for high-impact actions

These constraints are intentional and non-negotiable.

---

## What This Project Is Not

This project is not:

* An AutoGPT or autonomous agent loop
* A self-replicating AI system
* A fully autonomous decision-making platform

All behavior is explicitly defined and controlled.

---

## Current Status

This project is currently in the design phase. The focus is on validating architecture, constraints, and execution patterns before scaling implementation.

---

## Roadmap

* Define the agent registry schema
* Implement the supervisor workflow
* Build the first worker agent
* Demonstrate role switching
* Add evaluation and observability mechanisms

---

## Purpose of This Repository

The goal of this repository is to document practical agent orchestration patterns that can realistically be deployed and maintained in production environments.

---

## Contributions and Feedback

This is an exploratory project. Feedback on architecture, constraints, and design trade-offs is welcome.

---

## License

MIT License

---

Just tell me what you want to do next.
