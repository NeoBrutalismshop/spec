# NeoBrutalism Interaction & Motion Grammar

This document defines the family-wide interaction laws for NeoBrutalism design systems. Every flavor (Rivet, Soft, Commerce, Terminal, Raw, etc.) may tune intensity, timing, distance, shadow depth, and color, but should preserve the same physical interaction logic.

## Core Law: Compress, Never Float

Interactive surfaces should feel physical. Hover must never make a button, card, chip, tab, or other control rise toward the user.

The default interaction model is:

1. **Rest** — the control sits above the surface with visible structural depth.
2. **Hover / proximity** — the control compresses slightly toward the surface.
3. **Press / active** — the control compresses fully, reducing or removing its offset shadow.
4. **Release** — the control returns with a short, controlled rebound.

The illusion should feel like touching and pressing a physical object rather than levitating a digital layer.

## Mechanical Press Model

For hard-shadow components, motion should be derived from shadow depth.

Example reference values:

```css
:root {
  --nb-depth-rest-x: 4px;
  --nb-depth-rest-y: 4px;
  --nb-depth-hover-x: 2px;
  --nb-depth-hover-y: 2px;
  --nb-depth-active-x: 0px;
  --nb-depth-active-y: 0px;
}

.nb-button {
  transform: translate(0, 0);
  box-shadow: var(--nb-depth-rest-x) var(--nb-depth-rest-y) 0 var(--nb-shadow-color);
}

.nb-button:hover {
  transform: translate(2px, 2px);
  box-shadow: var(--nb-depth-hover-x) var(--nb-depth-hover-y) 0 var(--nb-shadow-color);
}

.nb-button:active {
  transform: translate(4px, 4px);
  box-shadow: var(--nb-depth-active-x) var(--nb-depth-active-y) 0 var(--nb-shadow-color);
}
```

The exact values are flavor tokens, not hardcoded component values.

## State Ladder

Every interactive primitive should define at least these states:

- Rest
- Hover
- Focus-visible
- Pressed / active
- Selected / toggled
- Loading
- Disabled
- Success / completion where relevant
- Error where relevant

### Hover

Hover is **pre-contact**. It should suggest that physical contact is about to happen.

Preferred cues:

- small downward/inward translation
- reduced hard-shadow offset
- slight surface color change
- border emphasis
- icon micro-shift if semantically useful

Avoid:

- translating upward
- increasing elevation
- enlarging shadows away from the surface
- generic scale-up effects

### Pressed / Active

Pressed is **full contact**.

Preferred cues:

- full translation into the shadow offset
- shadow collapse or near-collapse
- subtle visual compression
- label/icon may shift with the surface

The press should feel decisive and immediate.

### Release

Release should restore depth quickly without feeling bouncy or toy-like by default.

Use a short controlled rebound. More playful flavors may increase overshoot; Soft should remain restrained.

## Motion Tokens

All flavors should expose semantic motion tokens rather than component-specific arbitrary durations.

Recommended contract:

```css
:root {
  --nb-motion-instant: 70ms;
  --nb-motion-fast: 110ms;
  --nb-motion-standard: 170ms;
  --nb-motion-slow: 260ms;

  --nb-ease-press: cubic-bezier(.2, 0, 0, 1);
  --nb-ease-release: cubic-bezier(.2, .9, .3, 1.15);
  --nb-ease-standard: cubic-bezier(.2, 0, 0, 1);
}
```

Flavor implementations may tune values while preserving the semantic names.

## Interaction Principles

### 1. Motion must communicate cause and effect

Animation exists to explain state change, hierarchy, continuity, confirmation, or physical interaction. Decorative motion must never compete with task completion.

### 2. Actionable things react; static things stay stable

Do not animate every card merely because the pointer crosses it. Movement signals interactivity. Static content should not mimic controls.

### 3. Pointer, keyboard, and touch must express the same state model

Hover is not the only interaction state. Touch users receive the pressed state on pointer-down. Keyboard users receive clear focus-visible and pressed/selected feedback without relying on hover.

### 4. Shadow is part of motion

In NeoBrutalism, hard shadows are not decorative. They represent physical depth. Translation and shadow depth should change together.

### 5. Motion intensity is a flavor token

Rivet may feel mechanical. Soft may feel refined. Commerce may feel energetic. Raw may feel abrupt. All should follow the same physical laws while tuning intensity.

### 6. Micro-interactions should reward meaningful progress

Use micro-interactions for:

- successful save
- completed setup step
- license activation
- item added to cart
- copied API key
- connection established
- download started
- release published
- agent configuration applied

Feedback should be immediate, brief, and legible.

## Recommended Feedback Patterns

### Buttons

Rest -> hover compression -> full press -> controlled release.

### Toggles

Thumb movement plus surface compression at pointer-down. State color change should complete with the thumb, not lag behind.

### Checkboxes / radios

Press the control inward first, then reveal the selected mark. The mark is confirmation of the physical action.

### Tabs

Selected tabs should feel seated or locked into their track rather than elevated above it.

### Cards

Only interactive cards compress. Informational cards remain static.

### Menus / popovers

Entry motion should reveal origin and hierarchy, but the trigger itself follows the press model. Avoid excessive floating/elevation choreography.

### Drag and drop

Dragging is the primary exception to the no-lift rule: an object being physically picked up may temporarily separate from its resting surface. The lift must communicate actual drag state, not generic hover.

### Loading

Prefer local progress feedback over blocking global loaders. Preserve layout to avoid visual jumps.

### Completion

Use a compact confirmation motion: check, lock-in, stamp, snap, or brief structural accent. Avoid long celebratory animation for routine actions.

## Accessibility

### Reduced Motion

Respect `prefers-reduced-motion: reduce`.

Reduced motion should keep state feedback while removing non-essential travel and rebound.

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    scroll-behavior: auto !important;
    transition-duration: 0.01ms !important;
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
  }
}
```

Implementations may use a more targeted strategy, but interaction state must remain visually clear.

### Focus

Keyboard focus is not hover. `:focus-visible` must have a dedicated high-contrast treatment and must not rely solely on motion.

### Target size

Touch targets should remain comfortably usable even when visual controls are compact.

## Anti-Patterns

Do not use these as generic NeoBrutal interactions:

- `translateY(-2px)` on hover
- hover elevation increases
- large scale-up on hover
- long spring animations for routine controls
- animation on every decorative surface
- motion that delays action acknowledgement
- hover-only communication
- removing focus outlines without a replacement
- disabling TLS/security or functional state while animating

## Flavor Tuning

The family contract defines **direction and meaning**, while each flavor defines **personality**.

Examples:

### Soft

- shallow depth
- 1–2px hover compression
- controlled, quiet release
- subtle surface transitions
- minimal overshoot

### Rivet

- stronger mechanical depth
- obvious shadow collapse
- firm press
- restrained rebound

### Commerce

- stronger CTA compression
- faster feedback
- slightly more expressive release
- richer cart/add/success confirmation

### Raw

- abrupt compression
- hard shadow disappearance
- minimal easing

## Design Goal

NeoBrutalism should feel **touchable**.

Users should visually understand:

- what can be touched
- what is being touched
- what has been pressed
- what changed because of the press

The interface should feel alive because it responds physically and consistently, not because it constantly moves.
