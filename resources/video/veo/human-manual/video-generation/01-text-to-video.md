# Text-to-Video モード

## 概要

テキストプロンプトのみで動画を生成する最もシンプルなモード。

**いつ使う？**
- 素早くコンセプトを試したい
- 特定の開始画像が不要
- 風景、抽象映像、一般的なシーン

---

## 基本的なプロンプト構造

### Geminiへの依頼テンプレート

```
Veo 3.1のText-to-Videoプロンプトを生成してください。

【シーン説明】
[何が起きるか]

【技術仕様】
- カメラワーク: [static / dolly / tracking / orbit など]
- スピード: [slow / normal / fast]
- 雰囲気: [cinematic / documentary / commercial など]
- 時間帯: [golden_hour / night / noon など]

【オーディオ】
- 音声: [必要/不要]
- BGM: [ジャンル または 「なし」]
```

---

## 具体的な依頼例

### 例1: 風景動画

```
Veo 3.1で山の風景動画を生成するプロンプトを作って

シーン: 朝もやの中にそびえる雪山
カメラ: ゆっくりとしたパンで全景を見せる
雰囲気: 壮大、神秘的
BGM: オーケストラ、壮大な感じ
```

**Geminiの出力例**:
```json
{
  "shot": {
    "type": "wide establishing",
    "movement": "slow pan right",
    "lens": "24mm",
    "speed": "slow"
  },
  "subject": {
    "identity": "Snow-capped mountain range",
    "position": "Filling frame"
  },
  "scene": {
    "location": "Alpine mountain range at dawn",
    "time_of_day": "dawn",
    "weather": "Misty, clearing fog",
    "atmosphere": "Majestic, mysterious, pristine"
  },
  ...
}
```

### 例2: 人物動画

```
街を歩くビジネスマンの動画プロンプトを生成して

- 30代男性、スーツ姿
- 都市の歩道、昼間
- 追従ショット（サイドから）
- 自然なBGMなし、環境音のみ
```

### 例3: 製品イメージ（抽象）

```
テクノロジー企業のブランド動画用プロンプト

- 青い光の粒子が収束してロゴっぽい形に
- 黒背景、未来的
- スローモーション
- エレクトロニックなBGM
```

---

## カメラワークの指定方法

### 信頼性の高い指定

| カメラワーク | 指定例 |
|------------|--------|
| 固定 | `static shot`, `locked off camera` |
| 前進 | `slow dolly in`, `push in` |
| 後退 | `slow dolly out`, `pull out` |
| 追従 | `tracking shot`, `follow shot` |
| 周回 | `slow orbit`, `arc shot` |
| 上昇 | `crane up`, `rising shot` |
| 俯瞰 | `drone shot`, `aerial view` |
| 手持ち | `handheld`, `documentary style` |

### 避けるべき指定

- 複数の動きを同時に（例: pan + zoom + dolly）
- 速すぎる動き（例: rapid whip pan）
- 曖昧な指示（例: just "camera moves"）

---

## 時間帯とライティング

### よく使う時間帯

| 時間帯 | 効果 | 適したシーン |
|--------|------|-------------|
| `golden_hour` | 暖かい光、ドラマチック | ロマンス、美的、ポートレート |
| `blue_hour` | 涼しい光、神秘的 | ミステリー、都市夜景 |
| `noon` | 強い光、はっきり | ドキュメンタリー、アクション |
| `night` | 暗い、人工光 | ノワール、ナイトライフ |

### ライティングの追加指定

```
ライティング: golden_hour, 被写体を逆光で（シルエット気味に）
```

---

## 音声の指定

### 台詞を入れる場合

```json
"audio": {
  "dialogue": "Man says confidently: 'This is just the beginning.'"
}
```

### BGMの指定

```json
"audio": {
  "music": "Music: orchestral, triumphant, building intensity"
}
```

### BGMを防ぐ場合

```json
"audio": {
  "music": "NO music, ambient sounds only"
}
```

---

## ネガティブプロンプトの重要性

必ず含めるべき項目:

```json
"negative": {
  "exclude": [
    "blur",
    "distortion",
    "low quality",
    "watermark",
    "text overlay"
  ]
}
```

人物の場合は追加:
```json
"exclude": ["extra limbs", "morphing", "deformed"]
```

---

## プロトタイプから本番へ

### Step 1: fastモデルでテスト

```
プロトタイプ用に veo-3.1-fast で試したい
720pで構わない
```

### Step 2: プロンプト調整

結果を見て修正:
```
前回の結果、カメラが速すぎた
「very slow dolly in」に変更して再生成
```

### Step 3: 本番レンダリング

```
OKなので veo-3.1-generate-001 で本番
1080pで出力
```

---

## トラブルシューティング

| 問題 | 対策 |
|------|------|
| カメラが動かない | `static`を外して明示的に動きを指定 |
| 人物が歪む | `no morphing`, `consistent anatomy`を追加 |
| 音楽が勝手に入る | `NO music`を明記 |
| ぼやける | `blur`をネガティブに追加、`sharp`, `focused`を追加 |
| 背景が変わる | `consistent background`を追加 |

---

## 次に読む

- **画像から始めたい**: `02-image-to-video.md`
- **キャラを一貫させたい**: `03-ingredients.md`
- **AからBへの変化**: `04-frame-interpolation.md`
