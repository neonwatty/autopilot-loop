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

## After Two Real Trials

Use the current loop on two different project ideas before adding more infrastructure. For each trial, preserve the generated `.agent-loop` directory and note:

- What the scratchwork idea was
- How many iterations ran
- Which audit lenses produced useful work
- Which tasks were wrongly prioritized
- Where the state file was too thin or too noisy
- Which user decisions were needed
- Which verification commands mattered
- Why the loop stopped

After both trials, update this plugin in this order:

1. Tighten `skills/autopilot-loop/SKILL.md` where the agent needed more procedural guidance.
2. Revise the scoring and judge rubrics where task selection or stopping felt wrong.
3. Add CLI commands only for repeated state operations that were annoying or error-prone.
4. Consider MCP only if file-based CLI state blocked orchestration.

MCP is justified if the trials reveal a real need for concurrent worker coordination, cross-session supervision, remote loop execution, structured judge calls, or a live UI watching loop state. If the pain is mostly prompt quality or state shape, improve the skill and CLI first.

Process-level learnings that should inform future protocol changes live in
`skills/autopilot-loop/references/process-learnings.md`.
