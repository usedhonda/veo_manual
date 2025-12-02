# 音声統合ガイド

## 概要

Veo 3.1の音声生成機能を活用するためのガイドです。

**Veo 3.1の音声機能**:
- 台詞の生成（リップシンク対応）
- 効果音（SFX）の生成
- 環境音（アンビエンス）の生成
- BGM/音楽の生成

---

## 音声指示の基本形式

### 4つの音声カテゴリ

```
┌─────────────────────────────────────────────────────────────┐
│ Veo 3.1 音声カテゴリ                                        │
│                                                             │
│  1. Dialogue（台詞）                                        │
│     └→ キャラクターの発話、リップシンク                    │
│                                                             │
│  2. SFX（効果音）                                           │
│     └→ 具体的なアクション音、環境からの音                  │
│                                                             │
│  3. Ambience（環境音）                                      │
│     └→ 背景の持続的な音、場の雰囲気                        │
│                                                             │
│  4. Music（音楽）                                           │
│     └→ BGM、スコア、楽曲                                   │
└─────────────────────────────────────────────────────────────┘
```

---

## 台詞（Dialogue）の指定

### 基本形式

```
Character says: "台詞の内容"
```

### 声のスタイル指定

```
【形式】
Character says (スタイル修飾子): "台詞"

【修飾子の例】
- calm: 穏やか
- excited: 興奮
- whisper: ささやき
- shouting: 叫び
- sad: 悲しげ
- confident: 自信に満ちた
```

### 声の特徴指定

```
【性別・年齢】
- male voice / female voice
- young / adult / elderly
- child voice

【声質】
- deep: 低い
- high-pitched: 高い
- husky: ハスキー
- soft: 柔らかい
- rough: 荒い

【感情】
- emotional: 感情的
- monotone: 単調
- cheerful: 明るい
- serious: 真剣
```

### 台詞の例

```json
{
  "audio": {
    "dialogue": "Woman says (soft, young female voice): 'I've been waiting for this moment.'"
  }
}
```

```json
{
  "audio": {
    "dialogue": "Man says (deep, confident male voice): 'This is just the beginning.'"
  }
}
```

```json
{
  "audio": {
    "dialogue": "Child says (excited, high-pitched): 'Look at that!'"
  }
}
```

---

## 効果音（SFX）の指定

### 基本形式

```
SFX: 効果音の説明
```

### カテゴリ別の例

#### 人物関連

```
【動作音】
- SFX: footsteps on concrete
- SFX: running footsteps on grass
- SFX: clothing rustling
- SFX: breathing heavily

【インタラクション】
- SFX: door opening/closing
- SFX: glass shattering
- SFX: button click
- SFX: keyboard typing
```

#### 自然・環境

```
【自然現象】
- SFX: thunder rumbling
- SFX: rain hitting window
- SFX: wind howling
- SFX: leaves rustling

【動物】
- SFX: birds chirping
- SFX: dog barking
- SFX: cat meowing
```

#### 機械・テクノロジー

```
【乗り物】
- SFX: car engine starting
- SFX: motorcycle passing
- SFX: train approaching

【電子機器】
- SFX: phone notification
- SFX: computer startup sound
- SFX: camera shutter
```

#### アクション

```
【衝撃】
- SFX: punch impact
- SFX: explosion
- SFX: crash

【武器】
- SFX: sword clash
- SFX: gunshot
- SFX: arrow whoosh
```

---

## 環境音（Ambience）の指定

### 基本形式

```
Ambience: 環境の説明
```

### 場所別の例

#### 自然環境

```
【森林】
Ambience: forest sounds, birds singing, leaves rustling, distant stream

【海岸】
Ambience: ocean waves, seagulls, gentle breeze

【山】
Ambience: mountain wind, distant eagles, echoing silence
```

#### 都市環境

```
【繁華街】
Ambience: busy city street, traffic noise, pedestrian chatter, distant horns

【静かな住宅街】
Ambience: suburban neighborhood, occasional car passing, dogs barking in distance

【夜の街】
Ambience: quiet city night, distant traffic, occasional siren
```

#### 室内環境

```
【オフィス】
Ambience: office sounds, keyboard typing, air conditioning hum, muted conversations

【カフェ】
Ambience: cafe atmosphere, coffee machine, quiet chatter, soft background music

【家庭】
Ambience: home interior, clock ticking, refrigerator hum, muffled TV
```

