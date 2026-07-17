---
name: sources
description: 調査領域ごとの優先ソース定義（一次資料・権威あるデータベース・品質の目安）を作成・更新し、knowledge_base/sources/ に蓄積する。/research の前提整備。
argument-hint: <領域名>
model: sonnet
allowed-tools: WebSearch, WebFetch, Read, Write, Edit, Glob, Grep
---

# /sources — 領域別ソース定義

調査領域について「どこを見るべきか」を先に定義し、以後の調査をそれに従わせる。

## 手順

1. **既存確認**: `knowledge_base/sources/REGISTRY.md` を読み、対象領域の定義が既にあれば読み込んで差分更新モードにする。
2. **ソース調査**: 領域について次を調査して列挙する。
   - (a) 一次資料の所在
   - (b) 権威ある機関・データベース
   - (c) 定評ある二次資料
   - (d) 避けるべき低品質ソース
3. **品質割当**: 各ソースに `.claude/rules/source-quality.md` の A〜E 評価と選定理由を付す。
4. **保存**: `templates/source_domain.md` の形式で `knowledge_base/sources/domains/<slug>.md` に保存し、`REGISTRY.md` と `knowledge_base/_index_lite.md` に1行追記する。

## /research からの利用

/research 実行中に対象領域の定義が無い場合、司令塔はこの手続きを researcher ワーカーに委譲してよい（その場合も本手順と保存先に従わせる）。
