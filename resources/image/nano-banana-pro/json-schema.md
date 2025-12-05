# Nano Banana Pro (Gemini 3 Pro Image) JSON Schema

## Purpose
Generate high-quality static images with deterministic control using JSON structured prompts.

---

## Master JSON Schema

The complete schema for full control over Nano Banana Pro outputs:

```json
{
  "_meta": {
    "schema_version": "v3.0",
    "target_model": "Gemini 3 Pro Image (Nano Banana Pro)",
    "intent": "photorealistic_high_fidelity",
    "strict_mode": true
  },
  "subject": {
    "type": "person | object | scene | abstract",
    "count": 1,
    "identity": {
      "name": "string - optional identifier for consistency",
      "demographics": "string - age, ethnicity, gender if applicable",
      "persistent_features": [
        "feature that must remain consistent across images"
      ]
    },
    "current_state": {
      "pose": "string - body position, gesture",
      "expression": "string - emotional state",
      "gaze": "string - eye direction"
    },
    "attire": {
      "outfit": "string - clothing description",
      "colors": ["array of colors"],
      "details": "string - fabric, patterns, condition",
      "accessories": ["array of items"]
    }
  },
  "environment": {
    "location": "string - place description",
    "time": "string - time of day, weather",
    "spatial_structure": {
      "foreground": "string - elements closest to camera",
      "midground": "string - middle distance elements",
      "background": "string - distant elements",
      "depth": "string - perspective description"
    },
    "atmosphere": {
      "mood": "string - emotional tone keywords",
      "weather_effects": "string - rain, fog, steam, etc."
    }
  },
  "photography": {
    "camera_body": "string - camera model reference",
    "lens": {
      "focal_length": "string - mm value",
      "aperture": "string - f-stop",
      "type": "string - lens description"
    },
    "settings": {
      "shutter_speed": "string - exposure time",
      "iso": "string - sensitivity",
      "white_balance": "string - Kelvin or preset"
    },
    "composition": {
      "framing": "extreme_close_up | close_up | medium | full_body | wide",
      "angle": "eye_level | low_angle | high_angle | dutch_angle | bird_eye | worm_eye",
      "rule": "rule_of_thirds | center | golden_ratio | diagonal"
    },
    "visual_quality": {
      "resolution": "4K | 1080p | 720p",
      "texture": "string - detail level description",
      "artifacts": ["intentional imperfections for realism"]
    }
  },
  "lighting": {
    "setup": "string - lighting scheme name",
    "sources": [
      {
        "type": "key_light | fill_light | rim_light | practical | ambient",
        "position": "string - direction/angle",
        "color": "string - light color",
        "intensity": "high | medium | low",
        "effect": "string - optional specific effect"
      }
    ],
    "shadows": "string - shadow quality description"
  },
  "style": {
    "medium": "photorealistic | anime | 3d_render | illustration | oil_painting | watercolor | concept_art",
    "aesthetic": "string - art direction keywords",
    "color_palette": "string - dominant colors or scheme",
    "mood": "string - emotional atmosphere",
    "render_engine": "string - optional 3D engine reference (Octane, Unreal, etc.)"
  },
  "constraints": {
    "negative": [
      "elements to avoid"
    ],
    "must_include": [
      "required elements"
    ],
    "text_content": {
      "text": "string - exact text to render",
      "font": "string - font style",
      "position": "string - placement"
    }
  },
  "veo_optimization": {
    "intended_use": "first_frame | ingredient | last_frame | standalone",
    "planned_motion": "string - what movement will happen in video",
    "consistency_anchors": ["features to maintain across shots"],
    "negative_space": "string - where to leave room for motion"
  }
}
```

---

## Veo 3.1 Input Compatibility

| Parameter | Veo 3.1 Requirement | Recommendation |
|-----------|---------------------|----------------|
| Resolution | 720p or 1080p | Match target video resolution |
| Aspect Ratio | 16:9 or 9:16 | Match target video aspect ratio |
| Format | PNG or JPEG | PNG for transparency |
| Composition | Leave motion space | Don't center if movement planned |

---

## Minimal Schema (Quick Use)

For simpler requests:

```json
{
  "subject": {
    "identity": "string - main subject description",
    "pose": "string - position/gesture",
    "expression": "string - emotional state"
  },
  "environment": {
    "location": "string - setting",
    "lighting": "string - light description"
  },
  "style": {
    "medium": "photorealistic | anime | illustration",
    "mood": "string - atmosphere"
  },
  "technical": {
    "aspect_ratio": "16:9 | 9:16 | 1:1",
    "framing": "close_up | medium | full_body | wide"
  }
}
```

---

## Advanced Hacks

### Logic Gate (Counting/Positioning)

Force the reasoning engine to solve logical constraints:

```json
{
  "logic_gate": {
    "task": "Object Generation Challenge",
    "condition": "Generate exactly 5 objects that start with the letter 'S'",
    "constraints": ["Each object must be distinct", "All must be clearly visible"],
    "verification": "Ensure exactly 5 items are visible, verify spelling of labels"
  },
  "scene": "messy office desk top-down view"
}
```

### Split View Hack

Create side-by-side comparisons in one image:

```json
{
  "composition_hack": "Hard Split Screen",
  "layout": {
    "type": "horizontal_split | vertical_split",
    "ratio": "50:50",
    "divider": {
      "style": "solid white line | gradient | none",
      "thickness": "5px"
    }
  },
  "left_panel": {
    "content": "string - left side description",
    "style": "string - left side style",
    "background": "string"
  },
  "right_panel": {
    "content": "string - right side description",
    "style": "string - right side style",
    "background": "string"
  },
  "instruction": "Do not blend the two sides. Treat them as separate viewports."
}
```

### Search Grounding Injection

Trigger real-world knowledge retrieval:

```json
{
  "grounding_trigger": {
    "tool": "google_search",
    "query": "Tesla Cybertruck interior dashboard layout 2025",
    "intent": "visualize the exact UI based on latest data"
  },
  "prompt": "First-person view from the driver's seat of a Cybertruck",
  "details": {
    "screen_content": "Navigation map of downtown San Francisco based on real geography",
    "accuracy": "Match the exact design found in search results"
  }
}
```

---

## Schema Selection Guide

| Use Case | Recommended Schema |
|----------|-------------------|
| Character portrait | Full schema with identity + attire |
| Product photography | Full schema with photography + lighting |
| Scene/environment | Full schema with environment + spatial_structure |
| UI mockup | Minimal schema + layout constraints |
| Quick concept | Minimal schema |
| Multi-shot consistency | Full schema with veo_optimization |
| Before/after comparison | Split View hack |
| Exact counting/positioning | Logic Gate hack |
| Real-world accuracy | Grounding Injection hack |
