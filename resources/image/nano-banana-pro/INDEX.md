# Nano Banana Pro (Gemini 3 Pro Image) Reference Index

## Entry Point for AI Prompt Generation

This index guides you through the reference materials for generating optimized Nano Banana Pro prompts.

---

## Quick Start

1. **Read the System Prompt** → Understand your role and model capabilities
2. **Select a JSON Schema** → Choose full or minimal based on complexity
3. **Reference Keywords** → Build accurate parameter values
4. **Use Templates** → Start from proven examples

---

## File Reference

### Core Documents

| File | Purpose | Load When |
|------|---------|-----------|
| `00-system-prompt.md` | Role definition, model philosophy, principles | Always first |
| `json-schema.md` | Master schema, minimal schema, advanced hacks | Every prompt |
| `keywords.md` | Photography, lighting, composition, style terms | Filling schema values |

### Templates (Copy & Customize)

| Template | Use Case | Key Features |
|----------|----------|--------------|
| `templates/character-sheet.json` | Character consistency reference | Multi-view, identity anchors |
| `templates/cyberpunk-character.json` | Detailed character portrait | Full schema example, Veo-ready |
| `templates/product-shot.json` | E-commerce product photography | Lighting emphasis, commercial |
| `templates/scene-background.json` | Environment/scene generation | Spatial structure, atmosphere |
| `templates/manga-panel.json` | Manga/comic style artwork | Panel layout, speech bubbles |
| `templates/ui-mockup.json` | App/web interface design | Layout constraints, typography |
| `templates/architecture-floorplan.json` | Architectural visualization | Spatial logic, room connections |
| `templates/fashion-lookbook.json` | Fashion/lifestyle photography | Product + model variations |
| `templates/social-media-influencer.json` | SNS content generation | Authentic imperfections, candid |

---

## Model Characteristics

### Strengths
- **Reasoning-powered** - Thinks before rendering
- **JSON parsing** - Direct parameter injection
- **Text rendering** - Better than competitors (keep <6 words)
- **Counting/positioning** - Logic gates enable precision
- **Camera physics** - Accurate lens/aperture simulation
- **Search grounding** - Real-world accuracy via Google Search

### Limitations
- Not optimized for `((keyword))` weight syntax (Midjourney style)
- Complex text may still have errors
- Character consistency requires explicit identity anchors

---

## Schema Selection Decision Tree

```
User Request
    │
    ├─ Simple concept/quick idea
    │   └─ Use: Minimal Schema
    │
    ├─ Character portrait
    │   └─ Use: Full Schema (subject + attire + lighting)
    │
    ├─ Product photography
    │   └─ Use: Full Schema (photography + lighting emphasis)
    │
    ├─ UI/UX mockup
    │   └─ Use: templates/ui-mockup.json
    │
    ├─ Scene/environment
    │   └─ Use: Full Schema (environment + spatial_structure)
    │
    ├─ Counting/exact positioning
    │   └─ Use: Logic Gate Hack
    │
    ├─ Before/after comparison
    │   └─ Use: Split View Hack
    │
    └─ Real-world product accuracy
        └─ Use: Grounding Injection Hack
```

---

## Integration with Veo 3.1

Nano Banana Pro images serve as inputs for Veo 3.1 video generation:

| Veo Use | Nano Banana Optimization |
|---------|--------------------------|
| First Frame | Clear subject, motion-ready pose, negative space for direction |
| Ingredient (Character) | Neutral background, multiple angles, identity anchors |
| Last Frame | Arrival pose, settled composition |

Always include `veo_optimization` section when generating images for video use.

---

## Loading Order for Comprehensive Prompts

```
1. 00-system-prompt.md      [ALWAYS]
2. json-schema.md           [ALWAYS]
3. keywords.md              [AS NEEDED for specific terms]
4. templates/*.json         [AS NEEDED for starting point]
```

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| v3.0 | 2025-12 | Master schema, advanced hacks, use-case templates |
| v2.0 | 2025-11 | Initial Gemini 3 Pro support |
| v1.0 | 2025-10 | Gemini 2.5 Flash (original Nano Banana) |
