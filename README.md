# claude-samruk

私家製インテリジェンススタジオ for Claude Code — 調査・分析の結果をテキストとして蓄積する、常駐リサーチ環境フレームワーク。

## 思想

- **モデル分業＝コンテキストエンジニアリング**: 司令塔（メインセッション）は計画・統率・判断に徹し、生データの消費はサブエージェント（ワーカー）のコンテキストに隔離する。分業は節約のためではなく、司令塔のコンテキストを抽象度の高い状態に保つための設計である。
- **知識の二層構造**: 生の調査ログ（`research_notes/`）と、蒸留された確立知識・ソース定義（`knowledge_base/`）を分離し、git 管理で蓄積する。
- **インテリジェンス分析の規律**: BLUF（結論先出し）・ソース品質A〜E評価・確信度明示・反証探索・限界明示・5軸評価（LLM-as-judge）を標準装備する。

## 構成

```
CLAUDE.md                     司令塔憲章（常時ロード。軽量索引を@import）
.claude/
  rules/                      横断規約（品質定義・オーケストレーション規則・知識衛生）
  skills/                     動作モード（quick / research / sources / archive）
  agents/                     ワーカー定義（researcher / scout / synthesizer / verifier）
templates/                    レポート・ソース定義の雛形
knowledge_base/               確立知識・ソース定義 registry・索引
research_notes/               調査ログ（追記型）
```

## 使い方

| コマンド | 用途 |
|---|---|
| `/quick <質問>` | 単純な質問への高速回答（典拠付き） |
| `/research <テーマ>` | Deep Research（計画→ソース定義→並列調査→統合→反証→評価→永続化） |
| `/sources <領域>` | 調査領域ごとの優先ソース定義の作成・更新 |
| `/archive [--reindex]` | 調査ログの蒸留・昇格、索引の再生成 |

## 移植手順（3ステップ）

日常利用は本リポジトリをコピーした private repo で行う想定。

1. **コピー**: リポジトリ全体を移植先へコピーする（テンプレートとして複製、または `git clone` 後にリモートを差し替え）。
2. **個人設定の分離**: `CLAUDE.local.md`（gitignore 対象）を作成し、私的な調査領域・個人的なソース・好みを書く。公開リポジトリ側には個人情報を置かない。
3. **モデルの調整**: 利用可能なモデル階層に合わせて、下表の `model` フィールドを変更する。

### モデル指定の一覧（差し替え箇所）

| ファイル | model | 役割 |
|---|---|---|
| `.claude/agents/researcher.md` | sonnet | 調査実行 |
| `.claude/agents/scout.md` | haiku | 機械的整理 |
| `.claude/agents/synthesizer.md` | opus | 統合・起草 |
| `.claude/agents/verifier.md` | opus | 検証・評価 |
| `.claude/skills/quick/SKILL.md` | sonnet | 高速回答 |
| `.claude/skills/sources/SKILL.md` | sonnet | ソース定義 |
| `.claude/skills/archive/SKILL.md` | haiku | 索引整備 |

`/research` はモデル指定を持たない（司令塔＝メインセッションのモデルで統率する）。

## 公開性の注意

本リポジトリは公開を前提とし、フレームワークのみを含む。個人情報・私的ソース・認証情報は `CLAUDE.local.md` と private repo 側にのみ置くこと（`.claude/rules/knowledge-hygiene.md` 参照）。
