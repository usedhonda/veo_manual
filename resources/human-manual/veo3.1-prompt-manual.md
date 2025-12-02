# Veo 3.1 Prompt Generation Manual

> **For AI Use**: This manual provides instructions for generating Veo 3.1 compatible video prompts.
> **Last Updated**: 2025-12-02

---

## 1. Overview

Google Veo 3.1 is an AI video generation model available via Gemini API, Vertex AI, and Google Flow.

### Capabilities
- **Resolution**: 720p or 1080p
- **Duration**: 4, 6, or 8 seconds (extendable up to 60+ seconds via Scenebuilder)
- **Frame Rate**: 24 fps (fixed)
- **Aspect Ratio**: 16:9 (landscape) or 9:16 (portrait)
- **Audio**: Native dialogue, SFX, ambient sound generation with lip-sync

### Model Variants
| Model | Quality | Speed | Ingredients | Video Extension | Notes |
|-------|---------|-------|-------------|-----------------|-------|
| Veo 3.1 | Highest | Standard | Yes (up to 3) | Yes | Full features |
| Veo 3.1 Fast | Good | Fast | Landscape only | No | Quick iterations |

---

## 2. Prompt Formula

### Official Formula (Google)
```
[CINEMATOGRAPHY] + [SUBJECT] + [ACTION] + [CONTEXT] + [SOUND/AUDIO]
```

### Extended Formula
```
[CINEMATOGRAPHY] + [SUBJECT] + [ACTION] + [CONTEXT] + [STYLE/AMBIANCE] + [AUDIO]
```

### Components

| Component | Description | Example |
|-----------|-------------|---------|
| Cinematography | Shot type, camera angle, movement | "Medium shot, slow dolly in" |
| Subject | Main focus of the scene | "A tired corporate worker" |
| Action | What the subject is doing | "rubbing his temples in exhaustion" |
| Context | Setting, background, environment | "in a cluttered 1980s office at night" |
| Style/Ambiance | Mood, lighting, visual style | "harsh fluorescent lighting, retro aesthetic, shot on 35mm film" |
| Audio | Dialogue, SFX, ambient sounds | "Audio: keyboard clacking, fluorescent hum" |

### Example Prompt

```
Medium shot, a tired corporate worker, rubbing his temples in exhaustion,
in front of a bulky 1980s computer in a cluttered office late at night.
The scene is lit by harsh fluorescent overhead lights and the green glow
of the monochrome monitor. Retro 1980s aesthetic, slightly grainy, as if
shot on 35mm film. Audio: distant keyboard clacking, fluorescent light humming.
```

---

## 3. JSON Structured Prompts

For complex multi-shot control, use JSON format:

```json
{
  "title": "Scene Name",
  "duration_seconds": 8,
  "aspect_ratio": "16:9 (Cinematic Widescreen)",
  "fidelity": "Hyper-realistic, photorealistic 8K, cinematic master",
  "cinematography": "Medium close-up, slow dolly in",
  "subject": "A young woman",
  "action": "reacts with wide-eyed excitement",
  "context": "at her gaming desk",
  "lighting": "bathed in neon pink-blue LED lighting that pulses subtly",
  "audio": "keyboard clacking, ambient electronic hum"
}
```

### JSON Fidelity Keywords
- "Hyper-realistic 16K, IMAX quality"
- "Photorealistic 8K, cinematic master"
- "Film stock with subtle grain"
- "Zero-gravity aesthetics"

---

## 4. Keywords Dictionary

### Camera Shots
| Keyword | Description |
|---------|-------------|
| Wide shot | Full scene view |
| Medium shot | Subject from waist up |
| Medium close-up (MCU) | Head and shoulders |
| Close-up | Face or detail |
| Extreme close-up | Very tight on detail |
| POV shot | First-person perspective |
| Over-the-shoulder | From behind a character |
| Low-angle shot | Camera below subject (imposing) |
| High-angle shot | Camera above subject |
| Eye-level shot | Neutral perspective |
| Aerial shot | Bird's eye view |

### Camera Movements (Critical for Veo 3.1)
| Keyword | Description |
|---------|-------------|
| Dolly in / Dolly out | Push toward / Pull away from subject |
| Pan left / Pan right | Horizontal camera swivel |
| Tilt up / Tilt down | Vertical camera movement |
| Tracking shot | Camera follows moving subject |
| Orbit around | Circle around subject |
| Crane shot | Lifting/lowering camera |
| Steadicam | Smooth following movement |
| Handheld | Shaky, documentary feel |
| Static shot | No camera movement |

