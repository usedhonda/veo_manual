# Veo 3.1 Video Generation JSON Schema

## Purpose
Generate high-quality video clips with precise control over cinematography, action, and audio.

## Generation Modes

| Mode | Input | Use Case |
|------|-------|----------|
| **Text-to-Video** | Text prompt only | Quick concepts, abstract visuals |
| **Image-to-Video** | First Frame image + text | Animate specific starting composition |
| **Ingredients** | Reference images + text | Character/object consistency |
| **Frame Interpolation** | Start Frame + End Frame + text | Transitions, morphs, loops |

---

## Complete JSON Schema (8 Keys)

```json
{
  "shot": {
    "type": "wide | medium | close-up | extreme-close-up | establishing",
    "movement": "static | dolly_in | dolly_out | tracking | orbit | pan_left | pan_right | tilt_up | tilt_down | crane_up | crane_down | handheld",
    "lens": "24mm | 35mm | 50mm | 85mm | 135mm | macro | telephoto | anamorphic | fisheye",
    "speed": "very_slow | slow | normal | fast | very_fast",
    "focus": "deep | shallow | rack_focus"
  },
  "subject": {
    "identity": "string - detailed subject description",
    "appearance": {
      "clothing": "string - outfit details",
      "features": "string - physical characteristics",
      "distinguishing_marks": "string - unique identifiers for consistency"
    },
    "expression": "string - emotional state, facial expression",
    "position": "center | left | right | foreground | background | entering_frame | exiting_frame"
  },
  "action": {
    "primary": "string - main action verb (walks, runs, speaks, transforms)",
    "secondary": "string - supporting action",
    "speed": "slow | normal | fast",
    "direction": "toward_camera | away_from_camera | left_to_right | right_to_left | circular",
    "timing": "string - when action occurs within clip"
  },
  "scene": {
    "location": "string - environment description",
    "time_of_day": "dawn | morning | noon | afternoon | golden_hour | dusk | blue_hour | night | midnight",
    "weather": "clear | sunny | cloudy | overcast | rain | storm | snow | fog | mist | wind",
    "atmosphere": "string - mood descriptors"
  },
  "style": {
    "medium": "live_action | anime | 3d_animation | stop_motion | claymation | cel_animation | rotoscope",
    "film_reference": "string - camera or film stock reference",
    "color_grade": "string - color palette or grading style",
    "era": "string - time period aesthetic",
    "genre": "string - cinematic genre reference"
  },
  "audio": {
    "dialogue": "string - Character says: \"exact spoken line\"",
    "sfx": "string - SFX: specific sound effects",
    "ambience": "string - Ambience: environmental background sounds",
    "music": "string - Music: genre, mood, instruments (or 'NO music' to prevent)",
    "voice_style": "string - tone, accent, emotion of dialogue"
  },
  "negative": {
    "exclude": [
      "subtitles",
      "text_overlay",
      "watermark",
      "blur",
      "distortion",
      "extra_limbs",
      "morphing",
      "low_quality",
      "grainy"
    ]
  },
  "meta": {
    "duration": 8,
    "resolution": "1080p | 720p",
    "aspect_ratio": "16:9 | 9:16",
    "fps": 24,
    "model": "veo-3.1-generate-001 | veo-3.1-fast-generate-001"
  }
}
```

---

## Simplified Schema (Quick Prototyping)

```json
{
  "shot": "string - shot type and camera movement",
  "subject": "string - who/what is in frame",
  "action": "string - what happens",
  "scene": "string - where and when",
  "style": "string - visual aesthetic",
  "audio": "string - sounds and dialogue"
}
```

---

## Mode-Specific Schemas

### Text-to-Video
Standard schema, no additional fields required.

### Image-to-Video (First Frame)
```json
{
  "input_image": {
    "source": "base64 | gcs_uri",
    "role": "first_frame"
  },
  "shot": { ... },
  "subject": {
    "reference": "Use the subject from the input image",
    ...
  },
  "action": {
    "primary": "string - what the subject does STARTING from this frame",
    ...
  },
  ...
}
```

### Ingredients (Reference Images)
```json
{
  "reference_images": [
    {
      "source": "base64 | gcs_uri",
      "role": "asset",
      "description": "string - what this image provides (character, object, etc.)"
    }
  ],
  "subject": {
    "reference": "Using the character/object from reference image 1",
    "appearance": {
      "reinforce": "string - re-state key visual traits from reference"
    },
    ...
  },
  ...
}
```

**Important**: Maximum 3 reference images. Type must be "asset" (not "style" in Veo 3.1).

### Frame Interpolation (Start + End)
```json
{
  "input_image": {
    "source": "base64 | gcs_uri",
    "role": "first_frame"
  },
  "last_frame": {
    "source": "base64 | gcs_uri",
    "role": "last_frame"
  },
  "action": {
    "primary": "string - transition type (morphs, transforms, ages, moves to)",
    "interpolation_style": "smooth | dramatic | gradual"
  },
  ...
}
```

