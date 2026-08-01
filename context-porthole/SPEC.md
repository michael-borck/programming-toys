# Context Porthole — build specification

Sufficient to rebuild the toy from scratch. This toy was itself built from this spec — the
collection practises what it teaches.

---

## 1. The one thing it teaches

**The agent doesn't see what you see. Each session it knows exactly two things: what's written
in the folder, and what's in your message. Everything else you "know" does not exist for it.**

The student holds seven facts about a project in their head, sends a task through the porthole,
and gets back work with three mistakes — each one annotated with the fact that would have
prevented it, and where that fact lived: *in your head*. Writing a fact into the folder makes
its mistake vanish on the next send, one for one.

**The "wait, what?" moment** (if a build doesn't produce this, it isn't finished):

> The first send returns three mistakes, and every single one carries the same tag: *the fact
> that would have prevented this was in your head.* The band says it plainly: **it didn't
> ignore you — it never heard you.**

Secondary beats, both mandatory:

- **One fact refuses to be written.** *"It should feel premium — you'll know it when you see
  it"* wobbles when clicked: there is no sentence for it. When every writable fact is written
  and the mistakes hit zero, this one remains, amber, permanently: *what's left isn't a
  mistake — it's judgement, and it doesn't fit through any porthole.* The series' thesis, in
  one leftover chip.
- **The fix is always the folder, never the chat.** Facts animate into the specific file where
  they belong (`AGENTS.md`, `SPEC.md`, `DECISIONS.md`) — reinforcing Lab 6's file convention by
  sight.

## 2. Screen layout

Single column, max-width ~64em:

1. **Your head card** (teal): *"In your head — 7 things you know."* Three writable fact chips,
   one unwritable taste chip, and a note that three more are already written down (pointing at
   the folder card). Clicking a writable chip writes it into its destination file; clicking the
   taste chip wobbles it and explains itself.
2. **The porthole card** (purple): the folder as four file boxes — `AGENTS.md`, `SPEC.md`,
   `DECISIONS.md`, `checks/` — each listing its written lines (three pre-written facts at
   start; grows as the student writes), plus the outgoing message: *"Add a 'settle up' screen
   showing who pays whom."* Caption: *this card is everything the agent will know.*
3. **Send button** — *"Send it through the porthole ▸"* — and after the first send it re-runs
   automatically whenever a fact is written (with the button relabelled *Send again ▸*
   available too).
4. **What-came-back card**: the agent's work as a decision list — ✓ green lines for decisions
   backed by written facts (each citing its file), ✗ red lines for the mistakes (each tagged
   *the fact that would have prevented this was in your head*), and one ⚠ amber line always:
   *"Does it feel premium? It can't know — that one's yours to look at."*
5. **The verdict band** (`role="status" aria-live="polite"`): mistake count and state text.
6. **Closing prose card**: the porthole is real — it's called the context window; "the agent
   doesn't remember, it re-reads" (Lab 6's margin note, verbatim); fix the folder, not the
   chat.

## 3. The facts, exactly

Task sent: *"Add a 'settle up' screen showing who pays whom."*

| Fact | Lives at start | Written into | If unwritten: the mistake | If written: the line |
|---|---|---|---|---|
| The client hates popups — everything inline | head | `AGENTS.md` | ✗ Opened the result in a popup dialog | ✓ Kept everything inline (AGENTS.md) |
| We rejected accounts and sign-in in week one | head | `DECISIONS.md` | ✗ Added sign-in so people can "save their debts" | ✓ No accounts — DECISIONS.md settled that in week one |
| The default tip changed to 10% last Tuesday (phone call) | head | `SPEC.md` | ✗ Used the old 0% default tip | ✓ Default tip 10% (SPEC.md) |
| Money is whole cents; shares sum to the exact total | `AGENTS.md` | — | — | ✓ Shares sum to the exact total (AGENTS.md) |
| The checklist runs before anything is "done" | `checks/` | — | — | ✓ Ran the checklist before saying done (checks/) |
| No spreadsheet-looking grids | `DECISIONS.md` | — | — | ✓ Avoided the grid layout (DECISIONS.md) |
| It should feel premium — you'll know it when you see it | head, **unwritable** | — | ⚠ always | ⚠ always |

## 4. States of the verdict band

| State | Band | Text (spirit) |
|---|---|---|
| Before first send | neutral | You know 7 things. Count what the porthole card shows: 4 written lines and one message. That's the whole delivery. |
| After a send, mistakes > 0 | bad | N mistakes — every one traces to a fact that lived only in your head. **It didn't ignore you. It never heard you.** Click a fact to write it down. |
| Mistakes = 0 | good | Every mistake was a missing sentence. The amber line stays: what's left isn't a mistake — it's judgement, and it doesn't fit through any porthole. |

## 5. Mechanics & house rules

- Single self-contained `index.html`; no CDN, no fonts, no `fetch`; nothing leaves the page.
- The "agent" is a pure function of the written-facts set — same inputs, same output, honestly
  simulated (see the collection rule: the toys simulate so the moment is guaranteed offline).
- Style tokens from `STYLE.md`. Roles: teal `--user` for the head and everything the student
  writes; purple `--agent` for the porthole contents and the returned work. Verdicts
  green/red/amber, always paired with words.
- Chips are `<button>`s (disabled once written); the band is `role="status"
  aria-live="polite"`; ✓/✗/⚠ are characters plus words, never colour alone; keyboard-navigable;
  readable at 1024×768; usable at 375px.
- `?present` mode bumps the type scale for projectors.

## 6. Pairing

Warm-up for **Lab 6 — Teach the Intern** (the folder is the memory; fix the folder, not the
chat) and **Lab 7 — Trust, Then Verify** (what the agent doesn't know, it doesn't know it
doesn't know). The amber chip is the series thesis carried forward into Lab 8.
