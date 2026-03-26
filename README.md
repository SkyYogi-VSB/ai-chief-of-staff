# AI Chief of Staff

> "Do what you do best, let agents do the rest — if they can do it safely and securely."

A methodology for building a personal AI Chief of Staff — an always-on system that reads your email, calendar, and notes to produce daily briefs, triage your inbox, draft replies, and run your rhythm of business.

This isn't a SaaS product or a framework. It's a recipe — a set of principles, workflows, and prompt patterns that you adapt to whatever tools you already use.

## Philosophy

Your CoS handles the operational overhead — categorizing, summarizing, drafting, reminding — so you can focus on judgment calls, relationships, and creative work. The AI never acts autonomously on your behalf. It prepares; you decide.

## Core Principle: Drafts Only, Never Sends

The single most important safety constraint: **your CoS never sends anything on your behalf.** It creates drafts. You review, edit, and hit send. This isn't a training wheel — it's a permanent architectural decision. Trust is built through transparency, not automation.

## What's Inside

| Module | What It Covers |
|--------|---------------|
| [00 — Architecture](00-architecture.md) | The Brain + Hands model, three daily rhythms, platform-agnostic design |
| [01 — Voice Training](01-voice-training.md) | Teaching your agent to write like you using the Taste Interview method |
| [02 — Intake & Triage](02-intake-triage.md) | Voice capture on the go, then VIP/Priority/FYI/Noise categorization |
| [03 — Getting Things Done](03-gtd-system.md) | Todos, actions, projects, workstreams — and how they feed the brief |
| [04 — Building It](04-building-it.md) | Reference implementation patterns, file structure, scheduling |
| [prompts/](prompts/) | Starter system prompts you can adapt for your agent |

## Who This Is For

- Knowledge workers drowning in email and meetings
- People who already use an AI assistant and want to level it up from "ad hoc helper" to "operating system"
- Anyone willing to spend a weekend setting up a system that saves hours every week

## Prerequisites

- An AI agent you can talk to (Claude, ChatGPT, Gemini, Cursor, etc.)
- Access to your email and calendar (API, CLI tool, or manual copy-paste)
- A text editor and a folder on your computer
- 2-3 hours for initial setup, 30 minutes/day for the first week to tune it

## How I Built Mine

I built my CoS over several weeks of daily use, iterating in conversation with Claude Code. The system started as a morning brief script and grew into a full operating rhythm. Every module in this repo was born from a real need, not a spec.

The Taste Interview alone took 63 questions across multiple sessions before the writing style guide felt right. The triage system went through four rewrites before the categorization was fast and accurate enough to trust.

This is a living system. It gets better the more you use it.

## Credits & Inspiration

- [Peeyush Ranjan](https://www.linkedin.com/posts/peeyushr_ive-been-fortunate-to-work-with-some-incredible-activity-7435715831277387777-TgmH) — his post about building an AI Chief of Staff agent during a family vacation showed what a single builder can accomplish. Proof that the idea has legs.
- [Ruben Hassid](https://www.linkedin.com/posts/ruben-hassid_how-to-make-ai-sound-exactly-like-you-forever-share-7434595498042429440-oAVI) — his "Taste Interviewer" method for extracting your writing DNA through a structured 100-question self-interview directly inspired the Voice Training module in this repo.
- The Taste Interview question bank used here builds on Hassid's original prompt. The full 100-question set is linked in [01-voice-training.md](01-voice-training.md).
- [Voice Secretary](https://github.com/SkyYogi-VSB/voice-secretary-template) — an open-source Android PWA built by the author for voice-to-text capture that ships daily notes to your CoS. Used as the intake layer in this system.
- [Claude Code](https://claude.ai/claude-code) — the entire CoS system and this repo were built iteratively in conversation with Claude Code over several weeks.

## License

MIT — use it, adapt it, share it. If you build something cool with it, I'd love to hear about it.
