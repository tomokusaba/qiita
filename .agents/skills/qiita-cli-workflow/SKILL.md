---
name: qiita-cli-workflow
description: Qiita CLI を使って記事ファイルを安全に生成・確認するためのスキル。依存関係未導入時の対処、basename 生成、new 実行、生成確認、不要な lockfile 変更の扱いを定義する。
---

# Qiita CLI 記事生成ワークフロー スキル

このスキルは、このリポジトリで **Qiita CLI を使って新規記事を作成するときの実務フロー** を定義します。`npx qiita new` を実行する前提確認から、記事ファイルの生成確認、不要な差分の後始末までを一貫して扱います。

---

## 1. いつ使うか

次のような依頼を受けたときに、このスキルを先に参照します。

- 「新規記事を作って」
- 「Qiita CLI で記事ファイルを切って」
- 「記事のひな形を作ってから本文を書いて」
- `npx qiita new` を使う前提の作業全般

本文執筆そのもののトーン・構成・引用ルールは [`write-qiita-article`](../write-qiita-article/SKILL.md) に従います。  
このスキルは **CLI 操作とファイル生成の流れ** に限定します。

---

## 2. 基本方針

1. **手書きで `public/*.md` を作らない**。必ず Qiita CLI で生成する。
2. 20 文字の 16 進 basename を使い、既存ファイル名の慣習に合わせる。
3. `npx qiita new <basename>` が失敗したら、まず **依存関係未導入** を疑う。
4. CLI を動かすためだけに `npm install` した場合、ユーザーから依存更新を求められていない限り、**意図しない `package-lock.json` の差分は戻す**。
5. `publish` は明示依頼があるまで実行しない。

---

## 3. 推奨ワークフロー

### Step 1: 事前確認

最初に次を確認します。

- `package.json` に `@qiita/qiita-cli` があるか
- `.\node_modules\.bin\qiita` が存在するか
- すでに未コミット差分がある場合、今回の作業対象と衝突しないか

PowerShell 例:

```powershell
Set-Location '<repo-root>'
Test-Path .\node_modules\.bin\qiita
```

### Step 2: Qiita CLI が未導入なら依存関係を入れる

`Test-Path` が `False` の場合は、リポジトリ直下で依存関係を入れます。

```powershell
Set-Location '<repo-root>'
npm install --quiet
```

`npx qiita new ...` 実行時に `npm error could not determine executable to run` が出た場合も、まずこの状態を疑ってください。

:::message
このリポジトリでは `package.json` に `@qiita/qiita-cli` が定義されていても、`node_modules` が無ければ `npx qiita new` は失敗します。
:::

### Step 3: basename を生成する

basename は **20 文字の 16 進文字列** を使います。既存ファイルとの衝突を避けるため、`public/<basename>.md` の存在確認まで含めて生成します。

```powershell
$basename = node -e "const fs=require('fs'); const path=require('path'); const crypto=require('crypto'); let id; do { id = crypto.randomBytes(10).toString('hex'); } while (fs.existsSync(path.join('public', id + '.md'))); process.stdout.write(id);"
```

### Step 4: Qiita CLI で記事ファイルを生成する

```powershell
npx qiita new $basename
```

成功したら `public/<basename>.md` が生成されます。

### Step 5: 生成結果を確認する

少なくとも次の 2 点を確認します。

1. `git status --short` に `?? public/<basename>.md` が出る  
2. 生成された Markdown に Qiita の標準フロントマターが入っている

PowerShell 例:

```powershell
git --no-pager status --short
Get-Content ".\public\$basename.md"
```

### Step 6: 不要な差分を後始末する

CLI を動かすためだけに `npm install` を実行し、その結果 `package-lock.json` に差分が出た場合は、依存更新が今回の目的でない限り戻します。

```powershell
git restore --source=HEAD -- package-lock.json
```

---

## 4. 失敗時の対処

| 症状 | 原因候補 | 対処 |
|------|----------|------|
| `npm error could not determine executable to run` | `node_modules` 未導入 | `npm install --quiet` を実行して再試行 |
| `public/<basename>.md` が生成されない | CLI 実行失敗、または basename 競合 | エラーメッセージを確認し、basename を再生成 |
| `package-lock.json` だけ変更された | 依存解決の副作用 | 依存更新が目的でなければ restore |

---

## 5. このスキルの完了条件

次の状態になっていれば、このスキルの目的は達成です。

- `public/<basename>.md` が Qiita CLI で生成されている
- 生成ファイル以外の不要な差分が残っていない
- 本文執筆に進める状態になっている

執筆ルールやフロントマターの整形、構成作りは [`write-qiita-article`](../write-qiita-article/SKILL.md) に引き継ぎます。
