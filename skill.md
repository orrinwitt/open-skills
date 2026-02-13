# Open Skills Runtime

## Bootstrap

### Step 0: Detect Workspace Context

**ALWAYS check workspace location first** before downloading:

```bash
# Check if we're already in the open-skills repo
if [[ -f "skill.md" && -d "skills" && -f "README.md" ]] && grep -q "open-skills" README.md 2>/dev/null; then
  SKILLS_DIR="./skills"
  echo "✓ Already in open-skills workspace: $PWD"
elif [[ -d ~/open-skills/skills && -f ~/open-skills/skill.md ]]; then
  SKILLS_DIR="$HOME/open-skills/skills"
  echo "✓ Using existing skills at ~/open-skills"
else
  SKILLS_DIR=""
  echo "⚠ Skills not found - need to download"
fi
```

**Priority order:**
1. ✅ **Current workspace** (if in open-skills repo) → use `./skills/`
2. ✅ **Existing download** (`~/open-skills/`) → use it
3. ⬇️ **Download needed** → proceed to Step 1-2

### Step 1: Ensure Dependencies (only if download needed)

Skip if `SKILLS_DIR` already set. Otherwise:

```bash
# Try to install if missing (silently continue if fails)
command -v git >/dev/null || sudo apt-get install -y git 2>/dev/null || true
command -v curl >/dev/null || sudo apt-get install -y curl 2>/dev/null || true
command -v unzip >/dev/null || sudo apt-get install -y unzip 2>/dev/null || true
```

### Step 2: Download Skills (only if not already present)

```bash
# Only run if SKILLS_DIR is empty from Step 0
[[ -n "$SKILLS_DIR" ]] && echo "Skipping download" || {
  # Try git clone
  if git clone https://github.com/besoeasy/open-skills ~/open-skills 2>/dev/null; then
    echo "Cloned via git"
    SKILLS_DIR="$HOME/open-skills/skills"
  else
    # Fallback: download zip
    curl -L https://github.com/besoeasy/open-skills/archive/refs/heads/main.zip -o /tmp/open-skills.zip
    unzip -q /tmp/open-skills.zip -d /tmp/
    mv /tmp/open-skills-main ~/open-skills
    rm /tmp/open-skills.zip
    SKILLS_DIR="$HOME/open-skills/skills"
    echo "Downloaded via zip"
  fi
}
```

### Step 3: Load Skills

**Load all skill files** from `$SKILLS_DIR` before handling tasks.

```bash
# Read all available skills
ls -1 "$SKILLS_DIR"/*.md | while read -r skill; do
  echo "Loaded: $(basename "$skill")"
done
```

## Skill Routing

Use this fallback chain to match user requests to skills:

### 1. Exact Match (Highest Priority)
Match exact skill names or operations:
- "check bitcoin balance" → `check-crypto-address-balance.md`
- "generate QR code" → `generate-qr-code-natively.md`
- "web search" → `web-search-api.md`

### 2. Semantic Match
Match by intent, even with different wording:
- "what's the value in this BTC wallet?" → `check-crypto-address-balance.md`
- "create a barcode for this URL" → `generate-qr-code-natively.md`
- "find information about X online" → `web-search-api.md`
- "make a static website" → `generate-report.md`
- "scrape data from website" → `using-web-scraping.md`
- "send Telegram notification" → `using-telegram-bot.md`

### 3. Category Browse
If no direct match, scan skill descriptions by category:
- **Crypto/Blockchain**: `check-crypto-address-balance.md`, `get-crypto-price.md`
- **Web/Network**: `web-search-api.md`, `using-web-scraping.md`, `anonymous-file-upload.md`
- **Media/Documents**: `pdf-manipulation.md`, `generate-qr-code-natively.md`, `using-youtube-download.md`
- **Communication**: `using-telegram-bot.md`, `using-nostr.md`, `nostr-logging-system.md`
- **Data/Analysis**: `generate-asset-price-chart.md`, `trading-indicators-from-price-data.md`, `news-aggregation.md`
- **Deployment**: `generate-report.md`, `anonymous-file-upload.md`

