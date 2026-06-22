# GM91 — Blake Heartbeat Loop & Ritual

How Blake autonomously maintains this repo from GitHub Issues. This is the contract for the in-session
polling loop and the ritual run after every issue.

## TL;DR for Bala
1. **You** open a GitHub Issue describing a task (anything — a page, a fix, a tweak).
2. **Blake's loop** polls the repo, picks up any open issue that isn't already in-flight or done.
3. Blake builds it on a branch, previews locally, and runs the **ritual** below.
4. You get a **Slack DM** + an issue comment, the issue is moved to `awaiting-review` and assigned to you.
5. **Nothing goes live without your say-so.** Blake never pushes to `main` or deploys on its own.

## Repo
- `bala91px/gm91` · GitHub Pages auto-deploys from `main` (so `main` = production — handled carefully).
- Pages: `index.html` (in-person pitch, long-form) · `audit.html` (cold-traffic CRO ad landing page).

## Task state — driven by labels (single source of truth)
| Label | Meaning |
|---|---|
| *(no Blake label)* | New task — eligible for the loop to claim |
| `in-progress` | Blake is actively working it (claimed) |
| `awaiting-review` | Done by Blake — waiting on Bala's review |
| `blake-done` | Reviewed & approved by Bala (Bala sets this) |

The loop is **idempotent**: it only claims open issues with none of the above labels. This means it never
double-works an issue and is safe to run repeatedly.

## Kanban board sync (GitHub Projects)
There is a Projects v2 board — **"@bala91px's Growth machine"** (project #1) — linked to the repo, with a
**Status** field: `Backlog → Ready → In progress → In review → Done`. Every label move must be mirrored on
the board so the card reflects reality.

**Label → board Status mapping:**
| Label | Board Status |
|---|---|
| `in-progress` | In progress |
| `awaiting-review` | In review |
| `blake-done` | Done |

**Requires the `project` write scope** on the active gh token (read-only `read:project` is NOT enough —
moving a card fails with `missing required scopes [project]`). One-time grant by Bala:
`gh auth refresh -s project -h github.com`. (See LESSON 032.)

IDs for `gh project item-edit` (project `PVT_kwHODtMqjM4BbRc9`, Status field `PVTSSF_lAHODtMqjM4BbRc9zhWDGK4`):
`Backlog f75ad846 · Ready 61e4505c · In progress 47fc9ee4 · In review df73e18b · Done 98236657`. Resolve an
issue's item id via `gh project item-list 1 --owner bala91px --format json`.

## The Loop (in-session heartbeat)
- Mechanism: Claude Code `/loop`, self-paced (≈ every few minutes while a session is open).
- Each tick:
  1. `gh issue list --repo bala91px/gm91 --state open --json number,title,labels,assignees`
  2. Filter to issues with no `in-progress` / `awaiting-review` / `blake-done` label.
  3. If none → idle, check again next tick.
  4. If one+ → take the lowest number, label it `in-progress` (and move its board card to **In progress**), and work it (see Ritual).
- The loop runs while a Claude Code session is open. (A future always-on cloud watcher can ping Bala 24/7;
  not enabled yet — see CLAUDE.md.)

## The Ritual (run after every issue)
1. **Plan → build on the working branch** (never commit straight to `main`).
2. **Orchestrate** as needed: Kevin (research), Ben (production code + security review), Blake (architecture + integrate).
3. **Local preview** (`python3 -m http.server 8091`) + Playwright verify (desktop + mobile + key interactions).
4. **Commit** to the branch with a clear message. **Do not push to `main` or deploy.**
5. **Comment on the issue**: what was built, how it was verified, screenshots/preview notes, and any
   placeholders Bala must fill (keys, numbers, IDs).
6. **Relabel**: remove `in-progress`, add `awaiting-review`. **Assign the issue to Bala.** Also **move the
   board card** to the mapped Status (see Kanban board sync) — `in-progress`→In progress on claim,
   `awaiting-review`→In review on handoff, `blake-done`→Done on Bala's approval.
7. **Notify Bala on Slack** (DM fallback — `#blake-inbox` not created yet).
8. **Log to Obsidian**: write `SESSION-LOG-YYYY-MM-DD.md` under
   `02 — Blake-Genesis/sessions/`. If anything was learned/corrected, append a lesson to
   `02 — Blake-Genesis/lessons/lessons.md` as `PROPOSED — awaiting Bala`.

## Guardrails (non-negotiable)
- **No auto-deploy / no push to `main` without Bala's explicit approval.** Pages deploys from `main`, so a
  push *is* a deploy — gated.
- **No secrets in the repo.** Form keys, GA4 IDs, WhatsApp numbers stay as placeholders until Bala provides them.
- **Security-sensitive code → Ben reviews** before `awaiting-review`.
- **Honest content only** — no fabricated testimonials/metrics; proof must be real or clearly marked for Bala to fill.

## Review handoff (Bala's side)
- Review the issue + preview. If good → set `blake-done` and tell Blake to push/deploy.
- If changes needed → comment on the issue and remove `awaiting-review`; the loop will pick it back up.
