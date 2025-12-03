# Veo 3.1 API Technical Parameters

## Model Identifiers

| Model ID | Purpose | Quality | Speed | Cost |
|----------|---------|---------|-------|------|
| `veo-3.1-generate-001` | Production | High | Slower | ~100 credits |
| `veo-3.1-fast-generate-001` | Prototyping | Medium | Faster | ~20 credits |
| `veo-3.1-generate-preview` | Preview/Testing | High | Slower | Varies |
| `veo-3.1-fast-generate-preview` | Preview/Testing | Medium | Faster | Varies |

### Model Selection Guide
- **Use Standard** for: Final renders, client delivery, complex scenes
- **Use Fast** for: Storyboarding, motion tests, prompt iteration

---

## API Endpoint Structure

### Vertex AI Endpoint
```
POST https://{LOCATION}-aiplatform.googleapis.com/v1/projects/{PROJECT_ID}/locations/{LOCATION}/publishers/google/models/{MODEL_ID}:predictLongRunning
```

### Required Headers
```
Authorization: Bearer {ACCESS_TOKEN}
Content-Type: application/json
```

---

## Request Payload Structure

### Complete Request Schema

```json
{
  "instances": [
    {
      "prompt": "string - required for text-to-video",

      "image": {
        "bytesBase64Encoded": "string - base64 image data",
        "gcsUri": "gs://bucket/path/image.png",
        "mimeType": "image/png | image/jpeg"
      },

      "lastFrame": {
        "bytesBase64Encoded": "string - base64 image data",
        "gcsUri": "gs://bucket/path/image.png",
        "mimeType": "image/png | image/jpeg"
      },

      "video": {
        "bytesBase64Encoded": "string - base64 video data",
        "gcsUri": "gs://bucket/path/video.mp4",
        "mimeType": "video/mp4"
      },

      "referenceImages": [
        {
          "image": {
            "bytesBase64Encoded": "string",
            "gcsUri": "gs://bucket/path/ref.png",
            "mimeType": "image/png"
          },
          "referenceType": "asset"
        }
      ]
    }
  ],
  "parameters": {
    "sampleCount": 1,
    "durationSeconds": 8,
    "aspectRatio": "16:9",
    "resolution": "1080p",
    "personGeneration": "allow_adult",
    "negativePrompt": "blur, distortion, low quality",
    "storageUri": "gs://output-bucket/results/",
    "seed": 123456789
  }
}
```

---

## Parameter Details

### instances[].prompt
- **Type**: String
- **Required**: Yes for text-to-video, recommended for all modes
- **Language**: English only (officially supported)
- **Max Length**: ~32k tokens context window

### instances[].image (First Frame)
- **Type**: Object (Union field)
- **Use**: Image-to-Video mode
- **Format**: JPEG or PNG
- **Resolution**: Match target output resolution recommended
- **Note**: Provide EITHER `bytesBase64Encoded` OR `gcsUri`, not both

### instances[].lastFrame
- **Type**: Object (Union field)
- **Use**: Frame Interpolation mode
- **Supported Models**: veo-3.1-generate-preview, veo-3.1-generate-001
- **Note**: Creates transition video between image and lastFrame

### instances[].video (Extension)
- **Type**: Object (Union field)
- **Use**: Video Extension mode
- **Constraint**: Must be Veo-generated video
- **Max Input Duration**: 141 seconds
- **Resolution**: 720p only for extension

### instances[].referenceImages (Ingredients)
- **Type**: Array of objects
- **Max Count**: 3 images
- **referenceType**: `"asset"` only (no `"style"` in Veo 3.1)
- **Use**: Character/object consistency across generations

---

## parameters Object

### sampleCount
- **Type**: Integer
- **Range**: 1-4
- **Default**: 1
- **Note**: Multiple samples increase latency linearly

### durationSeconds
- **Type**: Integer
- **Valid Values**: `4`, `6`, `8` only
- **Default**: 8
- **Note**: Interpolation may force specific durations

### aspectRatio
- **Type**: String
- **Valid Values**: `"16:9"`, `"9:16"`
- **Default**: `"16:9"`
- **Note**: Other ratios not supported

### resolution
- **Type**: String
- **Valid Values**: `"720p"`, `"1080p"`
- **Default**: `"720p"`
- **Constraints**:
  - Video extension: 720p only
  - 1080p may limit duration options

