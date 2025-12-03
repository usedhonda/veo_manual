# Audio Instructions for Veo 3.1

## Overview

Veo 3.1 supports native audio generation including:
- **Dialogue**: Character speech with natural voice
- **Sound Effects (SFX)**: Environmental and action sounds
- **Ambience**: Background atmospheric audio
- **Music**: Background score and soundtrack

---

## Audio Instruction Format

### Standard Format Structure

```json
"audio": {
  "dialogue": "Character says: \"Exact spoken line here.\"",
  "sfx": "SFX: specific sound effect description",
  "ambience": "Ambience: environmental background sounds",
  "music": "Music: genre, mood, instruments",
  "voice_style": "tone, accent, emotion descriptors"
}
```

### Critical Rules

1. **Use quotation marks** for dialogue: `"Character says: \"Line\""`
2. **Prefix labels** are important: `SFX:`, `Ambience:`, `Music:`
3. **Be specific**: "footsteps on gravel" not just "footsteps"
4. **One voice per clip**: Multiple speakers can confuse generation
5. **Match audio to action**: Sync sound with what's happening

---

## Dialogue Instructions

### Format
```
"dialogue": "[Character Name] says: \"Exact dialogue here.\""
```

### Voice Style Modifiers

| Modifier | Effect |
|----------|--------|
| `whispered` | Quiet, breathy voice |
| `shouted` | Loud, projected voice |
| `monotone` | Flat, emotionless delivery |
| `excited` | Energetic, enthusiastic |
| `sad` | Melancholic, heavy tone |
| `angry` | Harsh, aggressive tone |
| `sarcastic` | Dry, ironic delivery |
| `nervous` | Shaky, uncertain voice |
| `confident` | Strong, assured delivery |
| `seductive` | Low, alluring tone |

### Accent/Voice Type

| Type | Description |
|------|-------------|
| `deep male voice` | Low, resonant |
| `high female voice` | Light, bright |
| `child voice` | Young, innocent |
| `elderly voice` | Aged, weathered |
| `robotic voice` | Mechanical, synthesized |
| `narrator voice` | Clear, authoritative |
| `British accent` | UK English |
| `American accent` | US English |
| `Southern drawl` | American South |
| `New York accent` | NYC dialect |

### Dialogue Examples

```json
// Basic dialogue
"dialogue": "Sarah says: \"I never thought I'd see this day.\""

// With emotion
"dialogue": "Detective Cole says angrily: \"Tell me where she is!\""

// Whispered
"dialogue": "The spy whispers: \"They're watching us.\""

// Narration
"dialogue": "Narrator (deep male voice): \"In a world changed forever...\""

// Character voice
"dialogue": "Young girl says cheerfully: \"Look what I found!\""
```

---

## Sound Effects (SFX)

### Format
```
"sfx": "SFX: [specific sound description]"
```

### Common SFX Categories

#### Human Sounds
| Sound | Keywords |
|-------|----------|
| Footsteps | `footsteps on [surface]`, `running footsteps`, `heel clicks` |
| Breathing | `heavy breathing`, `gasping`, `sighing` |
| Clothing | `fabric rustling`, `zipper sound`, `buttons clicking` |
| Actions | `clapping`, `snapping fingers`, `knocking` |

#### Environment Sounds
| Sound | Keywords |
|-------|----------|
| Doors | `door opening`, `door slamming`, `creaking door` |
| Glass | `glass breaking`, `glass clinking`, `window shatter` |
| Metal | `metal clanging`, `sword clash`, `metallic scrape` |
| Wood | `wood creaking`, `branches snapping`, `wooden door knock` |
| Water | `splash`, `dripping water`, `waves crashing` |

#### Vehicle Sounds
| Sound | Keywords |
|-------|----------|
| Cars | `engine revving`, `car door closing`, `tires screeching` |
| Motorcycles | `motorcycle engine`, `exhaust rumble` |
| Aircraft | `jet engine`, `helicopter blades`, `propeller plane` |

#### Technology Sounds
| Sound | Keywords |
|-------|----------|
| Electronics | `phone buzzing`, `computer beep`, `notification chime` |
| Sci-fi | `laser blast`, `energy hum`, `teleport whoosh` |
| Mechanical | `gears turning`, `hydraulic hiss`, `servo motor` |

#### Nature Sounds
| Sound | Keywords |
|-------|----------|
| Animals | `dog barking`, `bird chirping`, `wolf howling` |
| Weather | `thunder rumble`, `rain on window`, `wind howling` |
| Natural | `leaves rustling`, `fire crackling`, `water stream` |

### SFX Examples

```json
// Action scene
"sfx": "SFX: sword being drawn from sheath, metal ringing"

// Horror
"sfx": "SFX: creaking floorboards, distant whisper"

// Sci-fi
"sfx": "SFX: spaceship engine powering up, control panel beeps"

// Urban
"sfx": "SFX: car horn honking, traffic noise, pedestrian chatter"

// Multiple sounds
"sfx": "SFX: glass shattering, followed by alarm blaring"
```

---

## Ambience

### Format
```
"ambience": "Ambience: [environmental background description]"
```

### Location-Based Ambience

| Location | Ambience Keywords |
|----------|-------------------|
| City | `traffic hum`, `distant sirens`, `pedestrian murmur`, `urban buzz` |
| Forest | `birds singing`, `leaves rustling`, `insects chirping`, `wind through trees` |
| Ocean | `waves crashing`, `seagulls calling`, `wind`, `distant boats` |
| Office | `keyboard typing`, `air conditioning hum`, `muffled conversation` |
| Restaurant | `dishes clinking`, `conversation murmur`, `background music` |
| Hospital | `beeping monitors`, `PA announcements`, `footsteps on linoleum` |
| Factory | `machinery hum`, `metal clanking`, `industrial noise` |
| Rain | `rain pattering`, `thunder rolling`, `water dripping` |
| Night | `crickets`, `owl hooting`, `distant traffic` |
| Crowd | `crowd murmur`, `cheering`, `applause` |

