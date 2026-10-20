# NeoBrutalism Component Conformance

A component is NeoBrutalism-family conformant only when its visual states, interaction physics, accessibility, and semantics follow this contract.

## 1. Required state model

Every interactive primitive MUST explicitly define the states that apply to it.

Minimum set:

```text
rest
hover (when hover exists)
focus-visible
pressed/active
selected/toggled (when applicable)
loading (when applicable)
disabled
success/error feedback (when applicable)
```

Touch devices do not need hover, but MUST receive pressed feedback.

## 2. Tactile interaction contract

For ordinary pressable controls:

### Rest
- Full intended structural depth is visible.
- No press translation is applied.

### Hover / proximity
- The control MUST move toward the resting surface, not away from it.
- Visible offset-shadow depth SHOULD reduce proportionally.
- Hover MUST NOT be required to understand the control.

### Pressed
- The control SHOULD reach full or near-full compression.
- Hard-shadow depth SHOULD collapse or nearly collapse.
- Feedback MUST begin immediately on pointer/touch/key down.

### Release
- Depth SHOULD restore in a short, controlled motion.
- Routine controls SHOULD NOT use exaggerated bounce.

### Result
- The UI SHOULD communicate the consequence locally whenever possible.
- A result state MUST NOT depend only on a toast if the affected control can show meaningful feedback itself.

## 3. No generic hover lift

The following pattern is non-conformant for ordinary controls:

```css
:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 0 var(--shadow);
}
```

A lift MAY be used only when the interaction semantics actually mean lift/pick-up, such as drag-and-drop.

## 4. Component-specific behavior

### Buttons
MUST use the press model. Labels/icons move with the physical surface.

### Icon buttons
MUST provide the same tactile sequence as text buttons and maintain an adequate hit target.

### Checkboxes and radios
SHOULD compress on contact before or as the mark appears. Selection feedback must be immediate and unambiguous.

### Switches
SHOULD combine contact compression with thumb travel. State color and thumb position should resolve together.

### Tabs
Selected tabs SHOULD feel seated/locked into their rail rather than elevated above it.

### Chips / segmented controls
Pressable chips follow tactile compression. Selected state must remain distinguishable after release.

### Cards
Only cards with an action or navigation role MAY react to hover/press. Informational cards remain stable.

### Menus / popovers
The trigger follows tactile compression. The revealed surface may animate for hierarchy, but should not imply that the trigger itself floated upward.

### Tooltips
Tooltips MUST NOT introduce movement that makes the target appear actionable when it is not.

### Sliders
The thumb MAY visually lift while actively dragged because drag is a pick-up interaction. Track feedback must remain immediate.

### Drag-and-drop
Lift is permitted and encouraged when it clarifies that an object has been picked up. The object MUST visibly re-seat when dropped.

### Destructive controls
MUST retain tactile feedback but SHOULD use stronger visual confirmation and may require a confirmation step depending on consequence.

### Loading controls
The original action should acknowledge press immediately, then transition into a local loading state without layout jump where possible.

### Success
Prefer compact, structural confirmation: check, snap, stamp, lock-in, count update, or state replacement.

### Error / rejection
A brief resistance cue MAY be used, but error communication MUST include persistent visual/textual information where needed.

## 5. Keyboard contract

- `focus-visible` MUST be distinct from hover.
- Space/Enter activation MUST receive equivalent pressed/active feedback where platform semantics allow it.
- Focus indication MUST NOT be removed without an accessible replacement.
- Focus order MUST follow task and reading order.

## 6. Touch contract

- Touch MUST receive pressed feedback even without hover.
- Visual hit area and actual hit target may differ, but target size must remain comfortably usable.
- Motion MUST not delay tap acknowledgement.

## 7. Reduced motion

With reduced motion enabled:

- Press state remains visible.
- Large travel and overshoot SHOULD be removed.
- State changes SHOULD become near-instant or use subtle non-spatial transitions.
- Functionality and hierarchy MUST remain unchanged.

## 8. Motion and performance

Components SHOULD animate compositor-friendly properties where possible (`transform`, `opacity`).

Avoid broad `transition: all` in reusable primitives. Transitions SHOULD enumerate the properties involved so state changes are predictable and cheap.

## 9. Fluid sizing

Component dimensions, padding, gaps, and typography SHOULD consume shared fluid tokens rather than inventing local breakpoint values.

## 10. Agent-readable component metadata

A conforming component SHOULD expose or document:

```text
name
purpose
anatomy
variants
sizes
states
interactive: true/false
pressable: true/false
drag_lift_allowed: true/false
keyboard behavior
ARIA/accessibility requirements
motion tokens used
examples
anti-patterns
```

The goal is for both humans and authorized agents to know how a component behaves without reverse engineering CSS.

## Conformance checklist

A component passes family conformance when:

- [ ] hover never creates generic upward elevation
- [ ] press direction is toward the surface
- [ ] shadow/depth and translation remain physically coherent
- [ ] press acknowledgement is immediate
- [ ] keyboard focus is explicit
- [ ] touch works without hover
- [ ] reduced motion preserves state meaning
- [ ] static surfaces do not mimic interactive motion
- [ ] semantic tokens are used instead of arbitrary local motion values
- [ ] interaction result is communicated clearly
