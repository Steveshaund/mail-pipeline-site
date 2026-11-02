<!-- devsetup:begin -->
# Project rules

1. Read `docs/BRIEF.md` first. Run a full grill with the user (goals, scope, constraints, edge cases) before any plan, draft or code.
2. This project may not be software at all (research, writing, planning, admin, a decision). Don't assume code; pick tools and structure only after the grill.
3. Work freely inside your worktree. Stop and ask at every gate: merge, deploy, spend, sending anything to other people, usage cap.
4. Run anything that needs keys as `secrets run -- <cmd>`. Names go in `.secrets`. Never commit secrets, never create `.env` files.
5. Keep this repo outside synced folders (no Synology Drive). Large non-code files (images, PDFs, media) go in Synology Drive; link them from `docs/`.

## Coordinator rules

When you are started as a coordinator ("work on <project>: <goal>"):

1. Take one goal. Split it into parts that can run alone; write the checklist to `docs/plans/<date>-<goal>.md`. Create an Orca run: `orca orchestration run-create --objective "<goal>"`. With 2+ separable parts, make 2+ tasks.
2. Start every worker with `orca orchestration worker-start --spec <task> --worktree new-child --agent <claude|opencode> --model <id>`. Routine parts: `--agent opencode` (`--model opencode-go/deepseek-v4.1-flash`, the `bulk` model). Design, test and hard parts: `--agent claude`. Never do a worker part in your own worktree. Never bulk content in OpenCode: use `content-batch`.
3. Wait with `orca orchestration check --wait`. Review each diff, then merge the worker branch into yours.
4. Every gate (merge, deploy, spend, sending to people, cap) has two parts. The decision: `orca orchestration gate-create --task <id> --question "…" --options '[...]'`. The alert: `bin/gate <kind> "<text> — answer in Orca" --link <url>`. Then wait for gate-resolve; the user answers in Orca (desktop or mobile), never in Telegram.
5. For code: push your branch, `gh pr create`, then the merge gate with `--link <pr url>`. Never merge: the user merges all PRs.
6. Send a status line to Telegram (`bin/notify`) at start and when done.
7. Never commit `.claude/gearbox-log.jsonl`.
<!-- devsetup:end -->