### Ambience Examples

```json
// Outdoor nature
"ambience": "Ambience: peaceful forest, birds singing, gentle stream flowing"

// Urban night
"ambience": "Ambience: city at night, distant traffic, occasional siren, neon sign buzz"

// Interior quiet
"ambience": "Ambience: quiet library, pages turning, soft footsteps, clock ticking"

// Weather
"ambience": "Ambience: heavy rainstorm, thunder in distance, rain on windows"

// Busy location
"ambience": "Ambience: crowded market, vendors calling, people haggling, music playing"
```

---

## Music

### Format
```
"music": "Music: [genre], [mood], [instruments/style]"
```

### To Prevent Music
```json
"music": "NO music"
"music": "NO music, ambient sounds only"
"music": "silence, no background music"
```

### Music Genre Keywords

| Genre | Description |
|-------|-------------|
| `orchestral` | Full orchestra, cinematic |
| `electronic` | Synthesizers, digital |
| `ambient` | Atmospheric, textural |
| `jazz` | Swing, improvisation |
| `rock` | Guitar-driven, energetic |
| `pop` | Catchy, contemporary |
| `hip hop` | Beats, rhythmic |
| `classical` | Traditional orchestral |
| `folk` | Acoustic, traditional |
| `EDM` | Dance, electronic beats |
| `lo-fi` | Relaxed, warm distortion |
| `synthwave` | 80s electronic, retro |

### Music Mood Keywords

| Mood | Effect |
|------|--------|
| `tense` | Building anxiety |
| `triumphant` | Victorious, epic |
| `melancholic` | Sad, reflective |
| `uplifting` | Positive, inspiring |
| `mysterious` | Intriguing, unknown |
| `romantic` | Emotional, loving |
| `action` | Fast, driving |
| `peaceful` | Calm, serene |
| `dark` | Ominous, foreboding |
| `playful` | Fun, lighthearted |
| `dramatic` | Intense, emotional |
| `suspenseful` | Edge-of-seat tension |

### Instrument Keywords

| Instrument | Sound Character |
|------------|-----------------|
| `piano` | Emotional, versatile |
| `strings` | Dramatic, sweeping |
| `brass` | Powerful, heroic |
| `guitar` | Warm, intimate |
| `synthesizer` | Modern, electronic |
| `drums` | Rhythmic, driving |
| `choir` | Epic, spiritual |
| `woodwinds` | Light, whimsical |
| `bass` | Deep, grounding |

### Music Examples

```json
// Cinematic epic
"music": "Music: orchestral, triumphant, brass and strings building"

// Horror
"music": "Music: ambient, tense, low drone with sudden stingers"

// Romance
"music": "Music: soft piano, romantic, melancholic undertones"

// Action
"music": "Music: electronic, driving beat, intense and fast"

// Comedy
"music": "Music: jazz, playful, light piano and upright bass"

// Sci-fi
"music": "Music: synthwave, mysterious, retro electronic atmosphere"

// No music
"music": "NO music, focus on dialogue and ambient sounds"
```

---

## Complete Audio Examples

### Dialogue Scene
```json
"audio": {
  "dialogue": "Detective Miller says firmly: \"I know what you did last summer.\"",
  "sfx": "SFX: coffee cup placed on desk, chair creaking",
  "ambience": "Ambience: police station, phones ringing, typewriter clicks",
  "music": "NO music"
}
```

### Action Sequence
```json
"audio": {
  "dialogue": "",
  "sfx": "SFX: running footsteps, gunshots, glass shattering, car engine roaring",
  "ambience": "Ambience: urban alley, distant traffic, echo of enclosed space",
  "music": "Music: electronic, intense, driving beat with bass drops"
}
```

### Romantic Scene
```json
"audio": {
  "dialogue": "She whispers softly: \"I've waited so long for this moment.\"",
  "sfx": "SFX: gentle wind, leaves rustling",
  "ambience": "Ambience: quiet garden, evening birds, distant fountain",
  "music": "Music: soft piano, romantic, gentle strings"
}
```

### Horror Scene
```json
"audio": {
  "dialogue": "Child's voice (echoing): \"Come play with me...\"",
  "sfx": "SFX: creaking floorboard, door slowly opening",
  "ambience": "Ambience: old house, wind outside, distant thunder",
  "music": "Music: ambient drone, tense, occasional dissonant strings"
}
```

### Product Commercial
```json
"audio": {
  "dialogue": "Narrator (confident male voice): \"Introducing the future of sound.\"",
  "sfx": "SFX: product click, satisfying snap, power-on chime",
  "ambience": "Ambience: minimal, clean studio silence",
  "music": "Music: modern electronic, premium, subtle pulse"
}
```

---

## Audio Best Practices

1. **Sync with action**: Audio should match what's happening on screen
2. **Layer appropriately**: Don't overcrowd with too many sounds
3. **Prioritize clarity**: Dialogue should be clearly audible over other audio
4. **Use silence strategically**: Sometimes no music is more powerful
5. **Match tone**: Horror scenes need horror audio, comedy needs light audio
6. **Be specific**: "Footsteps on wet cobblestone" > "footsteps"
7. **Consider timing**: Mention if sounds occur at specific moments
