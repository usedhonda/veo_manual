# トラブルシューティング

## よくある問題と解決策

---

## カメラ関連

### 問題: カメラが動かない

**症状**: `tracking shot`と指定したのに固定ショットになる

**解決策**:
1. `static`や`locked`などの矛盾する指示がないか確認
2. より具体的に指定: `tracking shot following subject left to right`
3. 動きのスピードも指定: `slow tracking shot`

### 問題: カメラが速すぎる/遅すぎる

**症状**: 意図した速度と異なる

**解決策**:
1. 明示的にスピードを指定:
   - `very slow` - 非常にゆっくり
   - `slow` - ゆっくり（推奨）
   - `normal` - 通常
   - `fast` - 速い
2. 「slow」を付けた動きの方が安定: `slow dolly in` > `dolly in`

### 問題: 複数の動きが混ざる

**症状**: パンしながらズームするなど意図しない複合動作

**解決策**:
1. **1クリップ1動作の原則**: `pan`と`zoom`を同時指定しない
2. 複合動作が必要なら別クリップに分ける
3. ネガティブに追加: `unexpected camera movement`

---

## 人物/キャラクター関連

### 問題: 顔が歪む/変形する

**症状**: 途中で顔の形が変わる

**解決策**:
1. ネガティブに追加:
   ```
   "morphing", "deformed face", "distorted features"
   ```
2. 顔の極端なアップを避ける（ミディアムショット推奨）
3. 動きを控えめに

### 問題: 手や指がおかしい

**症状**: 指が6本ある、関節が変

**解決策**:
1. ネガティブに追加:
   ```
   "extra fingers", "extra limbs", "bad anatomy", "wrong proportions"
   ```
2. 手のクローズアップを避ける
3. 手が画面外になる構図を選ぶ

### 問題: 服装が変わる

**症状**: シーン途中で服のデザインが変わる

**解決策**:
1. 服装を詳細に記述:
   ```
   "white blouse with navy collar, red ribbon tie, navy pleated skirt"
   ```
2. Ingredientsモードで参照画像を使用
3. ネガティブに追加: `costume change`, `different outfit`

### 問題: キャラの一貫性がない（アニメ）

**症状**: 同じキャラなのにシーンごとに違って見える

**解決策**:
1. **必ずIngredientsモードを使用**
2. キャラクターシートを参照画像として指定
3. 毎回キャラの特徴を再記述
4. ネガティブに追加: `off-model`, `inconsistent style`

---

## スタイル関連

### 問題: アニメなのにリアルになる

**症状**: anime指定なのに実写風になる

**解決策**:
1. スタイルを強く指定:
   ```json
   "style": {
     "medium": "anime",
     "sub_style": "Japanese anime, cel-shaded, 2D animation"
   }
   ```
2. ネガティブに追加:
   ```
   "realistic", "photorealistic", "3D render", "CGI"
   ```

### 問題: 意図したスタイルにならない

**症状**: 「サイバーパンク」と言ったのに違う雰囲気

**解決策**:
1. より具体的に記述:
   ```
   "cyberpunk aesthetic: neon lights (cyan and magenta),
   rain-slicked streets, holographic ads, dark atmosphere"
   ```
2. 参考作品を挙げる: `Blade Runner inspired`
3. カラーパレットを明示

### 問題: 色が意図と違う

**症状**: 暖かい雰囲気なのに青っぽい

**解決策**:
1. 色温度を指定: `warm color temperature`, `golden tones`
2. カラーグレードを指定: `warm color grade`, `orange and teal`
3. 時間帯を合わせる: `golden_hour`で暖色、`blue_hour`で寒色

---

## 音声関連

### 問題: 勝手にBGMが入る

**症状**: 指定していないのに音楽が生成される

**解決策**:
1. 明示的に禁止:
   ```json
   "music": "NO music, ambient sounds only"
   ```
2. または: `"music": "silence"`

### 問題: 台詞が不自然

**症状**: リップシンクがずれる、声が変

**解決策**:
1. 台詞を短くする（長すぎると問題）
2. 声のスタイルを指定:
   ```
   "Character says (calm, deep male voice): '...'"
   ```
3. 台詞なしにして後から音声を追加

### 問題: 環境音がない/おかしい

**症状**: 街中なのに静か

**解決策**:
1. アンビエンスを詳細に:
   ```
   "Ambience: busy city street, traffic noise, pedestrian chatter, distant horns"
   ```
2. 効果音も追加:
   ```
   "SFX: footsteps on concrete, car passing"
   ```

---

## 技術的問題

### 問題: 生成が失敗する

**症状**: エラーが返ってくる

**原因と対策**:
| エラー | 原因 | 対策 |
|--------|------|------|
| INVALID_ARGUMENT | パラメータが不正 | aspectRatio, durationを確認 |
| RESOURCE_EXHAUSTED | レート制限 | 待ってリトライ |
| INTERNAL | モデルエラー | リトライ、プロンプト簡略化 |
| SAFETY | コンテンツフィルター | プロンプト見直し |

### 問題: 解像度が低い

**症状**: 720pしか出ない

**解決策**:
1. Video Extension使用時は720p固定（制約）
2. それ以外なら `resolution: "1080p"` を確認
3. 標準モデル（not fast）を使用

### 問題: 生成に時間がかかりすぎる

**対策**:
1. プロトタイプは `veo-3.1-fast` を使用
2. 720pで先にテスト
3. 複雑なプロンプトを簡略化

---

## Ingredientsモード特有

### 問題: 参照画像が効いていない

**症状**: 参照画像のキャラと違うものが出る

**解決策**:
1. 参照画像の品質を確認（クリアで見やすいか）
2. `referenceType: "asset"` を確認（`style`は非対応）
3. プロンプトで参照画像を明示的に言及:
   ```
   "Using the character from reference image..."
   ```

### 問題: 参照画像が3枚以上必要

**症状**: 複数キャラを出したいが制限がある

**対策**:
1. 最大3枚の制限を守る
2. 複数キャラを1枚のシートにまとめる
3. 優先度の高いキャラのみ参照画像を使用

---

## 延長（Extension）特有

### 問題: 延長がうまく繋がらない

**症状**: 延長部分で不連続になる

**解決策**:
1. ソース動画の終了状態を詳しく記述
2. 一貫性要素を再記述:
   ```
   "Continuing seamlessly: same lighting, same character appearance,
   same camera style, same environment"
   ```
3. ネガティブに追加:
   ```
   "discontinuity", "jump cut", "sudden change"
   ```

### 問題: 720pしか出ない

**説明**: Video Extensionは720p固定です。これは制約であり、回避できません。

---

## 一般的なベストプラクティス

### プロンプトの書き方

1. **具体的に**: 曖昧な表現を避ける
2. **一貫性を持たせる**: 矛盾する指示を避ける
3. **優先順位をつける**: 重要な要素を最初に
4. **テストファースト**: fastモデルで先に確認

### ネガティブプロンプトの活用

最低限含めるべき:
```
blur, distortion, low quality, watermark, text overlay
```

人物の場合追加:
```
morphing, deformed, extra limbs, bad anatomy
```

アニメの場合追加:
```
realistic, photorealistic, 3D render, off-model
```

### 段階的アプローチ

1. シンプルなプロンプトから始める
2. 問題があれば一つずつ調整
3. 大幅な変更は別プロンプトとして試す
4. うまくいったパターンを記録

---

## サポートリソース

- **キーワード辞書**: `gemini-reference/phase2-veo/keywords/`
- **テンプレート**: `gemini-reference/phase2-veo/templates/`
- **API仕様**: `gemini-reference/phase2-veo/api-parameters.md`
