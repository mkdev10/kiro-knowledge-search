# Kiro ナレッジ検索システム

Kiro IDE の機能（スキル・サブエージェント・ステアリング・MCP）だけを使って構築した、ローカルナレッジベース検索システムです。  
PDF などのドキュメントを Markdown に変換し、自然言語で質問できます。

## 特徴

- **コード不要** — Kiro のスキルとエージェント機能のみで動作
- **ドキュメント一括変換** — PDF / DOCX / PPTX 等を Markdown に自動変換
- **自然言語検索** — ナレッジベースに対して日本語で質問・回答
- **インデックス管理** — 変換済みドキュメントのメタデータを自動管理

## ディレクトリ構成

```
.
├── docs/                  # 元ドキュメント（PDF, DOCX, PPTX 等）
├── knowledge/             # 変換済みナレッジベース（Markdown）
│   └── INDEX.md           # ナレッジ全体のインデックス
└── .kiro/
    ├── agents/            # サブエージェント定義
    │   └── doc-converter.md
    ├── skills/            # スキル定義
    │   ├── knowledge-build/   # ナレッジ一括変換スキル
    │   └── knowledge-search/  # ナレッジ検索スキル
    ├── steering/          # ステアリング（プロジェクト規約）
    └── settings/
        └── mcp.json       # MCP サーバー設定（markitdown）
```

## 前提条件

- [Kiro IDE](https://kiro.dev)
- Python パッケージマネージャー `uv`（markitdown MCP の実行に必要）
  ```bash
  # macOS (Homebrew)
  brew install astral-sh/tap/uv
  ```

## 使い方

### 1. ドキュメントの変換（ナレッジ構築）

`docs/` フォルダにドキュメントを配置し、Kiro のチャットで `/knowledge-build` スキルを呼び出します。

- 未変換のドキュメントを自動検出
- markitdown MCP で Markdown に変換
- `knowledge/` フォルダに保存し、`INDEX.md` を更新

### 2. ナレッジ検索

Kiro のチャットで `/knowledge-search` スキルを呼び出し、自然言語で質問します。

```
/knowledge-search ランサムウェアへの対策を教えて
```

- INDEX.md から関連ファイルを特定
- 該当ナレッジを参照して根拠付きで回答
- 出典（ファイル名・セクション）を明記

## 対応ドキュメント形式

| カテゴリ           | 拡張子                            |
| ------------------ | --------------------------------- |
| ドキュメント       | `.pdf`, `.docx`, `.doc`           |
| プレゼンテーション | `.pptx`                           |
| スプレッドシート   | `.xlsx`, `.xls`, `.csv`           |
| Web・構造化データ  | `.html`, `.json`, `.xml`, `.rss`  |
| メディア           | 画像（EXIF/OCR）, `.wav`, `.mp3`  |
| その他             | `.epub`, `.ipynb`, `.zip`, `.msg` |

## 仕組み

```mermaid
flowchart LR
    A[docs/ にファイル配置] --> B[/knowledge-build スキル]
    B --> C[doc-converter サブエージェント]
    C --> D[markitdown MCP]
    D --> E[knowledge/ に Markdown 保存]
    E --> F[INDEX.md 更新]
    G[ユーザーの質問] --> H[/knowledge-search スキル]
    H --> I[INDEX.md 参照]
    I --> J[関連ファイル読み込み]
    J --> K[根拠付き回答]
```

## ライセンス

MIT
