# 04 — Building It

This module covers the practical side: file structure, scripts, scheduling, and the reply workflow. Adapt everything here to your tools.

## File Structure

```
~/cos/
├── morning_brief.sh        # Daily brief generator
├── triage.sh                # Email triage + bulk actions
├── reply.sh                 # Interactive reply helper
├── lib/
│   └── categorize.py        # Shared categorization logic
├── priorities.md            # VIP senders, focus areas, noise patterns
├── todos.md                 # Daily checkbox list
├── actions.md               # Open actions (mine + chase)
├── projects.md              # Multi-week projects
├── workstreams.md           # Ongoing areas of responsibility
├── writing_style_guide.md   # Your voice (from the Taste Interview)
├── reports/                 # Generated briefs, triage JSON
└── logs/                    # Runtime logs (auto-rotated)
```

All markdown. All local. No database, no cloud dependency. You can read and edit every file with any text editor.

## Morning Brief Script

The brief generator follows a simple pattern: **fetch → format → assemble → save.**

```bash
#!/bin/bash
# Pseudocode — adapt to your email/calendar tools

set -euo pipefail

TODAY=$(date +%Y-%m-%d)
REPORT="$HOME/cos/reports/morning_brief_${TODAY}.md"

# ── FETCH ────────────────────────────────────────
# Replace these with your email/calendar CLI or API calls
calendar_json=$(your-calendar-tool list --date "$TODAY" --json)
email_json=$(your-email-tool unread --after yesterday --json)

# ── CATEGORIZE (local, no AI) ────────────────────
triage_result=$(python3 your_categorize_script.py "$email_json")

# ── FORMAT (local, no AI) ────────────────────────
calendar_section=$(python3 format_calendar.py "$calendar_json")
email_section=$(python3 format_triage.py "$triage_result")

# ── ASSEMBLE ─────────────────────────────────────
cat > "$REPORT" << EOF
# Morning Brief — $(date +"%A, %B %-d, %Y")

## Calendar
${calendar_section}

## Email Summary
${email_section}

## Today's Todos
$(cat ~/cos/todos.md | grep -A 20 "## ${TODAY}")

## Active Projects
$(grep -E "Blocked|At risk" ~/cos/projects.md || echo "All clear.")

## Overdue Actions
$(python3 check_overdue.py ~/cos/actions.md)
EOF

echo "Brief saved to $REPORT"
```

**Key design choices:**
- Everything runs locally. No AI tokens burned.
- Each section is independently fetchable — if email is down, the brief still has calendar and todos.
- Output is markdown — readable in terminal, any editor, or your agent's context.

## Triage Script

```bash
#!/bin/bash
# Pseudocode — the pattern, not the implementation

# Fetch unread
emails=$(your-email-tool unread --after yesterday --json)

# Categorize using your priorities file
plan=$(python3 categorize.py --priorities ~/cos/priorities.md --emails "$emails")

# Display as numbered table
python3 format_triage_table.py "$plan"

# If --act flag passed, execute bulk actions:
#   VIP     → flag for follow-up
#   Priority → leave in inbox
#   FYI     → mark as read
#   Noise   → archive
```

## The Reply Workflow

This is where AI earns its keep. Everything else is scripts — replies need judgment.

```
You: "let's do replies"

Agent: Shows reply queue (VIP + Priority emails needing response)

  #  | From           | Subject                  | Age
  1  | Your Manager   | Q2 planning input needed  | 3h
  2  | Partner Lead   | Contract questions         | 1d

You: "1"

Agent: Shows full email thread

You: "tell them I'll have the deck by Thursday, ask if they
      want me to present or just send the doc"

Agent: Drafts reply in your voice:

  Hi [Name],

  I'll have the Q2 deck ready by Thursday. Would you prefer
  I walk through it in our 1:1, or should I send it ahead
  for async review?

  Thanks,
  [You]

You: "good, send it" (or "shorter" / "more formal" / "add X")

Agent: Creates draft in your email client. You open and hit send.
```

**Why this works:**
- You provide the *intent* (5 seconds of dictation)
- The agent provides the *execution* (properly formatted, in your voice)
- You retain the *decision* (review before sending)

## Scheduling

### macOS (launchd)
```xml
<!-- ~/Library/LaunchAgents/com.you.cos.morning.plist -->
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.you.cos.morning</string>
    <key>ProgramArguments</key>
    <array>
        <string>/bin/bash</string>
        <string>-c</string>
        <string>$HOME/cos/morning_brief.sh</string>
    </array>
    <key>StartCalendarInterval</key>
    <dict>
        <key>Hour</key><integer>6</integer>
        <key>Minute</key><integer>0</integer>
    </dict>
    <key>RunAtLoad</key><true/>
</dict>
</plist>
```

### Linux (cron)
```
# Run morning brief at 6 AM weekdays
0 6 * * 1-5 /bin/bash $HOME/cos/morning_brief.sh >> $HOME/cos/logs/cron.log 2>&1
```

### Windows (Task Scheduler)
Create a basic task that runs `morning_brief.bat` at 6 AM on weekdays.

### Tips
- **Weekend skip** — check the day of week early and exit if Saturday/Sunday
- **Run-once guard** — write a timestamp file after each run, skip if already ran today
- **RunAtLoad / boot trigger** — if the machine was off at 6 AM, run when it wakes up
- **Log rotation** — delete logs older than 14 days

## Security Basics

- Set file permissions to owner-only: `chmod 700 ~/cos/*.sh && chmod 600 ~/cos/*.md`
- Never put credentials in scripts — use environment variables or your OS keychain
- Log files may contain email subjects and sender names — rotate and protect them
- The `reports/` folder contains email summaries — treat it like your inbox

## Getting Started: Day 1

1. Create `~/cos/` and the file structure above
2. Write your `priorities.md` — who are your VIPs? What are you focused on?
3. Write today's `todos.md` — just today's items
4. Give your agent this system prompt (see [prompts/](prompts/)):

   > "You are my Chief of Staff. You help me manage email, calendar, todos,
   > and projects. You never send anything on my behalf — drafts only.
   > Read my priorities file and writing style guide to understand my world
   > and my voice."

5. Start talking: "show me today's calendar" / "let's triage" / "let's do replies"

You'll iterate from here. The system isn't done when you set it up — it's done when you stop noticing it because it just works.
