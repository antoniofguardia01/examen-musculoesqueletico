# Design

<!-- impeccable:design-schema 1 -->

## World

"Radiograph / scan room." The product identifies bones and muscles from real class diagrams, so the surface borrows the material world of an X-ray light box and film jacket: near-black film-blue ground, a single phosphor-cyan accent, hairline rules, mono stamp labels, precise sharp corners. Chosen 2026-09 to replace the earlier cream/green heraldic identity, at the user's explicit request, in favor of something minimalist, modern, bold, and animated.

Mode: primarily **Operate** (the student drilling questions) with a **Persuade**-flavored entry moment (the hero "plate"). Expression never outranks legibility of question content — the prompt/body text stays in a clean workhorse grotesk even where headlines get the bold condensed treatment.

## Color

Strategy: **Restrained** (neutrals + one accent), pushed hard at the accent's few moments (buttons, active states, the streak stat, the scan-sweep motion) rather than spread thin.

```
--bg          #0A0D10   page ground (film-blue-black, not pure black)
--bg-elev     #12161B   cards, stat tiles, tab rail
--bg-elev-2   #1A2025   inputs, options, chips (resting)
--bg-elev-3   #222930   active/selected surfaces, card header
--line        #242B31   hairline borders (resting)
--line-bright #39424A   hairline borders (cards, focal edges)
--ink         #EAF0F2   primary text
--ink-soft    #8B98A0   secondary text / labels
--ink-dim     #8B98A0   tertiary text (aliased to ink-soft — kept as a
                         separate token for future differentiation, but
                         must stay ≥4.5:1 on both --bg and --bg-elev)
--accent      #5EEAD4   the one accent — phosphor cyan
--accent-dim  #2DA593   accent borders / dashed rules
--accent-ink  #04211C   text/icon color on accent-filled surfaces
--accent-soft / --accent-soft-strong   rgba(94,234,212, .10 / .18) tints
--good        #4ADE80   correct state
--bad         #FB7185   incorrect state
```

All text-on-background pairs are verified ≥4.5:1 (body/labels) or ≥3:1 (large text) — recheck any new pairing before shipping it, including against composited backgrounds (radial vignette, tinted cards), not just the flat token values.

Dark is the deliberate scene: students drill on a phone at night or between classes, and the brief explicitly asked for a "dramatic, scanner/X-ray" dark direction over a light editorial one.

## Type

- **Display** — Big Shoulders Display, 800–900 weight, uppercase, tight leading (`line-height:.94`). Hero title and exam-results score only. `clamp()`-sized, never a fixed px past mobile.
- **Body / UI** — Archivo, 400–700. Question prompts, options, buttons, inputs. Chosen for a clean, confident grotesk that stays legible at exam-question length; body/prompt text is never set in the display face.
- **Mono / data** — JetBrains Mono, 500–700. Stat numbers, point badges, question-type tags, corner stamps, filter counts, word-bank codes — anything that reads as a technical readout or label.

Functional text floor: 11px, no exceptions (including decorative mono corner labels) — the mechanical detector enforces this; do not reintroduce anything under 11px.

## Shape & elevation

- Radius scale is small and precise: `--radius-sm:4px`, `--radius:6px`, `--radius-lg:10px` (cards). Sharper than a typical soft-UI scale, to read as clinical/technical rather than friendly-rounded.
- Static surfaces (the card, the diagram frame) commit to a **defined edge**: a `1px solid var(--line-bright)` border, no accompanying blur shadow. Reserve `--shadow-card` for surfaces that actually lift on interaction (`.stat:hover`, `.opt:hover`, `.id-opt:hover`) — never pair a hairline border with a wide diffuse shadow on the same resting element (the design-hook detector flags this combination).
- The scanned worksheet/diagram images keep their real white paper background — they are genuine class materials and must stay legible; do not invert or recolor them.

## Motion

One signature moment, not scattered effects: a slow (`6s`, `linear`, `infinite`) horizontal scan-line sweep on `.card::after`, top to bottom, fading in/out at the ends — the "scanner reading the page" motif. It is the only looping/ambient animation on the page.
Everything else is a one-shot: freshly-rendered question content (`.prompt`, `.opt`, `.id-opt`, `.bank`, `.pareo-row`, `.order-item`, …) fades/slides in once (`revealUp`, staggered by `nth-child` on list-like groups) because those DOM nodes are recreated per question; it is not re-triggered by JS.
The hero reticle mark pulses gently (`markPulse`, `3s`) as the page's one other ambient detail.
Exam progress uses `transform:scaleX()` (not `width`) so the fill animates on the compositor, not layout.
Glow is spent deliberately in exactly two places — the scan-sweep line and the reticle mark — both `filter:drop-shadow`, not `box-shadow`. Do not add colored `box-shadow` glows to hover/active states generally; the detector treats that as a default AI-UI tell. Prefer border-color + a neutral `box-shadow:var(--shadow-card)` for hover lift instead.

## Components (conventions, not an exhaustive list)

- **Top tabs / mode toggles**: pill rail (`--bg-elev`, 1px border) with a raised inner tile (`--bg-elev-3` + `inset` ring in `--accent-soft-strong`, no glow) for the active state.
- **Stat tiles**: mono numerals, `--ink`; the streak tile alone takes the accent color — it's the one stat meant to feel rewarding.
- **Card header**: `--bg-elev-3` strip, mono uppercase tag in `--accent`, point badge as an accent-tinted pill.
- **Options / chips**: resting on `--bg-elev-2`; selected = accent border + `--accent-soft` fill; correct = `--good`; incorrect = `--bad`. Same three-state vocabulary everywhere an answer can be marked (`.opt`, `.id-opt`, `.pareo-input`, `.fill-input`, `.order-num`, `.id-write-input`).
- **Buttons**: primary = solid `--accent` fill with `--accent-ink` text (dark-on-cyan, not white-on-cyan); secondary = accent-outlined ghost.
- **Hero "plate"**: a single bordered frame — corner mono labels (subject / product line, stacked on mobile), a pulsing reticle mark in place of a logo, the display headline, a mono subline, and the institutional credit line. No kicker/eyebrow above the headline (the headline carries its own weight).

## Provenance

No produced raster assets in this pass — the whole redesign is CSS/SVG/type; the two pre-existing raster assets (`assets/header-banner.png`, `assets/beaver-bg.jpg`) are no longer referenced by the page and were left in the repo rather than deleted.

## Open items

- The scanned worksheet diagrams (skeleton/muscle images) are real class materials on white paper and are intentionally not restyled — flagged here so a future pass doesn't "fix" that contrast against the dark card.
- No formal comp/finish-review round was run for this pass (single-file static site, no subagent/image-gen tooling invoked); verification was manual browser QA (desktop + mobile, all five question types, both practice modes, exam mode, keyboard nav) plus the mechanical `impeccable detect` pass, clean except one accepted advisory (the hero's ruler-tick rule, a single deliberate compositional device, not tiled decoration).