> **Important**: Camera motion terminology is CRITICAL for Veo 3.1 quality. Use proper cinematography vocabulary.

### Lens & Depth
| Keyword | Effect |
|---------|--------|
| Shallow depth of field | Blurry background, sharp subject |
| Deep focus | Everything sharp |
| Wide-angle lens | Broader view, some distortion |
| Macro lens | Extreme close-up of small objects |
| 35mm film | Organic, grainy feel |
| 50mm lens | Natural perspective |

### Lighting
| Keyword | Effect |
|---------|--------|
| Golden hour | Warm sunset/sunrise light |
| Soft light | Diffused, gentle shadows |
| Harsh light | Strong shadows, high contrast |
| Backlight | Light from behind subject |
| Rim lighting | Edge glow on subject |
| Silhouette | Subject as dark shape |
| Neon glow | Colorful artificial light |
| Neon pink-blue LED lighting | Gaming/streaming aesthetic |
| Moonlight | Cool, blue night light |
| Film noir | High contrast, dramatic shadows |
| Volumetric lighting | Visible light rays |
| Dynamic lighting | Changing light during scene |

### Time of Day
| Keyword | Light Quality |
|---------|---------------|
| Dawn / Sunrise | Soft warm, long shadows |
| Morning | Clean, neutral |
| Midday | Harsh overhead |
| Golden hour | Warm, cinematic |
| Twilight / Dusk | Purple/pink sky |
| Night | Dark, artificial lights |

### Visual Styles
| Keyword | Description |
|---------|-------------|
| Photorealistic | Real-world look |
| Cinematic | Film-like quality |
| Shot on Arri Alexa | Digital cinema look |
| Shot on RED | Crisp detailed look |
| 35mm film | Grainy organic feel |
| VHS style | Retro, degraded |
| Anime style | Japanese animation |
| Studio Ghibli style | Miyazaki animation |
| Wes Anderson style | Symmetrical, pastel |
| David Fincher style | Dark, moody, precise |
| Christopher Nolan style | Epic, high-contrast |
| Blade Runner 2049 | Neon futuristic |
| Film noir | 1940s black-and-white |

### Color & Mood
| Keyword | Effect |
|---------|--------|
| Teal and orange | Hollywood blockbuster grade |
| Muted tones | Desaturated, subdued |
| High saturation | Vivid, punchy colors |
| Warm tones | Orange, yellow dominant |
| Cool tones | Blue, cyan dominant |
| Black and white | Monochrome |
| High contrast | Strong darks and lights |

---

## 5. Audio Instructions

Veo 3.1 generates synchronized audio. **Always include audio cues.**

### Dialogue

Write speech in quotes with speaker identification:

```
The detective says, "Where were you last night?"
The woman replies nervously, "I was home alone."
```

#### Natural Dialogue Tips (Community Insights)
To make dialogue feel human, NOT robotic:

1. **Establish character mindset** in the prompt
2. **Specify accents** for authenticity
3. **Use intentional bad grammar** - people don't speak perfectly
4. **Include (actions/thoughts)** within dialogue
5. **Write the way people actually speak**

**Example - Stiff (Avoid):**
```
The man says, "I am going to the store to purchase some groceries."
```

**Example - Natural (Preferred):**
```
The tired man mutters (rubbing his eyes), "Gonna grab some... uh, groceries or whatever."
```

### Sound Effects (SFX)
Use "SFX:" prefix:

```
SFX: thunder cracks in the distance
SFX: footsteps on gravel
SFX: door slams shut
SFX: glass shattering
```

### Ambient Sound
Describe background sounds:

```
Audio: quiet hum of a starship bridge
Ambient noise: bustling cafe chatter
Audio: gentle rain on windows, distant thunder
```

### Music
Describe mood and instruments:

```
Audio: a soft piano melody plays in the background
Audio: tense string orchestra builds suspense
Audio: upbeat electronic music
```

### Audio Format Tips
- Write audio in **separate sentences** from visual description
- Use intensity words: "loud", "faint", "distant", "muffled", "echoing"
- Align sounds with visible actions

### Complete Audio Example

```
A woman walks through a rainy alley at night, looking over her shoulder nervously.
Neon signs reflect in puddles. Moody film noir lighting.
Audio: heavy rain pattering on pavement, distant thunder rumbling.
SFX: her heels clicking on wet concrete.
She whispers to herself (glancing behind), "Almost there..."
```

---

## 6. Parameters

