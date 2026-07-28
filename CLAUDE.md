# cubs-dashboards

Guidance for Claude Code sessions in this repo. Project specifics (stack, architecture,
conventions) are not documented here yet — add them as they stabilize.

## Terminal commands for Steve (Windows / PowerShell 5.1)

Any command handed to Steve to run must be a **single paste-and-run block** — he pastes it
verbatim and it works, with no editing and no assumed starting directory.

- **Fence it ```bash, not ```powershell.** The contents are still PowerShell; the `bash` tag is
  only there because the Claude Code app renders a **Run** button on bash-tagged blocks. Verified
  2026-07-28: the Run button executes in Windows PowerShell 5.1, so the tag is cosmetic.
- **Start with `Set-Location 'C:\Users\srshi\projects\cubs-dashboards'`** — full absolute path, quoted. Never assume a
  working directory, never `cd ~/...`, never relative paths.
- **One block per task, not per step.** Chain everything (venv activate, `$env:` vars, installs,
  the actual command) with `;` inside one fence. Multiple fences = multiple pastes = a missed step.
- **PowerShell 5.1 syntax only:** `;` never `&&` or `||`; no ternary `? :`, no `??`, no heredocs,
  no `/dev/null`, no `export VAR=`. 5.1-safe also runs in pwsh 7, so it is always the right target.
- **Secrets Steve must supply** go as a clearly marked placeholder line at the top of the block:
  `$env:TOKEN = 'PASTE_TOKEN_HERE'`.
- Explanation goes in prose above or below the block — never as the only place a required command
  appears, and never as inline comments he would have to strip.

Applies to commands *handed to Steve*. Claude's own Bash/PowerShell tool calls run in a separate
pwsh 7 sandbox and may use POSIX or 7+ syntax freely. Source of truth is the global
`~/.claude/CLAUDE.md`; this copy exists so cloud and scheduled sessions (which do not load the
local global file) get the rule too.
