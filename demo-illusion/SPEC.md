# Demo Illusion — build specification

Sufficient to rebuild the toy from scratch. This toy was itself built from this spec — the
collection practises what it teaches.

---

## 1. The one thing it teaches

**"It works" means "it worked for me, once, used the way I imagined." A product is the version
that survives everyone else.**

The student meets a shiny one-shot app — *SplitEase, split any bill in seconds* — watches the
happy-path demo land perfectly, and is invited to ship it Friday. Then they let real users in,
one at a time, and watch the same unchanged app print `$NaN`, invoice negative money, and divide
by zero — live.

**The "wait, what?" moment** (if a build doesn't produce this, it isn't finished):

> The first stranger presses the button with the boxes empty and the app says **"$NaN each"** —
> twenty seconds after the same app, untouched between then and now, said "$30.00 each" and felt
> finished. The closing line lands it: *same app, not one line changed. What changed was who
> used it.*

Secondary beats, all mandatory:

- **The failures are real, never staged.** The embedded app is implemented exactly as naively as
  a one-shot would write it (two lines: divide, then print). Simulated users put real values
  into the real inputs and the page runs the real code — `$NaN`, `$Infinity`, `$-21.13`,
  `$8.333333333333333e+22` are the app's actual output. The app's entire brain is shown as a code snippet in
  the closing card, so nobody can claim the toy cheated.
- **The failures become sentences.** After the last user, a teal card converts each failure into
  one plain-language done-means bullet — purple wreckage turning into teal spec lines, the
  collection's whole colour argument in one reveal. Caption: writing these before the demo is
  Lab 2; writing them before the build is Lab 3.

## 2. Screen layout

Two columns (app left, user feed right), collapsing to one below 820px:

1. **The app card** (purple — the agent built it): "SplitEase" with a tagline, two text inputs
   (bill total, people), a Split button, and a big result figure. The app inputs are genuinely
   usable by the student. The app sits inside a *frame* the toy can narrow to phone width — the
   app's own layout has a fixed minimum width, so narrowing genuinely clips it.
2. **Controls**: **Run the demo ▸** (auto-plays the happy path: 120 and 4 → "$30.00 each"),
   **Let a real user in ▸** (one stranger per click), **Let them all in ▸▸** (auto ~2.5s),
   **Start over ⟲**.
3. **The queue card**: a feed. First entry is You (demo day, green ✓). Each stranger appends:
   initial-avatar, name, what they did, and the app's actual output as a red ✗ chip.
4. **The verdict band** (`role="status" aria-live="polite"`): tally — *Survived: 1 of N users* —
   and state text.
5. **The done-means card** (teal, hidden until the last user has been in): the bullet list born
   from the failures.
6. **Closing prose card**: the app's entire brain (the naive code, monospace) plus the lesson —
   the gap between demo and product is closed by watching, defining, and directing, not by luck.

## 3. The users, exactly

Happy path: **You** — total `120`, people `4` → `$30.00 each` → ✓ "Ship it Friday?"

The strangers (order fixed; each row = inputs put into the real app):

| User | Does | Real inputs | Real output |
|---|---|---|---|
| Priya, in a hurry | presses Split with everything empty | `""` / `""` | `$NaN each` |
| Marcus, types like a human | writes the total in words | `one twenty` / `4` | `$NaN each` |
| Ana, solo diner | zero people | `60` / `0` | `$Infinity each` |
| Sam, the refund | negative total | `-84.50` / `4` | `$-21.13 each` |
| Dee, company dinner | pastes an absurd total | `999999999999999999999999` / `12` | `$8.333333333333333e+22 each` |
| Rosa, on the bus | opens it on her phone | *(frame narrows to ~20em)* | layout clips; the button is off-screen |

Rosa's failure is layout, not arithmetic: the toy narrows the app frame and the fixed-width app
genuinely overflows. Her feed line: *can only see half the app — the demo never left your
laptop.*

## 4. The done-means reveal

One bullet per failure class, in the strangers' order:

- Any input that isn't a number gets a polite message — never NaN.
- Zero or missing people explains itself — nothing divides by zero.
- Negative amounts are refused in words, not invoiced.
- Absurd totals get a sanity check before they get arithmetic.
- Readable and usable on a phone held in one hand.

## 5. Mechanics & house rules

- Single self-contained `index.html`; no CDN, no fonts, no `fetch`; nothing leaves the page.
- The naive splitter is one real function (`parseFloat`, `parseInt`, divide, `toFixed`, print).
  Simulated users set the real inputs and call it; feed text reads the real result element.
- Style tokens from `STYLE.md`. Roles: purple `--agent` for the app (the machine's build), teal
  `--user` for the done-means card (the student's words). Verdicts: green ✓ / red ✗, always
  paired with words.
- Buttons are real `<button>`s; the band is `role="status" aria-live="polite"`; feed entries are
  text, not colour alone; keyboard-navigable; readable at 1024×768; usable at 375px.
- `?present` mode bumps the type scale for projectors.
- Playable in 90 seconds with no instructions: the arc is three buttons read left to right.

## 6. Pairing

Warm-up for **Lab 2 — The Demo Illusion** (`programming-labs`): the toy is the lab's Part 1 in
miniature — a guaranteed handoff disaster in ninety seconds — and its done-means reveal is the
lab's Part 2, demonstrated. The lab then does it for real, on the student's own Lab 1 product,
with a human they had to go and borrow.
