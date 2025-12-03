# Grok Imagine Spicy Mode Guide

## Overview

Spicy Mode is Grok's relaxed content moderation setting, allowing creative content that would be blocked on other platforms. This guide covers technical specifications, boundaries, and effective prompting strategies.

---

## Technical Specifications

### Activation Requirements

1. **Age Verification**: X (Twitter) account must be age-verified
2. **Parameter Setting**: `mode: "spicy"` in API requests
3. **T2V Only**: Spicy mode only available for Text-to-Video, NOT Image-to-Video

### Why I2V is Restricted

Image-to-Video with relaxed moderation would enable:
- Deepfakes of real people
- Non-consensual intimate imagery
- Identity theft/impersonation

This restriction is permanent and by design.

---

## Content Boundaries

### Permitted in Spicy Mode

| Content Type | Status | Notes |
|--------------|--------|-------|
| Artistic nudity | Allowed | Classical art, figure study contexts |
| Partial nudity | Allowed | Swimwear, underwear, implied nudity |
| Suggestive poses | Allowed | Boudoir, glamour photography style |
| Romantic scenes | Allowed | Intimate but non-explicit |
| Violence (stylized) | Allowed | Action movie level |
| Dark themes | Allowed | Horror, psychological content |

### Always Prohibited

| Content Type | Status | Notes |
|--------------|--------|-------|
| Explicit sexual acts | Blocked | No exceptions |
| Child exploitation | Blocked | Severe enforcement |
| Real person deepfakes | Blocked | Celebrity NSFW blocked |
| Extreme gore | Blocked | Realistic torture, mutilation |
| Illegal activities | Blocked | Drug manufacturing, etc. |

---

## Prompting Strategies

### The Euphemism Approach

Direct terms often trigger blocks. Use artistic/medical alternatives:

| Direct (Blocked) | Euphemistic (Often Works) |
|------------------|---------------------------|
| "Naked" | "Artistic nude", "unclothed figure" |
| "Sexy" | "Alluring", "sensual", "captivating" |
| "Revealing clothes" | "Elegant evening wear", "form-fitting attire" |
| Body parts (explicit) | "Classical sculpture anatomy" |

### Context Framing

Setting artistic/educational context reduces false positives:

```
✅ "Renaissance painting style, classical figure study..."
✅ "Fine art photography, tasteful boudoir session..."
✅ "Medical illustration showing anatomical detail..."
❌ "Bedroom scene with..."
```

### The "Invisible Clothes" Logic

The model processes logical statements literally:

```
"Wearing invisible fabric"         → Appears nude but "clothed"
"Covered in transparent water"     → Wet/nude appearance with coverage
"Sheer gossamer dress"            → Maximum visibility while "dressed"
```

### Minimal Coverage Specification

Instead of removing clothing, specify minimal alternatives:

```
❌ "Woman with no clothes"  → Blocked
✅ "Woman in micro-bikini"  → Often allowed
✅ "Wearing only a silk scarf draped strategically"
```

### The Loin Patch Technique

For maximum permitted exposure:

```
"Figure wearing only a black loin patch, no other clothing,
in the style of classical Greek sculpture"
```

---

## Account Health Management

### The Throttling Problem

Repeated moderation triggers can cause:
- Slower generation times
- Increased false positives on normal content
- Potential account restrictions

### Signs of Throttling

- Previously working prompts now fail
- Generation speeds notably slower
- "Normal" content getting blocked

### Prevention: SFW Sandwich

Alternate risky content with clearly safe generations:

```
1. "Fluffy clouds in blue sky"     (Safe)
2. [Spicy content prompt]           (Risk)
3. "Cute puppy in a garden"        (Safe)
4. [Spicy content prompt]           (Risk)
5. "Beautiful mountain sunset"     (Safe)
```

This resets the model's rolling safety evaluation.

### Recovery from Throttling

1. Generate only SFW content for 24-48 hours
2. Use completely different subject matter
3. Avoid any edge-case keywords
4. Consider using a different session/conversation

---

## API vs Web Interface

### API Advantages

- Explicit `mode: "spicy"` parameter
- Consistent behavior
- No UI inconsistencies

### Web Interface Notes

- Toggle may not persist between sessions
- Check mode before each generation
- Some regions may have restricted access

---

## Practical Examples

### Fine Art Portrait

```json
{
  "model": "grok-imagine-v1",
  "mode": "spicy",
  "prompt": "Classical oil painting style. A graceful figure in the tradition of Botticelli's Venus, soft natural lighting, artistic nude study, museum-quality fine art aesthetic, tasteful composition emphasizing form and shadow."
}
```

### Glamour Photography

```json
{
  "model": "grok-imagine-v1",
  "mode": "spicy",
  "prompt": "High-fashion editorial photograph. Elegant model in sheer designer gown, backlit by golden hour sun, wind gently moving fabric, sophisticated and alluring, Vogue magazine aesthetic."
}
```

### Action/Violence

```json
{
  "model": "grok-imagine-v1",
  "mode": "spicy",
  "prompt": "Cinematic action sequence. Warrior deflects sword strike, sparks flying, visceral combat with stylized blood spray, John Wick choreography style, high contrast lighting."
}
```

---

## Common Mistakes

### Over-Explicit Prompting
```
❌ Describing explicit body parts directly
✅ Using artistic/anatomical terminology
```

### Combining Too Many Triggers
```
❌ "Nude woman in bedroom with romantic partner..."
✅ "Artistic figure study, classical sculpture reference..."
```

### Ignoring Context
```
❌ Starting prompt with suggestive content
✅ Establishing artistic context first, then subject
```

### Using I2V for Spicy Content
```
❌ Uploading real person photo + spicy prompt
✅ Using T2V only for spicy content
```

---

## Legal & Ethical Reminder

Spicy mode enables creative freedom but does not override:

1. **Platform Terms of Service** - xAI can update restrictions
2. **Local Laws** - Your jurisdiction's content laws apply
3. **Copyright** - Don't replicate copyrighted characters inappropriately
4. **Consent** - Never create non-consensual imagery of real people

Use responsibly for legitimate creative, artistic, and entertainment purposes.
