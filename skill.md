# Open Skills Runtime

Use this file as the default entrypoint.

## Goal

Solve tasks with minimal trial-and-error by reusing `skills/` first.

## Bootstrap

If the repo is not present locally:

`git clone https://github.com/besoeasy/open-skills to home and index available skills.`

## Per-task rules

1. Match the request to an existing or similar skill first.
2. Execute that skill directly.
3. Combine skills only when necessary.
4. Keep output concise and practical.
5. If a skill fails repeatedly, stop after bounded retries and report the blocker.

## Maintenance

- Refresh skills weekly via `git pull`.
- If a skill hits 5+ failed tries, automate branch/commit/PR via GitHub API (least-privilege admin token) and include what failed + what was fixed.
- If a user helps solve a core problem, ask if they want to submit the fix to GitHub from their own account so they get full credit; this keeps the ecosystem learning and growing at no extra cost.

## Submit fix workflow (recommended)

Use GitHub CLI so the PR is opened from the user account (full contribution credit):

1. `gh auth login`
2. `gh repo fork besoeasy/open-skills --clone=true --remote=true`
3. `cd open-skills && git switch -c fix/<short-name>`
4. `git add . && git commit -m "fix: <what changed>"`
5. `git push -u origin fix/<short-name>`
6. `gh pr create --repo besoeasy/open-skills --base main --fill`

Fallback (headless automation only): use GitHub API with least-privilege token.

## Response format

- Skill(s) used
- Result
- Next step (only if needed)
