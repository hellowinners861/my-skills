# asset-generation-soko

2Dゲームの**素材生成（スプライト/ピクセルアート/タイルセット等）**向けに探してきたスキル候補の保管用コピー（倉庫 = soko）。
現時点では**アクティブなスキルとして有効化していません**。後で参照・お試しするための置き場です。

各フォルダには上流の `SKILL.md`（＝スキル本体の指示書）のみを収録しています。実行に必要なスクリプトや依存は含めていないので、**実際に動かす時は下記の導入コマンドで入れ直してください**。

> ⚠️ `skills.sh` はこの環境の egress ポリシーで 403 ブロック中のため、`npx skills find` は使えません。導入は全て **github URL 直指定**（github は許可済み）で行います。

## 収録候補

### 1. `simota-agent-skills/`（[simota/agent-skills](https://github.com/simota/agent-skills)・★60）
Anthropic Skills 仕様準拠。**外部API不要のものが多く、この環境で最も確実に動く**見込み。2Dゲーム制作に一貫したセット:

| スキル | 用途 | API |
|---|---|---|
| `dot` | 🎨 **ピクセルアート素材生成**（SVG/Canvas/Phaser3/Pillow/CSS）。スプライトシート・タイルマップ | 不要（コード生成） |
| `quest` | 🧍 **ゲーム/キャラ設計**：GDD・コアメカニクス・バランス・レベル・ナラティブ | 不要（設計ドキュメント） |
| `tick` | 🕹 **2D実装**：ゲームループ・ECS・状態・衝突/物理・セーブ/ロード | 不要 |
| `ink` | 🖼 SVGアイコン/イラスト・スプライトシンボル | 不要 |

導入例:
```bash
npx skills add https://github.com/simota/agent-skills --skill dot --skill quest --skill tick --skill ink
```

### 2. `agent-sprite-forge/`（[0x0funky/agent-sprite-forge](https://github.com/0x0funky/agent-sprite-forge)・★3.2k）
プロンプト → スプライトシート/RPGマップ/タイルセット。背景透過・フレーム抽出・GIF出力まで。
`generate2dsprite`（キャラ/エフェクト）と `generate2dmap`（マップ/タイルセット）の2スキル。

- ⚠️ **Codex前提**（エージェント内蔵の画像生成を利用）。Claude Code には内蔵画像生成が無いため、**別途画像生成モデルの用意が必要な可能性**。Python(Pillow/numpy)要
- 上流は `~/.codex/skills/` へコピーする方式。詳細は `agent-sprite-forge/UPSTREAM-README.md`

### 3. `sprite-gen/`（[aldegad/sprite-gen](https://github.com/aldegad/sprite-gen)・★444）
ベース画像＋アクション一覧 → アニメアトラス生成、透過処理・フレーム抽出・`manifest.json`。等角(isometric)対応。
- 画像生成バックエンドは自前で用意。Python3.10+/Pillow。詳細は `sprite-gen/UPSTREAM-README.md`

### 4. `spritecook/`（[SpriteCook/skills](https://github.com/SpriteCook/skills)・★23）
SpriteCook の MCP経由でピクセル/HDアート生成・アニメ・タイルセット・Godot書き出し。
- ⚠️ **SpriteCook の MCPサーバ接続＋クレジット(アカウント)が必要**
```bash
npx skills add https://github.com/SpriteCook/skills
# または: npx spritecook-mcp setup
```

## 参考（今回は未収録）
- [willibrandon/pixel-plugin](https://github.com/willibrandon/pixel-plugin) — Aseprite を自然言語操作。ローカルに **Aseprite（有料アプリ）必須**
- 別倉庫 [`../game-development-soko`](../game-development-soko) — 生成ではなく**アート原則・設計・パイプラインを教える**バンドル（davila7・★28.5k）。補完関係

## 後で有効化したくなったら
Claude Code に認識させるには、対象スキルフォルダを `.claude/skills/` 配下に置く（またはリンク）だけです。ただし上記のうち生成系（sprite-forge / sprite-gen / spritecook）はスクリプトや外部依存が必要なので、**倉庫のコピーではなく導入コマンドで入れ直す**のが確実です。

> 注意: スキルはエージェント権限で動作します。有効化する前に各 SKILL.md の内容を確認してください。
