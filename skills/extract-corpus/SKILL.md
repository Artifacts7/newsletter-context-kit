---
name: extract-corpus
description: >
  Extract a writer's full published corpus from a Substack newsletter (vanilla or
  custom-domain) given only its URL — the complete archive at full fidelity, cleaned,
  segmented, and fidelity-tagged, with a coverage manifest. This is step 3 (Ingest)
  of the Context Kit. Use whenever someone wants to build AI context from a Substack
  newsletter, "load my newsletter," "pull my archive," or onboard a writer's body of
  work. v1 supports free Substack only; paid posts return previews.
allowed-tools: Bash(python3 *)
---

# Extract Corpus (Substack, v1)

Turns a Substack URL into a clean, full-fidelity corpus — the foundation every later
step (subject, voice, brief) depends on. White-labeled: no publication-specific
assumptions; works for any free Substack.

## When to use
- **The last step of Phase A** — "the agent reads it all." This is the heavy read.
- Refreshing a corpus with new issues (the Compound step).
- Any "load / pull / ingest my Substack archive" request.

## Precondition (don't fetch too early)
Run this **only after** the writer has gone through onboarding (0 — where work lives),
describe (1 — `newsletter-context/seed-context.md`), and stated identity (2 — `newsletter-context/identity-stated.md`). The
full corpus is the heaviest, last-loaded context (progressive loading, D8): pulling it
before the writer has said how they see their newsletter inverts the intended order.
If those earlier artifacts don't exist yet, do those first.

## How to run

**Default: fetch the 25 most recent issues** — that's the strongest signal for voice/identity and keeps token use sane. First check the archive size, then **ask the writer** before going bigger:

> "Your archive has ~N issues. I'll read the **most recent 25** by default — that's plenty for a sharp read and keeps it fast/cheap. Want me to pull the **full archive** instead? (more complete, but noticeably more tokens and time.)"

```
# default
python3 ${CLAUDE_SKILL_DIR}/substack_fetch.py <publication-url> ./newsletter-context/corpus --limit 25 [--appendix-markers "a,b,c"]
# only if the writer opts in to the full archive
python3 ${CLAUDE_SKILL_DIR}/substack_fetch.py <publication-url> ./newsletter-context/corpus
```
Custom domains work the same (`https://www.example.com`). Everything lands in **`./newsletter-context/`** (the kit's convention).

## Procedure (what the agent does)

1. **Acquire.** Run the fetcher on the URL. It paginates the archive API and pulls
   each free post's full body. Report the manifest: total posts, date range,
   full-prose vs. preview/short counts, any errors.
2. **Surface era/language splits.** Scan dates + language of the manifest/titles.
   If the archive spans languages or a clear style era (common in long-running
   newsletters), FLAG it — voice/identity must not be averaged across phases. Default
   downstream work to the current-language, recent era; treat older eras as history.
3. **Detect appendix sections (segmentation).** Read 2–3 recent issues. If the writer
   has recurring trailing sections (link roundups, book lists, footers), identify their
   headers and re-run with `--appendix-markers "..."` so those zones are split out of
   the essay body (they carry curation signal, not voice — D14). If none, skip — the
   tool safely keeps the whole essay in body.
4. **Report scope honestly.** State coverage (e.g. "78/80 full-prose, 2 paid/preview"),
   what was excluded, and any non-Substack/paywall limits hit.

## Output
- `<output-dir>/<slug>.md` — per issue: metadata + `## BODY` (essay) + `## APPENDICES`.
- `<output-dir>/manifest.json` — coverage, dates, fidelity per issue, sampled count.

Hand the corpus to the distillation steps (subject → reconcile → brief; then voice).

## Limits (v1)
- **Free Substack only.** Non-Substack URLs exit cleanly with a message. Paid posts → preview only (need the owner's Settings → Export).
- **Appendix markers are per-newsletter** — detected in step 3, not hardcoded.
- Rate-limited APIs handled via exponential backoff; very large archives take a few minutes.

_Validated across 4 publications (Artifacts, Astral Codex Ten, Gary Marcus, + graceful
fail on non-Substack)._

---
_**Language:** if the newsletter isn't in English, converse with the writer — and write outputs — in the newsletter's language._
