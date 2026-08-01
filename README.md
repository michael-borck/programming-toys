# Programming Toys

> **Part of the Speak Software series** — twelve hands-on labs teaching programming at the
> natural-language level, in [`programming-labs`](https://github.com/michael-borck/programming-labs).

Small self-contained web pages, each built to break **one** specific misconception about
programming with AI that lecture slides reliably fail to break.

No install, no account, no network, no backend. Save any page and it still works — in an offline
lab, from a USB stick, or uploaded to an LMS as a single file.

## The toys

| Toy | Kills | Pairs with lab | Status |
|---|---|:--:|:--:|
| **[Three Interpretations](three-interpretations/)** | "the AI knows what I meant" — one vague brief, three valid products; add spec lines and watch the space collapse | 3 | ✅ ready |
| **[Next Word](next-word/)** | "it thinks like me" — watch next-word choice happen, dice and all, from boring to unhinged | 1 | ✅ ready |
| **Demo Illusion** | "the demo is the product" — shiny app, then flip the *real users* toggle | 2 | 💡 designed |
| **Context Porthole** | "it sees what I see" — everything you know vs the porthole the agent looks through | 6, 7 | 💡 designed |
| **Confidence Dial** | "fluent = true" — statements at identical confidence; guess which are false | 7 | 💡 designed |
| **Tiny Tweak** | "small change, small work" — request a 'tiny' change, watch the actual blast radius | 9 | 💡 designed |

Add `?present` to any toy (e.g. `three-interpretations/?present`) to bump type sizes for a
projector.

## House rules

Inherited from the sibling collection [`security-toys`](https://github.com/michael-borck/security-toys),
which set the pattern. Every toy obeys all seven:

1. **Single self-contained `index.html`.** No CDN, no external fonts, no `fetch`. This is the
   load-bearing rule: it survives an offline lab, an LMS upload, and 2029.
2. **One idea per toy.** If it needs a tutorial, it's too big.
3. **Playable in 90 seconds** from cold, by someone who read no instructions.
4. **A named "wait, what?" moment** — the instant the misconception breaks. It's in every
   `SPEC.md`. If a build doesn't produce it, the build isn't finished.
5. **Shared identity** — the palette and type scale in [`STYLE.md`](STYLE.md).
6. **`?present` mode** for projection.
7. **A `SPEC.md` per toy**, sufficient to rebuild it from scratch.

Plus one absolute: **nothing leaves the page.** No storage, no analytics, no backend, anywhere in
this collection.

And one rule this collection adds:

8. **Every toy is vibe-coded from its own `SPEC.md`** — and says so. The collection demonstrates
   the method the labs teach: the spec is sufficient, the build is replaceable, and you can run
   the Replication Test on any toy here yourself. Try it.

One consequence worth stating: no toy ever calls a live model. The toys *simulate* the agent with
pre-authored content, because the misconception must break in 90 seconds, guaranteed, offline. The
labs provide the live experience; the toys provide the guaranteed one.

## Adding a toy

1. `cp -r three-interpretations/ new-toy/` — the scaffold *is* an existing toy
2. Write `SPEC.md` **first** (house rule 8 — the spec is the source; the build is the output)
3. Vibe-code `index.html` from it; paste the tokens from [`STYLE.md`](STYLE.md)
4. Write a short `README.md`
5. Add a card to the root `index.html` and a row to the table above

## What this deliberately doesn't have

No test framework (the check is manual: opens from `file://`, works with no network, readable at
1024×768 on a projector, usable on a phone, keyboard-navigable). No analytics. No framework, no
build step. No backend.

## Licence

MIT. Unit-agnostic teaching material — no institution or course branding.
