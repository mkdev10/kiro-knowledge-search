---
name: knowledge-build
description: docs/フォルダ内の未変換ドキュメントをナレッジベースに一括変換するスキル。並列でサブエージェントを呼び出し、全完了後にINDEX.mdを更新する。
---

# ナレッジ一括変換スキル

docs/ フォルダ内の未変換ドキュメントをすべてナレッジベースに変換します。

## 変換ルール

変換ルールの詳細は以下を参照してください：

#[[file:.kiro/skills/knowledge-build/references/conversion-rules.md]]

## 実行手順

### 手順1: 未変換ファイルの特定
docs/ フォルダ内のドキュメントと knowledge/ フォルダ内のMarkdownファイルを比較し、
まだ変換されていないファイルを特定してください。
knowledge/ 内の各Markdownファイルの「元ファイル」フィールドを参照して判定します。

### 手順2: 並列変換
未変換ファイルそれぞれに対して、doc-converter サブエージェント
（invokeSubAgent の name: "doc-converter"）を並列で呼び出してください。

各サブエージェントへのプロンプトには以下を含めること：
- 変換対象のファイルパス
- 「INDEX.mdは更新しないでください」という指示

また、各サブエージェント呼び出しの contextFiles に以下を含めること：
- `.kiro/skills/knowledge-build/references/conversion-rules.md`（変換ルール参照用）

### 手順3: INDEX.md 一括更新
すべてのサブエージェントの処理が完了した後に、
上記の変換ルール内のインデックス更新ルールに従って knowledge/INDEX.md を一括更新してください。

## 注意事項
- 未変換ファイルがない場合は「すべてのドキュメントは変換済みです」と報告してください
- 変換に失敗したファイルがあれば、成功分のINDEX更新は行いつつ、失敗分を報告してください