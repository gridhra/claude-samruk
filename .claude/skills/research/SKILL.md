---
name: research
description: 複雑な問いへのDeep Research。計画→ソース定義→並列調査→統合→反証→評価→永続化のサイクルを司令塔が統率する。単純な質問は /quick を使う。
argument-hint: <調査テーマ>
---

# /research — Deep Research

司令塔（メインセッション）が本手続きを直接オーケストレーションする。ワーカーの編成・起動数は `.claude/rules/research-orchestration.md`、品質規約は `.claude/rules/source-quality.md` に従う。

**実行前に必ず同ディレクトリの `phases.md` を読み、各フェーズの手順に従うこと。**

## フェーズ概要

| Phase | 内容 | 実行主体 |
|---|---|---|
| 0 | 計画: 問いの分解・既知の除外・複雑度判定 | 司令塔 |
| 1 | ソース定義の確認（無ければ `/sources` 手続きで作成） | 司令塔 → researcher |
| 2 | 並列調査ファンアウト | researcher ×N |
| 3 | 統合・起草 | synthesizer |
| 4 | 反証探索 | researcher |
| 5 | 5軸評価（未達なら差し戻し） | verifier |
| 6 | 永続化・索引追記 | 司令塔 |

## 成果物

- `research_notes/YYYY-MM-DD-<slug>.md`（`templates/report_full.md` 形式）
- `research_notes/INDEX.md` への1行追記
