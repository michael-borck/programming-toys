# Three Interpretations — build specification

Sufficient to rebuild the toy from scratch. This toy was itself built from this spec — the
collection practises what it teaches.

---

## 1. The one thing it teaches

**The AI doesn't know what you meant — a vague brief selects a *space* of products, and the agent
picks one without telling you it picked.**

The student sees one eight-word brief produce three different, individually defensible products.
Then they add plain-language spec lines and watch the space collapse: each line rules products out,
until one remains — at which point they have programmed, in English, without noticing.

**The "wait, what?" moment** (if a build doesn't produce this, it isn't finished):

> All three products sit side by side under the same brief, each captioned with its perfectly
> reasonable reading of the same eight words — and a line of text says: **none of them misheard
> you.** The ambiguity was never in the agent.

Secondary beats, both mandatory:

- **The contradiction state.** Some spec lines conflict. Select a contradictory set and *zero*
  products survive — and the toy says what a real agent would do: silently drop one of your
  requirements and build anyway, without telling you which.
- **The never-closes coda.** When exactly one product survives, the win text must include: run the
  same spec tomorrow and the survivor still varies in everything you didn't pin. A spec narrows
  the space; it never closes it.

## 2. Screen layout

Single column, max-width ~68em:

1. **The brief** (teal card — the student's side): the fixed text *"Make a tool that helps people
   split bills."* presented as a client's request. No input — the brief is deliberately not
   editable; the toy is about what happens *after* those words leave your mouth.
2. **Three product panels** in a row (purple cards — the agent's side), collapsing to one column
   below 820px. Each panel: product name, a small pure-CSS mockup, a caption *"How it read your
   eight words"*, and a status badge (`VALID` / `RULED OUT`).
3. **The spec builder** (teal card): six toggle chips, each one plain-language "done means" line.
   Heading: *"Now say what you meant — add the words you thought were obvious."* Plus a Reset.
4. **The verdict band** (`role="status" aria-live="polite"`): survivor count and the state text.
5. **Closing prose card**: the lesson in two sentences, always visible.

## 3. The three products

| | Name | Mockup shows | "How it read your eight words" |
|---|---|---|---|
| A | **Even Split** | total + people inputs, big per-head figure | "split" = divide equally · "bills" = tonight's one bill · "people" = whoever's at the table |
| B | **House Ledger** | named housemates with running +/− balances, add-expense button | "split" = share ongoing costs · "bills" = rent, wifi, power · "people" = named housemates with a history |
| C | **Item-by-Item** | receipt lines assigned to names, proportional tip/tax footer | "split" = pay for what you had · "bills" = an itemised receipt · "people" = whoever ordered what |

All three must look like *real products someone shipped* — distinct shapes at a glance, readable in
five seconds, built entirely from styled divs (no images, no canvas).

## 4. The chips and the verdict matrix

Six chips. ✓ survives, ✗ ruled out:

| Chip | A | B | C |
|---|:-:|:-:|:-:|
| Usable in 30 seconds at the table | ✓ | ✗ | ✓ |
| No accounts, no sign-in, nothing saved | ✓ | ✗ | ✓ |
| People can owe different amounts | ✗ | ✓ | ✓ |
| Tip and tax split by what each person had | ✗ | ✗ | ✓ |
| Remembers who owes whom across months | ✗ | ✓ | ✗ |
| Handles recurring bills like rent | ✗ | ✓ | ✗ |

Properties this matrix must keep (re-verify if editing):

- `{owe different amounts, tip/tax by consumption}` → only **C** survives (the restaurant path)
- `{remembers across months}` → only **B** survives (the housemate path)
- `{nothing saved, remembers across months}` → **zero** survive (the contradiction path)
- No single chip eliminates two products on its own except tip/tax and the two B-only chips —
  early clicks should feel surgical, not explosive.

A ruled-out panel greys, keeps its text readable, and shows a red tag quoting the *first* selected
chip that killed it: `✗ ruled out — "no accounts, no sign-in, nothing saved"`.

## 5. States of the verdict band

| Survivors | Band | Text (spirit, not verbatim) |
|---|---|---|
| 3, no chips | neutral | All three are valid. None of them misheard you. The ambiguity is in your head — start adding the words you thought were obvious. |
| 3–2, chips on | neutral | N readings still valid. Every word you add does work no agent can do for you. |
| 1 | good | **You just programmed.** You wrote no code — you eliminated products with words until one remained. That's a spec. (…then the never-closes coda from §1.) |
| 0 | bad | Your spec contradicts itself. A real agent won't stop — it will silently drop one requirement and build anyway. You won't know which one until the demo. |

## 6. Mechanics & house rules

- Single self-contained `index.html`. No CDN, no fonts, no `fetch`, nothing leaves the page.
- Interpretations are **pre-authored, never generated** — the toy simulates the agent so the
  moment is guaranteed in 90 seconds (see the series `DECISIONS.md`).
- Style tokens pasted from `STYLE.md`. Role colours: teal `--user` for everything the student
  controls (brief, chips), purple `--agent` for everything the agent decided (the three panels).
  Verdict colours fixed: green good, red bad.
- Chips are `<button aria-pressed>`; state is words + colour, never colour alone; band is
  `role="status" aria-live="polite"`; fully keyboard-navigable; readable at 1024×768; usable at
  375px.
- `?present` mode bumps the type scale for projectors.

## 7. Pairing

Warm-up for **Lab 3 — Say What You Mean** (`programming-labs`). The lab delivers the live version
of this experience with real agents; the toy delivers the guaranteed version in 90 seconds.
