# openASiC master orchestrator

These instructions apply only to an explicitly requested orchestration run.
Prepare an ignored local copy with `python3 scripts/prepare-orchestrator.py`.
Keep private checkpoints in `tmp/orchestrator-state.md`; never commit ticket
identifiers, credentials, local paths, or private documents.

## Mission and prerequisites

Act as one coordinator for bounded openASiC work. Read `AGENTS.md`, `README.md`,
`CONTRIBUTING.md`, `SECURITY.md`, `docs/architecture.md`, `docs/roadmap.md`, and
`docs/testing.md`. Read [runner setup](factory.md) and the installed Factory
protocol before claims. No runnable ticket or tracker registration is implied
by the scaffold. Do not start workers simply because this file exists.

Confirm the checkout and remote, preserve local changes, and verify authenticated
GitHub and private tracker routing. Reconcile live claims and any checkpoint;
resolve coordinator ownership before claiming. Verify current `develop` CI and
the required tools. No unattended dispatcher or service is configured.

Use an installed `factory-work` skill when explicitly running that workflow.
Keep manual `report_only: true` mode and obey the actual host registry. If the
protocol disallows a requested claim in that mode, explain the conflict; never
bypass it or change dispatch mode silently.

## Queue and ownership

Read each eligible unassigned `Todo` issue labelled `ai:agent-ready`, including
its dependencies. Require Problem & Context, Acceptance Criteria, Source File
Pointers, Owned Paths, and Verification Command. Unresolved profiles and source
contracts need specification, not invented implementation. The first discovery
should specify one ASiC-E/XAdES profile as described in the roadmap; confirm an
actual ready issue exists before acting. An empty queue is a terminal outcome.

Claim through the configured protocol, immediately re-read ownership, and skip
lost races. Use one isolated worktree and one `codex/<public-safe-slug>` branch
per issue from current `origin/develop`. Start with one implementation worker;
never exceed host concurrency. Workers never merge. Give each the complete
issue, exact worktree, owned paths, checks, boundaries, and instructions that
others share the codebase: preserve their changes and do not revert them.

Use the installed skill's worker-model routing where available. Reserve capable
implementation and independent review agents for substantive work; use bounded
read-only exploration for specific questions. Do not spawn agents only to wait
for CI. Respect host concurrency and keep heavy compilation serial if needed.

Workers heartbeat the private tracker at each phase change and at least every
20 minutes. On a blocker, preserve work, identify the exact missing evidence or
decision, and update the tracker state; never leave stalled work In Progress.
The coordinator rechecks dependencies and ownership before refilling a slot.

Separate follow-ups into private Triage issues. Do not expand scope to refactor
openSzigno, implement KRX, or add correspondence workflows. No service accounts,
provider onboarding, releases, or external notifications are implied.

## Verification and review

Run the issue's exact checks and the full baseline:

```sh
./scripts/check.sh
cargo build --release --locked
cargo run --locked -p openasic-cli -- capabilities --json
```

Do not weaken checks or advertise planned capabilities. Discovery work needs
source and claim review; document code and interoperability tests only when
performed. Keep private issue mappings in the tracker. Public commits and PRs
must not include private tracker identifiers, links, or maintainer-local paths.
Use Conventional Commits and PRs targeting `develop`.

Before moving a ticket to `In Review`, post a private structured handoff:

```text
## Handoff
- PR: <public PR URL>
- Verification: <exact ticket command> — pass, <result summary>
- UX critique: required — SHIP | skipped — <specific reason>
- Files: <count changed>, all within Owned Paths; explain any exception
- Risks: <review priorities or none known>
```

Include acceptance evidence and the reviewed head commit. Apply the review
state and `ai:needs-review`, removing `ai:in-progress`. A PR is not Done.
Keep this handoff in the private tracker, not in public GitHub comments.

For a materially changed user flow, request an independent UX assessment after
verification with the exact worktree and launch command. Resolve in-scope
recovery/usability findings. Record a justified skip for research-only work.

Require an independent reviewer with the issue, owned paths, complete diff,
and verification evidence. Act on MERGE, FIX, or ESCALATE findings. Wait for all
applicable CI at the reviewed commit, resolve conflicts, and re-review changes.
Stop after two unsuccessful fix rounds with a concrete explanation.

Use `factory-merge-reviewer` when available, otherwise a separate read-only
review agent. Green CI never substitutes for reviewing the complete diff.
Wait on the actual workflow using `gh run watch --exit-status`. After failure,
delegate minimal log diagnosis to `factory-ci-doctor` or a read-only specialist;
classify ticket, environment, or transient failure before deciding to retry.
New commits require fresh check evidence and review of the changed diff.

Only the coordinator merges, serially, within the session's authorization.
Recheck the reviewed commit, base, CI, and ownership. Never bypass protection.
Wait for post-merge `develop` CI before marking Done. `master`, releases,
credentials, destructive actions, and security-boundary changes need explicit
human review. No deployment smoke check exists for this scaffold.

Require all applicable CI and Security checks at the reviewed head, including
PR-only hygiene. Factory's eight-check CI fallback covers unconditional push
jobs only; it does not replace the full PR gate. Conditional skipped jobs need
an explicit non-applicable workflow condition, not an assumption of success.

After each merge, wait for CI and Security on the resulting `develop` commit.
If either fails, stop further merges immediately, delegate diagnosis, and
prepare a scoped reviewed fix before resuming. Never mark a red merge Done or
discard another contributor's work while recovering.

## Checkpoint and stop

Record phase, claims, worktrees, PRs, reviewed commits, CI state, blockers, and
next action in the ignored checkpoint. Never store secrets or private inputs.
Stop when the queue is exhausted, evidence or authorization is missing, or two
consecutive tasks fail for environment reasons. Do not poll indefinitely.
Report completed, PR-open, blocked, and skipped work with verification evidence.
Only notify through the current operator session and configured private tracker;
external chat or email needs explicit authorization.
