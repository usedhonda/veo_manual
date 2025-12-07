# Illustration Styles Reference

## Core Philosophy

### Flattening Aesthetics
Illustration styles prioritize **flat color** over 3D rendering. Key principles:
- Zero gradients (use solid blocks)
- No volumetric shadows
- Visible color boundaries
- Clean separation between elements

### Outline Emphasis
Strong outlines define illustration quality:
- **Bold outlines** - 3-5px visual weight
- **Thick defined outlines** - Traditional/print feel
- **Confident outlines** - No sketchy/hesitant lines

### Limited Palette Control
Color restriction enhances stylization:
- 3-5 dominant colors maximum
- High contrast between hues
- Strategic accent color usage

---

## Style Recipes

### 1. Cel-Shaded Anime (セルアニメ風)

**Core Keywords:**
```
flat color anime, cel-shaded, bold outlines, clean vector art aesthetic
```

**Enhancement Keywords:**
```
minimal shading, zero shadows, dynamic pose, wind-blown hair
```

**Parameter Recommendations:**
| Parameter | Value |
|-----------|-------|
| steps | 30 |
| cfg_scale | 7.0 |
| sampler | DPM++ 2M Karras |

**Negative Prompt (REQUIRED):**
```
3d render, realistic, photorealistic, thick painting, textured brushstrokes, gradient shading, volumetric lighting, complex background, low quality, bad anatomy, distorted face, missing limbs
```

**JSON Template:**
```json
{
  "parameters": {
    "width": 832,
    "height": 1248,
    "steps": 30,
    "cfg_scale": 7.0,
    "sampler_name": "DPM++ 2M Karras"
  },
  "prompt": "A flat color anime illustration in a clean cel-shaded style with bold outlines. [SUBJECT DESCRIPTION]. Clean vector art aesthetic, zero shadows.",
  "negative_prompt": "3d render, realistic, photorealistic, thick painting, textured brushstrokes, gradient shading, volumetric lighting, complex background, low quality, bad anatomy, distorted face, missing limbs"
}
```

---

### 2. Clean Vector Art (ベクターイラスト)

**Core Keywords:**
```
clean vector art aesthetic, minimal shading, flat colors, precise linework
```

**Enhancement Keywords:**
```
SVG-like rendering, geometric shapes, smooth curves, solid fills
```

**Negative Prompt (REQUIRED):**
```
3d render, realistic, photorealistic, detailed shading, gradient colors, volumetric lighting, complex background, low quality, bad anatomy, distorted face, messy lines
```

**Best For:**
- App illustrations
- Icon-style characters
- Infographic elements
- Logo-style artwork

---

### 3. Art Nouveau Fantasy (アールヌーヴォー・ファンタジー)

**Core Keywords:**
```
Art Nouveau influenced style, Japanese woodblock prints, thick defined outlines, flat muted colors
```

**Enhancement Keywords:**
```
sepia tone atmosphere, highly detailed line work, stylized clouds, retro fantasy, elegant flowing forms
```

**Atmosphere Keywords:**
```
majestic layered mountain ranges, colossal flat circular sun/moon disk, rugged rocky cliff edge
```

**Negative Prompt (REQUIRED):**
```
3d render, photorealistic, realistic, modern anime style, vibrant colors, glossy finish, volumetric lighting, heavy shading, blurry, low quality, sketchy, unfinished, bad anatomy, disfigured hands, extra fingers
```

**JSON Template:**
```json
{
  "parameters": {
    "width": 832,
    "height": 1216,
    "steps": 30,
    "cfg_scale": 7.0,
    "sampler_name": "DPM++ 2M Karras"
  },
  "prompt": "A retro fantasy illustration in an Art Nouveau influenced style, rendered with flat muted colors and thick defined outlines reminiscent of Japanese woodblock prints. [SUBJECT DESCRIPTION]. Sepia tone atmosphere, highly detailed line work.",
  "negative_prompt": "3d render, photorealistic, realistic, modern anime style, vibrant colors, glossy finish, volumetric lighting, heavy shading, blurry, low quality, sketchy, unfinished, bad anatomy, disfigured hands, extra fingers"
}
```

---

### 4. Comic Pop Art (コミックポップアート)

**Core Keywords:**
```
stylized comic pop art, limited color palette, high contrast, bold linework
```

**Enhancement Keywords:**
```
flat colors, urban street style aesthetic, graphic cityscape, dense composition
```

**Color Strategy:**
- Dominant: Black + 2 accent colors
- Example: Black, bright yellow, electric cyan
- Pink for accent elements (bubble gum, highlights)

**Negative Prompt (REQUIRED):**
```
3d render, realistic, photorealistic, painting, soft shading, gradient colors, blurred, low quality, bad anatomy, distorted face, messy lines, standard anime style, muted colors
```

**JSON Template:**
```json
{
  "parameters": {
    "width": 832,
    "height": 1248,
    "steps": 30,
    "cfg_scale": 7.0,
    "sampler_name": "DPM++ 2M Karras"
  },
  "prompt": "A stylized comic pop art illustration with a striking limited color palette dominated by black, [COLOR 1], and [COLOR 2] outlines. [SUBJECT DESCRIPTION]. High contrast, bold linework, flat colors, urban street style aesthetic.",
  "negative_prompt": "3d render, realistic, photorealistic, painting, soft shading, gradient colors, blurred, low quality, bad anatomy, distorted face, messy lines, standard anime style, muted colors"
}
```

