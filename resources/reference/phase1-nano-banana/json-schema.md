# Nano Banana Pro (Gemini 2.5 Flash Image) JSON Schema

## Purpose
Generate high-quality static images optimized for Veo 3.1 video production pipeline.

## Output Requirements for Veo 3.1 Compatibility

| Parameter | Veo 3.1 Requirement | Recommendation |
|-----------|---------------------|----------------|
| Resolution | 720p or 1080p | Match target video resolution |
| Aspect Ratio | 16:9 or 9:16 | Match target video aspect ratio |
| Format | PNG or JPEG | PNG for transparency, JPEG for photos |
| Composition | Leave motion space | Don't center subject if movement planned |

---

## Standard Schema

```json
{
  "subject": {
    "identity": "string - main subject description",
    "appearance": {
      "clothing": "string - outfit details",
      "features": "string - physical characteristics",
      "age": "string - age range",
      "accessories": "string - items worn/carried"
    },
    "expression": "string - emotional state, gaze direction",
    "pose": "string - body position, gesture"
  },
  "composition": {
    "framing": "full_body | three_quarter | waist_up | bust | close_up | extreme_close_up",
    "angle": "eye_level | low_angle | high_angle | bird_eye | worm_eye | dutch_angle",
    "subject_position": "center | rule_of_thirds_left | rule_of_thirds_right | off_center",
    "negative_space": "string - where to leave empty space for motion"
  },
  "background": {
    "type": "environment | studio | transparent | solid_color",
    "description": "string - detailed background description",
    "blur": "none | slight | moderate | heavy_bokeh"
  },
  "lighting": {
    "type": "natural | studio | dramatic | neon | ambient",
    "direction": "front | side | back | rim | rembrandt | butterfly",
    "quality": "soft | hard | diffused",
    "color_temperature": "warm | neutral | cool",
    "special": "string - volumetric, lens flare, etc."
  },
  "style": {
    "medium": "photorealistic | anime | 3d_render | illustration | oil_painting | watercolor",
    "aesthetic": "string - art direction keywords",
    "color_palette": "string - dominant colors",
    "mood": "string - emotional tone"
  },
  "technical": {
    "resolution": "1080p | 720p | 4K",
    "aspect_ratio": "16:9 | 9:16 | 1:1 | 4:3",
    "camera_reference": "string - camera/lens simulation",
    "post_processing": "string - color grade, filters"
  },
  "veo_optimization": {
    "intended_use": "first_frame | ingredient | last_frame | standalone",
    "planned_motion": "string - what movement will happen in video",
    "consistency_anchors": "array - features to maintain across shots"
  }
}
```

---

## Use Case Schemas

### Character Sheet (for Consistency)

```json
{
  "subject": {
    "identity": "Cyberpunk detective, female, late 20s",
    "appearance": {
      "clothing": "Black leather trench coat, neon-trimmed collar",
      "features": "Sharp jawline, cybernetic left eye glowing blue, short black hair with purple highlights",
      "age": "25-30",
      "accessories": "Holographic badge on belt, wireless earpiece"
    },
    "expression": "Determined, focused gaze",
    "pose": "Standing confidently, arms crossed"
  },
  "composition": {
    "framing": "full_body",
    "angle": "eye_level",
    "subject_position": "center",
    "negative_space": "minimal - character sheet focus"
  },
  "background": {
    "type": "solid_color",
    "description": "Pure white or neutral gray",
    "blur": "none"
  },
  "lighting": {
    "type": "studio",
    "direction": "front",
    "quality": "soft",
    "color_temperature": "neutral",
    "special": "even lighting for reference clarity"
  },
  "style": {
    "medium": "photorealistic",
    "aesthetic": "Clean character reference",
    "color_palette": "Accurate to character design",
    "mood": "Neutral presentation"
  },
  "technical": {
    "resolution": "1080p",
    "aspect_ratio": "16:9",
    "camera_reference": "Studio portrait lens 85mm",
    "post_processing": "Minimal, true colors"
  },
  "veo_optimization": {
    "intended_use": "ingredient",
    "planned_motion": "Various scenes - walking, talking, action",
    "consistency_anchors": ["cybernetic eye", "trench coat", "hair color", "badge"]
  }
}
```

