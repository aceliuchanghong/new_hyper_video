---
name: Terminal Pulse
colors:
  bg: "#0B1020"
  bg-elev: "#121A2E"
  ink: "#E6EDF3"
  ink-dim: "#8B98A9"
  accent: "#3DD9B0"
  accent-2: "#5BB8FF"
  warn: "#F0A35E"
  line: "#1E2940"
typography:
  display:
    fontFamily: Inter
    fontWeight: 700
  body:
    fontFamily: Inter
    fontWeight: 400
  code:
    fontFamily: JetBrains Mono
    fontWeight: 500
rounded:
  sm: 6px
  md: 12px
  lg: 20px
spacing:
  sm: 12px
  md: 24px
  lg: 48px
motion:
  energy: moderate
  easing:
    entry: "expo.out"
    entry2: "power3.out"
    ambient: "sine.inOut"
  duration:
    entrance: 0.6
    hold: 2.5
    transition: 0.5
  atmosphere:
    - grid-glow
    - cursor-blink
---

## Overview

Terminal / code-editor aesthetic for a developer-facing explainer. Deep navy-black canvas, a single mint-cyan accent that reads as a terminal highlight or active-token glow, monospace for all code, formulas, and labels. Breathable, not aggressive — content is dense (Chinese prose + code blocks), so the screen stays calm and lets the type lead. One glow color, one structure (the loop), disciplined.

## Colors

- `bg #0B1020` — base canvas (radial glow, never flat full-screen linear — banding)
- `bg-elev #121A2E` — cards / panels / code blocks
- `ink #E6EDF3` — primary text
- `ink-dim #8B98A9` — secondary / captions / labels
- `accent #3DD9B0` — the ONE highlight (terminal mint). Reserved for: the loop, formula operators, the cursor, active states.
- `accent-2 #5BB8FF` — sparing second accent for contrast pairs (e.g. Model vs Loop)
- `warn #F0A35E` — used ONLY on the "workflow ≠ Agent" warning beat
- `line #1E2940` — hairline dividers, borders

## Typography

- **Inter** for all display + body (Chinese + Latin). Weights 400/600/700.
- **JetBrains Mono** for all code, formulas, ASCII diagrams, and uppercase micro-labels. Weight 500.
- Display headlines 80–130px. Body 26–34px (Chinese needs the room). Code/formula 40–72px. Micro-labels 18–22px, letter-spacing 0.18em, uppercase.

## Elevation

Subtle. Cards are `bg-elev` with a 1px `line` border and a soft mint glow only on the focal element. No heavy drop shadows. Depth comes from the radial background glow, not boxes.

## Do's and Don'ts

- DO keep mint `#3DD9B0` scarce — it's the "this is the point" color.
- DO use JetBrains Mono for every formula, code block, and diagram label.
- DON'T use full-screen linear gradients (banding). Radial glow only.
- DON'T introduce colors outside this palette.
- DON'T use `warn` outside the workflow-≠-Agent beat.
