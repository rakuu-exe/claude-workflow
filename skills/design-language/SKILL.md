---
name: design-language
description: This user's own visual taste — minimal black and white interfaces, generous spacing, restrained motion — and the house numbers that override other design skills. Use before designing, building, restyling or reviewing any UI, page or component, and when discussing how something should look.
---

# Design language

This is the owner's taste. The other design skills in this plugin (Emil Kowalski's, impeccable, taste-skill) say how to do things well. This one says what the result should look like. Where they disagree with this file, this file wins.

## The idea

Simple enough that nothing needs explaining. A screen shows what the person came for and little else. Before adding an element, a colour, a border or an animation, ask what breaks if it is left out. If nothing breaks, leave it out.

## Colour

- Black, white and the greys between them. Build both a light and a dark theme from one neutral scale.
- No accent colour unless the owner asks for one. Emphasis comes from weight, size, space and contrast.
- Never pure `#000` text on pure `#fff` across a whole page, or the reverse. Step one notch in from each end so it is easy on the eyes.
- Borders and dividers are a faint grey, and used rarely. Space separates things before a line does.
- State colours (error, success) are the only exception, and they stay muted.
- All colours are tokens that switch with the theme. No raw colour values in components.

## Spacing

Spacing does most of the work in a minimal design, so it is never eyeballed.

- One scale, in px: 4, 8, 12, 16, 24, 32, 48, 64, 96. Every margin, padding and gap comes from it.
- Related things sit close, unrelated things sit far apart. The gap between groups is at least double the gap inside a group.
- Sections on a page get the large steps (64, 96), scaled down fluidly on small screens with `clamp()`.
- When a layout feels crowded, remove something or add space. Do not shrink the text.

## Type

- One typeface per project, two weights (regular and one heavier). A second family needs a reason.
- A short scale of sizes, each used for one job. Body text never smaller than 16px.
- Lines of text stay around 60 to 75 characters wide.

## Layout

- One main thing per screen, and it is obvious which.
- Left-aligned by default. Centre only short, standalone pieces.
- No card around something that does not need a boundary, and no cards inside cards.

## Motion

Motion is welcome, and it has a job each time: show where something came from, confirm an action, or tell the product's story on a landing page. Follow `emil:animate`, `emil:choreograph` and `emil:gestures` for how to build it. These house numbers replace the ranges those skills give:

| Rule | Value |
|---|---|
| Entrances | ease-out |
| Moves on screen | ease-in-out |
| Dropdowns and menus | 150–250ms |
| Exits | 20% shorter than the matching entrance |
| Popovers | start at `scale(0.95)`, grow from the trigger, shrink back to it |
| List rows appearing for the first time | 30ms stagger |
| Everyday UI | no bounce |
| Toggle knob while moving | stretches 12% along the direction of travel |
| Objects travelling across the screen | follow a slight arc, not a straight line |
| Success | one short pulse |
| Icon swap | crossfade with a small blur |
| Dragging past a limit | rubber-band |
| While the pointer is held down | follow it directly, no tween |
| Old and new state | overlap, never one fully gone before the next starts |
| Reveals and colour changes | a mask, where it reads better than a fade |
| One element moving between places | the same `layoutId` |
| Details inside a larger element | stagger in as the main element settles |

Menus, dropdowns and anything opened many times a day get no stagger at all, as `emil:choreograph` says.

Every animation has a reduced-motion version that keeps the fade and drops the movement.

### Signature pieces

Two effects the owner likes on landing pages. Use them there, not in product UI:

- **Scroll story.** The product is shown through a pinned, scroll-driven sequence. Simple reveals use CSS scroll-driven animations; pinning and scrubbing use GSAP ScrollTrigger.
- **Constellation.** Dots drift on a canvas at different speeds, lines join the ones that come close, and both dots and lines fade in and out with distance and age. Monochrome, low contrast, behind the content. It pauses off-screen and in a hidden tab, and draws one still frame under reduced motion.

## What to avoid

- Gradients as decoration, glows, coloured shadows, glass blur for its own sake.
- A centred hero above three identical cards.
- Icons added to fill space, emoji as icons.
- Several things animating at once to look lively.

## When discussing a design

Describe the proposal in plain words first: what is on the screen, what is left out and why, and where motion is used. Offer one recommendation, and a second option only when there is a real trade-off. Build after the owner agrees.
