---
name: start
description: >
  Walk through the ENTIRE Context Kit setup end-to-end — the single guided entry point. Runs every
  step in order (connect → describe → stated identity → read archive → distill subject → reconcile →
  Brief → Voice Profile), pausing at the points where the writer needs to answer. Use to begin:
  "start", "set up my newsletter", "walk me through the context kit", "build my newsletter context
  from scratch", "let's begin".
---

# Start — the guided walk-through

The **single entry point**. It drives the whole process, invoking each step's skill in order and
**stopping at the human gates (⏸)**. Go one beat at a time: run a step, show the result, then
continue only when the writer is ready. Everything is written to **`./newsletter-context/`** in the
current folder.

## Before you begin — set expectations (always do this first)
Open by telling the writer, briefly, **what this will do and what they'll walk away with** — then get a go-ahead:

> "Here's the plan: I'll read your newsletter's archive and build two things that live in `./newsletter-context/` and become the source of truth for all your writing:
> 1. a **Brief** — what your newsletter is about, how it's written, and where it's going;
> 2. a **Voice Profile** — an operational guide to *how you write*, used to catch AI-sounding text and protect your voice.
> Along the way I'll ask you a few short questions (how you see it; where the archive and what you say disagree). I'll read your **25 most recent issues by default** to keep it fast — we can go bigger if you want. I won't write your newsletter *for* you; I help you think, structure, and polish. Sound good?"

## Language (important)
Detect the newsletter's primary language (from the about page / corpus). **If it isn't English, conduct the entire conversation — and write the deliverables — in the newsletter's language.** Match the writer's language throughout.

## The sequence

**0 · Connect.** Ask for their **Substack URL** (required) and where else their work lives
(Notion/Drive/notes, optional). Confirm the URL resolves. Write `newsletter-context/workspace.md`.
(See the `onboard` skill for framing — but do NOT fetch the archive yet.)

**1 · ⏸ Describe.** Ask these one or two at a time; accept terse/partial answers, don't interrogate:
- your newsletter in one sentence (the punchline)
- a few lines: what it is, who it's for, the thesis
- who do you picture reading it?
- topics/angles you'd **never** touch
- one issue you're proud of, and one you'd disown today
- where do you want it to go — what should it **become**?

Write `newsletter-context/seed-context.md`. → then continue.

**2 · Stated identity.** Invoke **`pull-identity`** with the URL → `newsletter-context/identity-stated.md`.
Note any gap vs. the describe answers (for step 5); don't resolve it yet.

**3 · Read the archive.** Invoke **`extract-corpus`** with the URL. **Default: the 25 most recent
issues** (fast, cheap, strongest signal). Tell the writer the archive size and **ask** if they want
the full archive instead — warn it's noticeably more tokens/time. → `newsletter-context/corpus/` +
manifest. Report coverage; flag era/language splits; detect appendix markers.

**4 · Distill subject.** Invoke **`distill-subject`** → `newsletter-context/subject-observed.md`.

**5 · ⏸ Reconcile.** Invoke **`reconcile`**: surface the top 3–5 said/stated/shown gaps as **open
questions**, wait for the writer's answers, classify them. → `newsletter-context/reconcile.md`.

**6 · ⏸ Brief.** Invoke **`brief`**: write the source-of-truth Brief, present it, get the writer's
**confirmation** (the gate). → `newsletter-context/newsletter-brief.md`. ✅ **Milestone 1 complete.**

**7 · Voice (optional now).** Ask if they want the Voice Profile now. If yes, invoke **`distill-voice`**
and run the calibration. → `newsletter-context/voice-profile.md`. ✅ **Milestone 2.**

## ▶ When Milestone 2 completes — hand off clearly (the "you're set up" moment)
This is important UX: once the Brief + Voice Profile exist, tell the writer **the bulk is done, their context is ready, and how to use it from now on.** Present it warmly, roughly like this (in their language):

> **You're set up 🎉 — the hard part's done, and it's a one-time thing.**
>
> **Where everything lives:** in this folder, under `newsletter-context/`:
> - `newsletter-brief.md` — what your newsletter is about, how it's written, where it's going (your source of truth)
> - `voice-profile.md` — how you write (used to protect your voice and catch AI-sounding text)
> - `seed-context.md`, `identity-stated.md`, `corpus/` — the raw inputs behind them
>
> **Every time you want to write:** open Claude Code **in this folder** (select this folder/project) — that's what makes the skills use *your* context — then just say what you want, or use a skill:
> - **`brainstorm`** — *"help me find an angle for the next issue"* (grounded in your Brief + past issues, flags overlap)
> - *(you write the draft — the kit doesn't write for you)*
> - **`editorial-review`** — *"does this draft work?"* (substance: is the argument there, is it on-brief)
> - **`polish`** — *"does this sound like me?"* (voice check: flags AI texture, keeps your idiosyncrasies)
>
> **To keep it sharp over time:**
> - **`compound`** — at the end of a session, *"update my context"* folds what you learned back into the Brief/Voice Profile
> - **`prune`** — occasionally, *"clean up my context"* keeps it lean
> - If the newsletter pivots, just say so — we update the Brief first.
>
> That's the whole loop: **brainstorm → you write → review → polish.** The context quietly improves each time.

The kit assists and guards; it never writes the piece for them (D21).

## Rules
- **One beat at a time.** Never skip the ⏸ gates (describe · reconcile · brief-confirm · calibration).
- **Light → heavy:** never fetch the corpus (3) before describe (1) + stated identity (2).
- Everything lands in `./newsletter-context/`. If a step's output already exists, offer to reuse or redo.
