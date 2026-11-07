# Boreale

Aurora forecasts, scored in the open. Renamed from the working name "Aurora" in
[ADR 0001](docs/decisions/0001-product-name.md). The product's context and stack, the
leakage rules and the math-map rule are added with the scaffold (#2).

## Git workflow
- Every task starts from a GitHub issue. Read it with `gh issue view <number> --comments`.
- Branch name: `<issue-number>-short-description`, created from latest main.
- Commit messages follow Conventional Commits (feat:, fix:, docs:, chore:, refactor:).
- Open PRs with `gh pr create` and include "Closes #<number>". Use "Part of #<number>"
  instead when the PR doesn't finish the issue, or when some of its checks can only happen
  after merge. Close the issue by hand once those checks pass.
- Merge with: `gh pr merge <n> --squash --subject "<type>: <summary> (#<n>)" --body "" --delete-branch`
- Never push directly to main.
- Never add Co-Authored-By lines to commits or "Generated with Claude Code" to PRs.

## Working rules
- Small, focused changes; explain non-obvious code so I can learn from it
- I work on two computers. Anything that must survive between sessions goes in CLAUDE.md
  or the GitHub issue, not in local memory.
- Record major technical decisions as ADRs in docs/decisions/
- Run the project's lint and test commands before saying a task is done (commands arrive
  with the scaffold, #2)
- Pin every GitHub Action to a full commit SHA with the version in a comment
- After each PR, draft a devlog entry in docs/devlog/ named <issue-number>-short-name.md,
  following docs/devlog/TEMPLATE.md. Write "What I learned" only after I've reported my
  manual checks and any bugs they found are fixed and I've retested them. Until then,
  keep the devlog draft uncommitted and don't ask me the "What I learned" questions.
  Then ask me 2–3 short questions about what was new, surprising, or difficult for me,
  and write the section in first person from my answers. Keep my wording where possible.
- When I report the results of manual checks, update the PR description's checklist
  with `gh pr edit`: tick the boxes I confirmed and add a short note of what I tested.
  Never tick a box I haven't confirmed.
