# Transition Keywords for Veo 3.1

## Overview

Transitions in Veo 3.1 can be applied within clips or designed at clip boundaries for multi-shot sequences.

---

## Reliability Rating System
- ✅ **High**: Consistently works as expected
- ⚠️ **Medium**: Works but may need refinement
- ❌ **Low**: Unpredictable, avoid or use carefully

---

## In-Clip Transitions

These transitions occur within a single 8-second clip.

### Fade Transitions

| Keyword | Description | Reliability | Best For |
|---------|-------------|-------------|----------|
| `fade in from black` | Clip starts dark, fades to scene | ✅ High | Opening shots |
| `fade to black` | Scene fades to darkness at end | ✅ High | Ending shots |
| `fade in from white` | Clip starts white, fades to scene | ✅ High | Dream sequences |
| `fade to white` | Scene fades to white at end | ✅ High | Transcendence, memory |

### Motion-Based Transitions

| Keyword | Description | Reliability | Best For |
|---------|-------------|-------------|----------|
| `whip pan transition` | Fast pan creates blur | ✅ High | Energy, time skip |
| `zoom transition` | Rapid zoom in/out | ✅ High | Focus shift |
| `push through transition` | Camera moves through object | ⚠️ Medium | Reveal, dream |
| `pull back reveal` | Camera pulls back to show more | ✅ High | Scale reveal |

### Visual Effect Transitions

| Keyword | Description | Reliability | Best For |
|---------|-------------|-------------|----------|
| `glitch transition` | Digital glitch effect | ✅ High | Tech, cyberpunk |
| `flash transition` | Bright flash between scenes | ⚠️ Medium | Memory, impact |
| `ripple transition` | Water ripple effect | ⚠️ Medium | Dream, memory |
| `particle dissolve` | Dissolves into particles | ⚠️ Medium | Magic, sci-fi |

---

## Transition Timing Keywords

| Keyword | Effect | Usage |
|---------|--------|-------|
| `at the start` | Transition in first 1-2 seconds | Fade in, reveal |
| `at the end` | Transition in last 1-2 seconds | Fade out, setup for next |
| `midpoint transition` | Transition at 4 second mark | Scene change within clip |
| `gradual throughout` | Slow change across full clip | Time passage |

---

## Scene Change Keywords

For clips that contain a scene change:

| Keyword | Description | Reliability |
|---------|-------------|-------------|
| `scene shifts to` | Smooth transition to new scene | ⚠️ Medium |
| `transforms into` | Morphs to different environment | ⚠️ Medium |
| `match cut to` | Similar composition, new scene | ⚠️ Medium |
| `hard cut to` | Abrupt change to new scene | ✅ High |

---

## Multi-Shot Sequence Planning

When planning multiple clips for editing:

### Opening Shot Markers

```json
{
  "shot_position": "opening",
  "transition": {
    "in": "fade in from black",
    "in_duration": "2 seconds",
    "out": "none (hard cut to next)"
  }
}
```

### Middle Shot Markers

```json
{
  "shot_position": "middle",
  "transition": {
    "in": "match previous action",
    "out": "match next action"
  }
}
```

### Closing Shot Markers

```json
{
  "shot_position": "closing",
  "transition": {
    "in": "continue from previous",
    "out": "fade to black",
    "out_duration": "2 seconds"
  }
}
```

---

## Match Cut Patterns

For seamless multi-shot editing, design shots with matching elements:

### Action Match

```
Shot A: Character throws ball (ends mid-throw)
Shot B: Ball in flight (starts at same trajectory)
```

### Movement Match

```
Shot A: Camera panning left (ends at specific angle)
Shot B: Continues pan from same angle
```

### Position Match

```
Shot A: Subject on left of frame
Shot B: Same subject position, different angle
```

### Shape Match

```
Shot A: Close-up of circular object (wheel)
Shot B: Wide shot with circular element (sun, moon)
```

---

## Transition Combinations

### Effective Patterns

```
"fade in from black, static shot, hard cut at end" ✅
"whip pan right at end" + next clip "whip pan right at start" ✅
"zoom in at end" + next clip "zoomed in at start" ✅
"fade to black at end" + next clip "fade in from black" ✅
```

### Avoid These

```
"fade to black AND whip pan" ❌ (conflicting)
"multiple transitions in one clip" ❌ (confusing)
"slow fade AND hard cut" ❌ (contradictory)
```

---

## Audio Transition Considerations

### Sound Bridges

```json
"audio": {
  "bridge_out": "sound continues into silence for edit",
  "bridge_in": "sound begins before visual appears"
}
```

### J-Cut Setup (audio before video)

```
"audio": "Dialogue begins: 'We need to talk...' as scene fades in"
```

### L-Cut Setup (audio after video)

```
"audio": "Dialogue 'I understand' continues as scene begins to fade"
```

---

## Transition Templates

### Dramatic Opening

```json
{
  "transition_in": {
    "type": "fade in from black",
    "duration": "slow, 2-3 seconds",
    "audio": "ambient sounds fade in with visual"
  },
  "shot": {
    "type": "wide establishing",
    "movement": "subtle drift after fade complete"
  }
}
```

### Energy Transition

```json
{
  "transition_out": {
    "type": "whip pan right",
    "timing": "last 1 second",
    "blur": "motion blur at peak speed"
  },
  "next_clip_instruction": "start with whip pan completing from left"
}
```

### Dream Sequence Entry

```json
{
  "transition_in": {
    "type": "fade in from white",
    "duration": "gradual, 2 seconds",
    "effect": "soft focus sharpening"
  },
  "style": {
    "color_grade": "slightly desaturated, dreamy",
    "quality": "soft, ethereal"
  }
}
```

### Scene End/Chapter Close

```json
{
  "transition_out": {
    "type": "slow fade to black",
    "duration": "3 seconds",
    "audio": "music and ambience fade simultaneously"
  },
  "shot": {
    "movement": "gradually slowing or static"
  }
}
```

### Glitch Cut (Tech/Cyberpunk)

```json
{
  "transition_out": {
    "type": "glitch transition",
    "timing": "sudden at end",
    "effect": "digital artifacts, color shift"
  },
  "audio": {
    "sfx": "SFX: digital glitch, static burst"
  },
  "style": {
    "aesthetic": "cyberpunk, tech malfunction"
  }
}
```

---

## Best Practices

1. **One transition per cut point**: Don't stack multiple transitions
2. **Match energy**: Fast scenes = fast transitions, slow scenes = slow fades
3. **Plan the sequence**: Know your in/out transitions before generating
4. **Audio matters**: Sound bridges smooth visual cuts
5. **Test with fast model**: Iterate transitions on `veo-3.1-fast`
6. **Simple is safer**: Fades and hard cuts are more reliable than effects
