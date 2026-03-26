# 01 — Voice Training

The biggest gap in AI-drafted communication isn't accuracy — it's voice. An AI that writes *correct but generic* replies undermines your credibility. People can tell.

Voice training fixes this. The goal: your agent should write something you'd actually send with minimal editing.

## The Taste Interview Method

A structured interview where your AI agent asks you 100 questions about how you write, what you hate, and what you believe. The output is a **Writing Style Guide** — a document the agent references every time it drafts something for you.

### Why 100 Questions?

You don't know your own voice until someone pushes you. The first 20 questions surface the obvious stuff ("I like short sentences"). The next 30 uncover contradictions ("I said I'm direct, but I hedge constantly with peers — why?"). The final 50 capture the subtlety that makes your writing *yours*.

### The Seven Categories

| Category | Questions | What It Captures |
|----------|-----------|-----------------|
| Beliefs & Contrarian Takes | ~15 | What you believe about communication that most people get wrong |
| Writing Mechanics | ~20 | Sentence length, paragraph structure, punctuation habits |
| Aesthetic Crimes | ~15 | What makes you cringe — the patterns you'd never use |
| Voice & Personality | ~15 | How your personality shows up (or doesn't) in writing |
| Structural Preferences | ~15 | How you organize information, what goes first vs. last |
| Hard Nos | ~10 | Absolute rules — things you'd reject on sight |
| Red Flags | ~10 | Patterns that signal bad writing to you |

### Interview Rules

1. **One question at a time.** No batching. Each answer informs the next question.
2. **Push back on vague answers.** "I like clean writing" means nothing. What does clean mean? Give an example.
3. **Demand concrete examples.** "Show me an email you were proud of" beats "describe your style."
4. **Call out contradictions.** These are gold — they reveal the *real* rules.
5. **Follow interesting threads.** If an answer surprises, go deeper before moving to the next category.
6. **Don't accept "I don't know."** Reframe: "What would you *never* write?" often unlocks what you *would*.

### Sample Questions

**Beliefs & Contrarian Takes**
- What's a communication practice everyone follows that you think is wrong?
- When is being unclear actually the right move?

**Writing Mechanics**
- Read me the last email you sent that you were proud of. What made it good?
- What punctuation do you overuse? (Everyone has one.)

**Aesthetic Crimes**
- Show me a piece of writing (yours or someone else's) that made you cringe. What specifically was wrong?
- What's the corporate phrase that makes you stop reading?

**Voice & Personality**
- How does your humor show up in writing vs. in person? Are they the same?
- Do you write differently when you're under pressure? How?

**Structural Preferences**
- Bad news: do you lead with it or build up to it?
- How do you decide what goes in the email body vs. an attachment?

**Hard Nos**
- What word, phrase, or pattern would make you reject a draft on sight?
- Is there a formatting choice (emoji bullets, excessive bold, etc.) that you'd never approve?

**Red Flags**
- What tells you someone didn't actually read the thread before replying?
- What's the difference between "polished" and "overwritten"?

> The full 100-question bank with category breakdowns will be linked here when published separately.

### Running the Interview

Prompt your agent with something like:

```
You are interviewing me to extract my writing DNA. You'll ask me 100 questions
across 7 categories to build a comprehensive writing style guide.

Rules:
- One question at a time
- Push back on vague answers — demand specifics and examples
- Call out contradictions between my answers
- Follow interesting threads deeper before moving on
- Don't accept "I don't know" — reframe the question

Start with Beliefs & Contrarian Takes. Track your question count.
```

Plan for 3-5 sessions. The interview works best in 20-30 minute blocks where you're thinking carefully, not rushing.

## The Writing Style Guide

The interview output is a living document. Here's what a good one contains:

### Core Philosophy
Your 1-2 sentence compression principle. Mine is: **"As Much As Needed, As Little As Possible."** Find yours.

### Voice Registers
Most people have at least two: a professional voice and a casual/internal voice. Document both. Note when you switch and why.

| | Professional | Internal/Casual |
|---|---|---|
| Tone | Polite, hedged | Direct, compressed |
| Openings | "Hi [Name]" | Nothing, or first name only |
| Closings | "Thanks," "Best regards" | None, or just a dash |
| Hedging | Frequent | Almost zero |

### Rules by Audience
- **Peers:** How much do you hedge? Do you persuade or assert?
- **Leadership:** What changes when you write up?
- **Vendors/external:** How direct are you?
- **Under pressure:** What's your instinct? Do you override it?

### What to Do / What to Never Do
Two simple lists. The "never do" list is usually more useful — it's your taste made explicit.

### AI-Specific Instructions
Tell your agent how to handle:
- Draft length (write long for trimming, or write to target?)
- Formatting limits (max bolds, no emoji bullets, etc.)
- Uncertainty (hedge or omit?)
- Bad news delivery (recommend verbal? lead with it?)

## Maintaining the Guide

The style guide is version 1 after the interview. It gets better as you use it:

- When you heavily edit a draft, note *what* you changed and update the guide
- When a draft needs zero edits, that's signal too — note what worked
- Revisit the guide quarterly — your voice evolves

The goal isn't a perfect document. It's a document that makes your agent 80% right on the first draft, so your edits are tweaks, not rewrites.
