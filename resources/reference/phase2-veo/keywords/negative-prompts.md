# Negative Prompts for Veo 3.1

## Overview

Negative prompts tell Veo 3.1 what to **avoid** generating. They are critical for quality control and preventing common artifacts.

---

## API Parameter Format

```json
"parameters": {
  "negativePrompt": "blur, distortion, text overlay, watermark, low quality"
}
```

### JSON Schema Format

```json
"negative": {
  "exclude": [
    "subtitles",
    "text_overlay",
    "watermark",
    "blur",
    "distortion"
  ]
}
```

---

## Essential Negative Prompts

### Always Include (Universal)

| Keyword | Prevents |
|---------|----------|
| `blur` | Out-of-focus frames |
| `blurry` | General blur artifacts |
| `distortion` | Warped visuals |
| `low quality` | Poor resolution |
| `low resolution` | Pixelation |
| `grainy` | Excessive noise (unless intended) |
| `watermark` | Unwanted watermarks |
| `logo` | Branded logos |
| `text overlay` | Unwanted text |
| `subtitles` | Burned-in subtitles |

### Recommended Standard Set

```json
"negativePrompt": "blur, blurry, distortion, low quality, low resolution, grainy, watermark, logo, text overlay, subtitles, pixelated, noise, artifacts"
```

---

## Category-Specific Negatives

### Human/Character Videos

| Keyword | Prevents |
|---------|----------|
| `extra limbs` | Additional arms/legs |
| `extra fingers` | Wrong finger count |
| `missing limbs` | Missing body parts |
| `deformed` | Body deformation |
| `disfigured` | Facial distortion |
| `bad anatomy` | Incorrect body structure |
| `bad proportions` | Unnatural sizing |
| `mutated` | Unnatural mutations |
| `morphing` | Face/body morphing mid-clip |
| `melting` | Dissolving features |
| `duplicate` | Duplicated body parts |
| `clone` | Duplicate characters |

**Recommended for character videos:**
```json
"negativePrompt": "extra limbs, extra fingers, missing limbs, deformed, disfigured, bad anatomy, bad proportions, mutated, morphing, melting, duplicate, clone, blur, distortion, low quality"
```

### Product/Commercial Videos

| Keyword | Prevents |
|---------|----------|
| `logo` | Unwanted brand marks |
| `text` | Unintended text |
| `branding` | Wrong brand elements |
| `cheap` | Low-quality appearance |
| `plastic looking` | Artificial texture |
| `fingerprints` | Surface marks |
| `scratches` | Surface damage |
| `dust` | Particles on product |
| `reflections` | Unwanted reflections |

**Recommended for product videos:**
```json
"negativePrompt": "logo, text, branding, cheap, plastic looking, fingerprints, scratches, dust, unwanted reflections, blur, low quality, distortion"
```

### Anime/Stylized Videos

| Keyword | Prevents |
|---------|----------|
| `realistic` | Breaking anime style |
| `photorealistic` | Too realistic rendering |
| `3D render` | Unwanted 3D look |
| `uncanny valley` | Unsettling realism |
| `inconsistent style` | Style changes mid-clip |
| `off-model` | Character inconsistency |
| `wrong colors` | Palette deviation |

**Recommended for anime:**
```json
"negativePrompt": "realistic, photorealistic, 3D render, uncanny valley, inconsistent style, off-model, morphing, blur, distortion, low quality"
```

### Landscape/Environment Videos

| Keyword | Prevents |
|---------|----------|
| `people` | Unwanted humans |
| `crowds` | Background people |
| `vehicles` | Unwanted cars/transport |
| `buildings` | Modern structures (if historical) |
| `modern elements` | Anachronistic items |
| `urban` | City elements (if nature) |
| `industrial` | Man-made structures |

**Recommended for nature:**
```json
"negativePrompt": "people, crowds, vehicles, modern elements, industrial, blur, distortion, low quality, watermark"
```

---

## Technical Artifact Prevention

### Motion Artifacts

| Keyword | Prevents |
|---------|----------|
| `jittery` | Unstable motion |
| `stuttering` | Frame drops |
| `judder` | Unsmooth movement |
| `flickering` | Light inconsistency |
| `frame skip` | Missing frames |
| `motion blur` | Excessive blur (if unwanted) |
| `ghosting` | Motion trails |

