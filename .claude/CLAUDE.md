<instructions>
- Clarify the task briefly, then make the change.
- Prefer small, focused edits over large rewrites.
- This is a Claude Code plugin (markdown-only, no code). Changes are to SKILL.md and plugin.json.
- Scope issues to ~1-2 commits.
</instructions>

<heuristics>
- Via negativa: subtract before you add. When facing a problem, first ask what
  can be removed. Only add when removal alone cannot solve it — addition has
  unseen feedback loops, subtraction is robust.
- Lindy: prefer tools, libraries, and patterns that have survived longest.
  New doesn't mean better; unproven means fragile.
- Less is more: always pick the simplest solution. Complexity is debt with
  compound interest.
- Convexity: prefer designs where failure is contained and success compounds.
  Small reversible steps over big irreversible commitments.
- Optionality: present all options first before committing to a path.
- YAGNI: add only what is needed now.
- One reason: if you need more than one reason to justify a decision, don't do
  it. Real conviction needs no backup arguments. Multiple reasons signal
  rationalisation, not clarity.
- Catalogue negative results: when an approach fails, record what and why in
  <negative_results> below. Negative knowledge is durable — what failed won't
  unfail.
</heuristics>

<forbidden>
- No "just in case" abstractions.
- No mixing unrelated responsibilities.
- No premature optimisation or over-generalisation/engineering.
- No UI components outside of shadcn and Motion. No custom components, no other libraries.
- No code unless absolutely necessary. This plugin is markdown-driven.
</forbidden>

<validation>
Test by running: claude --plugin-dir /Users/Faruk/Desktop/projects/eyejazzy
Then invoke /eyejazzy:analyze to verify.
</validation>

<commits>
Use Conventional Commits (https://www.conventionalcommits.org):
  feat:     new feature or functionality
  fix:      bug fix
  refactor: restructure without behaviour change
  chore:    maintenance, deps, config, gitignore, etc.
  docs:     documentation only
  test:     adding or updating tests
  build:    build process or dependency changes
  ci:       CI/CD config changes
  perf:     performance improvement
  style:    formatting only (whitespace, semicolons)
  revert:   revert a previous commit

Format: <type>(<optional scope>): <description>
Example: feat(globe): add camera fly-to animation
</commits>

<cli_tools>
- `gh`: Issues and PRs. `gh issue list`/`create`/`view`. Labels: `bug`, `feature`, `question`.
- `npx shadcn@latest`: UI component scaffolding. `npx shadcn@latest init` to set up, `npx shadcn@latest add <component>` to add components. Runs inside `src/frontend/`.
- `render`: Deploy and tail production logs. `render deploys`, `render logs`.
- `px`: Phoenix CLI. `px traces --endpoint http://localhost:6006 --project defter --limit 5` lists recent traces. `px trace <trace-id> --endpoint ... --project defter` shows span tree. Add `--format json` for tool inputs/outputs.
- `docker compose`: Local dev environment (redis, phoenix, api, worker, ngrok).
- `notion`: Notion To-Do board. `notion db query <db-id>`, add --filter when needed.
- `tvly`: Web search and research. `tvly search`, `tvly extract`, `tvly research`.
- `himalaya`: Email via Fastmail. `himalaya envelope list`, `himalaya message read <id> --no-headers`, `himalaya message write`. Folders via `--folder Archive` (also: Drafts, Sent, Spam, Trash).
- `osascript`: Apple Calendar & Reminders via AppleScript. Calendar "Work" for events. Build dates programmatically (Dutch locale — string dates don't parse).
</cli_tools>
