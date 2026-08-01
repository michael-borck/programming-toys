# Next Word — build specification

Sufficient to rebuild the toy from scratch. This toy was itself built from this spec — the
collection practises what it teaches.

---

## 1. The one thing it teaches

**The model isn't answering you — it's continuing you. There is no sentence in there; there is
only ever the next word.**

The student watches a sentence get built one word at a time: at every step they see the candidate
next words with their probabilities, watch dice fall on one, and see the bars redraw for the step
after. A dial from **Boring** to **Unhinged** reshapes those probabilities live — the same dial
every real AI product ships under the name *temperature*.

**The "wait, what?" moment** (if a build doesn't produce this, it isn't finished):

> At the Boring end, every run produces the *word-for-word identical* sentence, forever — the
> history list proves it and labels the duplicates. One nudge of the dial and the same prompt
> scatters into different endings on every run — and the bars show exactly why. Nothing in there
> "decided" anything. It was the favourite word, or it was dice.

Secondary beats, both mandatory:

- **Forced steps teach too.** Some steps show a single candidate at ~100% ("practically
  forced") — mid-sentence, the next word is often nearly certain. Fluency is momentum, not
  intent.
- **The honesty caption**, always visible: *it has never read the end of its own sentence — there
  is only ever: given these words, which word next?*

## 2. Screen layout

Single column, max-width ~60em:

1. **The sentence card**: the fixed prompt *"To be successful, a business must"* in teal (the
   student's words), generated words appended in purple (the machine's picks), a caret while
   incomplete. The honesty caption sits under it.
2. **The dial card** (teal — the student controls it): a slider from **0 · Boring** to
   **3 · Unhinged**, default 1.0. Moving it redraws the candidate bars *live, between steps* —
   that's the point of it. At exactly 0 the toy always picks the favourite (no dice); the label
   says so.
3. **The candidates card** (purple — the machine's decision space): the next-word candidates as
   rows — word in monospace, animated probability bar, percentage — sorted by current adjusted
   probability. Controls: **Next word** (one step), **Run to the end** (auto-step ~0.6s), **Start
   over**. A live line reports each pick: *chose "listen" — had a 21% chance*.
4. **The history card**: every finished sentence, tagged with the dial value it ran at.
   Word-for-word repeats get a highlighted tag — *identical to run N* — because the repeats ARE
   the lesson at 0, and their absence is the lesson at 2+.
5. **Closing prose card**: real models do exactly this with ~50,000 word-pieces and a
   trillion-word reading habit, thousands of times per answer; the dial ships in real products as
   *temperature*. This is why the same prompt gives your classmate a different app (→ Lab 3).

## 3. The word graph

No model, no network: a hand-authored word-level graph. Each node = a list of
`[word, weight, nextNode]` options; terminal words end with `.`. Weights make ordinary
continuations dominant and whimsy rare, so Boring feels like a keynote and Unhinged feels like a
fever dream. Target ~20 reachable endings; the spirit of the bank (weights: 🟢 heavy / 🟡 mid /
🔴 rare):

- 🟢 …understand what its customers actually want. / secretly need.
- 🟢 …understand what people refuse to say.
- 🟢 …understand its numbers before its numbers understand it.
- 🟡 …understand its own story. / appetite.
- 🟢 …listen more than it talks.
- 🟡 …listen to the quietest person in the room. / to the angriest customer first.
- 🟢 …make something people would miss if it vanished. / closed.
- 🟡 …make a profit, eventually, ideally on purpose. / a profit, somehow.
- 🟡 …move faster than its excuses. / its doubts. · …move slowly and fix things.
- 🟡 …charge what it is actually worth. / enough to survive its own success.
- 🔴 …befriend the weather. / the postman. / its competitors' unhappy customers.
- 🔴 …outrun the rumour of its own decline.
- 🔴 …apologise to the ocean. / to the intern.

The first step must offer 6–8 candidates (the widest choice), later steps mix real branches with
forced chains.

## 4. The dial (temperature), exactly

Adjusted probability of option *i* with raw weight *w<sub>i</sub>* at dial value *T*:

- `T = 0`: the favourite gets 100%, deterministically (ties: first listed). No sampling.
- `T > 0`: `p_i = w_i^(1/T) / Σ w_j^(1/T)` — below 1 sharpens toward the favourite, above 1
  flattens toward uniform. Bars and percentages recompute on every dial input event.

Sampling uses plain `Math.random()` against the adjusted distribution.

## 5. Mechanics & house rules

- Single self-contained `index.html`; no CDN, no fonts, no `fetch`; nothing leaves the page.
- Style tokens from `STYLE.md`. Roles: teal `--user` = prompt + dial (what you control), purple
  `--agent` = candidates + generated words (what the machine picks). Never re-mapped.
- Buttons are real `<button>`s; the slider is `<input type="range">` with a visible value and an
  `aria-label`; picks and run-completions announce via `role="status" aria-live="polite"`;
  percentages are text, never bar-width alone; keyboard-navigable throughout.
- `?present` mode bumps the type scale for projectors.
- Playable in 90 seconds with no instructions: the affordances are three buttons and a slider.

## 6. Pairing

Warm-up for **Lab 1 — Hello, Department of One** (`programming-labs`): before (or right after)
their first one-shot build, the student sees what the "intelligence" mechanically is — and the
Lab 1 reveal prompt *"what did you decide that I never asked for?"* gains its real answer: every
word was a dice roll among candidates you never saw.
