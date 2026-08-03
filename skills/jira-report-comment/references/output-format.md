# Output Format

## Skeleton

The heading links to the ticket's browser URL (`https://your-company.atlassian.net/browse/<ISSUE_KEY>`). If the URL is unknown, render a plain `## <ISSUE_KEY>` with no link.

Root Cause appears when the ticket fixes an existing problem. Verify and Deploy are omitted unless a trigger in SKILL.md Step 4 fires.

```markdown
## [<ISSUE_KEY>](ISSUE_URL)

One or two sentences on what shipped, framed as outcome.

### Root Cause

- The underlying cause — not the symptom the ticket already describes
- The approach taken to fix it

### Verify

- Non-obvious test path, with the expected outcome

### Deploy

- Non-routine deploy step: env var, flag, migration, cron
```

## Limits

| Part       | Limit                                              |
| ---------- | -------------------------------------------------- |
| Summary    | 1–2 sentences, ~25 words                           |
| Root Cause | ≤2 bullets, ≤25 words each                         |
| Verify     | ≤3 bullets, ≤15 words each                         |
| Deploy     | ≤3 bullets, ≤15 words each                         |
| Total      | 60–100 words; up to 150 when Root Cause is present |

## Style

The reader is a PM, QA engineer, or architect with the ticket already open. They need what the ticket doesn't tell them.

- **Outcomes, not activities.** "Verification now checks the NPI Registry", not "Added NpiRegistryService".
- **Common IT terms only** — API, endpoint, database, deploy. No file paths, class names, or method names.
- **Present tense.**
- **No code blocks** unless an exact value matters: an env var, an endpoint path, a flag name.
- **Plain punctuation** — hyphens not em/en dashes, straight quotes, no semicolons or parenthetical asides.
- Sound like a teammate posting a quick update, not a formal report.
