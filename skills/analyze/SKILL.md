---
name: analyze
description: Analyze your Claude Code sessions to answer one question — do you drive, or does AI drive you? Run /eyejazzy:analyze
disable-model-invocation: true
allowed-tools: Read Bash Grep Glob
---

# eyejazzy

One question: **do you steer the AI, or does it steer you?**

## Scope

Parse `$ARGUMENTS` to determine what to analyze:

| Invocation | What to analyze |
|---|---|
| `/eyejazzy:analyze` | 10 most recent sessions across all projects |
| `/eyejazzy:analyze this` | Current session only (the JSONL for the active session in cwd) |
| `/eyejazzy:analyze project` | All sessions for the current project directory |
| `/eyejazzy:analyze last 5` | The N most recent sessions |
| `/eyejazzy:analyze defter` | Sessions matching a project name |

## Find the logs

Session logs live in `~/.claude/projects/` as JSONL files. Each subdirectory
is named after the project path (dashes replace slashes).

```bash
# Most recent sessions across all projects
find ~/.claude/projects/ -name "*.jsonl" -not -name "agent-*" -type f -exec stat -f "%m %N" {} \; | sort -rn | head -10

# Sessions for current project only
ls -lt ~/.claude/projects/-$(echo "$PWD" | tr '/' '-' | cut -c2-)/*.jsonl | head -10

# Match a project name
find ~/.claude/projects/ -path "*defter*" -name "*.jsonl" -not -name "agent-*" -type f
```

For "this" scope, find the JSONL matching the current sessionId in the
current project directory.

## Parse

Each line is a JSON object. Explore the first few lines to learn the schema —
don't assume. Look for user messages, assistant messages, and tool calls.

## Measure: Steering Ratio

Scan every user message that follows an assistant response. Classify it:

**Steers** — user redirects, rejects, refines, questions, or constrains:
- "no, do X instead"
- "wait, what about..."
- "why did you..."
- "actually, let's..."
- "change X to Y"
- Adds constraints Claude missed
- Questions a choice

**Accepts** — user approves without modification:
- "ok" / "looks good" / "great" / "thanks" / "continue"
- Moves to next task without reviewing

**Neutral** — ignore these (new tasks, commits, questions about existing code).

**Steering ratio** = steers / (steers + accepts)

| Ratio | Grade | Meaning |
|---|---|---|
| > 40% | A | You drive, AI assists |
| 25–40% | B | You review and adjust |
| 15–25% | C | You accept more than you should |
| < 15% | D | AI is driving |

## Report

```
# eyejazzy

**Sessions:** {N} · **Period:** {dates}

## Steering: {Grade} — {X}%

{One sentence: what this means for them.}

### Examples from your sessions

{3 specific examples. Quote their actual messages — show steers AND accepts.
Name the files and context. This is the value — the mirror.}

### Your strongest move
{The single best steer you found. Reinforce it.}

### One thing to try
{One specific, actionable change based on what you saw. Not generic.}
```

## One rule

Be honest. A passive user gets a D. Honesty is the product.
