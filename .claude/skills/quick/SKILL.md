---
name: quick
description: 単純な質問に典拠付きで高速回答する。事実確認・定義・単発の調べ物向け。多段調査はしない。複雑な問いは /research を使う。
argument-hint: <質問>
model: sonnet
allowed-tools: WebSearch, WebFetch, Read, Grep, Glob
---

# /quick — 高速回答（典拠付き）

単発の問いに、最小の調査で典拠付きの回答を返す。

## 手順

1. **既知の確認**: `knowledge_base/_index_lite.md` に関連トピックがあれば該当ファイルを読む。既存知識で答えられるならそれを典拠として即答する。
2. **調査**: WebSearch / WebFetch で1〜3ソースを確認する。サブエージェントは起動しない。
3. **回答**: `templates/report_quick.md` の形式（BLUF・典拠・確信度）で回答する。品質・確信度の定義は `.claude/rules/source-quality.md` に従う。
4. **保存判定**: 再利用価値のある新しい知見が得られた場合のみ、`templates/research_note.md` 形式での `research_notes/` への保存を**提案**する（自動保存はしない。保存した場合は INDEX に追記する）。
5. **エスカレーション**: 調査中にサブクエスチョンが2個以上に分解されると判明したら、深追いせず現時点の要点を示した上で `/research` の利用を提案する。