### Visual Quality Artifacts

| Keyword | Prevents |
|---------|----------|
| `compression artifacts` | Block artifacts |
| `banding` | Color banding |
| `aliasing` | Jagged edges |
| `noise` | Random pixel noise |
| `grain` | Film grain (if unwanted) |
| `overexposed` | Too bright |
| `underexposed` | Too dark |
| `washed out` | Low contrast |
| `oversaturated` | Excessive color |
| `desaturated` | Too little color (if unwanted) |

### Temporal Consistency

| Keyword | Prevents |
|---------|----------|
| `morphing` | Subject shape changes |
| `shifting` | Position drift |
| `warping` | Spatial distortion |
| `inconsistent lighting` | Light changes |
| `color shift` | Color changes mid-clip |
| `style drift` | Style changes |

---

## Use-Case Templates

### Professional Commercial
```json
"negativePrompt": "blur, distortion, low quality, watermark, logo, text, cheap looking, reflections, dust, scratches, noise, compression artifacts, overexposed, underexposed"
```

### Cinematic Narrative
```json
"negativePrompt": "blur, distortion, low quality, watermark, subtitles, text overlay, morphing, extra limbs, bad anatomy, flickering, jittery, inconsistent lighting"
```

### Character Animation
```json
"negativePrompt": "extra limbs, extra fingers, deformed, disfigured, bad anatomy, morphing, melting, clone, duplicate, blur, distortion, low quality, off-model, inconsistent style"
```

### Music Video
```json
"negativePrompt": "blur, distortion, low quality, watermark, logo, subtitles, text, morphing, flickering, compression artifacts"
```

### Product Hero Shot
```json
"negativePrompt": "blur, distortion, low quality, watermark, logo, text, branding, fingerprints, scratches, dust, cheap, plastic looking, overexposed"
```

### Anime Style
```json
"negativePrompt": "realistic, photorealistic, 3D, uncanny valley, off-model, inconsistent style, morphing, blur, distortion, low quality, subtitles, text"
```

### Horror/Dark
```json
"negativePrompt": "blur, distortion, low quality, bright, cheerful, colorful, comedy, cartoon, childish, watermark, text overlay"
```

---

## Common Mistakes to Avoid

### Too Many Negatives
❌ Don't do this:
```json
"negativePrompt": "blur, blurry, soft focus, out of focus, unfocused, hazy, fuzzy, distorted, warped, twisted..."
```
The model may become confused with too many similar terms.

✅ Instead:
```json
"negativePrompt": "blur, distortion, low quality"
```

### Contradictory Negatives
❌ Don't negate your style:
```json
// If you want film grain
"style": "35mm film, vintage",
"negativePrompt": "grain, noise, film grain"  // This contradicts the style!
```

✅ Be consistent:
```json
"style": "35mm film, vintage grain",
"negativePrompt": "blur, distortion, modern digital look"
```

### Over-Restrictive
❌ Don't block everything:
```json
"negativePrompt": "people, faces, hands, animals, vehicles, buildings, plants, water, sky..."
```
This leaves nothing for the model to generate!

✅ Be selective:
```json
"negativePrompt": "people, modern vehicles"  // If doing historical landscape
```

---

## Negative Prompt Best Practices

1. **Start minimal**: Begin with essential negatives, add more only if needed
2. **Be specific**: "extra fingers" is better than "bad hands"
3. **Match your content**: Character videos need character negatives
4. **Don't contradict style**: If you want grain, don't negate grain
5. **Prioritize**: Most important negatives first
6. **Test and iterate**: Add negatives based on actual generation issues
7. **Use fast model first**: Test negatives on `veo-3.1-fast` before final render

---

## Quick Reference Card

### Minimum Essential
```
blur, distortion, low quality, watermark
```

### Standard Professional
```
blur, distortion, low quality, watermark, text overlay, subtitles, noise, artifacts
```

### Character-Safe
```
blur, distortion, low quality, watermark, extra limbs, morphing, bad anatomy, deformed
```

### Product-Safe
```
blur, distortion, low quality, watermark, logo, text, scratches, dust, cheap looking
```

### Anime-Safe
```
blur, distortion, low quality, realistic, photorealistic, 3D render, off-model, morphing
```