### Product Shot (for Commercial)

```json
{
  "subject": {
    "identity": "Premium wireless headphones",
    "appearance": {
      "clothing": "N/A",
      "features": "Matte black finish, rose gold accents, memory foam ear cups",
      "age": "N/A",
      "accessories": "N/A"
    },
    "expression": "N/A",
    "pose": "45-degree angle, slight tilt showing both cups"
  },
  "composition": {
    "framing": "close_up",
    "angle": "slightly_elevated",
    "subject_position": "center",
    "negative_space": "generous on right side for text/motion"
  },
  "background": {
    "type": "studio",
    "description": "Gradient from dark charcoal to deep purple",
    "blur": "none"
  },
  "lighting": {
    "type": "studio",
    "direction": "rim",
    "quality": "hard",
    "color_temperature": "cool",
    "special": "Accent light highlighting rose gold, subtle reflection on surface"
  },
  "style": {
    "medium": "photorealistic",
    "aesthetic": "Premium tech advertising",
    "color_palette": "Black, rose gold, purple accent",
    "mood": "Luxurious, sophisticated"
  },
  "technical": {
    "resolution": "1080p",
    "aspect_ratio": "16:9",
    "camera_reference": "Macro lens, shallow depth of field",
    "post_processing": "High contrast, enhanced highlights"
  },
  "veo_optimization": {
    "intended_use": "first_frame",
    "planned_motion": "Slow rotation, light sweep across surface",
    "consistency_anchors": ["product shape", "color scheme", "lighting style"]
  }
}
```

### Scene Background (for Environment)

```json
{
  "subject": {
    "identity": "Empty cyberpunk street scene",
    "appearance": {
      "clothing": "N/A",
      "features": "Neon signs, wet pavement, steam vents, holographic advertisements",
      "age": "N/A",
      "accessories": "N/A"
    },
    "expression": "N/A",
    "pose": "N/A"
  },
  "composition": {
    "framing": "wide_shot",
    "angle": "eye_level",
    "subject_position": "N/A",
    "negative_space": "Center-left area clear for character insertion"
  },
  "background": {
    "type": "environment",
    "description": "Narrow alleyway between towering buildings, neon signs in Japanese and English, rain-slicked streets reflecting colorful lights, steam rising from grates",
    "blur": "slight at distant buildings"
  },
  "lighting": {
    "type": "neon",
    "direction": "multiple sources",
    "quality": "mixed",
    "color_temperature": "cool with warm neon accents",
    "special": "Volumetric fog, neon reflections on wet surfaces"
  },
  "style": {
    "medium": "photorealistic",
    "aesthetic": "Blade Runner inspired cyberpunk",
    "color_palette": "Teal, magenta, orange neon against dark blues",
    "mood": "Mysterious, atmospheric, noir"
  },
  "technical": {
    "resolution": "1080p",
    "aspect_ratio": "16:9",
    "camera_reference": "Wide angle 24mm",
    "post_processing": "Cinematic color grade, enhanced neon glow"
  },
  "veo_optimization": {
    "intended_use": "first_frame",
    "planned_motion": "Character walks into frame from right, camera follows",
    "consistency_anchors": ["neon color scheme", "wet surface reflections", "atmospheric haze"]
  }
}
```

---

## Key Differences from Video Schema

| Aspect | Image (Nano Banana) | Video (Veo 3.1) |
|--------|---------------------|-----------------|
| Motion | Static composition | Camera movement, subject action |
| Audio | N/A | Dialogue, SFX, music |
| Duration | N/A | 4, 6, or 8 seconds |
| Focus | Maximum detail | Motion-optimized |
| Negative Space | For future animation | For current action |

---

## Veo 3.1 Input Optimization Checklist

- [ ] Resolution matches target video (720p or 1080p)
- [ ] Aspect ratio matches target video (16:9 or 9:16)
- [ ] Subject has clear, identifiable features for consistency
- [ ] Composition leaves space for planned movement
- [ ] Lighting direction is consistent for multi-shot sequences
- [ ] Background doesn't conflict with planned overlays
- [ ] Key visual anchors are prominent and memorable
