# Ninety Days Ahead — a Claude Skill

A planning skill that makes sure nothing slips through the cracks. You give
it one big task and its date; it gives you back a complete, dated,
margin-protected plan, then gets it onto your calendar with 9 a.m. reminders:
directly if you have a calendar tool connected, otherwise as a calendar file
you import in a few clicks.

**Activate it** by calling it by name or just saying **"90 plan"**.

**The law it enforces:** a due date is where work *ends*, not where it
*begins*.

**Personal by design:** everything this skill produces belongs to the person
running it, on their machine. Plans are stored in that user's own directory,
placed only on *their* Google Calendar or Notion, and never read from or
written to anyone else's screen, storage, or account.

## What it does

1. **Takes the big task and its completion date.**
2. **Sets the markers** — 90 / 60 / 30 / 14 / 1 calendar days out (not
   business days; weekends count), each with its meaning: start · check ·
   confirm · final (buffer begins) · eve.
3. **Asks for every step required — then pushes back, then pitches in.**
   It does not accept your first list. It probes dependencies ("what has to
   happen before this? who touches it after you?"), forces verbs, breaks up
   steps over 5 days, hunts for missing sign-off and information-gathering
   steps — and after two rounds of probing, it proposes the steps it thinks
   you're missing. No step enters the plan without an owner and a one-line
   "done looks like ___".
4. **Grounds the pushback in evidence.** When it can see your real world —
   connected calendars, Notion, files and folders, past plans — it checks
   your dates and claims against what's actually there, and tells you what
   it found. "That week already holds three Crusade steps" beats "are you
   sure?"
5. **Times every step and tests the fit** — if the chain doesn't fit the
   runway, it says so plainly instead of shaving your estimates. Multiple
   tasks from multiple plans landing on the same day is normal — the rule is
   never "spread them out," it's that **every task shows up on the day it's
   required.** The skill shows you what else lives on a date so you decide
   with open eyes.
6. **Always asks: "Have you included margin?" — and then measures it.**
   Margin is printed as a number: days of slack and percent of runway.
   Under 15%, the plan isn't done. A plan that only works if nothing goes
   wrong is already broken.
7. **Sets the dates backwards, delivers the plan, and saves it** — the plan
   is written to storage (`~/.claude/ninety-days-ahead/plans/`, or Notion),
   so it outlives the conversation. Every plan ends with exactly one first
   action.
8. **Gets it onto your personal calendar** — the 9 a.m. alerts are what make
   the system fire without human memory. It always shows you the full event
   list and waits for your yes first. With a calendar tool connected it
   creates the events on *your own* calendar; with nothing connected it hands
   you a `.ics` file you import in a few clicks, which is the normal path on a
   fresh install. Every event carries the plan's `[TASK] ▸` prefix so replans
   update events instead of duplicating them.
9. **Optional themed wall calendar.** A separate local renderer (`90plan`) can
   draw a print-friendly wall calendar in a palette you pick once. It does
   **not** ship with this skill, and in its current form it renders a plan
   compiled into its own source rather than the plan you just made, so treat
   it as a template rather than an export. The skill checks whether it exists
   and stays quiet when it does not.
10. **Offers a Monday 9 a.m. week-ahead digest** — everything due that week
    across all your plans, grouped by day, plus a daily walk and a monthly
    reset on the 1st. How far this can be automated depends on your setup: a
    scheduler or connected email can send it to you, and where neither exists
    the skill falls back to a recurring Monday calendar reminder that tells
    you to ask for it. On a fresh install, expect the calendar reminder.

## Install

### Claude Code (terminal or desktop) — the agentic way
Open Claude Code and say:

> Clone https://github.com/lonnell-spec/NinetyDaysAhead and install it
> into my skills directory as `ninety-days-ahead`.

Claude will place it at `~/.claude/skills/ninety-days-ahead/` (available in
every project). That's the whole install, and nothing else has to be set up:
the planning conversation and the dated plan work as they are, and calendar
placement falls back to a `.ics` file you import. Connecting a calendar or
Notion tool later upgrades that to events created directly for you.

The optional `90plan` wall-calendar renderer mentioned in a couple of places
is a separate local tool and is deliberately not in this repo. Without it the
skill simply skips the theming step and never mentions it.

### Claude Code — the manual way
```bash
git clone https://github.com/lonnell-spec/NinetyDaysAhead ~/.claude/skills/ninety-days-ahead
```

### Claude.ai (web / desktop app)
Zip the `ninety-days-ahead` folder, then: **Settings → Capabilities →
Skills → Upload skill** and select the zip. The skill becomes available in
your conversations.

## Use

Say **"90 plan"** and name your task — or any of these:

- *"90 plan: the Crusade documentary is due April 1."*
- *"Back-map Baptism Sunday for me."*
- *"Plan this backwards: staff Christmas production, December 20."*

Then answer its questions honestly — especially when it pushes back on your
step list. The pushback is the feature. When it asks **"Have you included
margin?"**, the honest answer is usually no; let it fix that before it
sets a single date.

After a plan exists, four standing commands work anytime — they read from
stored plans, so they work in any conversation, any day:

- **"daily walk"** — everything due today, across every plan, in under
  5 lines. Several items from several plans on one day is normal; seeing
  them all is the point.
- **"week ahead"** — everything due this week, grouped by day (this is also
  what the Monday 9 a.m. digest sends you).
- **"monthly reset"** — the next 30 days, everything overdue, and every task
  whose 90-day marker falls this month.
- **"slipped"** — a step missed its date. The skill recomputes downstream
  dates, tells you exactly how much margin that spent and how much remains,
  and updates the stored plan. Where a calendar tool is connected it updates
  those events in place by their `[TASK] ▸` prefix rather than duplicating
  them; otherwise it gives you a corrected `.ics` to re-import. If margin hits
  zero it forces the honest options: cut scope, add hands, or move the date.

## The philosophy (60 seconds)

Busy people without a system will always drop something — it's physics, not
character. The fix is structural: one calendar, every major date mapped,
every deliverable broken into bite-size pieces and back-scheduled, walked
every day, reset every month. The five markers catch the slip while it's
still cheap. The margin question is humility in calendar form — dates move,
people get sick, plans meet reality. Ninety days ahead isn't about being
impressive. It's about never having to be behind.
