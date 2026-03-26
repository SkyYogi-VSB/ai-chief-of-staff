# 02 — Intake & Triage

## Capture: The Missing Piece

Before triage comes capture. Ideas, reminders, delegations, plan fragments — they hit you at random: in the shower, on a walk, mid-meeting. If you don't capture them instantly, they're gone.

Your CoS needs an always-on intake channel. The simplest version: a voice note app on your phone that transcribes and ships notes to your inbox (or a file your CoS watches).

### Voice Notes → CoS Pipeline

The pattern:

1. **Capture** — speak into your phone. The app transcribes and saves as a timestamped markdown entry.
2. **Batch** — notes accumulate throughout the day in a daily file.
3. **Ship** — at end of day (or on demand), the file is sent to your CoS inbox via email, file sync, or API.
4. **Ingest** — your CoS picks up the notes during triage and routes each entry: action items → todos, ideas → backlog, reminders → calendar, delegations → chase list.

```
Phone (capture)  →  Daily MD file  →  Email/sync  →  CoS triage  →  Routed
                                                        ↓
                                          todos / backlog / calendar / chase
```

### Why Voice, Not Typing?

Speaking is 3-4x faster than typing on a phone. And the goal isn't polished text — it's raw capture. Your CoS will clean it up during ingestion.

### Reference Implementation

[Voice Secretary](https://github.com/SkyYogi-VSB/voice-secretary-template) is an Android PWA (built by the author) that implements this pattern: speech-to-text capture, daily markdown files, and a "Ship to CoS" button that emails the day's notes. It's open source — fork it, adapt it, or use it as inspiration for your own.

> **Note:** This is an Android PWA. An iOS equivalent doesn't exist yet — if you build one, please share.

### Daily Note Format

```markdown
### 14:32 #idea
What if we bundled the onboarding docs as a single PDF instead of six links

### 15:10 #action
Need to follow up with [partner] on the contract review — they promised Thursday

### 16:45 #reminder
Prep slides for Monday all-hands — keep it to 3 slides max
```

Tags are optional but help your CoS route faster. Even without tags, the content usually makes the category obvious.

---

## Triage: Processing the Firehose

The average knowledge worker gets 100+ emails a day. Most are noise. The ones that matter are buried. Triage is the system that fixes this.

## The Four Buckets

Every incoming message falls into one of four categories:

| Bucket | Definition | Action |
|--------|-----------|--------|
| **VIP** | From someone in your management chain or key stakeholders | Surface immediately, flag for reply |
| **Priority** | Requires your action or decision, but not from a VIP | Queue for reply, review today |
| **FYI** | Useful context, no action needed | Mark read, skim in brief |
| **Noise** | Auto-notifications, calendar accepts/declines, newsletters, CC spam | Archive automatically |

### Why Four and Not More?

Because you need to make this decision in under a second per email. More buckets means more thinking. Four is the maximum that stays instinctive.

## The Priorities File

A single markdown file that tells your CoS who matters and what matters. This is the brain of your triage system.

```markdown
# Priorities

## VIP Senders
# Emails from these people always surface at the top.
- Your Manager (manager@company.com)
- Their Manager (skip-level@company.com)
- Key Partner Contact (partner@external.com)

## Focus Areas
- Project Alpha — shipping Q2, high visibility
- Customer Beta — renewal at risk
- Team hiring — three open reqs

## Noise Patterns
# Auto-archive anything matching these patterns
- Calendar accept/decline/tentative notifications
- Automated build notifications
- Newsletter digests
- "Out of office" auto-replies
```

Update this file as your world changes. New quarter? New VIPs and focus areas. Reorg? New management chain.

## How Triage Works

```
Unread Inbox
    │
    ▼
┌──────────────┐
│  Categorize  │  ← Rules-based (VIP list + keywords). No AI needed.
└──────┬───────┘
       │
  ┌────┴────┬──────────┬──────────┐
  ▼         ▼          ▼          ▼
 VIP     Priority      FYI      Noise
  │         │          │          │
 Flag    Queue for   Mark read  Archive
 for     reply                  silently
 reply
```

### The Key Insight: Categorization Is Free

You don't need AI to sort email. A Python script with your VIP list and a few keyword rules handles 90% of categorization. Save your AI tokens for the replies.

```python
# Pseudocode for categorization
def categorize(email, priorities):
    sender = email["from"].lower()

    # VIP: sender is in your VIP list
    if any(vip in sender for vip in priorities["vip_senders"]):
        return "VIP"

    # Noise: matches known noise patterns
    if is_calendar_notification(email) or is_auto_reply(email):
        return "NOISE"

    # Priority: mentions your focus areas or is addressed directly to you
    if is_direct_to_me(email) and mentions_focus_area(email, priorities):
        return "PRIORITY"

    # FYI: everything else
    return "FYI"
```

## The Triage Workflow

### Daily (automated, part of morning brief)
1. Script pulls unread emails
2. Categorizes each one
3. Morning brief shows: VIP count, Priority count, FYI count, Noise archived
4. You scan the VIP and Priority sections in the brief

### On-demand (interactive, when inbox feels heavy)
1. Tell your agent: "let's triage"
2. Agent runs triage, shows a numbered table:

```
#  | Bucket   | From              | Subject                    | Age
1  | VIP      | Your Manager      | Q2 planning — need input   | 2h
2  | VIP      | Partner Lead      | Contract review             | 5h
3  | Priority | Product team      | Launch timeline update       | 1d
4  | Priority | Finance           | Budget approval needed       | 3h
5  | FYI      | Engineering       | Deploy complete              | 1h
...
12 | Noise    | (auto-archived 12 messages)
```

3. You reference by number: "reply to 1, archive 5, flag 3 for tomorrow"
4. Agent executes. No re-querying — IDs are cached from the triage run.

## Batch Sizes

Process 25 messages at a time. Fewer than that and you're context-switching too often. More than that and the table becomes unwieldy.

## Reply Queue

After triage, your VIP and Priority emails form a reply queue. The reply workflow (described in [04-building-it.md](04-building-it.md)) processes this queue interactively:

1. Agent shows you the full email
2. You dictate the gist ("tell them yes, ask about timeline")
3. Agent drafts a reply using your voice (from the Writing Style Guide)
4. You approve or edit
5. Draft lands in your email client — you hit send

## Evolution

As you use triage daily, you'll notice:
- **New noise patterns** — add them to your priorities file
- **Missing VIPs** — someone important keeps landing in FYI
- **Bucket drift** — "Priority" starts meaning something different after a reorg

Tune the system weekly. It takes 2 minutes and compounds over time.
