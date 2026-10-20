# NeoBrutalism Flavor Contract

A flavor changes the **personality** of NeoBrutalism without changing the family interaction semantics.

## What a flavor MAY change

A flavor may define its own:

- palette and semantic color values
- typography and type proportions
- border thickness
- radius
- shadow depth and direction within the tactile model
- spacing density
- motion duration
- rebound strength
- feedback intensity
- icon treatment
- surface treatment
- visual density
- layout rhythm
- illustration/art direction

## What a flavor MUST preserve

Every flavor MUST preserve:

- compress-never-float interaction direction for ordinary controls
- coherent relationship between translation and visible depth
- immediate action acknowledgement
- equivalent touch, pointer, and keyboard semantics
- reduced-motion support
- shared semantic token names or documented mappings
- shared state meanings
- accessible focus behavior
- machine-readable component intent where provided by the implementation

## Physical personality model

Each flavor SHOULD define a conceptual material/physical personality. This is a design aid, not a requirement to render literal textures.

### Soft

Conceptual feel: coated plastic / soft-touch hardware.

- shallow depth
- small hover compression
- quiet, controlled release
- minimal overshoot
- calm SaaS/application density
- micro-interactions prioritize reassurance and continuity

### Rivet

Conceptual feel: mechanical control panel / fastened hardware.

- stronger structural depth
- firm press
- obvious hard-shadow collapse
- mechanical snap on release
- denser, more industrial rhythm

### Commerce

Conceptual feel: packaging / tactile retail controls.

- high CTA clarity
- stronger call-to-action compression
- slightly more expressive release
- richer add-to-cart, purchase, download, and success feedback
- motion may be more energetic but must remain task-focused

### Raw

Conceptual feel: printed card / ink / board.

- abrupt contact
- hard depth collapse
- minimal interpolation
- deliberately direct feedback

## Flavor manifest

Every flavor SHOULD publish a small manifest describing how it implements the family contract.

Example:

```json
{
  "family": "neobrutalism",
  "flavor": "soft",
  "specVersion": "0.1",
  "interactionModel": "compress-never-float",
  "motion": {
    "intensity": "low",
    "rebound": "minimal"
  },
  "depth": {
    "rest": "shallow",
    "hoverCompression": "partial",
    "activeCompression": "full"
  },
  "supports": {
    "light": true,
    "dark": true,
    "reducedMotion": true,
    "fluidTokens": true,
    "agentMetadata": true
  }
}
```

## Conformance principle

If switching from one flavor to another changes what a state **means**, the flavor has diverged too far.

If switching flavors changes how strongly, softly, quickly, or visually that state is expressed while preserving meaning, the family system is working as intended.