---

### 5. Retro Pop Anime (レトロポップアニメ)

**Core Keywords:**
```
retro pop style, bold confident outlines, minimal shading, zero shadows
```

**Enhancement Keywords:**
```
clean vector art aesthetic, plain solid background, dynamic wind effect
```

**Character Keywords:**
```
blush marks, dynamic hair blowing in the wind, plume of white breath
```

**Negative Prompt (REQUIRED):**
```
3d render, realistic, photorealistic, detailed shading, gradient colors, volumetric lighting, complex background, low quality, bad anatomy, distorted face, messy lines
```

**Background Strategy:**
- Solid plain color (off-white, light grey)
- No complex environments
- Maximum character focus

---

### 6. Cozy Retro Cafe (コージーカフェ)

**Core Keywords:**
```
cozy retro-style flat color anime, bold outlines, warm color palette, clean cel-shading style
```

**Enhancement Keywords:**
```
warm-lit atmosphere, reflecting indoor lights, gentle smile, steaming drink
```

**Color Strategy:**
- Dominant: Warm yellows, oranges, deep browns
- Avoid: Cold colors, blue tones
- Accent: Terracotta, cream, forest green (plants)

**Scene Elements:**
```
cafe terrace, wooden chair, steaming coffee cup, glass window, potted plants, menu board
```

**Negative Prompt (REQUIRED):**
```
3d render, realistic, photorealistic, detailed shading, gradient colors, cold colors, blurry, low quality, bad anatomy, distorted face, messy lines, daylight
```

**JSON Template:**
```json
{
  "parameters": {
    "width": 832,
    "height": 1248,
    "steps": 30,
    "cfg_scale": 7.0,
    "sampler_name": "DPM++ 2M Karras"
  },
  "prompt": "A cozy, retro-style flat color anime illustration with bold outlines. [SUBJECT DESCRIPTION]. The color palette is dominated by warm yellows, oranges, and browns. Clean cel-shading style.",
  "negative_prompt": "3d render, realistic, photorealistic, detailed shading, gradient colors, cold colors, blurry, low quality, bad anatomy, distorted face, messy lines, daylight"
}
```

---

## Keyword Reference Tables

### Line Style

| Keyword | Effect | Use Case |
|---------|--------|----------|
| bold outlines | Heavy visible borders | Standard illustration |
| thick defined outlines | Print-quality lines | Traditional/woodblock |
| confident outlines | No hesitation marks | Professional look |
| precise linework | Geometric accuracy | Vector/technical |
| highly detailed line work | Intricate patterns | Art Nouveau |

### Color Treatment

| Keyword | Effect | Use Case |
|---------|--------|----------|
| flat color | No gradients | All illustration styles |
| flat muted colors | Desaturated flats | Retro/vintage |
| limited color palette | 3-5 colors max | Pop art, poster |
| high contrast | Strong value differences | Impact/drama |
| sepia tone | Brown-tinted palette | Nostalgic/historic |

### Shading Control

| Keyword | Effect | Use Case |
|---------|--------|----------|
| zero shadows | Completely flat | Maximum stylization |
| minimal shading | Subtle depth hints | Balanced illustration |
| cel-shaded | Anime-style sharp shadows | Character art |
| no volumetric lighting | Prevents 3D look | All illustration |

### Background Style

| Keyword | Effect | Use Case |
|---------|--------|----------|
| plain solid [color] background | Single color | Character focus |
| graphic cityscape | Stylized urban | Pop art |
| stylized clouds | Non-realistic atmosphere | Fantasy |
| off-white/light grey | Neutral backdrop | Portfolio/clean |

---

## Negative Prompt Patterns

### Universal Illustration Negatives (ALWAYS include)
```
3d render, photorealistic, realistic, volumetric lighting, low quality, bad anatomy, distorted face
```

### Style-Specific Additions

| Style | Additional Negatives |
|-------|---------------------|
| Cel-Shaded Anime | thick painting, textured brushstrokes, gradient shading, missing limbs |
| Vector Art | detailed shading, gradient colors, complex background, messy lines |
| Art Nouveau | modern anime style, vibrant colors, glossy finish, heavy shading, sketchy |
| Comic Pop Art | painting, soft shading, gradient colors, blurred, standard anime style, muted colors |
| Retro Pop | detailed shading, gradient colors, complex background, messy lines |
| Cozy Cafe | cold colors, daylight, gradient colors, messy lines |

---

## Quick Style Selector

| I want... | Use Style | Key Negative |
|-----------|-----------|--------------|
| Modern anime look | Cel-Shaded Anime | gradient shading |
| App/icon style | Clean Vector | messy lines |
| Fantasy poster | Art Nouveau | modern anime style |
| Street/urban art | Comic Pop Art | soft shading |
| Retro character | Retro Pop | complex background |
| Warm lifestyle scene | Cozy Cafe | cold colors |

---

## Prompt Length Guidelines

**Recommended: 800-1200 characters**

Structure your prompt:
1. **Style declaration** (50-100 chars): "A flat color anime illustration in cel-shaded style..."
2. **Subject details** (300-500 chars): Character, pose, clothing, expression
3. **Dynamic elements** (100-200 chars): Wind, motion, breath effects
4. **Background** (100-200 chars): Environment or solid color
5. **Style reinforcement** (50-100 chars): "Clean vector art aesthetic, zero shadows."
