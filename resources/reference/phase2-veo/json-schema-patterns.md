# Veo 3.1 JSON Schema Patterns

## Overview

This document catalogs different JSON prompt structures discovered from the community.
Each pattern has its strengths for specific use cases.

---

## The 3 Primary Schema Patterns

### 1. Meta-Director Schema (Nested Structure)

**Best for**: Cinematic scenes, high style adherence, complex lighting

**Philosophy**: Break prompt into semantic categories that force model attention to each element.

```json
{
  "project_name": "Scene_Title",
  "visual_style": {
    "medium": "2D Animation | 3D | Live Action",
    "aesthetic": "High-budget anime, production I.G style",
    "art_direction": {
      "line_work": "Sharp, thin outlines",
      "color_palette": "Neon purples, deep blacks",
      "effects": "Speed lines, particle effects"
    }
  },
  "scene": {
    "environment": "Location description",
    "weather": "Weather conditions",
    "elements": ["Background element 1", "Element 2"]
  },
  "subject": {
    "character": "Character description",
    "appearance": "Visual details",
    "action": "What they're doing"
  },
  "camera": {
    "shot_type": "Close-up | Wide | Medium",
    "movement": "Dolly | Pan | Static",
    "angle": "Low | High | Eye level"
  },
  "technical": {
    "aspect_ratio": "16:9",
    "fps": 24,
    "seed": 12345
  }
}
```

**When to use**:
- Anime/manga style videos
- Scenes requiring specific art direction
- Complex multi-element compositions

---

### 2. Timeline/Sequence Schema

**Best for**: Commercials, music videos, choreographed action

**Philosophy**: Define exactly what happens at each time marker to prevent hallucination.

```json
{
  "type": "Commercial",
  "product": "Product_Name",
  "aspect_ratio": "9:16",
  "duration": "8s",
  "timeline": [
    {
      "time": "0s-2s",
      "action": "Opening shot description",
      "camera": "Camera movement",
      "lighting": "Lighting setup",
      "sound_fx": "Audio for this segment"
    },
    {
      "time": "2s-5s",
      "action": "Middle action",
      "camera": "Camera movement",
      "sound_fx": "Audio"
    },
    {
      "time": "5s-8s",
      "action": "Closing shot",
      "camera": "Final camera move",
      "lighting": "Final lighting"
    }
  ],
  "negative_prompt": "things to avoid",
  "brand_guidelines": {
    "primary_color": "#000000",
    "secondary_color": "#4B0082"
  }
}
```

**When to use**:
- Product commercials with specific cuts
- Music videos with beat-synced visuals
- Any video requiring precise timing control

---

### 3. Flat API Schema

**Best for**: Programmatic generation, API integration

**Philosophy**: Single prompt string with separate parameters, matching actual API structure.

```json
{
  "model": "veo-3.1-generate-001",
  "prompt": "Cinematic 8k footage. SCENE: Description. SUBJECT: Details. LIGHTING: Setup. CAMERA: Movement. ATMOSPHERE: Mood.",
  "negative_prompt": "things to avoid",
  "aspect_ratio": "21:9",
  "resolution": "1080p",
  "duration_seconds": 8,
  "frame_rate": 24,
  "seed": 123456789,
  "guidance_scale": 7.5,
  "generate_audio": true
}
```

**When to use**:
- Direct API calls
- Batch processing systems
- When you need maximum compatibility

---

## Extended Patterns (Community-Discovered)

### 4. Audio-Reactive Schema (Music Videos)

**Unique features**: BPM sync, energy curves, beat-matched cuts

```json
{
  "genre": "Synthwave / Retrowave",
  "track_title": "Track_Name",
  "audio_sync": {
    "bpm": 128,
    "rhythm_match": "Cut on beat",
    "energy_curve": "Build-up to drop"
  },
  "visuals": {
    "setting": "Environment",
    "objects": ["Object 1", "Object 2"],
    "color_grading": "VHS glitch aesthetic"
  },
  "sequence": {
    "intro": "Opening visual description",
    "build_up": "Tension building visuals",
    "drop": "Peak moment visuals"
  },
  "camera_work": {
    "style": "FPV Drone style",
    "motion": "Fast, fluid",
    "shake": "Synced to bass kicks"
  },
  "generate_audio": true
}
```

---

### 5. Noir/Stylized Anime Schema

**Source**: @_YoungTurbo_ on X

**Unique features**: High contrast focus, noir aesthetics, minimal color

