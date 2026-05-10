---
inclusion: always
---
# ナレッジ検索システムについて

このワークスペースは、Kiro IDEの機能のみを使ったナレッジ検索システムです。

## 構成

- `docs/` - 元ドキュメント（PDF, DOCX, PPTX, XLSX 等）
- `knowledge/` - 変換済みナレッジベース（Markdown）
- `knowledge/INDEX.md` - ナレッジ全体のインデックス
- `.kiro/skills/` - スキル（ナレッジ検索・一括変換）
- `.kiro/agents/` - サブエージェント（ドキュメント変換）
- `.kiro/steering/` - ステアリング（プロジェクト規約）

## 使い方

1. `/knowledge-search` スキルを使ってナレッジベースに質問する
2. `/knowledge-build` スキルを使って docs/ 内の未変換ドキュメントを一括変換する