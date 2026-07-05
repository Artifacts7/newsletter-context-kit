# Newsletter Context Kit

_by [Artifacts](https://artifactstech.substack.com)_

**A plugin to start using AI agents to help brainstorm, review, and write your newsletter.**

Most people shy away from using Claude Code or similar AI agents because getting them to work isn't immediate. With newsletters, most people bounce off these tools because of the cold start: they run the AI raw, get generic slop, and blame the tool.

But AI agents are far from the 'old' chatbots. Fed with the right context, they're valuable assistants.

So the problem isn't in *using* the agents, but before: how the agents learn and digest the context of what you've been doing for years.

Newsletter Context Kit tries to fix this by guiding you through the automated generation of the accurate context needed to get up and running with AI agents for your newsletter.

With no manual uploads, and just by chatting with you, this Kit helps AI agents get up to speed with your newsletter — so they can read your previous publications and get what your newsletter is about (a **Brief**), how you write (a **Voice Profile**), and where you want to go next. And you also get pre-set skills that brainstorm, review, and polish, based on what you've been doing for years.

So that, in the end, you get back the context your AI agents need to start helping with your newsletter.

> v1 supports **free Substack** newsletters (vanilla or custom-domain).

## Start (two ways)

**Easiest — paste the link.** Drop this into Claude Code and say *"set up my newsletter"*:
```
https://github.com/Artifacts7/context-kit
```
Claude reads the repo and walks you through it — no install, no setup. Perfect to try it.

**For regular use — install the plugin** (namespaced commands + a session-end nudge). Two commands, run **one at a time**:
```
/plugin marketplace add https://github.com/Artifacts7/context-kit.git
```
```
/plugin install context-kit@context-kit
```
> Use the full `https://….git` URL — the `owner/repo` shorthand isn't accepted for `marketplace add`.

Then invoke by name (`/context-kit:start`) — or just say what you want ("set up my newsletter", "help me brainstorm", "does this sound like me").

## Quick start

Run these in your project; everything the kit generates lands in **`./newsletter-context/`**.

| Phase | Skill | What happens |
|---|---|---|
| Setup | `/context-kit:onboard` | tell it your tools + your Substack URL |
| | `/context-kit:pull-identity` | pulls your about-page / stated identity |
| | `/context-kit:extract-corpus` | pulls your full archive (clean, full-text) |
| **Understand** | `/context-kit:distill-subject` → `reconcile` → `brief` | → your **Brief** (source of truth) |
| **Voice** | `/context-kit:distill-voice` | → your **Voice Profile** (+ checklist) |
| **Write** | `brainstorm` → *you draft* → `editorial-review` → `polish` | ideate · substance · language |
| Maintain | `/context-kit:compound` (session end) · `prune` | context improves & stays lean |

A describe step (your own words) happens during onboarding. Order is deliberate: **what you say → what your page states → what your archive shows**, light to heavy.

## What it is — and isn't

- **Is:** a partner that *grounds, sharpens, and guards* your writing — a Brief that keeps you honest, a Voice Profile that flags AI texture and protects your idiosyncrasies.
- **Isn't:** a generator. No skill writes reader-facing prose for you. The thinking and the words stay yours.

## Your context lives in `./newsletter-context/`
`brief.md` · `voice-profile.md` · `seed-context.md` · `identity-stated.md` · `corpus/`. These are *yours*, generated from *your* newsletter — they're what makes the generic skills specific to you.

## For the curious (build-in-public)
This kit was built in the open, dogfooded on the [Artifacts](https://artifactstech.substack.com) newsletter. The reasoning trail lives in [`docs/`](docs/) — [decisions](docs/decisions.md) (D1–D25, each with a "reverses if"), [the journey](docs/user-journey.md), [open questions](docs/open-questions.md), [devlog](docs/devlog.md) — and the method specs behind each skill in [`method/`](method/). *(The author's own Artifacts context isn't shipped — your `newsletter-context/` is generated fresh from your archive.)*