```json
{
  "title": "Scene_Title",
  "duration_seconds": 8,
  "style": "Hand-drawn anime, black and white, high-contrast noir",
  "format": "16:9",
  "camera": "Camera movement description",
  "frame_rate": 24,
  "scene_description": "Full scene description",
  "characters": [
    {
      "name": "Character Name",
      "appearance": "Visual description",
      "action": "What they do"
    }
  ],
  "ui_elements": [],
  "lighting": {
    "type": "Noir lighting style",
    "shadows": "Deep, dramatic",
    "highlights": "Sharp contrast"
  },
  "music_visual_sync": {
    "mood": "Mood description",
    "tempo": "Slow | Medium | Fast"
  },
  "voiceover": {
    "character": "Speaker name",
    "dialogue": "What they say",
    "tone": "How they say it"
  },
  "tags": ["noir", "anime", "dramatic"]
}
```

---

### 6. Action/Visuals Split Schema

**Source**: @bmxai13 on X

**Unique features**: Clear visual/audio separation, motion emphasis

```json
{
  "visuals": {
    "style": "Visual style description",
    "subject": {
      "type": "Character | Object",
      "description": "Detailed subject info",
      "state": "Current state"
    },
    "environment": {
      "setting": "Location",
      "details": ["Detail 1", "Detail 2"]
    },
    "motion": {
      "primary": "Main movement",
      "secondary": "Supporting movement",
      "camera": "Camera motion"
    },
    "lighting": {
      "type": "Lighting setup",
      "mood": "Atmosphere"
    }
  },
  "audio": {
    "soundtrack": {
      "genre": "Music genre",
      "tempo": "BPM or descriptive",
      "mood": "Audio mood"
    },
    "effects": ["SFX 1", "SFX 2"],
    "voice": {
      "dialogue": "Speech if any",
      "character": "Speaker"
    }
  }
}
```

---

### 7. Cinematography-First Schema

**Source**: @CharaspowerAI on X

**Unique features**: Professional film terminology, lens specifications

```json
{
  "shot": {
    "composition": "Rule of thirds, golden ratio, etc.",
    "lens": "24mm anamorphic",
    "frame_rate": "60fps",
    "camera_movement": "Technical movement description"
  },
  "subject": {
    "primary": "Main subject",
    "secondary": "Supporting elements",
    "action": "Subject movement"
  },
  "scene": {
    "location": "Setting",
    "time": "Time of day",
    "weather": "Conditions"
  },
  "visual_details": {
    "color_grade": "LUT or color style",
    "contrast": "High | Medium | Low",
    "texture": "Film grain, clean, etc."
  },
  "cinematography": {
    "depth_of_field": "Shallow | Deep",
    "focus": "What's in focus",
    "bokeh": "Background blur style"
  },
  "audio": {
    "ambience": "Environmental audio",
    "music": "Score description",
    "dialogue": "Speech with quotes"
  },
  "dialogue": {
    "speaker": "Character name",
    "line": "\"Exact dialogue here\"",
    "delivery": "How it's said"
  }
}
```

---

## Schema Selection Guide

| Use Case | Recommended Schema | Reason |
|----------|-------------------|--------|
| Anime scene | Meta-Director | Art direction control |
| Product commercial | Timeline | Precise timing control |
| API integration | Flat API | Direct compatibility |
| Music video | Audio-Reactive | Beat synchronization |
| Film noir style | Noir Anime | Contrast focus |
| Character action | Visuals Split | Motion emphasis |
| Cinematic quality | Cinematography-First | Professional terminology |

---

## Combining Schemas

You can combine elements from different schemas based on need:

```json
{
  // From Meta-Director
  "visual_style": {
    "medium": "cinematic anime",
    "art_direction": {...}
  },

  // From Timeline
  "timeline": [
    {"time": "0s-3s", ...},
    {"time": "3s-8s", ...}
  ],

  // From Audio-Reactive
  "audio_sync": {
    "bpm": 120,
    "rhythm_match": "cut on beat"
  },

  // Veo 3.1 specific
  "ingredients": [...],
  "generate_audio": true
}
```

---

## Best Practices

1. **Be consistent**: Pick one primary schema per project
2. **Use quotes for dialogue**: `"Character says: \"Hello!\""` enables lip-sync
3. **Specific > vague**: "24mm anamorphic" > "wide lens"
4. **Timeline for commercials**: Always use timeline schema for ads
5. **Test and iterate**: Schemas may need adjustment per scene type
