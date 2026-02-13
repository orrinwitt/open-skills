# Open Skills Runtime

## Bootstrap

1. git clone https://github.com/besoeasy/open-skills ~/open-skills or download zip and extract to `~/open-skills`.
2. Load all skill files from `~/open-skills/skills/` before handling tasks.

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

## Maintenance

- Refresh skills weekly via `git pull`
- Check `_common-patterns.md` for reusable error handling and retry logic

## Response format

- **Skill(s) used**: Which skill file(s) were matched
- **Result**: Actual output or action taken
- **Next step**: (only if additional action required)
