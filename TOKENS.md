# NeoBrutalism Token Contract

This document defines the semantic token vocabulary shared across NeoBrutalism flavors.

Values are flavor-specific. Names and meanings are family-level contracts.

## 1. Tactile depth tokens

Every interactive flavor MUST define a depth model.

Recommended semantic tokens:

```css
:root {
  --nb-depth-rest-x: 4px;
  --nb-depth-rest-y: 4px;

  --nb-depth-hover-x: 2px;
  --nb-depth-hover-y: 2px;

  --nb-depth-active-x: 0px;
  --nb-depth-active-y: 0px;

  --nb-press-hover-x: 2px;
  --nb-press-hover-y: 2px;

  --nb-press-active-x: 4px;
  --nb-press-active-y: 4px;
}
```

The translation and visible shadow depth SHOULD form one physical model:

- **Rest:** full visible depth, zero press translation.
- **Hover:** partial translation into the surface, reduced visible depth.
- **Active:** full translation into the surface, collapsed or near-collapsed depth.

Components MUST NOT hardcode their own unrelated press distances when equivalent family tokens exist.

## 2. Motion duration tokens

Every flavor MUST provide semantic motion timings.

```css
:root {
  --nb-motion-instant: 70ms;
  --nb-motion-fast: 110ms;
  --nb-motion-standard: 170ms;
  --nb-motion-slow: 260ms;
}
```

Recommended use:

- `instant` — physical press acknowledgement.
- `fast` — release, toggle, icon confirmation.
- `standard` — common state transitions.
- `slow` — larger structural transitions.

Durations MAY differ by flavor, but semantic intent MUST remain stable.

## 3. Easing tokens

```css
:root {
  --nb-ease-press: cubic-bezier(.2, 0, 0, 1);
  --nb-ease-release: cubic-bezier(.2, .9, .3, 1.15);
  --nb-ease-standard: cubic-bezier(.2, 0, 0, 1);
}
```

- `press` SHOULD feel immediate and decisive.
- `release` MAY include restrained overshoot.
- `standard` SHOULD remain calm and legible.

A flavor MAY define additional material/personality tokens, but MUST preserve these semantic roles.

## 4. Motion intensity tokens

Flavors SHOULD expose an intensity scale so motion can be tuned without rewriting components.

Example:

```css
:root {
  --nb-motion-intensity: 1;
  --nb-rebound-strength: .08;
  --nb-feedback-strength: 1;
}
```

Possible flavor tendencies:

- Soft: low intensity, minimal rebound.
- Rivet: firm, mechanical compression.
- Commerce: energetic but controlled feedback.
- Raw: abrupt, low-easing response.

## 5. Fluid UI tokens

Responsive dimensions SHOULD use fluid values where they improve continuity.

Example:

```css
:root {
  --nb-space-1: clamp(.25rem, .22rem + .12vw, .375rem);
  --nb-space-4: clamp(.875rem, .75rem + .4vw, 1.25rem);
  --nb-text-body: clamp(.9375rem, .9rem + .15vw, 1rem);
  --nb-text-display: clamp(2.5rem, 1.7rem + 4vw, 6rem);
}
```

The family SHOULD prefer fluid interpolation over excessive breakpoint-only jumps.

## 6. Interaction state tokens

Conforming flavors SHOULD expose state tokens for:

```text
rest
hover
focus-visible
active/pressed
selected
loading
success
warning
error
disabled
```

State tokens may affect color, border, shadow, opacity, motion, or iconography, but state meaning MUST remain consistent.

## 7. Focus tokens

Keyboard focus MUST be independent from hover.

Recommended contract:

```css
:root {
  --nb-focus-width: 3px;
  --nb-focus-offset: 3px;
  --nb-focus-style: solid;
}
```

A flavor MUST provide a high-contrast focus treatment that does not rely on motion alone.

## 8. Reduced-motion behavior

The token system SHOULD support a reduced-motion mode in which:

- non-essential travel becomes zero or near-zero;
- rebound/overshoot is removed;
- state changes remain visually obvious;
- progress and completion remain understandable.

Reduced motion MUST NOT remove state feedback.

## 9. Token implementation rule

Components consume **semantic tokens**, not flavor identity directly.

Good:

```css
transform: translate(var(--nb-press-hover-x), var(--nb-press-hover-y));
transition-duration: var(--nb-motion-fast);
```

Avoid:

```css
/* component-specific magic values */
transform: translate(3px, 3px);
transition: all 143ms ease;
```

This separation is what allows a shared component contract to feel different in Soft, Rivet, Commerce, and future flavors without changing interaction semantics.
