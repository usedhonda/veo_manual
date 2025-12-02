# 製品CM完全ガイド

## 概要

このガイドでは、製品CMの動画を作成する完全なワークフローを解説します。

**完成イメージ**:
- 高級感のある製品プロモーション動画
- 8秒のプロダクトヒーローショット
- プレミアムなライティングと動き

---

## 全体フロー

```
┌─────────────────────────────────────────────────────┐
│ 1. 企画: 製品の魅力ポイントを決める                  │
└─────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────┐
│ 2. Phase 1: Nano Banana Pro で製品画像を生成        │
│    └→ First Frame として使用                        │
└─────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────┐
│ 3. Phase 2: Veo 3.1 Image-to-Video で動画化         │
│    └→ オービット/ドリー/ライトスイープ              │
└─────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────┐
│ 4. （オプション）延長、追加ショット生成             │
└─────────────────────────────────────────────────────┘
```

---

## Step 1: 企画

### 製品情報の整理

Geminiに伝える情報:
- 製品名と種類
- 素材・仕上げ
- ブランドカラー
- ターゲット層
- 見せたい特徴

### 例: 高級イヤホン

```
製品情報:
- 製品: ProSound X1 ワイヤレスイヤホン
- 素材: アルミニウムフレーム、レザー充電ケース
- カラー: ミッドナイトブラック × ローズゴールドアクセント
- ターゲット: 30代プロフェッショナル
- 特徴: タッチ操作、LEDインジケーター、ノイズキャンセリング
```

---

## Step 2: Phase 1 - 製品画像の生成

### Geminiへの依頼

```
製品CM用のFirst Frame画像プロンプトを生成してください。

【製品情報】
- 製品: ProSound X1 ワイヤレスイヤホン
- 素材: アルミフレーム、レザーケース
- カラー: ブラック × ローズゴールド

【撮影仕様】
- 構図: クローズアップ、斜め45度
- 背景: チャコールグレーのグラデーション
- ライティング: リムライト、プレミアム感重視
- 解像度: 1080p, 16:9
- 余白: 右側にオービット用の空間を確保

【動画での使用予定】
- カメラ: 時計回りの180度オービット
- この画像がスタートフレームになる
```

### 生成される画像プロンプト例

```json
{
  "subject": {
    "identity": "ProSound X1 Premium Wireless Earbuds with charging case",
    "appearance": {
      "features": "Matte black aluminum frame, rose gold touch panel accent, LED indicator visible, leather charging case with embossed logo",
      "pose": "45-degree angle, case open showing earbuds"
    }
  },
  "composition": {
    "framing": "close_up",
    "angle": "slightly_elevated",
    "subject_position": "rule_of_thirds_left",
    "negative_space": "Right side clear for orbit motion"
  },
  "background": {
    "type": "gradient",
    "description": "Smooth charcoal to deep black gradient",
    "blur": "none"
  },
  "lighting": {
    "type": "studio",
    "direction": "rim from back-right",
    "quality": "hard",
    "color_temperature": "cool",
    "special": "Strong rim light on aluminum edges, subtle reflection below"
  },
  ...
}
```

---

## Step 3: Phase 2 - 動画の生成

### Geminiへの依頼

```
Phase 1で生成した画像を使って、Veo 3.1 Image-to-Videoプロンプトを生成してください。

【動き】
- カメラ: 時計回りのスローな180度オービット
- スピード: ゆっくり、8秒で半周
- 追加効果: ライトが製品表面を滑るように移動

【一貫性】
- ライティング: Phase 1のリムライトを維持
- 背景: 同じグラデーション
- 製品: 位置固定、回転のみ

【オーディオ】
- BGM: モダンエレクトロニック、ミニマル、プレミアム感
- SE: 微かなスイープ音、満足感のあるクリック

【避けるもの】
- 指紋、傷、埃
- 安っぽい見た目
- ロゴやテキスト
```

### 生成される動画プロンプト例

```json
{
  "input_image": {
    "source": "gcs_uri",
    "role": "first_frame",
    "description": "ProSound X1 earbuds on dark gradient"
  },
  "shot": {
    "type": "close-up hero",
    "movement": "slow 180-degree orbit clockwise",
    "speed": "slow"
  },
  "subject": {
    "reference": "The earbuds and case from the input image",
    "maintain": "Product position, aluminum finish, rose gold accents",
    "highlight": "LED indicator, seamless design"
  },
  "action": {
    "primary": "Product slowly rotates revealing all angles",
    "secondary": "Light sweeps across surface highlighting contours",
    "timing": "Continuous 180-degree rotation over 8 seconds"
  },
  "audio": {
    "sfx": "SFX: subtle whoosh, satisfying material sound",
    "music": "Music: modern electronic, minimal pulse, premium feel"
  },
  "negative": {
    "exclude": ["blur", "fingerprints", "dust", "cheap", "logo", "text"]
  },
  "meta": {
    "duration": 8,
    "resolution": "1080p",
    "aspect_ratio": "16:9"
  }
}
```

---

## Step 4: バリエーション

### 複数ショットの組み合わせ

一つのCMに複数のショットを生成:

| ショット | 内容 | 秒数 |
|---------|------|------|
| Shot 1 | フルオービット | 8秒 |
| Shot 2 | ディテールクローズアップ | 8秒 |
| Shot 3 | 使用シーン（人物装着） | 8秒 |

### Shot 2: ディテール用の依頼

```
同じ製品のマクロディテールショットを生成

- 極端なクローズアップ
- タッチ表面のテクスチャに焦点
- LEDインジケーターの光
- 静止、またはごくわずかな動き
```

### Shot 3: ライフスタイル用の依頼

```
製品使用シーンを生成

- ビジネスマンがイヤホンを装着
- モダンなオフィス環境
- 自然光、プロフェッショナルな雰囲気
- 製品がさりげなく目立つ
```

---

## 製品タイプ別のヒント

### テクノロジー製品

- **ライティング**: ハードなリムライト、クリーンな反射
- **動き**: スローオービット、精密な動き
- **カラー**: 高コントラスト、暗い背景
- **音**: ミニマルエレクトロニック

### 美容・コスメ製品

- **ライティング**: ソフトな自然光、ゴールデン
- **動き**: ドリーイン、ドロッパー動作
- **カラー**: 暖かいトーン、エレガント
- **音**: ピアノ、スパ的なアンビエント

### 食品・飲料

- **ライティング**: サイドライト、テクスチャ強調
- **動き**: 湯気、液体の動き
- **カラー**: 食欲をそそる暖色
- **音**: 環境音、調理音

### 高級時計・宝飾品

- **ライティング**: ドラマチックなサイドライト
- **動き**: 微細な動き、光の移動
- **カラー**: リッチ、深い影
- **音**: ミニマル、時計のチック音

---

## チェックリスト

### 生成前

- [ ] 製品情報を整理した
- [ ] 見せたい特徴を決めた
- [ ] 動きの方向を計画した
- [ ] ブランドカラーを確認した

### Phase 1 後

- [ ] 製品が正確に描写されている
- [ ] 動きに必要な余白がある
- [ ] ライティングが適切

### Phase 2 後

- [ ] 一貫性が保たれている
- [ ] 動きがスムーズ
- [ ] オーディオがブランドに合っている
- [ ] 不要な要素がない

---

## 次に読む

- **より長い動画が必要**: `../phase3-extend/01-video-extension.md`
- **複数ショットの連結**: `../phase3-extend/02-multi-shot-sequence.md`
- **他の用途**: `anime-character.md`, `music-video.md`
