# Copilot Instructions — tomokusaba/qiita

## リポジトリ概要

このリポジトリは [Qiita CLI](https://github.com/increments/qiita-cli) で管理する技術ブログ記事のソースです。

| パス | 内容 |
|---|---|
| `public/*.md` | 公開・下書き記事（20 文字 16 進 basename） |
| `.github/agents/` | カスタムエージェント定義 |
| `.github/skills/` | スキル定義 |

---

## 記事執筆のルール（必読）

### フロントマター

```yaml
---
title: "..."
tags:
  - Tag1   # 3〜5 個
private: false
updated_at: ""        # 新規記事は空文字のまま
id: null              # 新規記事は null のまま
organization_url_name: null
slide: false
ignorePublish: false
---
```

### 文体・構成
- **敬体（です・ます調）**、一人称「私」
- 対話的な呼びかけを適度に入れる
- 絵文字は **見出し末尾か段落末尾に 1〜2 個**、1 段落に 3 個以上入れない
- 「いかがでしたでしょうか」などの定型句で締めない
- 全コードブロックに **言語名を必ず付ける**
- 全画像に **意味のある alt テキスト**を書く

### Microsoft 系記事の必須事項
- 一次情報は `learn.microsoft.com` / `devblogs.microsoft.com` を参照
- Microsoft Learn URL には必ず **`?WT.mc_id=DT-MVP-5004827`** を付与する
- 未検証の API・仕様は書かない。不明な箇所は `<!-- TODO: 一次情報で要確認 -->` を残す

### ファイル作成
- **必ず `npx qiita new <basename>` で作成する**。手動でファイルを作らない
- `npx qiita publish ...` はユーザーが手動で実行する（エージェントは実行しない）

---

## 利用可能なカスタムエージェント

| エージェント | 用途 |
|---|---|
| `qiita-article-orchestrator` | 記事を完成品まで仕上げるオーケストレーター（執筆→レビュー→修正ループ） |
| `qiita-tech-writer` | Qiita 記事ドラフト執筆（新規・リライト） |
| `japanese-proofreader` | 日本語推敲（文体・表記ゆれ・冗長表現） |
| `narrative-flow-reviewer` | 構成・論理展開レビュー |
| `primary-source-fact-checker` | 一次情報によるファクトチェック |

**記事を仕上げる場合は `qiita-article-orchestrator` を呼ぶ。** 個別フェーズだけ実行したいときに各専門エージェントを直接呼ぶ。

---

## Fluent UI 記事シリーズ（再利用コンテキスト）

このリポジトリには Fluent UI 2 コンポーネント解説記事が多数あります（`public/` 参照）。

- **対象**: Fluent UI React v9（`@fluentui/react-components`）と Fluent UI Blazor 5 の比較
- **構成テンプレート**: はじめに → Fluent UI 2 とは → コンポーネント概要 → ガイダンス・レイアウト → アクセシビリティ → Fluent UI Blazor 5 との違い → まとめ
- **MCP ツール**: `Fluent-UI-Blazor-5-get_component_details` / `Fluent-UI-Blazor-5-search_icons` 等を積極利用
- **参考 URL**: `https://fluent2.microsoft.design/` / `https://fluentui-blazor-v5.azurewebsites.net/`
- 毎回「Fluent UI 2 とはセクション」と「これまでのシリーズ記事一覧」を `public/` から検索して収録する

---

## ツール使用優先順位（コスト削減）

### ファイル検索
1. built-in **`grep`** ツール（ファイル内テキスト検索）
2. built-in **`glob`** ツール（ファイルパターン検索）
3. built-in **`view`** ツール（ファイル内容参照）
4. `powershell` / `rg` はどうしても必要な場合のみ

> `bash`/`powershell` 経由の `rg` や `cat` はコンテキストに生テキストが流れ込む。built-in ツールを優先すること。

### コンテキスト肥大化の防止
- **長いセッションでは `/compact` を活用する**（目安: 20〜30 ターン経過後、または MCP 調査フェーズ完了後）
- Fluent UI 記事セッションは MCP 調査が終わったタイミングで `/compact` を実行してから執筆フェーズへ移行する
- 2,000 字を超えるテキストはペーストせずファイルに保存してパスを渡す

### モデル選択
- 初稿執筆・技術調査: デフォルトモデル
- 反復編集・校正・フォーマット整理: `/model gpt-5.4-mini` に切り替えてコストを抑える
