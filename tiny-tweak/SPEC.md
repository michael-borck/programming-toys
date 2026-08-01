# Tiny Tweak — build specification

Sufficient to rebuild the toy from scratch. This toy was itself built from this spec — the
collection practises what it teaches.

---

## 1. The one thing it teaches

**A change's size is decided by the inside of the product, and you can't see the inside — so
"just quickly" is a guess, not a measurement.**

The student sees a small coffee-run order page and six innocent change requests. For each they
guess Small / Medium / Large; the card immediately reveals the real size — spots touched,
approximate lines, and the ripple of consequences — and keeps score. The requests are authored
so surface cues mislead: the visual change is tiny, the one-word wording change isn't, and the
"nice little convenience" is a monster.

**The "wait, what?" moment** (if a build doesn't produce this, it isn't finished):

> Changing the button colour: 1 line. Changing "Cheers!" to "Thanks!": three places, because
> the same word lives in the banner, the copied café summary, and the receipt — *miss one and
> the product disagrees with itself.* The wording change outweighs the visual one, and every
> instinct said otherwise.

Secondary beats, all mandatory:

- **One request is genuinely tiny** (the button colour) and its reveal says so: *sometimes tiny
  is tiny — the point isn't that everything is big, it's that you can't tell from out here.*
  Without this, the toy teaches paranoia instead of measurement.
- **One reveal contains a non-code question** (the euros request: *which exchange rate, whose
  rounding rules?*) — some of a change's size lives outside the code entirely, in decisions
  only the client can make.
- **The closing names the pro move**: before saying "just quickly," ask the agent — *"what does
  this actually touch?"* The inside is invisible, but it answers questions.

## 2. Screen layout

Single column, max-width ~56em:

1. **The product card** (purple — compact, `aria-hidden` static mock of the coffee-run order
   page: name field, drink list with prices, Add button, order rows, total, Copy-for-the-café
   button, "Cheers!" confirmation line). Caption: *this is all you can see. Now size some
   changes.*
2. **Legend strip**: S = 1–2 spots touched · M = 3–5 · L = 6+ (or a question the code can't
   answer).
3. **Six request cards**, each with the client's sentence and three guess buttons **S / M / L**
   (`aria-pressed`). Guessing reveals that card immediately: the true size, spots touched,
   ~lines, and the ripple as a short list. Card border tints green (guessed right) or red
   (missed), always with words.
4. **The verdict band** (`role="status" aria-live="polite"`): running score; after all six, the
   tier text.
5. **Closing prose card**: the pro move, plus: *"small change, small work" assumes the outside
   predicts the inside — it never did, in any era of programming.*

## 3. The requests, exactly

| # | Request | Truth | Spots · ~lines | Ripple (spirit) |
|---|---|---|---|---|
| 1 | "Make the Add button blue instead of orange." | **S** | 1 · 1 | None. Sometimes tiny is tiny — you just couldn't *know* from out here. |
| 2 | "Change 'Cheers!' to 'Thanks!'" | **M** | 3 · 3 | The word lives in the banner, the copied summary, and the receipt. Miss one and the product disagrees with itself. |
| 3 | "Add oat milk (+$0.50) as an option." | **M** | 5 · ~12 | Options list, price table, order rows, summary text — and anything touching money touches the checks. |
| 4 | "Show prices in euros as well." | **L** | 9 · ~40 | Every price appears twice, totals and summary double, the phone layout squeezes — plus a question no code can answer: whose exchange rate, updated when? |
| 5 | "Let people edit a drink after adding it." | **L** | 7 · ~60 | New state, edit controls on every row, live totals, brand-new failure modes (edit a name to empty?), and checks for all of it. |
| 6 | "Remember my usual order." | **L** | 8 · ~45 | Storage, first-run behaviour, a forget button (it's personal data now), and what happens when prices changed since last time. Ten lines of feature; the consequences are the product. |

Guess-matching: exact letter match scores. Fixed truths, fixed order (easy → misleading).

## 4. Verdict tiers (after all six)

| Score | Text (spirit) |
|---|---|
| 0–2 | The outside told you nothing — as it told everyone. "Just quickly" has cost the industry more than any bug. |
| 3–4 | Half right — and each miss was a sincere promise you'd have made to a client. |
| 5–6 | Sharp. Now notice you *still* had to be told the insides — you measured well only where you guessed what the code hides. The agent will just tell you: ask. |

All tiers end with: *the fix isn't better guessing — ask what it touches.*

## 5. Mechanics & house rules

- Single self-contained `index.html`; no CDN, no fonts, no `fetch`; nothing leaves the page.
- Truth values pre-authored (the collection rule: simulate, guarantee the moment).
- Style tokens from `STYLE.md`. Roles: purple `--agent` for the product mock and reveals (the
  inside is the machine's domain); guess buttons take the standard selected state. Verdict
  green/red always paired with words.
- Guess buttons are `<button aria-pressed>`; reveals are text; band is `role="status"
  aria-live="polite"`; keyboard-navigable; readable at 1024×768; usable at 375px.
- `?present` mode bumps the type scale for projectors.

## 6. Pairing

Warm-up for **Lab 9 — The Last 20%** (`programming-labs`): the polish ledger's size-guess
column is this toy played for real, and the lab's S-that-went-L trap (humanising times, the
grey button dragging in the two-blues problem) is request #2's lesson at full scale.
