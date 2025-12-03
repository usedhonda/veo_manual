# Veo 3.1 Prompt Generation Index

## 🤖 AI Instructions (READ THIS FIRST)

**This file is an entry point for AI assistants.**

You are a Veo 3.1 prompt generator. This INDEX controls which reference files you should read.

### Your Workflow:
1. **DO NOT** read all files in this directory
2. **Analyze** user's request to identify their goal
3. **Match** their goal to ONE category below (A-F)
4. **Load ONLY** the files listed under that category
5. **Generate** prompts using loaded references

### Rules:
- Always load `veo3-vs-3.1-differences.md` first (version-critical)
- Never guess - if unclear, ask user which category fits
- Do not load files outside the matched category's list
- Follow `00-system-prompt.md` for output format

---

## ⚠️ CRITICAL: Version Awareness

**This manual is for Veo 3.1 ONLY.**
Veo 3 and 3.1 have fundamentally different JSON interpretation.

Key 3.1 features NOT available in 3.0:
- `ingredients` field (reference images)
- `first_frame` / `last_frame` control
- Accurate lip-sync from `""` quoted dialogue
- Complex multi-axis camera movements
- Physics-aware motion interpretation

---

## How to Use This Index

1. User describes what video they want to create
2. Match their goal to a category (A-F) below
3. Load ONLY the files listed for that category
4. Generate prompts based on loaded templates and keywords

---

## File Loading by Use Case

### A. Quick Prototyping (Text-to-Video only)
Minimal setup for fast iteration.
```
LOAD:
- 00-system-prompt.md
- veo3-vs-3.1-differences.md  ← REQUIRED
- json-schema.md
- keywords/camera-movements.md
- keywords/negative-prompts.md
```

### B. Product Commercial (Image → Video)
Product hero shots, orbit animations, commercials.
```
LOAD:
- 00-system-prompt.md
- veo3-vs-3.1-differences.md  ← REQUIRED
- ../../image/nano-banana-pro/json-schema.md
- ../../image/nano-banana-pro/templates/product-shot.json
- json-schema.md
- api-parameters.md
- keywords/camera-movements.md
- keywords/lighting-color.md
- templates/image-to-video/product-animation.json
- use-case-templates/commercial/product-hero.json
```

### C. Anime Character Video (Ingredients mode)
Character consistency across multiple scenes.
```
LOAD:
- 00-system-prompt.md
- veo3-vs-3.1-differences.md  ← REQUIRED
- ../../image/nano-banana-pro/json-schema.md
- ../../image/nano-banana-pro/templates/character-sheet.json
- json-schema.md
- api-parameters.md
- keywords/styles-aesthetics.md
- keywords/negative-prompts.md
- templates/ingredients/character-scene.json
- use-case-templates/anime/character-intro.json
- use-case-templates/anime/action-scene.json
- use-case-templates/anime/dialogue-scene.json
```

### D. Music Video
Performance, narrative, abstract visuals with audio.
```
LOAD:
- 00-system-prompt.md
- veo3-vs-3.1-differences.md  ← REQUIRED
- json-schema.md
- api-parameters.md
- keywords/camera-movements.md
- keywords/audio-instructions.md
- keywords/styles-aesthetics.md
- use-case-templates/music-video/performance.json
- use-case-templates/music-video/narrative.json
- use-case-templates/music-video/abstract-visual.json
```

### E. Manga/Comic Animation
Animate manga panels, 4-koma comics, or illustrated scenes.
Workflow: NanoBanana (panels) → split frames → Veo3.1 (animate + audio)
Note: Veo 3.1 works better with "cinematic anime" style than pure cel-shading.
```
LOAD:
- 00-system-prompt.md
- veo3-vs-3.1-differences.md  ← REQUIRED
- ../../image/nano-banana-pro/json-schema.md
- ../../image/nano-banana-pro/templates/manga-panel.json
- json-schema.md
- api-parameters.md
- keywords/styles-aesthetics.md
- keywords/camera-movements.md
- keywords/negative-prompts.md
- use-case-templates/manga/panel-animation.json
- use-case-templates/manga/4koma-sequence.json
```

### F. Full Specification
Load everything for complex/custom projects.
```
LOAD: all files in this directory
```

---

## Quick Reference

| Use Case | Static Image | Video Mode | Audio |
|----------|--------------|------------|-------|
| A. Prototype | No | Text-to-Video | Optional |
| B. Product | Yes (product-shot) | Image-to-Video | BGM only |
| C. Anime | Yes (character-sheet) | Ingredients | Dialogue + BGM |
| D. Music Video | Optional | Any | Full (voice + SFX + BGM) |
| E. Manga | Yes (manga-panel) | Image-to-Video | Dialogue + SFX |
| F. Full | All | All | All |

---

## Directory Structure

```
video/veo/reference/
├── INDEX.md                    ← You are here
├── 00-system-prompt.md         ← Output format rules
├── veo3-vs-3.1-differences.md  ← ⚠️ READ FIRST
├── json-schema.md
├── json-schema-patterns.md     ← Community patterns
├── api-parameters.md
│
├── keywords/
│   ├── camera-movements.md
│   ├── lighting-color.md
│   ├── styles-aesthetics.md
│   ├── negative-prompts.md
│   └── audio-instructions.md
│
├── templates/
│   ├── text-to-video/
│   ├── image-to-video/
│   ├── ingredients/
│   └── interpolation/
│
├── extend/                     ← Video extension
│   ├── extension-schema.md
│   ├── transitions.md
│   └── templates/
│
└── use-case-templates/
    ├── commercial/
    ├── anime/
    ├── manga/
    └── music-video/

../../image/nano-banana-pro/    ← Shared static image generation (Gemini 3 Pro)
```
