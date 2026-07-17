---
paths:
  - "knowledge_base/**"
  - "research_notes/**"
---

# 知識管理の衛生規則

## 命名規則

- 調査ログ: `research_notes/YYYY-MM-DD-<slug>.md`（slug は半角英数とハイフン）
- 確立知識: `knowledge_base/topics/<slug>.md`
- ソース定義: `knowledge_base/sources/domains/<slug>.md`

## 索引の維持

- ファイルを追加したら、**同じ作業の中で**対応する索引に1行追記する（必須手順）:
  - 調査ログ → `research_notes/INDEX.md`
  - 確立知識 → `knowledge_base/INDEX.md`
  - ソース定義 → `knowledge_base/sources/REGISTRY.md`
- 追記フォーマット: `- [YYYY-MM-DD] <タイトル>（確信度: 高/中/低）: <ファイルパス> — 一言要約`
  - 例外: `REGISTRY.md` のみ `- [YYYY-MM-DD] <領域名>: domains/<slug>.md — 適用範囲の一言`（ソース定義には確信度を付さない）
- `knowledge_base/_index_lite.md`（常時ロードされる軽量索引）には見出しレベルの情報のみを追記し、50行以内に保つ。
- 索引の整合性の最終責任は `/archive --reindex` が負う。追記漏れ・リンク切れが疑われたら実行する。

## 昇格（research_notes → knowledge_base）

- 昇格は `/archive` の手続きでのみ行う。自動昇格しない。
- 昇格の目安: 複数の調査で再利用された知見、確信度「高」で安定した知見。
- 昇格時は出典を保持し、元ログの冒頭に「昇格済 → <パス>」と記す。元ログは削除しない。

## 書いてはいけないもの

- 個人情報・私的なソース・認証情報。本リポジトリは**公開前提**である。私的な内容は `CLAUDE.local.md`（gitignore対象）と private repo 側にのみ置く。
- Auto Memory への依存: マシンローカルでgit共有されないため、残すべき知識は必ずリポジトリ内ファイルへ書く。