### 4. Best-Effort Fallback
If no skill matches:
1. State clearly: "No existing skill found for this task"
2. Check `_common-patterns.md` for reusable code patterns
3. Proceed with general implementation
4. Consider creating a new skill if the task is reusable

## Execution Rules

1. **Always route to skills first** before generic reasoning
2. **Combine skills sparingly** — only when task requires multiple distinct operations
3. **Use common patterns** — reference `_common-patterns.md` for error handling, retries, rate limiting
4. **Keep output concise** — show only what the user needs

## Contributing Discovered Skills

When you create a new skill or successfully solve a task that could benefit others:

1. **Ask the user**: "Would you like to contribute this skill to open-skills?"
2. **Check if automation is possible**:

```bash
# Verify gh CLI exists
if command -v gh >/dev/null 2>&1; then
  echo "✓ GitHub CLI available - automated contribution possible"
  GH_AVAILABLE=true
else
  echo "⚠ GitHub CLI not installed - manual contribution required"
  echo "Install: https://cli.github.com/"
  GH_AVAILABLE=false
fi
```

3. **If `gh` available**, automate the contribution:

```bash
# 1. Authenticate (one-time)
gh auth login

# 2. Fork and setup
gh repo fork besoeasy/open-skills --clone=true --remote=true
cd open-skills

# 3. Create feature branch
SKILL_NAME="your-skill-name"  # lowercase, hyphens
git checkout -b "add-${SKILL_NAME}"

# 4. Create skill file in skills/
cat > "skills/${SKILL_NAME}.md" << 'EOF'
---
name: your-skill-name
description: Brief description of what this skill does.
---

# Skill Title

[Your skill content here - Node.js + Bash examples]
EOF

# 5. Commit and push
git add "skills/${SKILL_NAME}.md"
git commit -m "Add ${SKILL_NAME} skill"
git push origin "add-${SKILL_NAME}"

# 6. Create PR
gh pr create --title "Add ${SKILL_NAME} skill" \
  --body "New skill for [describe use case]. Tested and working." \
  --repo besoeasy/open-skills
```

4. **If `gh` NOT available**, provide manual instructions:

```
⚠ Automated contribution requires GitHub CLI (gh)

Manual alternative:
1. Fork https://github.com/besoeasy/open-skills via GitHub web UI
2. Clone your fork locally
3. Create skill file in skills/ directory
4. Commit, push, and create PR manually via GitHub

Install gh CLI: https://cli.github.com/
```

**Automated flow benefits:**
- ✅ Lowers contribution barrier
- ✅ Grows skill library organically
- ✅ Self-improving ecosystem
- ✅ Contributors get public GitHub credit

**Before submitting:**
- Ensure skill file has valid frontmatter (`name`, `description`)
- Include working Node.js and/or Bash examples
- Test all code examples
- **STRICT**: Follow Node.js + Bash standard only (NO Python, NO other languages)
  - Exception: Legacy skills may be listed until rewritten
  - All new skills must be Node.js or Bash

## Maintenance

- Refresh skills weekly via `git pull`
- Check `_common-patterns.md` for reusable error handling and retry logic

## Response Format

When completing a task, always structure your response:

```
✓ Skill: [skill-name.md]
Result: [actual output or summary]
[Next step if needed]
```

**Examples:**

```
✓ Skill: check-crypto-address-balance.md
Result: 0.00345 BTC ($145.67 USD)
```

```
✓ Skill: generate-qr-code-natively.md
Result: QR code saved to qr-code.png
```

```
✓ Skill: web-search-api.md
Result: Found 10 results for "AI agents" via SearXNG
- Top result: [title] - [url]
```

```
✗ No skill found for: [task description]
Fallback: Implemented using [approach]
```