### personGeneration
- **Type**: String
- **Values**:
  - `"allow_adult"`: Generate photorealistic adults (default)
  - `"dont_allow"`: Block realistic human generation
- **Note**: Regional restrictions may apply

### negativePrompt
- **Type**: String
- **Use**: Exclude unwanted elements
- **Example**: `"blur, distortion, text, watermark, low quality"`

### storageUri
- **Type**: String (GCS URI)
- **Format**: `gs://bucket/path/`
- **Recommendation**: Use for production (avoids base64 response bloat)

### seed
- **Type**: Integer
- **Use**: Reproducible generations
- **Note**: Same seed + same prompt = similar output

---

## Response Structure

### Initial Response (Operation Started)
```json
{
  "name": "projects/{PROJECT}/locations/{LOCATION}/operations/{OPERATION_ID}",
  "metadata": {
    "@type": "type.googleapis.com/google.cloud.aiplatform.v1.GenericOperationMetadata",
    "createTime": "2025-12-02T10:00:00Z",
    "updateTime": "2025-12-02T10:00:00Z",
    "state": "RUNNING"
  }
}
```

### Polling for Completion
```
GET https://{LOCATION}-aiplatform.googleapis.com/v1/{operation_name}
```

### Completed Response
```json
{
  "name": "projects/{PROJECT}/locations/{LOCATION}/operations/{OPERATION_ID}",
  "done": true,
  "response": {
    "videos": [
      {
        "bytesBase64Encoded": "AAAAIGZ0eXBpc29t...",
        "mimeType": "video/mp4"
      }
    ]
  }
}
```

### Error Response
```json
{
  "name": "projects/{PROJECT}/locations/{LOCATION}/operations/{OPERATION_ID}",
  "done": true,
  "error": {
    "code": 400,
    "message": "Invalid aspect ratio",
    "status": "INVALID_ARGUMENT"
  }
}
```

---

## Common Error Codes

| Code | Status | Cause | Solution |
|------|--------|-------|----------|
| 400 | INVALID_ARGUMENT | Invalid parameter values | Check aspectRatio, resolution, duration |
| 400 | INVALID_ARGUMENT | Incompatible input combination | Don't mix Ingredients with lastFrame |
| 429 | RESOURCE_EXHAUSTED | Rate limit exceeded | Implement backoff, check quota |
| 500 | INTERNAL | Model inference failure | Retry with exponential backoff |
| N/A | SAFETY | Content filter triggered | Rephrase prompt, check negatives |

---

## Mode Compatibility Matrix

| Feature | Text-to-Video | Image-to-Video | Ingredients | Interpolation | Extension |
|---------|---------------|----------------|-------------|---------------|-----------|
| prompt | ✅ Required | ✅ Recommended | ✅ Required | ✅ Recommended | ✅ Required |
| image | ❌ | ✅ Required | ❌ | ✅ Required | ❌ |
| lastFrame | ❌ | ❌ | ❌ | ✅ Required | ❌ |
| video | ❌ | ❌ | ❌ | ❌ | ✅ Required |
| referenceImages | ❌ | ❌ | ✅ Required | ❌ | ❌ |
| 1080p | ✅ | ✅ | ✅ | ✅ | ❌ (720p only) |
| 8s duration | ✅ | ✅ | ✅ | ✅ | ✅ |
| 4s/6s duration | ✅ | ✅ | ⚠️ May vary | ⚠️ Usually 8s | ✅ |

---

## Best Practices

### Polling Strategy
```python
import time

def poll_operation(operation_name, max_wait=300):
    start = time.time()
    interval = 10  # Start with 10 seconds

    while time.time() - start < max_wait:
        response = get_operation_status(operation_name)
        if response.get('done'):
            return response
        time.sleep(interval)
        interval = min(interval * 1.5, 30)  # Exponential backoff, max 30s

    raise TimeoutError("Operation did not complete")
```

### Storage vs Base64
- **Use storageUri** for production pipelines
- **Use base64** only for quick tests or small-scale use
- Base64 increases response size by ~33%

### Seed Usage
- Use fixed seeds during prompt iteration for fair comparison
- Remove seed for production diversity
- Document seeds for reproducible results
