# Veo 3.1 クイックスタート

## 5分で最初の動画を生成する

### Step 1: Geminiにプロンプトを依頼する

Geminiに以下のように依頼します：

```
Veo 3.1で「草原を歩く女性」の動画プロンプトをJSONで生成して
```

### Step 2: Geminiが生成するJSON例

```json
{
  "shot": {
    "type": "medium",
    "movement": "tracking",
    "lens": "35mm",
    "speed": "normal"
  },
  "subject": {
    "identity": "Young woman in her 20s",
    "appearance": "Flowing white summer dress, long brown hair",
    "expression": "Peaceful, content smile",
    "position": "Center frame"
  },
  "action": {
    "primary": "walks gracefully",
    "direction": "left_to_right",
    "timing": "Throughout clip"
  },
  "scene": {
    "location": "Open grass field with rolling hills",
    "time_of_day": "golden_hour",
    "weather": "Clear with light breeze",
    "atmosphere": "Serene, dreamy"
  },
  "style": {
    "medium": "live_action",
    "color_grade": "Warm, soft, pastoral",
    "genre": "Lifestyle"
  },
  "audio": {
    "sfx": "SFX: grass rustling, soft wind",
    "ambience": "Ambience: open field, birds, breeze",
    "music": "Music: gentle acoustic guitar"
  },
  "negative": {
    "exclude": ["blur", "distortion", "low quality", "watermark"]
  },
  "meta": {
    "duration": 8,
    "resolution": "1080p",
    "aspect_ratio": "16:9"
  }
}
```

### Step 3: APIに送信

このJSONをVeo 3.1 APIの`prompt`フィールドに変換して送信します。

---

## 基本的な依頼パターン

### パターン1: シンプルな説明
```
「海辺の夕日」の動画プロンプトを生成して
```

### パターン2: 詳細な指定
```
以下の条件でVeo 3.1プロンプトを生成して：
- 被写体: ビジネスマン
- シーン: 東京の夜景
- カメラ: スローなドリーイン
- 雰囲気: プロフェッショナル、都会的
```

### パターン3: 用途指定
```
製品CM用の「高級腕時計」動画プロンプトを生成して
オービットショット、8秒、プレミアム感重視
```

---

## 3つのワークフロー

### A. テキストのみ（最速）
1. Geminiに説明を渡す
2. JSONプロンプトを生成
3. Veo 3.1で動画生成

### B. 画像から動画
1. **Phase 1**: Nano Bananaで開始フレーム画像を生成
2. **Phase 2**: その画像をVeo 3.1のImage-to-Videoモードで動画化

### C. キャラクター一貫性
1. **Phase 1**: Nano Bananaでキャラクターシートを生成
2. **Phase 2**: Veo 3.1のIngredientsモードで参照画像として使用

---

## よく使う指示フレーズ

| 目的 | フレーズ例 |
|------|-----------|
| カメラワーク | 「スローなドリーインで」「オービットショットで」 |
| 雰囲気 | 「映画的に」「ドキュメンタリー風に」 |
| ライティング | 「ゴールデンアワーで」「ネオンライトで」 |
| スタイル | 「アニメ風で」「プロダクトCM風に」 |
| 音声 | 「BGMなしで」「台詞を入れて」 |

---

## 次のステップ

- **詳細を知りたい**: `01-workflow-selector.md`を読む
- **製品CMを作りたい**: `use-cases/commercial-product.md`を参照
- **アニメを作りたい**: `use-cases/anime-character.md`を参照
- **MVを作りたい**: `use-cases/music-video.md`を参照
