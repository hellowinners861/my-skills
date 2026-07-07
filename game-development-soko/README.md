# game-development-soko

2Dゲーム制作向けに探してきた **game-development スキルバンドル**の保管用コピー（倉庫 = soko）。
現時点では**アクティブなスキルとして有効化していません**。後で参照・お試しするための置き場です。

## 出所

- リポジトリ: [`davila7/claude-code-templates`](https://github.com/davila7/claude-code-templates)（★28.5k）
- 元パス: `cli-tool/components/skills/creative-design/game-development/`
- 取得コマンド: `npx skills add https://github.com/davila7/claude-code-templates --skill game-development`

## 中身

`game-development`（オーケストレーター）が、状況に応じて以下のサブスキルへ振り分けます。

| サブスキル | 用途 |
|---|---|
| `game-art` | 素材作成：ビジュアルスタイル選定・アセットパイプライン・アニメワークフロー |
| `game-design` | キャラデザ/設計：GDD・バランス・プレイヤー心理・進行設計・コアループ |
| `2d-games` | 2D実装：スプライト/アトラス・タイルマップ・物理・カメラ |
| `game-audio` | サウンド：効果音・BGM統合・アダプティブ音響 |
| `web-games` / `mobile-games` / `3d-games` / `multiplayer` / `pc-games` / `vr-ar` | 各プラットフォーム別 |

## 後で有効化したくなったら

Claude Code に認識させるには、`.claude/skills/` 配下に置く（またはリンクする）だけです。例:

```bash
# このリポジトリのルートで
mkdir -p .claude/skills
ln -s ../../game-development-soko .claude/skills/game-development
```

または改めて Skills CLI で入れ直す:

```bash
npx skills add https://github.com/davila7/claude-code-templates --skill game-development
```

> 注意: スキルはエージェント権限で動作します。有効化する前に各 SKILL.md の内容を確認してください。
