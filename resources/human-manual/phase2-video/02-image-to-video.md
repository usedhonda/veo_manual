# Image-to-Video モード

## 概要

静止画（First Frame）から動画を生成するモード。開始点を正確にコントロールできます。

**いつ使う？**
- 特定の構図から始めたい
- 製品のヒーローショット
- 正確なスタートフレームが必要
- Nano Banana Proで生成した画像を活かしたい

---

## 基本的なワークフロー

```
┌─────────────────────────────────────────────────────────────┐
│ Image-to-Video ワークフロー                                  │
│                                                             │
│  1. Nano Banana Pro で First Frame を生成                   │
│                         ↓                                   │
│  2. 画像をアップロード（Base64 または GCS URI）             │
│                         ↓                                   │
│  3. 動きのプロンプトを作成                                  │
│                         ↓                                   │
│  4. Veo 3.1 で動画生成                                      │
└─────────────────────────────────────────────────────────────┘
```

---

## Geminiへの依頼テンプレート

### 基本テンプレート

```
Veo 3.1のImage-to-Videoプロンプトを生成してください。

【入力画像の説明】
- 内容: [画像に写っているもの]
- 構図: [どんな構図か]
- ライティング: [光の状態]

【動きの指示】
- カメラワーク: [static / dolly / tracking / orbit など]
- スピード: [slow / normal / fast]
- 方向: [in / out / left / right / clockwise など]

【維持すべき要素】
- [画像から維持したい要素をリスト]

【オーディオ】
- SE: [効果音]
- BGM: [音楽またはなし]
```

---

## 具体的な依頼例

### 例1: 製品オービット

```
製品画像からオービット動画を生成するプロンプト

【入力画像】
- イヤホンと充電ケース
- 45度俯瞰、黒背景
- リムライトでエッジが光っている

【動き】
- カメラ: 時計回りの180度オービット
- スピード: スロー（8秒で半周）
- 追加効果: ライトが表面を滑るように

【維持】
- 製品の位置（中央固定）
- ライティングの質
- 背景の一貫性

【オーディオ】
- SE: 微かなスイープ音
- BGM: ミニマルエレクトロニック
```

### 例2: ポートレート動き出し

```
ポートレート画像から動き出す動画のプロンプト

【入力画像】
- 女性のミディアムショット
- ゴールデンアワーの光
- 少し微笑んでいる状態

【動き】
- 人物: 髪が風になびく、瞬きをする
- カメラ: 非常にスローなドリーイン
- 表情: 微笑みから笑顔へ

【維持】
- 顔の特徴
- ライティングの方向
- 服装と髪型

【オーディオ】
- SE: そよ風の音
- BGM: なし
```

### 例3: 風景動画

```
風景画像からシネマティック動画を生成

【入力画像】
- 山の遠景、朝もや
- 横長の壮大な構図
- 冷たい青みがかった色調

【動き】
- カメラ: ゆっくりとした右へのパン
- 環境: 霧がゆっくり流れる
- スピード: 非常にスロー

【維持】
- 山のシルエット
- 色調と雰囲気
- 構図のバランス

【オーディオ】
- アンビエンス: 山の静寂、遠くの鳥
- BGM: オーケストラ、壮大
```

---

## カメラワークの指定

### 信頼性の高い動き

| 動き | 指定方法 | 効果 |
|------|---------|------|
| オービット | `slow orbit clockwise around subject` | 製品周回 |
| ドリーイン | `slow dolly in toward subject` | 近づく |
| ドリーアウト | `slow dolly out from subject` | 引く |
| パン | `slow pan right/left` | 横移動 |
| クレーン | `slow crane up/down` | 縦移動 |
| 静止 | `static camera, subject moves` | カメラ固定 |

### 動きの速度

```
【速度の指定】
- very slow: 非常にゆっくり（推奨）
- slow: ゆっくり
- normal: 通常
- fast: 速い

【ヒント】
遅い方が安定して品質が高い
「slow」を付けることを推奨
```

---

## 入力画像の要件

### 技術要件

```
【形式】
- PNG または JPEG
- Base64エンコード または GCS URI

【解像度】
- 推奨: 1920x1080以上
- 最低: 720p相当

【アスペクト比】
- 16:9（横長）
- 9:16（縦長）
- その他は自動クロップされる可能性
```

### 品質要件

```
【必須】
- シャープでクリア
- 適切な露出
- 動きに必要な余白

【避けるべき】
- ブラー、ノイズ
- 過度な圧縮
- 極端な明暗
```

---

## 一貫性の維持

### プロンプトでの指定

```json
{
  "input_image": {
    "role": "first_frame",
    "description": "Maintain exact appearance from input"
  },
  "subject": {
    "reference": "Subject from input image",
    "maintain": "Position, lighting, colors, style"
  },
  "consistency": {
    "preserve": [
      "lighting direction",
      "color temperature",
      "background elements",
      "subject appearance"
    ]
  }
}
```

### ネガティブプロンプト

```json
{
  "negative": {
    "exclude": [
      "style change",
      "lighting change",
      "color shift",
      "sudden appearance change",
      "discontinuity"
    ]
  }
}
```

---

## 製品動画のベストプラクティス

### オービットショット

```
【入力画像の準備】
- 製品を中央に配置
- 周囲に十分な空間
- 均一な背景

【プロンプトのコツ】
- `slow 180-degree orbit`
- `maintain product position`
- `light sweeps across surface`
- `premium, high-end feel`
```

### ドリーインショット

```
【入力画像の準備】
- 製品をやや奥に配置
- 前方に空間
- 焦点となるディテールを意識

【プロンプトのコツ】
- `very slow dolly in`
- `reveal product details`
- `focus on [特定の機能]`
```

---

## トラブルシューティング

| 問題 | 原因 | 対策 |
|------|------|------|
| 画像と違う見た目 | 一貫性指定不足 | `maintain exact appearance`追加 |
| 動きが速すぎる | 速度指定なし | `slow`または`very slow`追加 |
| 背景が変わる | 背景指定なし | `consistent background`追加 |
| ライティングが変わる | ライト指定矛盾 | 画像のライティングを記述 |
| 色が変わる | 色温度の問題 | `maintain color temperature`追加 |

---

## APIでの使用

### 入力形式

```json
{
  "image": {
    "bytesBase64Encoded": "[Base64文字列]"
  }
}
```

または

```json
{
  "image": {
    "gcsUri": "gs://bucket/path/image.png"
  }
}
```

### 完全なリクエスト例

```json
{
  "model": "veo-3.1-generate-001",
  "input": {
    "image": {
      "gcsUri": "gs://my-bucket/product.png"
    }
  },
  "config": {
    "aspectRatio": "16:9",
    "durationSeconds": 8,
    "resolution": "1080p"
  },
  "prompt": "Slow 180-degree orbit around the product..."
}
```

---

## 次に読む

- **キャラの一貫性が必要**: `03-ingredients.md`
- **2つの画像間の変化**: `04-frame-interpolation.md`
- **製品CMを作りたい**: `../use-cases/commercial-product.md`
