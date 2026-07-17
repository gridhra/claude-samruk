---
name: archive
description: research_notes の調査ログを knowledge_base の確立知識へ蒸留・昇格し、索引を整備する。--reindex で全索引を実ファイルから再生成する。
argument-hint: "[<トピック> | --reindex]"
model: haiku
allowed-tools: Read, Write, Edit, Glob, Grep
---

# /archive — 蒸留・昇格・索引整備

## `--reindex`（索引再生成）

1. `research_notes/` と `knowledge_base/` の実ファイルを列挙する。
2. 各索引（`research_notes/INDEX.md`・`knowledge_base/INDEX.md`・`knowledge_base/sources/REGISTRY.md`）を実ファイルに基づき再生成する。knowledge-hygiene 規則の1行フォーマットに従う。
3. `knowledge_base/_index_lite.md` を再構築する（見出しレベルのみ・50行以内）。
4. 索引にあるが実体のないエントリ、実体があるが索引にないファイルを検出し、報告する。

## `<トピック>`（蒸留・昇格）

判断を要する工程のため、司令塔・ユーザーの確認を取りながら進める。

1. 指定トピックに関連する調査ログを `research_notes/INDEX.md` から特定して読む。
2. 確信度「高」で安定した知見を抽出し、出典を保持したまま `knowledge_base/topics/<slug>.md` に統合する（既存ファイルがあれば重複を統合する）。
3. 元ログの冒頭に「昇格済 → <パス>」を追記する（削除はしない）。
4. `knowledge_base/INDEX.md` と `_index_lite.md` に追記する。

## 肥大対策

蒸留の際、古く確信度の低いログを見つけたら、INDEX 上の「アーカイブ」節への移動を提案する（ファイルの削除はしない）。