| Parameter | Options | Notes |
|-----------|---------|-------|
| Aspect Ratio | 16:9, 9:16 | 16:9 default; some features require 16:9 |
| Resolution | 720p, 1080p | 1080p requires 8s duration |
| Duration | 4s, 6s, 8s | 8s required for advanced features |
| Negative Prompt | Text | Describe what to avoid |
| Seed | Number | For reproducibility (not guaranteed identical) |
| Reference Images | 1-3 images | For character/style consistency |

### Negative Prompt Examples

```
negativePrompt: "cartoon, drawing, low quality, blurry, distorted faces"
negativePrompt: "text, watermark, logo, signature"
negativePrompt: "anime, illustration, 3D render"
```

---

## 7. Advanced Features

### Ingredients (Reference Images)

Supply 1-3 reference images for consistency:

**Use Cases:**
- Keep same character across multiple shots
- Maintain consistent art style
- Preserve specific object/setting appearance
- Product videos with consistent item appearance

**Requirements:**
- 16:9 aspect ratio only
- 8-second duration only
- Use clear, neutral reference images
- **Veo 3.1 Fast**: Landscape mode only

**Tip (Official):** To use more than 3 references, combine multiple images into a single collage and upload as one ingredient.

**Prompt Pattern:**
```
Using the provided character reference, create a medium shot of the detective
sitting at his desk, examining evidence. Film noir lighting, office setting.
```

### First & Last Frame (Keyframe Control)

Specify start and end images for controlled transitions:

**Use Cases:**
- Precise camera movements
- Scene transformations
- Morphing effects
- Animate between two specific poses

**Prompt Pattern:**
```
Transition from the provided start frame to the end frame with a smooth
camera orbit, revealing the full landscape. Golden hour lighting.
Audio: wind blowing gently, birds chirping.
```

### Scenebuilder (Google Flow)

Build longer videos with scene-by-scene control:

**Features:**
- Portrait Mode support
- Annotations (Doodles) for movement control
- Extend function for 60+ second videos
- Insert function for adding new scenes

**How to Create 8+ Second Videos:**
1. Go to Google Flow
2. Generate first 8-second scene
3. Click "add to scene"
4. Scenebuilder opens
5. Click + icon → "extend"
6. Select Veo 3.1 model
7. Repeat for longer sequences

**Cost Tip:** Using start frame from prior clip costs NO credits.

### Video Extension

Chain clips for longer sequences (up to 60+ seconds):

- Veo uses last second of previous clip as context
- Maintains visual and audio continuity
- Request continuation with similar prompt + modifications

**Limitation:** Extend feature may have quality/consistency issues for some content types.

### Camera Adjustment (Post-Generation)

Available after initial generation:
- Tweak camera movements
- Adjust framing
- Fine-tune motion

---

## 8. Best Practices

### Do
- **Front-load important details** (early words weighted more heavily)
- **Use proper cinematography terms** (critical for camera motion)
- **One main action per prompt**
- **Be specific**: "shuffling with hunched shoulders" not "walking sadly"
- **Include audio cues** for realism
- **Use specific style references** instead of generic terms
- **Generate multiple variations** (up to 4 per request) and select best
- **Write dialogue like humans speak** (imperfect grammar, pauses, filler words)

### Don't
- Use vague terms: "beautiful", "amazing", "high quality"
- Request multiple unrelated actions in one prompt
- Combine conflicting styles: "Tarantino meets Pixar"
- Use complex compound camera movements
- Write long monologues (keep dialogue brief)
- Forget audio (silent videos feel incomplete)
- Write overly formal/robotic dialogue

### Prompt Quality Checklist

1. [ ] Shot type specified?
2. [ ] Camera movement terms correct?
3. [ ] Subject clearly described?
4. [ ] Action is specific and singular?
5. [ ] Environment/context included?
6. [ ] Lighting/mood described?
7. [ ] Style reference (not generic)?
8. [ ] Audio cues included?
9. [ ] Dialogue sounds natural?
10. [ ] Negative prompt if needed?

---

## 9. Language Notes

### Japanese Content
- Direct Japanese text prompts may be rejected
- **Workaround**: Use Romaji for Japanese speech generation
- Example: "Arigatou gozaimasu" instead of "ありがとうございます"

### Veo 3.1 Fast on Hugging Face
- May accept Japanese prompts in some cases
- Test and iterate

---

## 10. Limitations

### Technical Constraints
- Maximum 8 seconds per generation
- 24 fps fixed (no 60fps option)
- 1080p requires 8s duration
- Reference images require 16:9 and 8s
- Ingredients only in Veo 3.1 Fast + Landscape mode

