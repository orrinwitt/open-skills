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

## Response format

- Skill(s) used
- Result
- Next step (only if needed)
