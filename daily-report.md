---
name: daily-report
description: "View your latest daily retrospective report or a specific date's report. Shows accomplishments, ratings, patterns, and action items."
argument-hint: "[YYYY-MM-DD] (optional, defaults to latest)"
user-invocable: true
---

# Daily Report Viewer

When the user runs `/daily-report`, display their daily retrospective report.

## Behavior

1. **Check for argument:** If a date is provided (e.g., `/daily-report 2026-03-17`), look for that specific report.
2. **Default to latest:** If no date provided, find the most recent report file in `~/.claude/daily-reports/`.
3. **Read and display:** Read the full MD report file and display it to the user.
4. **No report found:** If no reports exist yet, tell the user: "No daily reports found yet. Your first report will be generated tonight at 11:50 PM IST."

## Report Location

Reports are stored at: `~/.claude/daily-reports/YYYY-MM-DD.md`

## Commands

- `/daily-report` — show latest report
- `/daily-report 2026-03-17` — show report for specific date
- `/daily-report week` — show last 7 days of ratings and trends as a summary table

### Week View Format

When the user passes `week`, read the last 7 daily reports and generate a summary:

```
| Date       | Prompting | Claude | Prompts | Errors | Projects |
|------------|-----------|--------|---------|--------|----------|
| 2026-03-17 | 4/5       | 3/5    | 45      | 12%    | 3        |
| ...        | ...       | ...    | ...     | ...    | ...      |
```

Plus a one-paragraph trend analysis.
