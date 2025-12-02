# Veo 3.1 Prompt Generation Manual

Google Veo 3.1 動画生成のためのプロンプトマニュアル。GeminiなどのAIにこのリファレンスを読み込ませることで、最適なプロンプトを生成させることが目的。

## Purpose

**Target Reader**: Gemini AI
**Output**: Veo 3.1 compatible JSON prompts
**Language**: English (prompts) / Japanese (documentation)

## resources/ Structure

```
resources/
├── human-manual/     # 人間向けマニュアル（日本語）
└── reference/        # AI向けリファレンス（英語）
```

### human-manual/

**目的**: 人間がワークフローを理解するためのガイド

| File | Description |
|------|-------------|
| `00-quick-start.md` | 5分で始めるクイックスタート |
| `01-workflow-selector.md` | ユースケース別ワークフロー選択 |
| `veo3.1-prompt-manual.md` | 総合マニュアル |
| `troubleshooting.md` | よくある問題と解決策 |
| `phase1-image/` | 静止画生成（Nano Banana Pro）手順 |
| `phase2-video/` | 動画生成（Veo 3.1）手順 |
| `phase3-extend/` | 動画延長・編集手順 |
| `use-cases/` | ユースケース別詳細ガイド |

### reference/

**目的**: GeminiがVeo 3.1プロンプトを生成する際に参照するリファレンス

| File | Description |
|------|-------------|
| `INDEX.md` | **エントリーポイント** - Geminiが最初に読むファイル |
| `00-system-prompt.md` | Geminiへのロール定義・出力フォーマット |
| `phase1-nano-banana/` | 静止画生成のJSONスキーマ・キーワード・テンプレート |
| `phase2-veo/` | 動画生成のJSONスキーマ・APIパラメータ・キーワード辞書 |
| `phase3-extend/` | 動画延長のスキーマ・トランジション定義 |
| `use-case-templates/` | ユースケース別JSONテンプレート |

## Usage

### For Humans

1. `resources/human-manual/00-quick-start.md` を読む
2. 作りたい動画に応じて `use-cases/` から該当ガイドを参照
3. Geminiに依頼する際の参考にする

### For Gemini

Geminiに以下のように指示する：

```
resources/reference/INDEX.md を読んで、
[ユースケース] のVeo 3.1プロンプトを生成して
```

`INDEX.md`が必要なファイルのみを選択的にロードする。

## Workflow Overview

```
[Phase 1: Image]        [Phase 2: Video]        [Phase 3: Extend]
Nano Banana Pro    →    Veo 3.1            →    Video Extension
(optional)              Text-to-Video           8s → longer
                        Image-to-Video
                        Ingredients mode
```

## Integration for App Development

アプリ開発でVeo 3.1プロンプト生成機能を組み込む場合、`resources/reference/` フォルダをプロジェクトに取り込んで使用すると効果的。

```
your-app/
├── src/
└── prompts/
    └── veo-reference/    ← resources/reference/ をコピー
        ├── INDEX.md
        ├── 00-system-prompt.md
        └── ...
```

LLM APIに `INDEX.md` をエントリーポイントとして渡す。`INDEX.md` がユースケースに応じて必要なファイルを指示するので、それに従ってコンテキストを構築する。

## Key Concepts

- **Nano Banana Pro**: Gemini 3 Pro による静止画生成
- **Veo 3.1**: Google の動画生成AI（4/6/8秒）
- **Ingredients**: 参照画像を使ったキャラクター一貫性機能
- **JSON Prompt**: 構造化されたプロンプトフォーマット
