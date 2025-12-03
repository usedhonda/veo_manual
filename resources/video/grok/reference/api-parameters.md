# Grok Imagine API Parameters

## API Overview

Grok Imagine provides video generation through REST API endpoints. This document covers the available parameters and their usage.

---

## Endpoints

### Text-to-Video
```
POST /api/v1/video/generate
```

### Image-to-Video
```
POST /grok-imagine/image-to-video
```

### Status Check
```
GET /api/v1/video/status?taskId=YOUR_TASK_ID
```

---

## Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `prompt` | string | Yes | Text description of desired video (max 380 chars) |
| `duration` | string | No | Video length: `"5"` or `"8"` seconds |
| `quality` | string | No | Resolution: `"720p"` or `"1080p"` |
| `aspectRatio` | string | No | Frame ratio (see below) |
| `imageUrl` | string | No | Source image URL for Image-to-Video |
| `mode` | string | No | Creative mode (see below) |

---

## Aspect Ratios

| Value | Use Case |
|-------|----------|
| `"16:9"` | Widescreen (YouTube, desktop) |
| `"9:16"` | Vertical (TikTok, Reels, Stories) |
| `"1:1"` | Square (Instagram feed) |
| `"4:3"` | Classic TV ratio |
| `"3:4"` | Portrait |

---

## Creative Modes

| Mode | Description |
|------|-------------|
| `normal` | Polished, safe results (default) |
| `fun` | Playful effects added |
| `spicy` | Adult/provocative content (restricted) |

**Note**: Spicy mode may be downgraded to Normal when using external image URLs.

---

## Example Request (cURL)

```bash
curl -X POST https://api.grokimagine.ai/v1/video/generate \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "prompt": "Epic sunrise over mountains, camera fly-over shot with dramatic light rays, cinematic color grading",
    "duration": "5",
    "quality": "720p",
    "aspectRatio": "16:9"
  }'
```

---

## Example Request (Python)

```python
import requests

API_KEY = "YOUR_API_KEY"
headers = {
    "Authorization": f"Bearer {API_KEY}",
    "Content-Type": "application/json"
}

data = {
    "prompt": "Slow zoom-in on product with elegant lighting",
    "duration": "5",
    "quality": "1080p",
    "aspectRatio": "16:9"
}

response = requests.post(
    "https://api.grokimagine.ai/v1/video/generate",
    headers=headers,
    json=data
)

result = response.json()
print(result)
```

---

## Response Format

### Initial Response
```json
{
  "success": true,
  "data": {
    "taskId": "ee603959-debb-48d1-98c4-a6d1c717eba6",
    "status": "pending",
    "creditsUsed": 10
  }
}
```

### Status Values

| Status | Description |
|--------|-------------|
| `pending` | Queued for processing |
| `processing` | Generation in progress |
| `completed` | Video ready |
| `failed` | Generation failed |

---

## Image-to-Video Example (Python)

```python
import requests

API_KEY = "YOUR_API_KEY"
headers = {"Authorization": f"Bearer {API_KEY}"}

data = {
    "image_urls": ["https://example.com/product.jpg"],
    "prompt": "Slow zoom-in with text: 'New Arrival'",
    "mode": "normal",
    "aspect_ratio": "9:16"
}

response = requests.post(
    "https://api.kie.ai/grok-imagine/image-to-video",
    headers=headers,
    json=data
)

result = response.json()
print(result)
```

---

## Rate Limits & Credits

- API calls require authentication via Bearer token
- Credit consumption varies by quality and duration
- Higher quality (1080p) uses more credits
- Check provider documentation for specific limits

---

## Error Codes

| Code | Description |
|------|-------------|
| 400 | Invalid request parameters |
| 401 | Authentication failed |
| 429 | Rate limit exceeded |
| 500 | Server error |

---

## Best Practices

1. **Start with 720p** for testing, upgrade to 1080p for final
2. **Use 5-second duration** for quick iterations
3. **Poll status endpoint** every 2-3 seconds until complete
4. **Handle async nature** - video generation takes time
5. **Cache taskIds** to avoid duplicate requests
