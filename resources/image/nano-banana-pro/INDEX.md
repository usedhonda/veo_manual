# Nano Banana Pro (Gemini 3 Pro Image) Reference Index

## Router Instructions for AI

**IMPORTANT**: Do not load all files at once. Use this index to select only the files needed for the current task. This prevents token overload and improves response quality.

---

## File Loading Decision Tree

```
Step 1: ALWAYS load these first
├── 00-system-prompt.md
└── logic/json-schema.md

Step 2: What type of request?
│
├─ Multiple reference images (2+)?
│   └─ Load: logic/multi-image-slots.md
│
├─ Real product/brand/historical accuracy needed?
│   └─ Load: logic/grounding-rules.md
│
├─ Text/typography in image?
│   └─ Load: vocabulary/typography.md + vocabulary/text-integration.md
│
├─ Liquid/material physics (food, product)?
│   └─ Load: vocabulary/fluid-dynamics.md
│
├─ Video generation (Veo 3.1)?
│   └─ Load: strategies/video-workflow.md
│
├─ Need specific camera/lens/lighting terms?
│   └─ Load: vocabulary/photography.md OR vocabulary/cinematography.md
│
├─ Artistic style request?
│   └─ Load: styles/artistic-styles.md
│
├─ Anime/illustration style (cel-shaded, vector, pop art)?
│   └─ Load: styles/illustration-styles.md
│
├─ Data visualization/infographic?
│   └─ Load: styles/corporate-data-viz.md
│
├─ UI/UX/app mockup?
│   └─ Load: styles/ui-ux-design.md
│
├─ Encountering generation issues?
│   └─ Load: strategies/troubleshooting.md
│
├─ Need creative techniques?
│   └─ Load: strategies/prompt-techniques.md
│
└─ Need higher quality (physics, grounding)?
    └─ Load: strategies/quality-techniques.md
```

---

## Directory Structure

```
nano-banana-pro/
├── INDEX.md                 ← You are here (Router)
├── 00-system-prompt.md      ← Always load first
│
├── logic/                   # Rules & Structure
│   ├── json-schema.md       # Master JSON schema (always load)
│   ├── multi-image-slots.md # 14-slot mixing guide
│   └── grounding-rules.md   # Search trigger conditions
│
├── vocabulary/              # Keywords & Terms
│   ├── photography.md       # Camera, lens, composition
│   ├── cinematography.md    # Lighting, atmosphere, motion
│   ├── typography.md        # Text rendering, fonts
│   ├── fluid-dynamics.md    # Liquid, material physics
│   └── text-integration.md  # Text embedding techniques
│
├── strategies/              # Techniques & Workflows
│   ├── prompt-techniques.md # 7 tips, Pro features
│   ├── video-workflow.md    # Veo 3.1 integration
│   ├── troubleshooting.md   # Problem solving, negatives
│   └── quality-techniques.md # Advanced quality boosting
│
├── styles/                  # Artistic Styles
│   ├── artistic-styles.md   # 11 style recipes (abstract/painting)
│   ├── illustration-styles.md # Anime/vector/pop art styles
│   ├── corporate-data-viz.md # Infographics, charts
│   └── ui-ux-design.md      # App/web UI styles
│
└── templates/               # Ready-to-use JSON
    └── *.json               # Use-case templates
```

---

## Quick Reference: File Purpose

### Logic (Load based on task complexity)

| File | Load When |
|------|-----------|
| `logic/json-schema.md` | **ALWAYS** - Defines prompt structure |
| `logic/multi-image-slots.md` | Using 2+ reference images |
| `logic/grounding-rules.md` | Need real-world accuracy |

### Vocabulary (Load based on content type)

| File | Load When |
|------|-----------|
| `vocabulary/photography.md` | Camera settings, poses, composition |
| `vocabulary/cinematography.md` | Lighting setups, atmosphere |
| `vocabulary/typography.md` | Text in image, fonts, labels |
| `vocabulary/fluid-dynamics.md` | Liquid, material, physics effects |
| `vocabulary/text-integration.md` | Embedding text naturally in scene |

### Strategies (Load based on workflow)

| File | Load When |
|------|-----------|
| `strategies/prompt-techniques.md` | Need creative tips |
| `strategies/video-workflow.md` | Creating images for Veo |
| `strategies/troubleshooting.md` | Fixing generation issues |
| `strategies/quality-techniques.md` | Physics, grounding, text quality |

### Styles (Load based on aesthetic)

| File | Load When |
|------|-----------|
| `styles/artistic-styles.md` | Abstract, painting, fine art styles |
| `styles/illustration-styles.md` | Anime, cel-shaded, vector, pop art |
| `styles/corporate-data-viz.md` | Charts, infographics, dashboards |
| `styles/ui-ux-design.md` | App UI, web design mockups |

---

## Templates (Copy & Customize)

| Template | Use Case |
|----------|----------|
| `templates/character-sheet.json` | Character consistency reference |
| `templates/cyberpunk-character.json` | Detailed character portrait |
| `templates/product-shot.json` | E-commerce product photography |
| `templates/scene-background.json` | Environment/scene generation |
| `templates/manga-panel.json` | Manga/comic style artwork |
| `templates/ui-mockup.json` | App/web interface design |
| `templates/architecture-floorplan.json` | Architectural visualization |
| `templates/fashion-lookbook.json` | Fashion/lifestyle photography |
| `templates/social-media-influencer.json` | SNS content generation |
| `templates/illust-cel-shaded.json` | Flat anime cel-shaded style |
| `templates/illust-art-nouveau.json` | Art Nouveau fantasy style |
| `templates/illust-retro-pop.json` | Retro pop anime style |
| `templates/illust-comic-pop-art.json` | Comic pop art urban style |
| `templates/illust-cafe-cozy.json` | Cozy warm cafe lifestyle |

---

## Model Characteristics

### Strengths
- **Reasoning-powered** - Thinks before rendering
- **JSON parsing** - Direct parameter injection
- **Text rendering** - Better than competitors (keep <6 words)
- **14-image mixing** - Combine multiple references
- **Camera physics** - Accurate lens/aperture simulation
- **Search grounding** - Real-world accuracy via Google Search

### Limitations
- Not optimized for `((keyword))` weight syntax
- Complex text may still have errors
- Character consistency requires explicit identity anchors

---

## Schema Selection (Step 2 of generation)

```
User Request
    │
    ├─ Simple concept/quick idea
    │   └─ Use: Minimal Schema
    │
    ├─ Character portrait
    │   └─ Use: Full Schema + character-sheet.json
    │
    ├─ Product photography
    │   └─ Use: Full Schema + product-shot.json
    │
    ├─ UI/UX mockup
    │   └─ Use: templates/ui-mockup.json + styles/ui-ux-design.md
    │
    ├─ Data visualization
    │   └─ Use: styles/corporate-data-viz.md
    │
    ├─ Scene/environment
    │   └─ Use: Full Schema + scene-background.json
    │
    ├─ Counting/exact positioning
    │   └─ Use: Logic Gate Hack (in json-schema.md)
    │
    └─ Video frame (Veo 3.1)
        └─ Use: strategies/video-workflow.md + veo_optimization
```

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| v4.0 | 2025-12 | Reorganized structure (logic/vocabulary/strategies/styles) |
| v3.0 | 2025-12 | Master schema, advanced hacks, use-case templates |
| v2.0 | 2025-11 | Initial Gemini 3 Pro support |
| v1.0 | 2025-10 | Gemini 2.5 Flash (original Nano Banana) |
