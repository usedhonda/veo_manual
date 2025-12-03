# Grok Imagine Audio Instructions

## Overview

Aurora engine integrates native audio generation synchronized with video. Audio can include BGM, SFX, dialogue, and even singing. Proper audio instructions significantly enhance output quality.

---

## Audio Instruction Format

Use brackets or explicit labels for best recognition:

```
[Audio: description]
Audio: description
SFX: specific sound
Music: genre and mood
Dialogue: "spoken words"
```

---

## Sound Effects (SFX)

| Category | Examples |
|----------|----------|
| **Impact** | glass shattering, metal clang, punch, explosion |
| **Movement** | footsteps, tire screech, whoosh, rustling |
| **Mechanical** | engine roar, clock ticking, door creak, keyboard typing |
| **Nature** | rain, thunder, wind, bird chirping, waves |
| **Ambient** | crowd murmur, traffic, machinery hum, forest sounds |

### SFX Sync Technique

Match visual and audio triggers with the same word:

```
Visual: Glass shatters against the wall.
Audio: Loud glass shattering sound.
```

The model recognizes "shatter" in both and synchronizes timing.

---

## Music/BGM

| Descriptor | Effect |
|------------|--------|
| **Epic orchestral** | Grand, dramatic swells |
| **Soft ambient synth** | Electronic, atmospheric |
| **Upbeat electronic** | Energetic, modern |
| **Melancholic piano** | Sad, reflective |
| **Jazz lounge** | Smooth, sophisticated |
| **Heavy metal** | Aggressive, intense |
| **Lo-fi beats** | Chill, nostalgic |

### Music Specification Example

```
Music: Tense orchestral build-up with low brass, transitioning to triumphant strings
```

---

## Dialogue

Include exact spoken words in quotes:

```
Dialogue: "We need to leave now!"
Character says: "I've been waiting for you."
Voiceover: "In a world where..."
```

### Dialogue Tips

- Keep lines short (under 10 words works best)
- Specify speaker emotion: "whispers nervously", "shouts angrily"
- Aurora attempts lip-sync with character faces

---

## Suppressing Unwanted Audio

Since negative prompts don't work, use these techniques:

### To Remove Music

❌ "No music" (often adds music)
✅ "Silence, ambient sounds only"
✅ "[Gym sounds only]" (specific environment)
✅ "Muted atmosphere, environmental audio only"

### To Remove All Audio

✅ "Complete silence"
✅ "No audio, visual only"

---

## Audio Mood Combinations

| Visual Mood | Audio Pairing |
|-------------|---------------|
| Action | Engine roars, impacts, tense percussion |
| Romance | Soft piano, wind, gentle breathing |
| Horror | Low drone, distant footsteps, sudden silence |
| Comedy | Upbeat, cartoon SFX, comedic timing |
| Epic | Orchestral swells, choir, bass drums |
| Mystery | Ambient tension, creaking, whispers |

---

## Practical Examples

### Car Chase
```
Audio: V8 engine roaring at high RPM, tire screeching on asphalt, wind rushing, police sirens in distance
```

### Product Commercial
```
Audio: Satisfying mechanical click, soft luxury synth swell, subtle wind chimes
```

### Horror Scene
```
Audio: Electrical buzzing, light bulb shattering, distant heavy footsteps, low frequency dread drone, sudden silence
```

### Character Dialogue
```
Audio: Character says "I never thought I'd see you again" with trembling voice, soft rain in background
```

### Nature Documentary
```
Audio: Birds chirping, gentle stream flowing, wind through leaves, narrator voiceover: "In the heart of the Amazon..."
```

---

## Audio Sync Issues

If audio doesn't match visuals:

1. **Use matching trigger words** in visual and audio descriptions
2. **Simplify** - fewer audio elements = better sync
3. **Shorter duration** - 5-6 second clips sync better
4. **Explicit timing** - "At the moment of impact, loud crash"

---

## Advanced: Singing

Aurora can generate singing voices:

```
Audio: Female voice singing soft melody, ethereal and haunting
Music: Acoustic guitar accompaniment with gentle singing
```

Best results with:
- Simple melodies
- Clear emotion descriptors
- Matching visual context (performer, concert, etc.)
