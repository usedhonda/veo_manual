# Veo 3 vs Veo 3.1: JSON Interpretation Differences

## CRITICAL: This Manual Targets Veo 3.1 ONLY

**Do NOT apply Veo 3 assumptions when generating prompts.**
Veo 3.1 has fundamentally different JSON interpretation logic.

---

## Summary

| Aspect | Veo 3 | Veo 3.1 |
|--------|-------|---------|
| **Prompt adherence** | Loose (unpredictable creativity) | Strict (follows instructions precisely) |
| **Description verbosity** | Requires many adjectives | Simpler with reference images |
| **Dialogue understanding** | Poor lip-sync | Recognizes `""` as speech, generates lip-sync |
| **Camera work** | Complex movements often fail | Executes combined movements accurately |
| **Physics** | Uses morphing to fake motion | Considers mass/inertia realistically |

---

## 1. Prompt Order Weighting

### Veo 3 Behavior
- **Front-loading required**: First words in prompt are weighted extremely heavily
- Later instructions (camera, lighting) often ignored
- Required placing important nouns at the beginning of `subject` and `action`

### Veo 3.1 Behavior
- **Contextual understanding**: Evaluates entire JSON structure evenly
- `style` and `negative_prompt` at the end are properly considered
- Better temporal logic: understands "A does B, then becomes C" sequences

**Implication**: You no longer need to artificially front-load keywords in 3.1.

---

## 2. Ingredients (Reference Images) - 3.1 EXCLUSIVE

The biggest difference: Veo 3.1 can process **reference images** directly in JSON.

### 3.1-Only JSON Structure
```json
{
  "prompt": "...",

  "ingredients": [
    {
      "type": "character_reference",
      "image_base64": "..."
    }
  ],

  "first_frame": "...",
  "last_frame": "..."
}
```

### Supported Ingredient Types
- `character_reference` - Maintain character consistency
- `style_reference` - Visual style guidance
- `object_reference` - Specific object appearance

**Implication**: Character descriptions can be much shorter when using reference images.

---

## 3. Audio/Dialogue Interpretation

### Veo 3 Behavior
- Audio treated as "bonus feature"
- Writing `says "Hello"` often resulted in:
  - Mismatched lip movement
  - Generic BGM instead of speech

### Veo 3.1 Behavior
- Text in quotation marks `""` explicitly parsed as **Dialogue**
- Attempts to generate lip-sync matching the speech
- Clear distinction between:
  - `"Hello!"` → Dialogue with lip-sync
  - `SFX: explosion` → Sound effect
  - `Music: orchestral` → Background music

**Implication**: Always use quotation marks for character speech.

---

## 4. Physics and Motion Interpretation

### Veo 3 Behavior
- Unrealistic actions (flying, transforming) → morphing/melting effect
- Lacks physical weight understanding
- Sudden movements appear "floaty"

### Veo 3.1 Behavior
- Considers physical mass and inertia
- "Sudden stop" → character leans forward slightly
- "Heavy object falls" → appropriate impact and bounce
- More realistic motion physics

**Implication**: You can specify realistic physics-based actions without workarounds.

---

## 5. Complex Camera Work

### Veo 3 Behavior
- Single camera movements work
- Combined movements (rotate + zoom + track) often fail
- Dutch angles inconsistent

### Veo 3.1 Behavior
- Executes multi-axis camera movements accurately
- Examples that now work:
  - "Orbital tracking while zooming out"
  - "Dutch tilt with dolly-in"
  - "Whip pan to rack focus"

---

## Migration Guide: Veo 3 → 3.1

### What to STOP doing
1. ❌ Front-loading keywords artificially
2. ❌ Overly verbose character descriptions (use ingredients instead)
3. ❌ Avoiding complex camera movements
4. ❌ Using workarounds for physics

### What to START doing
1. ✅ Use `ingredients` for character/style consistency
2. ✅ Use `""` for all dialogue
3. ✅ Specify complex camera choreography confidently
4. ✅ Trust physics descriptions to be interpreted realistically
5. ✅ Use `first_frame` and `last_frame` for transition control

---

## JSON Schema Additions in 3.1

### New Top-Level Fields
```json
{
  "ingredients": [],        // Reference images array
  "first_frame": "base64",  // Starting frame control
  "last_frame": "base64",   // Ending frame control
  "generate_audio": true    // Explicit audio generation flag
}
```

### Enhanced Audio Object
```json
{
  "audio": {
    "dialogue": "Character says: \"Exact speech here\"",
    "sfx": "SFX: [specific sound effects]",
    "ambience": "Ambience: [environmental sounds]",
    "music": "Music: [style/mood description]"
  }
}
```

---

## Version Detection

When working with Veo, always verify which version is being used:

| Model ID | Version |
|----------|---------|
| `veo-3.0-generate-001` | Veo 3.0 (legacy) |
| `veo-3.1-generate-001` | Veo 3.1 (current) |

**This manual assumes Veo 3.1 (`veo-3.1-generate-001`) exclusively.**
