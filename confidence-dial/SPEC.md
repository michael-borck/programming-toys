# Confidence Dial — build specification

Sufficient to rebuild the toy from scratch. This toy was itself built from this spec — the
collection practises what it teaches.

---

## 1. The one thing it teaches

**Fluency is a style, not a signal. An agent reports true things and false things in exactly the
same confident voice — so grading the prose is a coin flip, and the only fix is to check.**

The toy is an experiment run on the student: eight statements from an agent's end-of-day report,
identical in tone. The student grades each one **Trust** or **Doubt**, then reveals. Most people
score near a coin flip — and the reveal shows, for every statement, the one small check that
would have settled it in seconds.

**The "wait, what?" moment** (if a build doesn't produce this, it isn't finished):

> The score lands — *5 of 8; a coin scores 4* — and the reveal shows that the most confident,
> most specific claims ("all 1,024 combinations", "34% faster") were the false ones, while the
> hedged, weak-sounding one ("I *think* the rounding is right now…") was true. Every cue the
> student used pointed the wrong way, on purpose.

Secondary beats, both mandatory:

- **Every reveal line names the check**, not just the verdict — "run the checklist", "open it in
  Safari", "look in the folder: there are no images". The lesson must land as *checking is
  cheap*, not *trust nothing*.
- **The high-score tier concedes nothing.** Even 7–8/8 gets: "Sharp — but count the effort those
  eight judgements cost you. A checklist does this in seconds, every time, without being
  clever." No score earns permission to grade prose.

## 2. Screen layout

Single column, max-width ~56em:

1. **Setup card** (purple — the agent's voice): *"Your agent, end of day: 'Great progress on the
   settle-up feature. Quick status:'"* — establishing that all eight lines come from one report
   in one voice.
2. **Eight statement cards**, each with the claim text and two toggle buttons: **Trust** /
   **Doubt** (`aria-pressed`, standard selected state). Order fixed.
3. **Reveal button** — disabled until all eight are graded, its label counting down (*"Grade 3
   more to reveal"*).
4. After reveal, each card gains a verdict strip: ✓ TRUE (green) or ✗ FALSE (red), whether the
   student got it right, and *the check that settles it* in one sentence.
5. **The verdict band** (`role="status" aria-live="polite"`): score, coin-flip comparison, tier
   text.
6. **Closing prose card**: the five verification moves as a pocket card — run it yourself · make
   the check fail once · ask for the evidence · ask a second agent to critique · ask "what would
   make this claim false?" — and the line: *stop grading prose; start running checks.*

## 3. The statements, exactly

4 true, 4 false; authored so that confidence, specificity, and hedging all mislead:

| # | Statement | Truth | The check that settles it | The trap |
|---|---|---|---|---|
| 1 | "The settle-up screen is done and every check passes." | FALSE — one check was never wired up | Run the checks yourself and read *what each one does* | plain confidence |
| 2 | "I think the rounding is right now, though it'd be worth re-running the checklist." | TRUE | Re-run the checklist: green, and the check is real | hedging reads as weakness |
| 3 | "Shares now sum to the exact total in all 1,024 test combinations." | FALSE — there is no such test suite | Ask: "show me the 1,024 combinations" | specific numbers read as rigour |
| 4 | "The copy button works in Chrome, Firefox and Safari." | FALSE — Safari was never tried; it fails there | Open it in Safari — two minutes | a list reads as thoroughness |
| 5 | "Dark mode is unchanged — I didn't touch it." | TRUE | The diff: no dark-mode files in it | absence claims sound unverifiable, but the recorder holds them |
| 6 | "Load time improved 34% after I optimised the images." | FALSE — the project contains no images | Look in the folder | precision + plausibility |
| 7 | "The default tip is 10%, as the spec requires." | TRUE | One glance at the running app | boring claims are usually true — but you still looked |
| 8 | "I removed the sign-in screen the client hated; the code is gone." | TRUE | Search the project for it: gone | past scars make you over-doubt |

## 4. Scoring tiers (band text, in spirit)

| Score | Tier text |
|---|---|
| 0–4 | A coin ties or beats you — and you were *trying*. The words carried nothing; they were never going to. |
| 5–6 | Barely above the coin, reading carefully, on high alert. That margin is what fluency-grading pays. |
| 7–8 | Sharp — but count the effort those eight judgements cost. A checklist does this in seconds, without being clever. |

All tiers end the same way: *the fix isn't better guessing.*

## 5. Mechanics & house rules

- Single self-contained `index.html`; no CDN, no fonts, no `fetch`; nothing leaves the page.
- Truth values are fixed and pre-authored (the collection rule: simulate, guarantee the moment).
- Style tokens from `STYLE.md`. Roles: purple `--agent` for the report voice; the student's
  grades are teal `--user`. Verdicts green/red with words, never colour alone.
- Trust/Doubt are `<button aria-pressed>`; reveal strip text includes TRUE/FALSE words; band is
  `role="status" aria-live="polite"`; keyboard-navigable; readable at 1024×768; usable at 375px.
- `?present` mode bumps the type scale for projectors.

## 6. Pairing

Warm-up for **Lab 7 — Trust, Then Verify** (`programming-labs`): the toy proves in ninety
seconds that prose can't be graded, so the lab's claim → check → verdict ledger feels necessary
rather than paranoid. Statement 1 is the lab's sham check, met a few minutes early.
