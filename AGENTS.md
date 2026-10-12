# AGENTS.md

Rules for every AI agent working in this repository. Read this file and `Agent-Feedback.md`
in full before starting any task.

The Skylyx company rules also apply: `rules.md`, `how-we-work.md` and `flight-safety.md` in
Skylyx Hub. Where they disagree with this file, this file wins for work in this repository.

## 1. Don't assume. Ask.

- If the request, the code or a company page does not answer a question, stop and ask.
  Do not fill the gap with what sounds likely.
- Ask before anything that changes behaviour, scope, data, public interfaces or is hard to
  undo. Small internal choices (a variable name, a helper's location) follow the
  surrounding code; you do not need to ask about those.
- When you ask, say what you checked, what is still unknown, and what options you see.
- Never report something as done, tested or working unless you checked it. Say plainly
  which checks you did not run.

## 2. Never work on `main`

- Never commit to `main`, never push to `main`, never rebase or reset `main`.
- If you find yourself on `main`, stop and create a worktree (below) before changing anything.

## 3. One feature, one worktree

Every feature or fix I ask for gets its own git worktree and branch:

```bash
git fetch origin
git worktree add ../<repo>-worktrees/<branch-name> -b <branch-name> origin/main
```

- Branch names: `feature/<short-name>` for features, `fix/<short-name>` for bug fixes.
- Do all the work for that feature inside its worktree. Do not mix two features in one
  worktree or one branch.
- Stage files by path (`git add path/to/file`). Never `git add -A` or `git add .`.
  Never commit or revert a file you did not touch.
- If the repository has submodules, use `--recurse-submodules`, and never commit a
  submodule pointer to a commit that has not been pushed.

## 4. Open a PR when the feature is done. Never merge.

- When the feature is finished, push its branch and open a pull request against `main`.
  This standing instruction is my yes for pushing the feature branch and opening the PR.
  It does not cover anything else (merging, deploying, posting elsewhere).
- **Never merge a PR, never enable auto-merge, never close someone else's PR.** I merge.
- The PR description must include:
  - **What changed and why**
  - **How to run it**, and what to click or do to see it working
  - **What was tested**, and **what was not tested**
  - **Screenshots** if anything visual changed (section 5)
  - **Agent feedback**: any entries you added to `Agent-Feedback.md` (section 7)
- A bug fix comes with a test that fails without the fix.

## 5. Visual changes need screenshots

- Any PR that changes anything visible (layout, colours, text, icons, a new screen,
  a dialog, an animation) must have screenshots attached to the PR as proof.
- Show **before and after** for every screen or state the change touches, including
  error and empty states if the change affects them.
- If you cannot take a screenshot (no device, needs an aircraft connected, etc.), do not
  open the PR as if it were complete: say so at the top of the PR description, list
  exactly which screens need checking, and ask me.

## 6. No code file over 2000 lines. Ever.

- No source code file may be longer than 2000 lines.
- If a change would take a file past 2000 lines, first split the file into smaller,
  well-named modules in a separate commit, then make the change.
- If a file is already over 2000 lines, do not make it longer. Tell me, and propose how to
  split it.
- Exempt: generated files, lock files, vendored third-party code and data files (JSON,
  CSV, etc.). If you are unsure whether a file is exempt, ask.

## 7. Agent-Feedback.md

If you notice something every future agent should know (a trap in the code, a convention
nobody wrote down, a rule that is missing from this file, a rule here that is wrong),
write it in `Agent-Feedback.md`.

- **Do not edit `AGENTS.md` yourself.** I read the feedback and decide what moves in here.
- Add entries at the top of `Agent-Feedback.md`, using the format in that file.
- Commit the entry in your feature branch, and list it under "Agent feedback" in the PR
  description so I see it even before the PR is merged.
- One entry per finding. Be specific: file paths, commands, what happened.

## 8. Working across macOS and Windows

- Refer to files by path inside the repository, never by an absolute path.
- Scripts must run under bash on macOS and under Git Bash on Windows. Avoid GNU-only flags.
- Do not assume `python3` exists on Windows; check for it.
- Secrets go in a git-ignored `.env` file. Never commit secrets, keys or certificates.

## 9. Real aircraft

Never plan, script or describe a flight with a real aircraft without reading
`flight-safety.md` first. Every flight needs two people present.
