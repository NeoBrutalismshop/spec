# NeoBrutalism Family Specification

A shared contract for the NeoBrutalism design-system family: Rivet, Soft, Commerce, and future flavors.

Status: **Draft 0.1**

## Purpose

This specification separates **family laws** from **flavor personality**.

Every flavor may choose its own typography, palette, border weight, radius, shadow depth, density, and motion intensity. It must still behave like a member of the same family so humans and software agents can move between flavors without relearning the interaction model.

## Normative language

- **MUST** — required for family conformance.
- **SHOULD** — expected unless a documented product constraint justifies an exception.
- **MAY** — optional.

## Family laws

### 1. Touchable, not floaty

Interactive surfaces MUST feel physically touchable.

The default directional rule is:

> **Compress, never float.**

For ordinary controls, hover/proximity MUST NOT increase apparent elevation. A hover should move the control **toward** its resting surface and reduce visible depth. Pressing should continue that motion until the control feels seated.

Upward/lift motion is reserved for interactions whose meaning is actually “pick up,” such as drag-and-drop.

See [INTERACTION.md](./INTERACTION.md).

### 2. Shadow represents depth

Hard or offset shadows are structural, not decorative. When a control moves toward the surface, its visible depth MUST reduce correspondingly.

A component MUST NOT translate downward while leaving a full-depth shadow behind in a way that breaks the physical illusion.

### 3. Movement is information

Motion MUST communicate at least one of:

- affordance
- cause and effect
- hierarchy
- continuity
- progress
- confirmation
- resistance/error

Static content SHOULD remain stable. Decorative animation MUST NOT make non-interactive surfaces look actionable.

### 4. State feedback is immediate

User input MUST receive immediate visible feedback. Network or background work may continue afterward, but the interface should acknowledge the action at once.

The canonical interaction sequence is:

`rest -> hover/proximity -> pressed -> release -> result`

Touch skips hover. Keyboard adds a distinct `focus-visible` state.

### 5. Flavor changes personality, not semantics

Rivet may feel mechanical; Soft may feel restrained; Commerce may feel energetic. They MUST preserve the same state meanings and directional physics.

### 6. Fluid by default

Responsive size, spacing, and typography SHOULD use fluid tokens (including `clamp()`) where appropriate rather than relying only on breakpoint jumps.

### 7. Accessible by construction

Focus, reduced motion, target size, contrast, disabled states, and input modality behavior are part of component conformance, not optional polish.

### 8. Human- and agent-readable

Every conforming flavor SHOULD expose semantic tokens, component metadata, state contracts, usage guidance, and machine-readable documentation so an authorized LLM/agent can apply the system without guessing.

## Required specification documents

- [INTERACTION.md](./INTERACTION.md) — tactile physics and motion grammar.
- [TOKENS.md](./TOKENS.md) — shared token vocabulary and tactile depth contract.
- [COMPONENTS.md](./COMPONENTS.md) — component state and conformance requirements.
- [FLAVORS.md](./FLAVORS.md) — what flavors may change and what they must preserve.

## Family principle

> **NeoBrutal interfaces should feel touchable.**

A user should understand what can be touched, when contact begins, when an action is pressed, and what changed because of that action.

The family is not defined by thick borders alone. It is defined by **structure + tactile feedback + meaningful motion + strong visual hierarchy**.