---

## Key Field Details

### shot.movement Values (Reliability Ranked)

| Movement | Reliability | Notes |
|----------|-------------|-------|
| `static` | ✅ High | Use with First+Last Frame for locked shots |
| `slow dolly_in` | ✅ High | Gentle push-in |
| `slow dolly_out` | ✅ High | Gentle pull-out |
| `tracking` | ✅ High | Follow moving subject |
| `orbit` | ✅ High | Circle around subject |
| `crane_up` | ✅ High | Vertical rise |
| `crane_down` | ✅ High | Vertical descent |
| `pan_left/right` | ✅ High | Horizontal sweep |
| `tilt_up/down` | ✅ High | Vertical sweep |
| `handheld` | ✅ High | Slight natural shake |
| `zoom_in/out` | ⚠️ Medium | Can be unpredictable |

**Rule**: Use ONE camera movement per clip. Multiple movements cause artifacts.

### action.primary Effective Verbs

| Category | Verbs |
|----------|-------|
| Movement | `walks`, `runs`, `jumps`, `falls`, `rises`, `spins`, `dances` |
| Interaction | `picks up`, `puts down`, `opens`, `closes`, `pushes`, `pulls` |
| Expression | `smiles`, `frowns`, `laughs`, `cries`, `screams`, `whispers` |
| Transform | `transforms`, `morphs`, `ages`, `dissolves`, `materializes` |
| Communication | `speaks`, `gestures`, `nods`, `shakes head`, `points` |

**Rule**: One action per 8-second clip. Complex sequences = multiple clips.

### audio Format Standards

```json
"audio": {
  "dialogue": "Detective Cole says: \"We need to find her before midnight.\"",
  "sfx": "SFX: footsteps on wet pavement, distant thunder",
  "ambience": "Ambience: rain falling, city traffic hum, neon sign buzz",
  "music": "Music: tense orchestral, low strings, building suspense"
}
```

**To prevent unwanted music**: `"music": "NO music, ambient sounds only"`

---

## Validation Rules

### Duration Constraints
- Valid values: `4`, `6`, `8` seconds only
- Interpolation: typically locked to `8` seconds
- Extension input: max 141 seconds

### Resolution Constraints
- `1080p`: Full quality, standard generation
- `720p`: Required for video extension
- Extension: 720p output only

### Aspect Ratio Constraints
- `16:9`: Landscape (standard)
- `9:16`: Portrait (vertical video)
- Other ratios not supported

### Reference Image Constraints
- Maximum: 3 images
- Type: `"asset"` only (no `"style"` in Veo 3.1)
- Format: JPEG or PNG
- Resolution: Match target video resolution recommended

---

## Common Patterns

### Dialogue Scene
```json
{
  "shot": {
    "type": "medium",
    "movement": "static",
    "lens": "50mm",
    "focus": "shallow"
  },
  "subject": {
    "identity": "Woman in her 30s, professional attire",
    "expression": "concerned, speaking earnestly"
  },
  "action": {
    "primary": "speaks",
    "timing": "throughout clip"
  },
  "audio": {
    "dialogue": "She says: \"I think we need to reconsider our approach.\"",
    "ambience": "Ambience: quiet office, air conditioning hum",
    "music": "NO music"
  },
  "negative": {
    "exclude": ["subtitles", "text_overlay"]
  }
}
```

### Action Sequence
```json
{
  "shot": {
    "type": "wide",
    "movement": "tracking",
    "lens": "24mm",
    "speed": "fast"
  },
  "subject": {
    "identity": "Athletic man in running gear",
    "position": "center, moving left to right"
  },
  "action": {
    "primary": "sprints",
    "secondary": "leaps over obstacle",
    "direction": "left_to_right",
    "timing": "0-4s sprint, 4-6s leap, 6-8s landing"
  },
  "audio": {
    "sfx": "SFX: rapid footsteps, whoosh of jump, heavy landing",
    "ambience": "Ambience: urban environment, distant traffic"
  }
}
```

### Product Hero Shot
```json
{
  "shot": {
    "type": "close-up",
    "movement": "slow orbit",
    "lens": "macro",
    "focus": "shallow"
  },
  "subject": {
    "identity": "Premium headphones on reflective surface",
    "reference": "Using product from reference image"
  },
  "action": {
    "primary": "rotates slowly",
    "secondary": "light sweeps across surface"
  },
  "style": {
    "color_grade": "high contrast, deep blacks, bright highlights",
    "genre": "commercial product photography"
  },
  "audio": {
    "music": "Music: modern electronic, subtle pulse, premium feel"
  }
}
```
