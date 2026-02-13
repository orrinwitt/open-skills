# Contributing to open-skills

Thank you for helping make AI agents smarter and more efficient! 🎉

## What Makes a Good Skill?

A good skill should:
- ✅ **Solve a real problem** — Something agents commonly need to do
- ✅ **Work out of the box** — Tested, copy-paste ready code
- ✅ **Use free/open tools** — No paid APIs or proprietary services required
- ✅ **Respect privacy** — Minimal tracking, no unnecessary data collection
- ✅ **Be well-documented** — Clear examples, error handling, agent prompts

## Skill Template

Every skill should follow this structure:

```markdown
---
name: skill-name
description: A description of what this skill does and when to use it.
---

# [Skill Name]

Brief description (1-2 sentences) of what the skill does.

## When to use
- Bullet points explaining use cases
- When this skill is appropriate
- When to use alternatives

## Required tools / APIs
- List dependencies
- Installation commands
- API endpoints used

## Skills

### [Operation 1]

**Node.js:**
```javascript
// Working Node.js code with error handling
```

**Bash (if applicable):**
```bash
# Simple curl/shell one-liner
```

### [Operation 2]
(repeat structure)

## Agent prompt
\```text
Pre-written prompt for AI agent to understand and use this skill
\```

## Best practices
- Rate limiting guidance
- Error handling tips
- Security considerations

## Troubleshooting
Common errors and solutions

## See also
- Links to related skills
```

## Submission Process

1. **Check existing skills** — Make sure it doesn't already exist
2. **Create skill file** — Use `your-skill-name.md` format (lowercase, hyphens)
3. **Add required front matter** — Include `name` and `description` at the top of the file
4. **Test all examples** — Every code snippet must work
5. **Open a Pull Request**

The repository uses skill file front matter for indexing, so no README skill listing is required.

## Code Examples Requirements

- ✅ **Node.js first** — Primary language for all skills (npm has excellent module coverage)
- ✅ **Bash for simple cases** — Include curl/shell examples when it's a simple one-liner or system command
- ✅ Show full working code (not snippets that won't run)
- ✅ Handle errors gracefully
- ✅ Include comments for complex logic
- ✅ Use modern syntax (async/await, not callbacks)
- ✅ Pin versions when relevant

**Why Node.js + Bash only?**
- Reduces file size by 50-60%
- npm ecosystem is comprehensive and well-maintained
- Agents can translate to Python/other languages on demand
- Easier to maintain and contribute
- Bash covers universal CLI/curl operations

## Testing Checklist

Before submitting, verify:
- [ ] All code examples run without errors
- [ ] Dependencies are clearly listed
- [ ] Front matter is present and valid (`name`, `description`)
- [ ] Free tier / no API key examples included
- [ ] Agent prompt section is complete
- [ ] Cross-references to related skills added
- [ ] No hardcoded credentials or API keys

## Privacy & Security Guidelines

**DO:**
- ✅ Use public APIs with no authentication when possible
- ✅ Mention rate limits and ethical usage
- ✅ Show how to store secrets securely (env vars)
- ✅ Warn about potential privacy implications

**DON'T:**
- ❌ Include working API keys or tokens
- ❌ Promote services that violate ToS
- ❌ Share code that bypasses paywalls
- ❌ Use tracking pixels or analytics without disclosure

## Skill Priority List

We're especially interested in these categories:

### High Priority
- Email automation (SMTP/IMAP)
- Cloud storage (S3, GCS, Dropbox)
- Image processing & OCR
- Audio transcription (Whisper)
- Database operations (Postgres, MySQL, SQLite, MongoDB)

### Medium Priority
- GitHub/GitLab operations
- Slack/Discord integration
- Calendar scheduling
- Vector databases & embeddings
- CI/CD automation

### Nice to Have
- SMS/Twilio integration
- Payment processing (Stripe, crypto)
- Authentication flows
- Kubernetes/Docker operations
- Machine learning deployment

## Questions?

Open an issue with the `question` label, or start a discussion.

## Code of Conduct

- Be respectful and constructive
- Focus on helping AI agents work better
- Share knowledge freely
- Respect intellectual property and terms of service
- Help maintain quality standards

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
