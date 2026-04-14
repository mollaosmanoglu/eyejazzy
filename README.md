<p align="center">
  <img src="docs/logo.png" alt="eyejazzy logo" width="200"/>
</p>

# eyejazzy

![Claude Code](https://img.shields.io/badge/Claude_Code-skill-8A63D2)
![License](https://img.shields.io/badge/license-MIT-blue)

Claude Code skill that measures engineering ownership. Do you steer the AI, or does it steer you?

## Visual Overview

<p align="center">
  <img src="docs/analysis-flow.png" alt="Analysis workflow" width="700"/>
</p>

## Install

```bash
# Clone into your Claude Code skills directory
git clone https://github.com/mollaosmanoglu/eyejazzy.git ~/.claude/skills/eyejazzy
```

## Usage

```bash
# Analyze 10 most recent sessions across all projects
/eyejazzy:analyze

# Analyze current session only
/eyejazzy:analyze this

# Analyze all sessions for current project
/eyejazzy:analyze project

# Analyze last N sessions
/eyejazzy:analyze last 5

# Analyze sessions matching a project name
/eyejazzy:analyze bivium
```

## What It Measures

Parses Claude Code session logs (`~/.claude/projects/*.jsonl`) and classifies every user message that follows an assistant response:

- **Steers** — You corrected, redirected, or added new requirements
- **Accepts** — You approved, confirmed, or let it continue

**Steering Ratio** = Steers / (Steers + Accepts)

| Grade | Ratio      | Interpretation                               |
| ----- | ---------- | -------------------------------------------- |
| A     | 80-100%    | You drive. AI is the tool.                   |
| B     | 60-79%     | Balanced collaboration.                      |
| C     | 40-59%     | AI leads, you steer occasionally.            |
| D     | 0-39%      | You're along for the ride.                   |

## Why It Matters

High steering ratio = you maintain context, think critically, catch mistakes.
Low steering ratio = you accept without judgment, lose architectural coherence.

This skill reveals your engineering posture, not just code output.

## Tech Stack

| Component | Tools                                 |
| --------- | ------------------------------------- |
| Platform  | Claude Code skill framework           |
| Format    | JSONL session log parsing             |
| Tools     | Read, Bash, Grep, Glob (no LLM calls) |
| Language  | Shell scripting via skill DSL         |

## Example Output

```
Session: bivium (2026-04-14)
Messages analyzed: 47
Steers: 32 (68%)
Accepts: 15 (32%)
Grade: B

Top steering moments:
- "No, use Gemini Flash not GPT-4" (redirected model choice)
- "Coverage dropped, add the patch function back" (caught regression)
- "Make leader field mandatory" (enforced data constraint)
```

## License

MIT
