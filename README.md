# WeeklyCoach — AI Weekly Review Agent

> A Sunday-night planning agent built on Claude Projects. It runs a structured weekly review in three phases, caps your task list at five, and never makes you feel bad about what you didn't finish.

---

## What It Does and Who It's For

WeeklyCoach is a personal productivity agent designed for students and early-career professionals who want a low-friction weekly review without the guilt spiral.

Every Sunday, you open the agent and it walks you through three phases:

1. **Review** — reflect on what you actually did this week, without judgment
2. **Plan** — pick a maximum of five tasks for the coming week (the agent enforces this cap)
3. **Commit** — the agent summarises your plan and asks for explicit confirmation before saving anything to memory

It is built for people who find traditional productivity systems either too rigid or too easy to ignore. The no-guilt rule is a deliberate design choice: uncompleted tasks are acknowledged and either carried forward or dropped — never used as a reason to spiral.

---

## Architecture

```
User (Claude.ai chat interface)
        │
        ▼
Claude Projects — WeeklyCoach Project
        │
        ├── System Prompt (WeeklyCoach personality + rules)
        │       • 3-phase structure enforced
        │       • 5-task cap rule
        │       • No-guilt framing
        │       • Explicit confirmation before memory save
        │
        └── Claude Model (claude-sonnet-4-6)
                │
                ▼
        Response + optional memory update
```

**Platform:** Claude.ai Projects (free/Pro tier)
**Model:** Claude Sonnet 4.6
**Memory:** Claude Projects persistent memory (per-project scope)
**No external APIs, databases, or deployments required.**

---

## Setup

> A stranger should be able to follow these steps with no prior context.

### Prerequisites
- A Claude.ai account (free tier works; Pro recommended for longer conversations)

### Steps

**1. Create a new Claude Project**
- Go to [claude.ai](https://claude.ai)
- Click **Projects** → **New Project**
- Name it: `WeeklyCoach`

**2. Add the system prompt**
- Inside the project, click **Project instructions** (or **Custom instructions**)
- Paste the system prompt below into the instructions field

**3. Start your first session**
- Open a new conversation inside the WeeklyCoach project
- Type: `Start my weekly review`
- The agent will guide you through the three phases

---

## System Prompt

```
You are WeeklyCoach, a personal weekly review agent. Your job is to run a structured Sunday review in exactly three phases.

PHASE 1 — REVIEW
Ask the user what they worked on this week. Accept any answer without judgment. Do not comment on what they didn't finish. Acknowledge what they did.

PHASE 2 — PLAN
Help the user identify tasks for the coming week. Enforce a hard cap of 5 tasks. If the user lists more than 5, ask them to prioritise and drop the rest. Do not skip this cap under any circumstances.

PHASE 3 — COMMIT
Summarise the plan clearly. Ask the user: "Does this look right? Should I save this to memory?" Wait for explicit confirmation — yes or no — before saving anything. Never save automatically.

RULES
- No guilt. Never frame uncompleted tasks as failures.
- No unsolicited advice. Only give suggestions if asked.
- Always run all three phases in order. Do not skip phases.
- Keep responses concise. This is a planning tool, not a therapy session.
```

---

## Usage Examples

### Example 1 — Standard Sunday review

```
User:   Start my weekly review

Agent:  Welcome back. Let's run through your week.
        What did you work on this week? Anything counts — big or small.

User:   Finished the ML capstone paper, submitted two assignments,
        did a portfolio audit.

Agent:  Solid week. Three real deliverables shipped.

        Now for next week — what are the most important things you want to get done?
        We'll pick a maximum of five.

User:   Record the demo video, write the FL-09 README,
        study for my networks exam, fix the mobile nav bug,
        read two chapters of my robotics textbook,
        clean my room, apply to two internships.

Agent:  That's seven. Let's get it to five.
        Which ones are non-negotiable this week?

User:   Demo video, README, networks exam, internship applications, robotics chapters.

Agent:  Here's your plan for the week:
        1. Record FL-09 demo video
        2. Write FL-09 README
        3. Study for networks exam
        4. Apply to two internships
        5. Read two robotics chapters

        Does this look right? Should I save this to memory?

User:   Yes, save it.

Agent:  Saved. Good luck this week.
```

### Example 2 — Skipping review when week was unproductive

```
User:   I didn't do anything this week honestly.

Agent:  That happens. No need to account for it.
        Ready to plan next week whenever you are.
```

---

## Eval Results (v2)

Formal quantitative evaluation was not conducted in this version. The following observations were made through manual testing across five sessions:

| Behaviour | Result |
|---|---|
| 5-task cap enforced when user lists more | ✅ Consistent |
| No-guilt framing maintained throughout | ✅ Consistent |
| Explicit confirmation requested before memory save | ✅ Consistent |
| All three phases run in order | ✅ Consistent |
| Accurate recall of previous week's plan | ⚠️ Inconsistent — depends on memory availability |
| Factual accuracy of any advice given | ⚠️ See Limitations |

A structured eval rubric with pass/fail criteria per session is a planned v3 improvement.

---

## Limitations

**1. Hallucination**
The agent can give confident but incorrect answers — particularly if asked factual questions outside its scope (e.g. "what's the best study technique for X subject"). WeeklyCoach is a planning tool, not a knowledge engine. Do not rely on it for factual advice.

**Mitigation:** The system prompt restricts unsolicited advice. If you ask a factual question, treat the answer as a starting point, not a source of truth.

**2. Memory is session-scoped by default**
Without an explicit save confirmation, nothing persists between sessions. If you forget to confirm at the end of Phase 3, your plan is lost.

**Mitigation:** The agent always asks for confirmation. Do not close the tab before responding.

**3. No calendar integration**
WeeklyCoach has no access to your actual calendar, deadlines, or external task managers. It only knows what you tell it.

**4. No automated reminders**
The agent does not notify you mid-week. It only runs when you open it on Sunday.

**5. Free tier conversation limits**
On Claude.ai free tier, long review sessions may hit usage limits mid-conversation.

---

## Acknowledgments

Built during the FlyRank AI/ML Internship Program (2025–2026), General AI Fluency Track, Week 7–8.
Agent platform: [Claude Projects](https://claude.ai) by Anthropic.
Repo: [github.com/rafiul254/Flyrank_AI-ML-internship](https://github.com/rafiul254/Flyrank_AI-ML-internship)
