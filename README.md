# AI Video Prompt Generation Manual

動画生成AI（Veo 3.1 / Grok Imagine）のためのプロンプトマニュアル。GeminiなどのAIにリファレンスを読み込ませることで、最適なプロンプトを生成させることが目的。

## Purpose

**Target Reader**: Gemini AI (or other LLMs)
**Output**: Veo 3.1 / Grok Imagine compatible prompts
**Language**: English (prompts) / Japanese (documentation)

---

## resources/ Structure

```
resources/
├── image/                    # 静止画生成
│   └── nano-banana-pro/      # Gemini 3 Pro
└── video/                    # 動画生成
    ├── veo/                  # Veo 3.1（高品質・プロ向け）
    │   ├── human-manual/
    │   └── reference/
    └── grok/                 # Grok Imagine（高速・コスト重視）
        └── reference/
```

---

## Veo vs Grok: Which to Use?

| 項目 | Veo 3.1 | Grok Imagine |
|------|---------|--------------|
| **価格** | $0.40-0.75/秒 | $30/月（500本/日） |
| **品質** | プロフェッショナル | 実験・プロトタイプ向け |
| **動画長** | 4-8秒 | 5-15秒 |
| **生成速度** | 数分 | 30秒以下 |
| **ネガティブプロンプト** | 対応 | 非対応 |
| **参照画像** | 最大3枚（Ingredients） | 限定的 |
| **オーディオ** | 対応 | ネイティブ統合 |
| **最適用途** | 最終制作物 | 高速イテレーション |

**推奨:**
- **プロダクション品質** → Veo 3.1
- **実験・プロトタイプ・大量生成** → Grok Imagine
- **静止画生成** → 両者共通で Gemini 3 Pro (Nano Banana Pro)

---

## Image Generation (`resources/image/`)

### nano-banana-pro/

静止画生成（Gemini 3 Pro）のリファレンス。VeoとGrok両方で共通使用。

| File | Description |
|------|-------------|
| `json-schema.md` | JSON構造定義 |
| `keywords.md` | キーワード辞書 |
| `templates/` | ユースケース別テンプレート |

---

## Video: Veo 3.1 (`resources/video/veo/`)

### human-manual/

人間がワークフローを理解するためのガイド（日本語）

| File | Description |
|------|-------------|
| `00-quick-start.md` | 5分で始めるクイックスタート |
| `01-workflow-selector.md` | ユースケース別ワークフロー選択 |
| `troubleshooting.md` | よくある問題と解決策 |
| `image-generation/` | 静止画生成手順 |
| `video-generation/` | 動画生成手順 |
| `extend/` | 動画延長手順 |
| `use-cases/` | ユースケース別詳細ガイド |

### reference/

GeminiがVeo 3.1プロンプトを生成する際のリファレンス（英語）

| File | Description |
|------|-------------|
| `INDEX.md` | **エントリーポイント** |
| `00-system-prompt.md` | Geminiへのロール定義 |
| `json-schema.md` | 動画生成スキーマ |
| `keywords/` | カメラ・ライティング・スタイル |
| `use-case-templates/` | ユースケース別JSONテンプレート |

---

## Video: Grok Imagine (`resources/video/grok/`)

### reference/

GeminiがGrok Imagineプロンプトを生成する際のリファレンス（英語）

| File | Description |
|------|-------------|
| `INDEX.md` | **エントリーポイント** |
| `00-system-prompt.md` | Geminiへのロール定義 |
| `json-schema.md` | **6要素フォーマット・JSONサンプル** |
| `api-parameters.md` | APIパラメータ仕様 |
| `workflows.md` | ワークフローテクニック（Last Frame等） |
| `troubleshooting.md` | トラブルシューティング |
| `spicy-mode.md` | Spicy Mode詳細 |
| `keywords/` | カメラ・ライティング・スタイル・オーディオ |

---

## Usage

### For Humans

1. 作りたい動画のプラットフォーム（Veo/Grok）を選択
2. 該当する `human-manual/00-quick-start.md` を読む
3. Geminiに依頼する際の参考にする

### For Gemini (Veo)

```
resources/video/veo/reference/INDEX.md を読んで、
[ユースケース] のVeo 3.1プロンプトを生成して
```

### For Gemini (Grok)

```
resources/video/grok/reference/INDEX.md を読んで、
[ユースケース] のGrok Imagineプロンプトを生成して
```

---

## Integration for App Development

アプリ開発でプロンプト生成機能を組み込む場合、`reference/` フォルダをプロジェクトに取り込む。

```
your-app/
├── src/
└── prompts/
    ├── image-reference/   ← resources/image/nano-banana-pro/ をコピー
    ├── veo-reference/     ← resources/video/veo/reference/ をコピー
    └── grok-reference/    ← resources/video/grok/reference/ をコピー
```

LLM APIに `INDEX.md` をエントリーポイントとして渡す。`INDEX.md` がユースケースに応じて必要なファイルを指示する。

---

## Workflow Overview

### Veo 3.1 Workflow
```
[Image]                 [Video]                 [Extend]
Nano Banana Pro    →    Veo 3.1            →    Video Extension
(Gemini 3 Pro)          Text-to-Video           8s → longer
                        Image-to-Video
                        Ingredients mode
```

### Grok Imagine Workflow
```
[Image]                 [Video]
Nano Banana Pro    →    Grok Imagine
(Gemini 3 Pro)          Text-to-Video
                        Image-to-Video
                        Native Audio
```

---

## Key Concepts

- **Nano Banana Pro**: Gemini 3 Pro による静止画生成
- **Veo 3.1**: Google の動画生成AI（高品質、4/6/8秒）
- **Grok Imagine**: xAI の動画生成AI（高速、5-15秒、Aurora Engine）
- **6-Component Formula**: Grok用プロンプト構造（Subject + Action + Camera + Lighting + Environment + Audio）
- **Ingredients**: Veo用参照画像によるキャラクター一貫性機能
- **JSON Prompt**: 構造化されたプロンプトフォーマット
- **Last Frame Method**: Grokで長尺動画を作成するテクニック
- **Spicy Mode**: Grokの緩和されたコンテンツモデレーション

---

## docs/ Structure

```
docs/
├── sources/              # 調査資料（収集した生データ）
│   ├── official/         # 公式ドキュメント
│   ├── community/        # コミュニティ情報
│   └── grok/             # Grok Imagine調査資料
├── ask/                  # AI会話ログ（自動保存）
└── log/                  # 作業ログ
```
