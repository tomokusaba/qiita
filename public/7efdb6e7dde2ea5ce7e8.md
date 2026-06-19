---
title: Fluent UI 2 の Spin button を理解する — Slider との違い、Fluent UI Blazor 5 の Number / StepButtons 比較とアクセシビリティ
tags:
  - UI
  - React
  - Blazor
  - アクセシビリティ
  - fluentui
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに 🌟

Fluent UI 2 の Spin button は、範囲の中から値を少しずつ増減させるためのコンポーネントです。  
「おおよその値を選ぶ Slider」とは役割が違い、小さな範囲を正確に調整したいときに向いています。

この記事では、まず Fluent UI 2 とは何かを短く整理し、これまでの Fluent UI 2 シリーズ記事をすべて紹介します。  
そのうえで、Spin button のガイダンス、動作、レイアウト、アクセシビリティ、コンテンツの書き方をまとめ、最後に Slider と Fluent UI Blazor 5 の `FluentNumberInput<T>` + `StepButtons` との違いを整理します。

参照した一次情報:

- [Fluent UI 2 Spin button usage](https://fluent2.microsoft.design/components/web/react/core/spin/usage)
- [Fluent UI 2 Slider usage](https://fluent2.microsoft.design/components/web/react/core/slider/usage)
- [Fluent UI Blazor 5 Number](https://fluentui-blazor-v5.azurewebsites.net/Number)

## Fluent UI 2 とは

Fluent UI 2 は、Microsoft Fluent 2 デザインシステムに沿って UI を設計・実装するためのガイダンスとコンポーネント群です。  
見た目をそろえるだけではなく、情報設計、操作の一貫性、アクセシビリティ、コンテンツ設計をまとめて扱うのが特徴です。

Spin button も同じで、単なる上下ボタンではありません。  
「どの範囲の値を、どの精度で、どう読み上げてもらうか」まで含めて設計する部品です。

## これまでの Fluent UI 2 シリーズ 📚

※ 本記事執筆時点で公開済みのシリーズ記事をすべて掲載しています。

| # | 記事 | 導入ポイント |
|---|---|---|
| 1 | [Fluent UI 2 の Accordion を理解する](https://qiita.com/tomokusaba/items/6a9a8bd2eb278cffb83b) | 情報の折りたたみと展開をどう設計するか |
| 2 | [Fluent UI 2 の Breadcrumb を理解する](https://qiita.com/tomokusaba/items/337b0de5fb5bd238c2a8) | 現在地を迷わせない階層導線の作り方 |
| 3 | [Fluent UI 2 の Card を理解する](https://qiita.com/tomokusaba/items/d9b72ccddacd948aaec4) | 情報ブロックの意味づけと配置 |
| 4 | [Fluent UI 2 の Checkbox を理解する](https://qiita.com/tomokusaba/items/6b43dddf9803786f01ed) | 複数選択と状態管理の基本 |
| 5 | [Fluent UI 2 の Button を理解する](https://qiita.com/tomokusaba/items/14928a4a52850c4eb09f) | 操作を促す基本アクション設計 |
| 6 | [Fluent UI 2 の Badge を理解する](https://qiita.com/tomokusaba/items/1b334d303ed207f956c6) | 補助情報を過不足なく伝える方法 |
| 7 | [Fluent UI 2 の Avatar を整理しつつ Fluent UI Blazor 5 でどう実装するか](https://qiita.com/tomokusaba/items/db6f552e0e853d0ce0f2) | 人物表現の一貫性と代替表現 |
| 8 | [Fluent UI 2 の Dialog を理解する](https://qiita.com/tomokusaba/items/5dcfce6246b5f5017bec) | 中断を伴う UI の使い分け |
| 9 | [Fluent UI 2 の Combobox を理解する](https://qiita.com/tomokusaba/items/af200d11891210cfc03b) | 選択と入力を両立する設計 |
| 10 | [Fluent UI 2 で始めるアクセシビリティ実装](https://qiita.com/tomokusaba/items/5603457cab9f2cbb1757) | キーボード/支援技術前提の実装基礎 |
| 11 | [Fluent UI 2 のアクセシビリティを色から読む](https://qiita.com/tomokusaba/items/c1c5d0faed184fb27da4) | 色に依存しない情報伝達の要点 |
| 12 | [Fluent UI 2 の Label を理解する](https://qiita.com/tomokusaba/items/5fb6729fb6caa207f335) | 入力の意味を短く正確に伝える方法 |
| 13 | [Fluent UI 2 の Popover を理解する](https://qiita.com/tomokusaba/items/d5209f1b271ef9ad267e) | 軽量オーバーレイの適用境界 |
| 14 | [Fluent UI 2 の Input を理解する](https://qiita.com/tomokusaba/items/0e2f80eff7e8afbb51ee) | テキスト/数値入力の基本設計 |
| 15 | [Fluent UI 2 の Divider を理解する](https://qiita.com/tomokusaba/items/fd3a94940a76a3a08498) | 視覚的グルーピングの作法 |
| 16 | [Fluent UI 2 の Image を理解する](https://qiita.com/tomokusaba/items/6f522ad550c6a853e623) | 画像の意味づけと代替テキスト |
| 17 | [Fluent UI 2 の Menu を理解する](https://qiita.com/tomokusaba/items/f2e681262a8e304981c8) | コマンド群の整理と操作導線 |
| 18 | [Fluent UI 2 の Nav を理解する](https://qiita.com/tomokusaba/items/c323de23e753455eeb7c) | 主要導線の情報設計 |
| 19 | [Fluent UI 2 の Icon を理解する](https://qiita.com/tomokusaba/items/4446e4ab89b5eaa55987) | 記号表現と意味伝達の整合 |
| 20 | [Fluent UI 2 の Link を理解する](https://qiita.com/tomokusaba/items/bf6f2d4d6cd875042d2a) | 遷移行動を予測しやすい文言設計 |
| 21 | [Fluent UI 2 の MessageBar を理解する](https://qiita.com/tomokusaba/items/7152b61fdf418239bbb8) | 状態通知の優先度と読みやすさ |
| 22 | [Fluent UI 2 の Drawer を理解する](https://qiita.com/tomokusaba/items/0ea1e4cdea16dcaaf97c) | 主画面文脈を保った補助操作 |
| 23 | [Fluent UI 2 の Field を理解する](https://qiita.com/tomokusaba/items/f8adff1e4bdff753a8e4) | 入力群の説明責任を担う枠組み |
| 24 | [Fluent UI 2 の Persona を理解する](https://qiita.com/tomokusaba/items/5ca07275ad4a3a685aee) | ユーザー情報表現の粒度設計 |
| 25 | [Fluent UI 2 の Progress Bar を理解する](https://qiita.com/tomokusaba/items/221c4b8bf08e8b700a84) | 待ち時間を可視化して不安を減らす |
| 26 | [Fluent UI 2 の Dropdown を理解する](https://qiita.com/tomokusaba/items/7f92dfabf9b32967b2f1) | 選択 UI の誤用を防ぐ判断基準 |
| 27 | [Fluent UI 2 の Radio Group を理解する](https://qiita.com/tomokusaba/items/65e2c45869018cd1f06d) | 単一選択の明快な提示 |
| 28 | [Fluent UI 2 の Rating を理解する](https://qiita.com/tomokusaba/items/d3b54e147dec86ec7086) | 評価表示と評価入力の使い分け |
| 29 | [Fluent UI 2 の Searchbox を理解する](https://qiita.com/tomokusaba/items/47ecb093c6ffb2f5bebe) | 検索体験の導線設計と補助機能 |
| 30 | [Fluent UI 2 の Slider を理解する](https://qiita.com/tomokusaba/items/591d70614596fe9e0d6c) | 概算入力と精密入力の線引き |

## Spin button とは

Spin button は、小さな範囲の値を正確に増減させるための specialized input です。  
月内の日付のように、候補が限られていて、しかも 1 ずつ動かしたい値に向いています。

公式ガイダンスでも、Spin button は precise increments in small ranges に向くとされています。  
逆に、範囲が大きすぎる場合や、値が 3 個未満のように極端に小さい場合は、Spin button ではなく input を検討します。

## Slider との違い 🔀

Spin button と Slider はどちらも「値を動かす UI」ですが、得意分野が違います。

| 観点 | Spin button | Slider |
|---|---|---|
| 🎯 主目的 | 小さな範囲を正確に増減する | 範囲内のおおよその値を素早く選ぶ |
| 🔢 精度 | 高い | 低〜中 |
| 🖐 操作 | 入力欄、矢印キー、上下ボタン | サムをドラッグ、トラックをクリック |
| 👀 値の見え方 | 数値そのものを直接見る | 範囲上の位置として見る |
| 🧭 向く場面 | 日付、数量、段階的な設定 | 音量、明るさ、割合の調整 |
| ⚠️ 注意点 | 範囲が広すぎると扱いにくい | 精密値には向かない |

公式の言い方を並べると、役割の差がはっきりします。

> Spin buttons are good for precise increments in small ranges. If the range is very large or very small (less than three values), use an input instead. If the values can be imprecise and a visual representation of the value on the range is helpful, try a slider.  
> — [Fluent UI 2 Spin button usage](https://fluent2.microsoft.design/components/web/react/core/spin/usage)

> Use a slider for imprecise values. Don't use them for ranges that are very small or very large. For precise numerical inputs, like a dollar amount, try an input.  
> — [Fluent UI 2 Slider usage](https://fluent2.microsoft.design/components/web/react/core/slider/usage)

要するに、Spin button は精密な段階調整、Slider は感覚的な範囲選択です。  
同じ数値入力でも、ユーザーに「値を見て調整してほしい」のか、「見た位置で決めてほしい」のかで選び分けます。

## Fluent UI Blazor 5 の Number / StepButtons との違い 🔄

Fluent UI Blazor 5 では、Spin button にそのまま対応する単独コンポーネントよりも、`FluentNumberInput<T>` を中心に考えるのが自然です。  
そして、上下の増減操作は `StepButtons` で補います。

| 観点 | Fluent UI 2 Spin button | Fluent UI Blazor 5 `FluentNumberInput<T>` |
|---|---|---|
| 🧩 役割 | 小さな範囲の値を増減する | 数値入力 + 増減操作をまとめて扱う |
| 🔼 補助操作 | 上下ボタン | `StepButtons` |
| 🔢 値の型 | UI 側のガイダンス中心 | `TValue` で整数/小数を明示 |
| 📏 範囲 | ガイダンスとして説明 | `Min` / `Max` / `Step` |
| 🌍 表示と解釈 | コンテンツ設計が中心 | `Culture` で表記と解釈を制御 |
| 🏷 単位 | ラベルやプレースホルダーで補う | `StartTemplate` / `EndTemplate` でも補える |

Blazor 側で特に大事なのは、`FluentNumberInput<T>` がただの数字欄ではなく、型・範囲・刻み幅・文化圏まで含めた数値入力だという点です。  
`StepButtons` は、その数値入力に「押して増減する」という Spin button に近い体験を足すための補助機能と考えると整理しやすいです。

## ガイダンス

Spin button のガイダンスでまず押さえるべきなのは、精密さと範囲のバランスです。

1. 小さな範囲に使う
2. 値は 1 ずつ、または妥当な刻み幅で動かす
3. 値の意味が明確なときだけ使う
4. 範囲が大きいときは input を検討する
5. 値の位置を視覚的に見せたいなら Slider を検討する

とくに、単なる「上下ボタンつき入力」に見えても、何を増減しているのかが曖昧なら失敗しやすいです。  
Spin button は、値の説明責任があるときにこそ強いコンポーネントです。

## 動作

Spin button の操作は、次の 3 つが中心です。

- 値を直接入力する
- キーボードの矢印キーで増減する
- スピンボタンを押して増減する

公式ガイダンスでは、増減幅は無理のない値にすべきとされています。  
たとえば月の日付なら 1 ずつ、複数の値をまたぐときは Page Up / Page Down のような bulk step も役に立ちます。  
さらに、Home キーで最小側、End キーで最大側へ飛べるのも大事な挙動です。

もう 1 つ重要なのが、最小値または最大値に達したとき、該当するスピンボタンだけが無効になることです。  
ただし、入力欄そのものは常に有効でなければなりません。これはアクセシブルな操作対象の大きさを保つためです。

## レイアウト

Spin button のレイアウトは、基本的に入力欄を中心にしたコンパクトな 1 つのコントロールです。  
値が見えることと、上下の操作が近くにあることが大切です。

実務では次の点を意識すると扱いやすくなります。

- ラベルはコントロールの意味を短く示す
- 単位があるなら、値のそばで一緒に見えるようにする
- スピンボタンは補助操作であって、入力欄の代わりではない
- フォームでは `Field` 的な枠組みと組み合わせて説明を補う

つまり、Spin button は見た目の密度を上げるための装飾ではなく、精密入力を短い操作で済ませるための配置と考えるのが自然です。

## アクセシビリティ ♿

ここは特に重要です。  
Spin button は見た目よりも、支援技術にどう伝わるかを先に考えるべきコンポーネントです。

### 1. 範囲を明示する

公式ガイダンスでは、`aria-valuemin` と `aria-valuemax` で範囲の大きさを伝えることが求められています。  
これがないと、スクリーンリーダー利用者は「どこまで動かせるのか」を把握しにくくなります。

### 2. 入力欄は常に有効にする

上下ボタンが無効になっても、入力欄そのものは有効に保ちます。  
これにより、到達可能な操作対象の大きさを確保できます。

### 3. キーボードだけで完結できるようにする

矢印キー、Page Up / Page Down、Home / End が使える前提で設計します。  
マウス操作だけで成立する UI にはしない、ということです。

### 4. ラベルは必須

ラベルは短い名詞または短い句で十分です。  
`Value` のような曖昧な語ではなく、`月`、`人数`、`表示件数` のように、何を入力するかをそのまま示します。

### 5. 単位は見える形で補う

単位があるなら、`0 cm` や `12 pt` のように、値と一緒に読める形にします。  
必要な情報を placeholder に逃がさず、ラベルや補助文言でも補完するのが安全です。

:::message alert
Spin button は「上下ボタンが付いた数値欄」ではありますが、アクセシビリティ上は範囲・現在値・単位の 3 点がそろって初めて扱いやすくなります。
:::

## コンテンツの説明 ✍️

コンテンツ設計では、短く、具体的に、重複なくが基本です。

| 観点 | 方針 | 例 |
|---|---|---|
| 🏷 ラベル | 何を入れるかを短く示す | `月` / `人数` / `表示件数` |
| ↔ 範囲 | 最小値と最大値を見える化する | `1〜12` / `0〜100` |
| 🔢 単位 | 値の意味を補う | `%` / `pt` / `cm` |
| 🧾 補足 | ルールを短く伝える | `1 ずつ増減します` |

ポイントは、ラベルは名詞で足りることが多い、という点です。  
説明文を長くするより、ラベル・単位・範囲を分けて見せたほうが読みやすくなります。

また、英語表記にする場合は sentence-style capitalization を意識し、先頭の単語だけを大文字にします。  
`0 cm` や `12 pt` のような単位表現は、 placeholder に入れるのも自然です。

## まとめ

Spin button は、小さな範囲を正確に増減させるためのコンポーネントです。  
Slider が「見ながら感覚的に決める UI」なら、Spin button は「値を見ながら確実に合わせる UI」です。

Fluent UI Blazor 5 では、これに近い体験を `FluentNumberInput<T>` と `StepButtons` で組み立てるのが自然です。  
最後は見た目よりも、範囲・単位・ラベル・読み上げの整合ができているかで選ぶと、実務では迷いにくくなります。