### Quality Issues
- Complex morphing may produce artifacts
- Text rendering is imperfect
- Physics can be violated occasionally
- Multiple simultaneous actions may fail
- Extend feature may have consistency issues

### Content Restrictions
- No celebrity likenesses
- No copyrighted characters
- Some regions restrict to adult characters only
- Safety filters may block certain content

### Audio Limitations
- Music generation is basic
- Long dialogue may be truncated
- Complex layered audio may be inconsistent

### Veo 3.1 Fast Limitations
- Sharper output but leans toward "stock video" aesthetic
- No Ingredients feature (except Landscape mode)

---

## 11. Example Prompts

### Cinematic Scene
```
Wide establishing shot at dawn. A medieval village square with colorful market
tents being set up. Slow pan across the scene as villagers begin their day.
Soft golden morning light creates long shadows. Shot on 35mm film, Studio
Ghibli inspired aesthetic. Audio: roosters crowing, distant church bells,
merchants calling out, wooden cart wheels on cobblestones.
```

### Action Sequence
```
Low-angle tracking shot. A cyberpunk samurai with glowing blue armor sprints
through a neon-lit alley in Neo-Tokyo. Rain pours down, reflecting city lights
in puddles. Blade Runner 2049 cinematography, high contrast, volumetric
lighting. SFX: heavy rain, splashing footsteps, distant sirens wailing,
electronic hum of neon signs.
```

### Dialogue Scene (Natural Style)
```
Medium shot, over-the-shoulder. A weary detective in a dimly lit office faces
a nervous woman across his desk. Film noir lighting with harsh shadows.
1940s aesthetic. The detective exhales slowly, "So... tell me what you saw."
The woman fidgets (avoiding eye contact), "I... I saw everything. All of it."
Audio: rain against window, ticking clock, creak of leather chair.
```

### Product Shot
```
Extreme close-up with shallow depth of field. A luxury watch rotating slowly
on a black velvet surface. Soft rim lighting highlights the metallic details.
Clean, high-end commercial aesthetic. Slow dolly around the product.
Audio: subtle ambient tone, soft mechanical ticking.
```

### Nature Documentary
```
Aerial drone shot descending toward a misty forest at sunrise. Golden light
breaks through the canopy. David Attenborough documentary style, photorealistic.
Crane down into the trees revealing wildlife below. Audio: morning birdsong,
gentle wind through leaves, distant waterfall.
```

### Gaming/Streaming Scene
```
Medium close-up shot of a young woman streaming live at her gaming desk,
bathed in neon pink-blue LED lighting that pulses subtly in the background.
She reacts with wide-eyed excitement, leaning forward toward the screen.
Photorealistic, modern aesthetic. Audio: keyboard clacking, excited gasp,
"Oh my god, did you SEE that?!"
```

---

## 12. Quick Reference Card

### Prompt Template
```
[Shot type], [Subject], [Action], [Setting]. [Lighting/Style].
[Style reference]. Audio: [ambient]. SFX: [effects].
[Speaker] says (action), "[Dialogue]."
```

### Essential Keywords
- **Shots**: wide, medium, MCU, close-up, POV, tracking
- **Movement**: dolly, pan, tilt, orbit, crane, static, steadicam
- **Light**: golden hour, soft, harsh, neon, silhouette, rim lighting
- **Style**: 35mm film, cinematic, [Director] style, [Movie] aesthetic
- **Audio**: SFX:, Audio:, Ambient:, "[Dialogue]"

### Parameters Cheat Sheet
| Need | Setting |
|------|---------|
| Landscape video | 16:9 |
| Vertical/mobile | 9:16 |
| Best quality | 1080p + 8s |
| Quick preview | 720p + 4s |
| Character consistency | Reference images + 16:9 + 8s |
| More than 3 references | Combine into collage |
| Avoid unwanted elements | Use negative prompt |
| Videos 60+ seconds | Use Scenebuilder extend |

### Workflow Combinations (Popular)
| Purpose | Tool Combination |
|---------|------------------|
| Character consistency | Nano Banana Pro → Veo 3.1 |
| Keyframe animation | Flux 1.1 → Veo 3.1 |
| Character reference | Midjourney → Veo 3.1 |
| Dialogue + Action | Veo 3.1 (dialogue) + Wan 2.2 (effects) |

### Platforms Supporting Veo 3.1
- Google Flow (official, full features)
- Gemini App
- Vertex AI
- Runway API
- LTX Studio
- Hugging Face
- Pippit
- Arcads.ai

---

*This manual is designed for AI consumption. For human readers, more context may be needed.*
*Community insights sourced from X (Twitter) as of 2025-12-02.*
