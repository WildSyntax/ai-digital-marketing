---
name: brand-identity
description: "Builds or evaluates a brand's identity: positioning and personality, then the visual system decisions (logo system, colour, typography, imagery, iconography, motion) that express them. Returns suggested text for the owner to paste into brand/profile.md (\"## One-line description\", \"## Tone\", \"## Visual identity\"); it never creates brand files. Use when the owner wants to define or rethink a visual identity, choose brand colours or typography, plan logo variants, set imagery direction, or audit an existing identity for cohesion and accessibility. Triggers on brand identity, visual identity, logo system, wordmark, brand colours, colour palette, brand typography, type system, iconography, imagery direction, motion principles, identity audit. To apply an existing identity to an artifact use brand-guidelines; to define voice from writing samples use voice-builder; to check a draft against the brand use brand-review."
license: MIT
metadata:
  source: "rampstackco/claude-skills@9b90db257f7395fab76ff9bfcb808456709f6af3"
  path: "skills/brand-identity"
  modified: "yes"
---

# Brand Identity

> Vendored from [rampstackco/claude-skills](https://github.com/rampstackco/claude-skills/tree/9b90db257f7395fab76ff9bfcb808456709f6af3/skills/brand-identity) under MIT.
> Changes for this workspace: focused on defining positioning, personality and visual system decisions; output is suggested text for brand/profile.md instead of an `identity/` file set; links to rampstackco sibling skills replaced with workspace skills (voice-builder, brand-guidelines, brand-review) or made optional; catalogue-only front matter and generated README dropped. Read brand/profile.md first. Return text; workspace skills own files under content/.

Define or evaluate a brand's identity: its positioning and personality, and the visual system decisions that express them (logo system, color, typography, imagery, iconography, and motion). Stack-agnostic. Tool-agnostic.

This skill produces decisions and rules as text. It does not draw logos or export assets; where a logo or icon set is needed, it returns a brief for a designer (or for the workspace `canvas-design` skill).

Start by reading `brand/profile.md`. If positioning, audience or personality are unclear or still "Example:" values, settle them first with the owner (step 1 of the workflow) before making visual decisions.

---

## When to use

- Defining positioning, personality and the one-line description that the visual system must express
- Designing a logo system (decisions and a designer brief, not the artwork)
- Defining a brand color palette
- Choosing brand typography
- Developing iconography or illustration style
- Defining imagery direction (photography, illustration)
- Establishing motion principles
- Auditing an existing identity for cohesion or gaps

## When NOT to use

- Applying an already-defined identity to a deck, document, graphic or page (use `brand-guidelines`, which reads "## Visual identity" in brand/profile.md)
- Defining voice and tone from writing samples (use `voice-builder`)
- Checking a draft against the brand (use `brand-review`)
- Building UI components or code from an existing brand (out of scope for this workspace)

---

## Required inputs

- `brand/profile.md` (brand name, one-line description, audience, tone, any existing visual identity)
- The brand name and positioning (confirm with the owner if the profile does not state it)
- The mood direction and personality (from the owner, or supplied as references)
- Audience and category context
- Application contexts (web, print, packaging, motion - whatever applies)
- Constraints (parent brand requirements, regulatory marks, accessibility minimums)

---

## The framework: 5 elements

A complete identity has five elements. Each element should reinforce the others. Inconsistency between them is the most common identity failure.

### 1. Logo system

Most brands need not one logo but a system of marks for different contexts.

**Components of a logo system:**

- **Primary mark.** The main logo. Used wherever there is room.
- **Wordmark.** Just the typography, no symbol. Used in tight horizontal contexts.
- **Symbol or glyph.** Just the symbol, no type. Used in app icons, favicons, social avatars.
- **Lockup variations.** Horizontal, stacked, square - whichever apply.
- **Monogram.** The initial(s) styled as a mark. Optional but useful for small contexts.

**Design principles:**

- **Legible at 16 pixels.** Test the logo at favicon size. If it falls apart, redesign.
- **Reproducible in single-color.** If the logo only works in full color, it cannot be screen-printed, embroidered, or rendered in browser favicons.
- **Distinctive silhouette.** Squint at it. Can you still tell what it is? If it looks like every other logo in the category at silhouette, redesign.
- **Construction grid.** Every curve and angle is intentional. Document the construction.

**Common failure:**
- Designing only the primary mark and discovering at launch that the wordmark, glyph, and small-size variants do not exist.

### 2. Color system

A color system is more than a palette. It is the rules for how color carries meaning.

**Components:**

- **Primary color.** The signature color most associated with the brand.
- **Secondary colors.** 1 to 3 supporting colors that extend the palette.
- **Neutrals.** The grays and tints that make up most of the surface area.
- **Semantic colors.** Success, warning, error, info - if the brand operates in product UI.
- **Accent colors.** Used sparingly for highlight and emphasis.

**Per color, document:**
- Hex, RGB, HSL, CMYK (if print is in scope), and Pantone (if brand-critical print exists)
- WCAG AA contrast against the other colors in the system
- Allowed and disallowed pairings (some brand colors look terrible together)
- Usage notes (when to use, when not to use)

**Design principles:**

- **Test for accessibility.** WCAG AA requires 4.5:1 contrast for normal text, 3:1 for large text. If the brand color cannot pass either against white, you have a problem.
- **Test for color blindness.** Around 8 percent of men have some form of color blindness. Critical UI signals should not rely on color alone.
- **Define neutrals carefully.** Neutrals are 80 percent of the surface area in most brand applications. They carry more weight than the brand color.
- **Limit the palette.** A 30-color palette is unmanageable. 5 to 8 carefully chosen colors beats a sprawling system.

### 3. Typography

Type is the second-most-recognizable element of a brand after the logo.

**Components of a type system:**

- **Display typeface.** For headlines and brand moments.
- **Body typeface.** For long-form reading. Often the same as display, sometimes different.
- **Monospace typeface** (if applicable for technical brands).
- **Type scale.** The set of sizes used across applications. Typically 5 to 8 steps.
- **Type weights and styles.** Which weights and italics are part of the system.

**Design principles:**

- **Pairing.** If using two typefaces, they must work together at body and display sizes. Common pattern: serif display + sans body, or geometric sans display + humanist sans body.
- **Web licensing.** Confirm web licensing covers expected pageviews. Some popular typefaces have prohibitive web licenses.
- **Variable fonts** are increasingly the right call for performance and flexibility.
- **Fallback stack.** Specify system fallbacks for when the brand font fails to load. The fallback should be visually similar.
- **Open-source alternatives.** Document open-source equivalents for situations where licensing is impractical (third-party tools, embedded contexts).

### 4. Imagery and illustration

Imagery direction is often underspecified, leading to brand drift over time.

**Photography direction:**

- **Subject matter.** What does the brand show?
- **Composition style.** Tight crops, wide environments, candid, posed?
- **Lighting.** Bright and natural, dramatic and directional, soft and diffused?
- **Color treatment.** True color, warm shifted, desaturated, high-contrast?
- **What to reject.** Stock photo aesthetics, specific cliches in the category.

**Illustration direction:**

- **Style.** Flat, dimensional, hand-drawn, geometric, abstract, representational?
- **Color use.** Full palette, restricted palette, brand colors only?
- **Line treatment.** Bold and outlined, soft and shaded, no outlines?
- **Subject matter.** What gets illustrated and what does not?

**Iconography:**

- **Style.** Filled or outline. Rounded or sharp. Single weight or variable.
- **Grid.** Pixel-perfect grid (often 24x24 or 16x16 base).
- **Stroke weight.** Consistent across the icon set.
- **Set.** Which icons exist, and how new icons get added consistently.

### 5. Motion

If the brand lives in any digital product, marketing video, or animated touchpoint, motion is part of the identity.

**Motion principles to define:**

- **Easing curves.** Default easings used across animations. Linear, ease-in-out, custom.
- **Duration scale.** Fast (100ms), medium (200-300ms), slow (500ms+) and when each applies.
- **Choreography.** How elements enter, exit, and respond to interaction.
- **Brand moments.** Signature animations (logo build, page transitions, loaders).

**Design principles:**

- **Restraint.** Most motion in product UI should be quick and subtle. Reserve dramatic motion for brand moments.
- **Reduced motion.** Always provide a `prefers-reduced-motion` alternative for users with vestibular sensitivities.
- **Performance.** Animations must be 60fps on the target devices. Profile before shipping.

---

## Workflow

1. **Confirm brand direction.** Positioning, personality, mood, audience. If brand/profile.md does not settle them, ask the owner a few short questions (who it is for, what it replaces, three personality adjectives, brands they admire or want to avoid looking like) and agree a one-line description before going further.
2. **Audit applications.** List every place the brand will appear (web, print, packaging, app, social, signage, video). The application contexts drive what the system needs to handle.
3. **Element-by-element design.** Start with logo and color, since these constrain typography. Then type. Then imagery, iconography, motion.
4. **Stress-test.** Apply the system to 3 to 5 mock applications (homepage, social post, business card, product UI, signage). Where does it break? Iterate.
5. **Document.** Each element with rules, examples, and dos/don'ts, using `references/identity-system-spec.md` as a checklist. Condense the decisions into the profile text described under Output format.
6. **Get sign-off** from the owner before broad rollout. Identity changes after rollout are 10x the cost of changes during design. The owner pastes the approved text into brand/profile.md; from then on `brand-guidelines` applies it.

---

## Failure patterns

- **Designing logos in isolation from application.** A logo that looks great on a hi-res mockup but illegible at favicon size is a design failure.
- **Picking a brand color without contrast testing.** A brand color that fails WCAG AA against white means UI built on the brand will be inaccessible by default.
- **Specifying typography without checking web licensing.** Discovering at deploy that the foundry charges per-pageview for the chosen typeface is a budget-buster.
- **Skipping imagery direction.** Without it, the brand becomes whatever stock photos the next person picks.
- **Treating motion as decoration.** Inconsistent motion erodes brand cohesion as fast as inconsistent color.
- **Designing only primary states.** What does the brand look like in error? In dark mode? In a localization where the wordmark needs to flip direction? These are not edge cases; they are the brand.

---

## Output format

Return text in the chat; do not create or edit files. The reply has two parts:

**1. Suggested text for brand/profile.md**, ready for the owner to paste, using the profile's existing headings and field names:

```markdown
## One-line description
<who the brand helps, with what, in one sentence>

## Tone
Three adjectives: <personality adjectives agreed in step 1>
(Only suggest a Tone change if the personality work changed it; for a full voice guide, run voice-builder.)

## Visual identity
- Primary colour: <hex> (text/UI variant if the signature colour fails WCAG AA: <hex>)
- Secondary colour: <hex>
- Accent colour: <hex>
- Heading font: <family> (fallback: <system font>)
- Body font: <family> (fallback: <system font>)
- Logo usage: <variants, colour versions, clear space, minimum size, misuse rules>
- Image style: <photography/illustration direction, what to reject, icon style>
```

Keep each line short; brand/profile.md is read by every skill. Mention only the sections that change.

**2. Rationale and detail** (not for the profile): why each choice fits the positioning, contrast ratios checked (see `references/contrast-and-accessibility.md`), neutrals and semantic colours if product UI is in scope, type scale, motion principles, open questions from `references/identity-system-spec.md`, and a logo or icon brief for a designer if one is needed.

---

## Reference files

- [`references/identity-system-spec.md`](references/identity-system-spec.md) - Detailed spec template for documenting each element.
- [`references/contrast-and-accessibility.md`](references/contrast-and-accessibility.md) - Accessibility checks for color and type, with the math.
