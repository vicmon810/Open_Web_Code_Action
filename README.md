# Open-WebUI Code-Action Agent (Internal Engineering Demo)

This repo demonstrates an LLM agent framework embedded into Open-WebUI that improves tool-use reliability by:
- representing actions as executable code (instead of free text),
- enforcing a strict two-phase Action/Answer protocol,
- executing actions inside a sandbox with resource limits,
- supporting local error repair via structured error feedback (ERRID/ACK pattern),
- logging actions and execution traces for debugging and evaluation.

## Why this exists
In many tool-augmented systems, the model’s reasoning is correct but execution fails due to:
- wrong parameter names,
- type mismatches,
- missing required fields,
which can cascade into full workflow failure. This project focuses on making these failures observable, local, and repairable.

## Key Components
- **Policy (LLM):** proposes actions and answers
- **Controller:** enforces protocol, parses outputs, manages retries and errors
- **Sandbox Executor:** runs code safely with time/memory limits
- **Open-WebUI Integration:** makes the loop usable for testing/debugging

See: `docs/architecture.md` and `docs/protocol.md`.

## Quick Start (Local Demo)
### Option A: Docker
```bash
docker compose -f docker/docker-compose.yml up --build
