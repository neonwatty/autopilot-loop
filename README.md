# Autopilot Loop

Reusable Codex plugin for turning a scratchwork idea into repeated build, audit, fix, verify, and judge iterations.

## What It Provides

- A Codex skill: `autopilot-loop`
- Durable project-local state in `.agent-loop/state.json`
- Task scoring and judge rubrics
- A small dependency-free CLI for initializing and updating loop state

## Use

From this repo:

```bash
node scripts/autopilot-loop.mjs init --dir /path/to/project --goal "Build the scratchwork idea"
```

Then ask Codex in the target project:

```text
Use the autopilot-loop skill. Continue from .agent-loop/state.json.
```

## CLI vs MCP

Start with the CLI. It is portable, inspectable, and works in any repo without a long-running service. Add MCP after the state model and iteration protocol stabilize.

MCP is the right later layer if the loop needs:

- Cross-session orchestration
- Multiple concurrent worker or judge agents
- A UI that watches loop state
- Remote execution
- Structured tool calls instead of file edits

The CLI is the right first layer for:

- Local project state
- Cheap smoke testing
- Git-friendly artifacts
- Avoiding premature protocol lock-in
