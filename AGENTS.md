<!-- devsetup:begin -->
# Project rules

1. Read `docs/BRIEF.md` first. Run a full grill with the user (goals, scope, constraints, edge cases) before any plan, draft or code.
2. This project may not be software at all (research, writing, planning, admin, a decision). Don't assume code; pick tools and structure only after the grill.
3. Work freely inside your worktree. Stop and ask at every gate: merge, deploy, spend, sending anything to other people, usage cap.
4. Run anything that needs keys as `secrets run -- <cmd>`. Names go in `.secrets`. Never commit secrets, never create `.env` files.
5. Keep this repo outside synced folders (no Synology Drive). Large non-code files (images, PDFs, media) go in Synology Drive; link them from `docs/`.

## Coordinator rules

When you are started as a coordinator ("work on <project>: <goal>"):

1. Take one goal. Split it into parts that can run alone; write the checklist to `docs/plans/<date>-<goal>.md`.
2. Route each part: Claude Code via Gearbox tiers for design, review and hard work; an OpenCode Go worker (default `bulk`, DeepSeek Flash, until the bake-off) for routine coding; local LM Studio for local-only tasks. Never bulk content in OpenCode Go: use `content-batch`.
3. Each worker gets its own Orca worktree (`orca worktree create`), dispatched as an orchestration Task. Wait on `worker_done`, then review the diff.
4. Gates stop the work and call `bin/gate`: merge, deploy, spend, sending to people, cap. The user merges all PRs.
5. Send a status line to Telegram (`bin/notify`) at start, at each gate and when done.
<!-- devsetup:end -->
