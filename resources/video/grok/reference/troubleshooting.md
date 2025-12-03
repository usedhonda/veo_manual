# Grok Imagine Troubleshooting Guide

## Overview

Common issues and proven solutions for Grok Imagine video generation.

---

## Generation Stuck at 0%

### Symptoms
- Progress bar shows 0% indefinitely
- Generation times out or fails silently
- No error message provided

### Causes & Solutions

#### 1. Server Overload
**Solution**: Wait 5-10 minutes and retry. Peak hours (US evening) have longer queues.

#### 2. Silent Moderation Block
**Solution**: Review prompt for potentially flagged content. Even innocent phrases can trigger:
- Anatomical terms
- Violence-adjacent words
- Celebrity names

**Test**: Try a simple prompt like "Blue sky with clouds" to verify account isn't throttled.

#### 3. Sliding Window Rate Limit
**Important**: Free/basic limits are 24-hour SLIDING windows, not daily resets.
- First generation at 2pm → limit resets at 2pm next day
- NOT at midnight

**Solution**: Wait for oldest generation to "age out" of the window.

#### 4. App Cache Issues (Mobile)
**Solution for iOS/Android**:
1. Clear app cache
2. Force quit and restart app
3. If persistent, reinstall app

---

## Face/Body Morphing

### Symptoms
- Character's face changes mid-video
- Extra limbs appear briefly
- Body proportions shift

### Prevention

#### Use Image-to-Video Mode
Always anchor with a reference image for characters that must stay consistent.

#### Add Stability Keywords
```
"Detailed anatomy, perfect hands, symmetrical face,
consistent proportions, stable identity"
```

#### Reduce Motion Intensity
```
❌ "Running frantically while fighting"
✅ "Walking slowly, subtle movements"
```

Slower motion = fewer frames for model to "drift"

#### Shorter Clips
- 5-6 seconds: Most stable
- 10 seconds: Moderate risk
- 15 seconds: Highest morphing risk

### Post-Fix Solutions
- FaceFusion for face consistency
- Frame interpolation to smooth transitions
- Manual frame editing for severe cases

---

## Audio Desynchronization

### Symptoms
- Sound effects don't match visual impacts
- Dialogue doesn't sync with lip movement
- Music cues are mistimed

### Solutions

#### Use Trigger Word Matching
Match the same word in visual and audio descriptions:

```
Visual: "The balloon pops suddenly"
Audio: "Loud popping sound"
```

The model aligns on shared token "pop".

#### Explicit Timing Cues
```
"At the exact moment of impact, loud crash sound"
"Simultaneously with the door opening, creaking noise"
```

#### Simplify Audio Requests
```
❌ "Orchestra swells while footsteps echo and wind howls and dialogue plays"
✅ "Footsteps on gravel, light wind"
```

Fewer audio elements = better sync accuracy.

#### Shorter Duration
5-6 second clips maintain sync better than 15-second clips.

---

## Text Rendering Issues

### Symptoms
- Text on signs is gibberish
- Letters are distorted or merged
- Numbers are incorrect

### Current Limitations (Dec 2025)
Aurora is improving but still imperfect at text. Expect:
- 1-3 word signs: ~70% accuracy
- 4+ words: Significant degradation
- Small text: Usually fails

### Best Practices

#### Quote the Text
```
✅ A neon sign that says "OPEN"
❌ A neon sign saying open
```

#### Keep It Short
```
✅ "EXIT"
✅ "CAFE"
❌ "Emergency Exit - Push Bar to Open"
```

#### Use Familiar Formats
Common signs work better than unique text:
- "STOP", "EXIT", "OPEN", "CLOSED"
- Single numbers (speed limits, countdowns)

#### Post-Production Recommendation
For important text, add in post-production:
1. Generate video with placeholder or no text
2. Track motion in editing software
3. Overlay clean text graphics

---

## "I Can't Generate Images" Hallucination

### Symptoms
Grok responds: "I'm a text-only model and cannot generate images"
(Despite having image generation capability)

### Causes
- Model hallucination
- Temporary system prompt inconsistency
- Session state confusion

### Solutions

#### Force Retry
```
"You do have image generation capabilities.
You have generated images for me before.
Please try again."
```

#### Start New Session
Often resolves immediately in fresh chat.

#### Explicit Capability Reminder
```
"Using your Grok Imagine video generation feature, create..."
```

---

## Color/Quality Degradation

### Symptoms
- Colors become oversaturated across generations
- Image becomes increasingly blurry
- "Deep-fried" appearance

### Causes
Compression artifacts accumulate when using Last Frame Method.

### Solutions

#### AI Upscaling Between Cycles
Use between each generation cycle:
- Topaz Video AI
- Magnific AI
- Real-ESRGAN

#### Limit Chain Length
Maximum 3-4 generations before quality reset.

#### High-Quality Frame Extraction
- Use PNG format (lossless)
- Extract at native resolution
- Avoid JPEG for intermediate frames

---

## Unwanted Music/Sound

### Symptoms
- BGM appears despite not requesting it
- Wrong genre of music
- Sound effects when silence requested

### Solutions

#### Don't Use Negatives
```
❌ "No music"          → Often ADDS music
❌ "Without soundtrack" → May add soundtrack
```

#### Use Positive Alternatives
```
✅ "Silence, ambient sounds only"
✅ "Environmental audio only"
✅ "[Gym sounds only]" (specific environment)
✅ "Muted atmosphere, natural sounds"
✅ "Complete silence, no audio"
```

#### Specify Environment Sounds
Being specific about WHAT sounds you want prevents music injection:
```
"Audio: Only footsteps on gravel, distant traffic, wind"
```

---

## Spicy Mode Not Working

### Symptoms
- Mode reverts to "normal"
- Content still blocked despite spicy selection
- No difference from normal mode

### Causes & Solutions

#### Age Verification Required
Account must be age-verified on X (Twitter) for API access to spicy mode.

#### I2V Restriction
**Important**: Spicy mode is NOT available for Image-to-Video to prevent deepfake abuse. Only works with Text-to-Video.

#### Content Still Prohibited
Spicy mode relaxes but doesn't remove all limits:
- Explicit acts: Always blocked
- Real people in compromising situations: Blocked
- Illegal content: Blocked

See `spicy-mode.md` for detailed boundaries.

---

## Quick Reference: Error → Solution

| Error | Quick Fix |
|-------|-----------|
| 0% stuck | Wait + retry, check for moderation trigger |
| Face morphing | Use I2V, add stability keywords, shorten duration |
| Audio desync | Match trigger words, simplify audio, shorter clips |
| Bad text | Keep to 1-3 words, quote text, add in post |
| "Can't generate" | New session, explicit capability reminder |
| Quality loss | AI upscale between cycles, use PNG |
| Unwanted music | "Ambient sounds only", specify environment |