---

## 音楽（Music）の指定

### 基本形式

```
Music: ジャンル, ムード, 楽器
```

### ジャンル別の例

```
【オーケストラ】
Music: orchestral, epic, triumphant, full orchestra

【エレクトロニック】
Music: electronic, ambient, pulsing synths, minimal

【ピアノ】
Music: solo piano, melancholic, slow tempo

【ロック】
Music: rock, energetic, driving guitars, powerful drums

【ジャズ】
Music: jazz, smooth, saxophone, late night feel
```

### ムードの指定

```
【感情】
- triumphant: 勝利感
- melancholic: 憂鬱
- uplifting: 高揚
- tense: 緊張
- peaceful: 平和
- mysterious: 神秘的
- romantic: ロマンチック

【テンポ】
- slow tempo
- moderate pace
- fast-paced
- building intensity
```

### 音楽を止める場合

```json
{
  "audio": {
    "music": "NO music, ambient sounds only"
  }
}
```

または

```json
{
  "audio": {
    "music": "silence"
  }
}
```

---

## 音声の組み合わせ

### 完全な音声指定

```json
{
  "audio": {
    "dialogue": "Woman says (calm, soft voice): 'The sun is setting.'",
    "sfx": "SFX: gentle waves, seagulls calling",
    "ambience": "Ambience: beach at sunset, ocean breeze, distant children laughing",
    "music": "Music: acoustic guitar, peaceful, warm"
  }
}
```

### レイヤリングのコツ

```
【優先順位】
1. 台詞（最前面）- 明瞭に聞こえる
2. 重要なSFX - アクションに合わせて
3. 音楽 - 背景として
4. アンビエンス - 最背面

【バランス】
- 台詞がある場合は音楽を控えめに
- アクションシーンはSFXを優先
- 静かなシーンはアンビエンス重視
```

---

## 用途別の推奨設定

### 製品CM

```json
{
  "audio": {
    "sfx": "SFX: subtle whoosh, satisfying click",
    "music": "Music: modern electronic, minimal, premium feel"
  }
}
```

### アニメシーン（会話）

```json
{
  "audio": {
    "dialogue": "Character says (emotional): '...'",
    "ambience": "Ambience: quiet classroom, distant birds",
    "music": "NO music"
  }
}
```

### MV（パフォーマンス）

```json
{
  "audio": {
    "dialogue": "Singer says: 'Lyrics here...'",
    "sfx": "SFX: stage reverb, crowd cheering",
    "music": "Music: [ジャンル], energetic"
  }
}
```

### 風景動画

```json
{
  "audio": {
    "ambience": "Ambience: mountain morning, birds, gentle wind",
    "music": "Music: orchestral, majestic, building"
  }
}
```

---

## トラブルシューティング

### 問題: 勝手にBGMが入る

```
【対策】
明示的に禁止:
"music": "NO music, ambient sounds only"
または
"music": "silence"
```

### 問題: リップシンクがずれる

```
【対策】
1. 台詞を短くする
2. 声のテンポを指定
3. 複雑な口の動きを避ける
```

### 問題: SFXが聞こえない

```
【対策】
1. 具体的に記述
2. タイミングを明示
3. 「prominent」「clear」を追加
```

### 問題: 音が多すぎて混乱

```
【対策】
1. 要素を減らす
2. 優先順位を決める
3. 最も重要な音のみに絞る
```

---

## ベストプラクティス

### 1. 具体的に記述

```
【悪い例】
"sfx": "SFX: sounds"

【良い例】
"sfx": "SFX: glass shattering on concrete floor"
```

### 2. シーンに合わせる

```
【整合性】
- 室内なのに屋外の環境音は不自然
- 夜なのに鳥の声は不自然
- 静かなシーンに激しい音楽は不適切
```

### 3. 感情を補強

```
【例】
悲しいシーン:
- 音楽: melancholic, slow
- アンビエンス: quiet, empty feel
- SFX: 控えめ

嬉しいシーン:
- 音楽: uplifting, bright
- アンビエンス: lively, warm
- SFX: 明るい効果音
```

---

## 次に読む

- **動画を延長したい**: `../phase3-extend/01-video-extension.md`
- **MVを作りたい**: `../use-cases/music-video.md`
- **トラブルシューティング**: `../troubleshooting.md`
