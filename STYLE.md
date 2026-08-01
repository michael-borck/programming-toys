# Shared style

House rule 1 says every toy is a **single self-contained file**, so there is no shared stylesheet
to link — that would make a toy unable to travel on its own, which is the property worth
protecting. Consistency comes from pasting the block below instead. Duplicating ~30 lines of CSS
six times is a much cheaper problem than a toy that only works inside its folder.

Inherited from the sibling collection `security-toys` (which inherited it from
`defence-in-depth`), so the two collections read as one family on a course site.

## Paste this into every toy

```css
:root{
  --bg:#0b1220; --panel:#111a2e; --panel2:#0e1626; --line:#22304d;
  --ink:#e6edf7; --muted:#93a4c3;
  --accent:#fbbf24; --good:#34d399; --warn:#fbbf24; --bad:#f87171;
  --user:#2dd4bf; --agent:#a78bfa;
  --fs:16px;
}
body.present{--fs:20px;}
body{
  background:radial-gradient(1200px 800px at 30% -10%, #16223c 0%, var(--bg) 55%);
  color:var(--ink); font-family:ui-sans-serif,system-ui,-apple-system,"Segoe UI",Roboto,sans-serif;
  font-size:var(--fs);
}
.card{background:var(--panel); border:1px solid var(--line); border-radius:14px; padding:14px 16px;}
h3{font-size:.72em; text-transform:uppercase; letter-spacing:1.2px; color:var(--muted);}
```

And the projector switch, at the end of every toy's script:

```js
if(new URLSearchParams(location.search).has("present")) document.body.classList.add("present");
```

## Rules for using it

- **Size everything in `em`**, never `px`, so `?present` scales the whole page from one variable.
  A hard-coded `font-size:14px` is a bug — it won't grow on the projector.
- **Selected state** is always `border-color:#3b82f6` + `linear-gradient(180deg,#1a2a4a,#12203d)` +
  `box-shadow:0 0 0 1px #3b82f655`, and is expressed with `aria-pressed`, not a class, so screen
  readers get it free.
- **Verdict colours are fixed**: `--good` green, `--warn` amber, `--bad` red. Don't re-map them
  per toy — a red band must mean the same thing in every toy.
- **Monospace only for data** the student is meant to read as a value: amounts, diffs, tokens,
  code. Never for prose.

## Role colours

This collection's central visual argument is *who decided what*. Two roles carry it — keep them
consistent across every toy:

| Role | Token | Colour |
|---|---|---|
| What **you** control — briefs, specs, chips, prompts | `--user` | `#2dd4bf` teal |
| What **the agent** decided — builds, guesses, claims | `--agent` | `#a78bfa` purple |

The whole series turns on moving things from purple to teal — from *the agent guessed* to *you
said*. A student who plays every toy should absorb that mapping without it ever being taught.

(`security-toys` uses teal/purple/red for user/system/attacker; `--agent` here sits on the same
purple as its `--system` — the entity that decides things you didn't specify.)

## Accessibility floor

Every toy must clear this, checked by hand:

- Contrast ≥ 4.5:1 for body text against `--panel` (the palette above already does)
- Fully keyboard-navigable; visible focus ring (don't remove the default outline)
- Live results in `role="status" aria-live="polite"` so the answer is announced, not just drawn
- Colour is never the *only* signal — pair every band with a word
- Readable at 1024×768 and usable at 375px wide
