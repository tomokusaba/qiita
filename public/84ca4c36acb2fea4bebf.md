---
title: Fluent UI 2 の Icon を理解する — Fluent UI Blazor の FluentIcon 比較とアクセシビリティ
tags:
  - UI
  - React
  - アクセシビリティ
  - Blazor
  - fluentui
private: false
updated_at: '2026-06-11T20:58:13+09:00'
id: 4446e4ab89b5eaa55987
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに 🌟

Fluent UI 2 の `Icon` は、単なる飾りではありません。  
公式の Usage ページでも、アイコンは concepts / objects / actions を表し、レイアウトの中で semantic purpose を持つものだと説明されています。

そのため、Icon を扱うときは「どの絵柄を置くか」より先に、何を伝えるのか、その意味が支援技術にも伝わるのかを考える必要があります。特に icon-only ボタン、状態表示、補助アイコンは、実装者の判断がそのまま使いやすさに表れやすい領域です。

この記事では、まず Fluent UI 2 そのものを短く整理し、そのあとでこれまでの Fluent UI 2 シリーズを振り返ります。  
その上で、Fluent UI 2 の Icon と Fluent UI Blazor の `FluentIcon` を比べながら、使い方の違い、提供される機能の違い、アクセシビリティ、コンテンツ記述の考え方をまとめます。

参照した一次情報はこちらです。

- [Fluent UI 2 Icon usage](https://fluent2.microsoft.design/components/web/react/core/icon/usage)
- [Fluent UI Blazor Icon](https://fluentui-blazor-v5.azurewebsites.net/Icon)
- [WAI-ARIA APG: Names and Descriptions](https://www.w3.org/WAI/ARIA/apg/practices/names-and-descriptions/)

## Fluent UI 2 とは

Fluent UI 2 は、Microsoft のデザインシステム Fluent 2 を UI 実装へ落とし込むための考え方とコンポーネント群です。  
重要なのは、見た目の統一だけでなく、情報の優先順位、操作の一貫性、アクセシビリティまで含めて設計する点です。

つまり Fluent UI 2 は、きれいな部品集というより、意味のある UI を作るための土台です。  
Icon もその例外ではありません。見た目がそろっていても、意味が曖昧だったり、操作名が伝わらなかったりすれば、良い Icon 実装とは言えません。

今回の Icon は、まさにその差が出やすいテーマです。  
アイコンは小さい部品ですが、ボタン、ナビゲーション、状態表示、入力補助のどこにでも入るため、プロダクト全体の体験へ広く影響します。

## これまでの Fluent UI 2 シリーズ 🧭

ここまで、私は Fluent UI 2 をコンポーネントごとに少しずつ整理してきました。  
今回の Icon は、その中でも Button、Breadcrumb、Card、アクセシビリティ記事と特に相性が良いテーマです。

| テーマ | 記事 |
|---|---|
| 🔘 Button | [Fluent UI 2 の Button を理解する](https://qiita.com/tomokusaba/items/14928a4a52850c4eb09f) |
| 🧩 Accordion | [Fluent UI 2 の Accordion を理解する](https://qiita.com/tomokusaba/items/6a9a8bd2eb278cffb83b) |
| 🗂️ Breadcrumb | [Fluent UI 2 の Breadcrumb を理解する](https://qiita.com/tomokusaba/items/337b0de5fb5bd238c2a8) |
| 🪪 Card | [Fluent UI 2 の Card を理解する](https://qiita.com/tomokusaba/items/d9b72ccddacd948aaec4) |
| ☑️ Checkbox | [Fluent UI 2 の Checkbox を理解する](https://qiita.com/tomokusaba/items/6b43dddf9803786f01ed) |
| 🏷️ Badge | [Fluent UI 2 の Badge を理解する](https://qiita.com/tomokusaba/items/1b334d303ed207f956c6) |
| 👤 Avatar | [Fluent UI 2 の Avatar を整理しつつ Fluent UI Blazor 5 でどう実装するか](https://qiita.com/tomokusaba/items/db6f552e0e853d0ce0f2) |
| 🗨️ Dialog | [Fluent UI 2 の Dialog を理解する](https://qiita.com/tomokusaba/items/5dcfce6246b5f5017bec) |
| ⌨️ Combobox | [Fluent UI 2 の Combobox を理解する](https://qiita.com/tomokusaba/items/af200d11891210cfc03b) |
| ⬇️ Dropdown | [Fluent UI 2 の Dropdown を理解する](https://qiita.com/tomokusaba/items/7f92dfabf9b32967b2f1) |
| ♿ アクセシビリティ実装 | [Fluent UI 2 で始めるアクセシビリティ実装](https://qiita.com/tomokusaba/items/5603457cab9f2cbb1757) |
| 🎨 色とWCAG | [Fluent UI 2 のアクセシビリティを色から読む](https://qiita.com/tomokusaba/items/c1c5d0faed184fb27da4) |

Button や Dropdown の記事でも、実は「可視ラベルとアイコンの関係」「icon-only UI の命名」は何度も出てきました。  
ただ、Icon は個別コンポーネントの中に埋め込まれるだけでなく、ボタン、入力、ナビゲーション、状態表示を横断して影響します。  
今回の Icon 記事は、その前提をまとめて扱う位置づけです。

## 今回のゴール ✅

- ✅ Fluent UI 2 における Icon の役割を理解する
- ✅ Fluent UI 2 と Fluent UI Blazor の Icon の違いを整理する
- ✅ decorative icon と meaningful icon を区別できるようになる
- ✅ accessible name をどこへ付けるべきか判断できるようになる
- ✅ icon-only ボタンのラベル付けを安全に実装できるようになる
- ✅ コンテンツ記述を「絵柄の説明」ではなく「意味の説明」として書けるようになる

## Icon は何をするのか

Fluent UI 2 の Usage ページは短いですが、要点はかなり明確です。  
Icon は、概念・オブジェクト・操作を表すものであり、recognizable / functional / easily understood であるべきだとされています。

この 3 つを実務向けに言い換えると、次のようになります。

| 観点 | 実務での意味 |
|---|---|
| 👀 Recognizable | 見た瞬間に何を示したいか推測できる |
| 🛠️ Functional | 単なる飾りではなく、操作や状態の理解を助ける |
| 🧠 Easily understood | 文脈の中で意味を取り違えにくい |

たとえば、保存ボタンのディスクアイコン、警告メッセージのアラートアイコン、Breadcrumb の区切り矢印は、見た目はすべてアイコンですが役割が違います。  
この違いを無視して全部同じように扱うと、支援技術では冗長になったり、逆に意味が抜け落ちたりします。

## Fluent UI Blazor の FluentIcon とは

Fluent UI Blazor 側では、`FluentIcon` はかなり具体的なコンポーネント API として提供されています。  
公式ドキュメントでは、Fluent UI System Icons は 2200 以上の distinct icons、filled / regular のバリエーション、複数サイズを持つコレクションとして説明されています。

また、Blazor 側の `FluentIcon` には次のような機能があります。

- `Value` でアイコンを指定する
- `Slot` でボタンなどの named slot に配置する
- `Color` / `CustomColor` で色を変える
- `Title` を設定できる
- `OnClick` を扱える
- `Icon.FromImageUrl(...)` やカスタム Icon クラスで独自アイコンを使える

特にドキュメントで強調されているのが、**`Icon` プロパティではなく `Value` プロパティを使うこと**です。  
公開時の trimming によって未参照アイコンが削除されるため、`Value` を使って明示的に参照することが推奨されています。

つまり、React 側の Icon usage が「どう使うべきか」という意味設計のガイド寄りなのに対して、Blazor 側の `FluentIcon` は「どう描画し、どう差し込むか」を扱う実装 API がかなり充実しています。

## Fluent UI 2 Icon と Fluent UI Blazor の比較

ここが本題です。  
両者は同じ Fluent 2 の文脈を共有していますが、重点が置かれている場所がかなり違います。

| 観点 | Fluent UI 2 Icon | Fluent UI Blazor `FluentIcon` |
|---|---|---|
| 🎯 主眼 | アイコンを意味ある UI として使うためのガイド | アイコンを Razor から描画・配置するためのコンポーネント API |
| 🧭 公式ページの焦点 | semantic purpose、recognizable、functional、easily understood | `Value`、`Slot`、`Color`、`Title`、`OnClick`、カスタム化 |
| 🧱 実装の入口 | コンポーネントや操作の中で Icon をどう位置づけるかを考える | `<FluentIcon>` を直接置く、または Button などの slot に差し込む |
| 🎨 バリエーション | 絵柄の意味と文脈が中心 | filled / regular、複数サイズ、カスタム色、画像 URL、独自アイコン |
| 🧩 合成のしやすさ | ボタン、入力、状態表示などの意味設計が中心 | named slot や `IconStart` / `IconEnd` のような配置で組み込みやすい |
| ♿ アクセシビリティ | アイコンの意味をどう伝えるかが中心課題 | API は豊富だが、最終的なラベル付け責任は実装者側 |
| 🚚 運用上の注意 | 絵柄選びと文脈依存の誤読に注意 | trimming を考慮し `Value` で参照するのが安全 |

言い換えると、Fluent UI 2 Icon は意味設計の入口、Fluent UI Blazor の `FluentIcon` は描画 API の入口です。  
設計の基準は Fluent UI 2 側に置きつつ、具体的な実装は Blazor 側の API で組み立てる、という見方をすると整理しやすいです。  
Blazor 側はできることが多い分、アクセシビリティを API の存在だけで満たした気にならないことが大切です。次は、その最重要論点であるアクセシビリティを見ていきます。

## アクセシビリティ（最重要）♿

ここは特に重要です。  
Icon 実装でまず押さえたいのは、**名前は操作要素に付ける**、装飾アイコンは隠す、意味のあるアイコンはテキストで補う、の 3 点です。

### 1. decorative icon か meaningful icon かを最初に決める

実装前に、まずそのアイコンがどちらなのかを決めます。

| 種類 | 役割 | 基本方針 |
|---|---|---|
| 🎀 Decorative icon | 見た目の補助 | 支援技術から隠す |
| 🧭 Meaningful icon | 状態・操作・対象を伝える | テキストや適切な accessible name と組み合わせる |

たとえば次のように考えると整理しやすいです。

- ボタン内の保存アイコン + `保存` という可視テキスト → decorative
- Breadcrumb の区切り矢印 → decorative
- エラー行の警告アイコン + `入力内容を確認してください` → decorative に近く、意味はテキストが担います
- アイコンだけの閉じるボタン → meaningful。名前はボタンに付ける

### 2. accessible name は icon ではなく、操作主体に付ける

WAI-ARIA APG の Names and Descriptions でも、button や link のような要素は通常、子孫コンテンツから accessible name を計算すると整理されています。  
そのため、可視テキストがあるボタンでは、わざわざ `aria-label` で上書きしない方が安全です。

特に次の 2 つを区別しておくと迷いにくいです。

| ケース | 何に名前を付けるか |
|---|---|
| `保存` のように可視テキストがあるボタン | テキストに任せる。アイコンは `aria-hidden` |
| icon-only ボタン | ボタン自体へ `aria-label` などで名前を付ける |

つまり、閉じるボタンに `X` やバツ印のアイコンだけを置くなら、名前は `閉じる` や `通知を閉じる` のようにボタン側に付けます。  
アイコンへ `title` を付けるだけで済ませるのは不十分です。

:::message alert
icon-only ボタンで付けるべき名前は、絵柄の名前ではなく **利用者に起きる結果** です。  
`ゴミ箱アイコン` ではなく `削除`、`バツ` ではなく `閉じる` と考えるとぶれにくいです。
:::

### 3. Title や Tooltip は補助として使う

Fluent UI Blazor の `FluentIcon` には `Title` を設定できますし、ツールチップ表示が必要なら `FluentTooltip` などを別途組み合わせられます。  
これは有用ですが、インタラクティブ要素の accessible name をそれだけで満たしたと見なさない方が安全です。

理由は単純で、Tooltip は常時見えている情報ではなく、ポインターやフォーカスに依存するからです。  
また、`title` は fallback として accessible name になることがあっても、主要な命名手段としては弱く、利用者が本当に知りたいのは「この図形の名前」ではなく、「この操作で何が起きるか」です。

### 4. 状態アイコンは、アイコンだけに意味を閉じ込めない

エラー、警告、成功、同期済み、未読のような状態表示では、アイコンだけで意味を完結させない方が安全です。  
特に色とアイコン形状だけに依存すると、読み上げでも視覚でも情報の取りこぼしが起きやすくなります。

実務では、次の形が扱いやすいです。

- アイコンは補助として置く
- 状態を表す短いテキストを近くに置く
- 必要なら `role="status"` や `aria-live` で変化を伝える

## コンテンツ記述は「絵柄」ではなく「意味」を書く ✍️

ここは、accessible name や状態説明を実際にどう書くか、という実践編です。  
Icon の説明文やラベルで迷ったときは、その絵が何に見えるかではなく、**その UI が何を意味するか**を書くのが基本です。

### よくある書き分け

| 場面 | 避けたい書き方 | 書きたい内容 |
|---|---|---|
| 🔍 検索ボタン | 虫眼鏡アイコン | 検索 |
| 🗑️ 削除ボタン | ゴミ箱アイコン | 削除 |
| ❌ 閉じるボタン | バツ印 | 閉じる |
| ⚠️ 警告表示 | 三角アイコン | 入力内容を確認してください |
| ✅ 成功表示 | チェックマーク | 保存しました / 同期済み |

特に日本語 UI では、アイコン名をそのまま説明文にすると、利用者にとっての意味が抜けやすいです。  
利用者が知りたいのは「虫眼鏡がある」ことではなく、「検索できる」ことです。

### 可視テキストがあるなら、まずそれを活かす

APG のガイダンスでも、visible text を活かせるならそれを優先するのが基本です。  
たとえば `保存` と見えているボタンに、さらに `aria-label="保存するボタン"` のような上書きを入れる必要は普通ありません。

むしろやりたいのは次の 2 つです。

- visible text があるなら、そのテキストを短く分かりやすく書く
- visible text がないなら、操作要素へ短い accessible name を付ける

この整理をしておくと、Icon の説明が冗長になりにくいです。

## コード例

短い例で、React 側と Blazor 側の考え方を並べておきます。

### React の例

```tsx
import { Button, Text } from "@fluentui/react-components";
import {
  AlertRegular,
  DismissRegular,
  SaveRegular,
} from "@fluentui/react-icons";

export function IconExamples() {
  return (
    <>
      <Button icon={<SaveRegular aria-hidden="true" />}>
        保存
      </Button>

      <Button
        appearance="subtle"
        icon={<DismissRegular aria-hidden="true" />}
        aria-label="通知を閉じる"
      />

      <div role="status" aria-live="polite" style={{ display: "flex", gap: 8 }}>
        <AlertRegular aria-hidden="true" />
        <Text>入力内容を確認してください</Text>
      </div>
    </>
  );
}
```

ポイントは次のとおりです。

- `保存` のように可視テキストがあるボタンでは、アイコンは decorative として隠す
- icon-only ボタンでは、`aria-label` をボタン側に付ける
- 状態表示では、アイコンだけに意味を背負わせずテキストも出す

### Fluent UI Blazor の例

```razor
@using Microsoft.FluentUI.AspNetCore.Components
@using Icons = Microsoft.FluentUI.AspNetCore.Components.Icons

<div style="display:flex; gap:12px; align-items:center;">
    <FluentButton>
        <FluentIcon Value="@(new Icons.Regular.Size20.Save())"
                    Slot="@FluentSlot.Start"
                    Focusable="false"
                    aria-hidden="true" />
        保存
    </FluentButton>

    <FluentButton Appearance="ButtonAppearance.Subtle" aria-label="通知を閉じる">
        <FluentIcon Value="@(new Icons.Regular.Size20.DismissCircle())"
                    Focusable="false"
                    aria-hidden="true" />
    </FluentButton>
</div>

<div role="status" aria-live="polite" style="display:flex; gap:8px; align-items:center;">
    <FluentIcon Value="@(new Icons.Filled.Size20.Alert())"
                Color="@Color.Warning"
                Focusable="false"
                aria-hidden="true" />
    <span>入力内容を確認してください</span>
</div>
```

Blazor 側で特に大事なのは、`FluentIcon` の API が豊富でも、accessible name をどこに持たせるかは別問題だという点です。  
`Title` や `FluentTooltip` の組み合わせは補助情報としては便利ですが、icon-only ボタンの名前はやはりボタンへ与えるのが基本です。

## 使い分けの目安

最後に、実務での判断を短くまとめます。

| こうしたい | 向いている考え方 |
|---|---|
| Icon を UI の意味設計から整理したい | Fluent UI 2 Icon usage を基準に考える |
| Razor で具体的に差し込みたい | Fluent UI Blazor の `FluentIcon` を使う |
| ボタンや入力補助へ自然に組み込みたい | slot / icon slot を使いつつ、名前は親要素へ持たせる |
| アイコンの色やバリエーションを細かく調整したい | Blazor の `Color` / filled / regular / サイズを活用する |
| icon-only UI を安全に作りたい | アイコンは隠し、ボタン自体へ短い accessible name を付ける |
| 状態を確実に伝えたい | アイコンだけでなく短いテキストも併記する |

私としては、Icon でいちばん大事なのは「どの絵を選ぶか」より、**その意味をどこに置くか**だと感じます。  
React でも Blazor でも、見た目のアイコンと accessible name の責任場所を切り分けられると、かなり事故が減ります。

## おわりに ✅

Fluent UI 2 の Icon は、小さな部品ですが、実際には UI の意味づけそのものに関わります。  
公式 Usage が短くても、semantic purpose、recognizable、functional、easily understood という軸はかなり本質的です。

一方で Fluent UI Blazor の `FluentIcon` は、実装 API としてとても強力です。  
`Value`、`Slot`、`Color`、`Title`、カスタム Icon など、できることは多いです。ただし、その豊富さとアクセシビリティの正しさは別問題です。

最後に判断基準を 3 つだけ残します。

1. そのアイコンは decorative か meaningful か
2. accessible name は icon ではなく、どの操作要素に付くべきか
3. コンテンツ記述は絵柄ではなく、利用者に伝えたい意味になっているか

この 3 つを先に決めるだけで、Icon 実装はかなり安定します。  
次に Button や Input、Navigation へアイコンを入れるときも、まずは「何を伝えるためのアイコンか」から考えてみてください 🌟

参考:

- [Fluent UI 2 Icon usage](https://fluent2.microsoft.design/components/web/react/core/icon/usage)
- [Fluent UI Blazor Icon](https://fluentui-blazor-v5.azurewebsites.net/Icon)
- [WAI-ARIA APG: Names and Descriptions](https://www.w3.org/WAI/ARIA/apg/practices/names-and-descriptions/)
- [Fluent UI 2 で始めるアクセシビリティ実装 — キーボード操作・支援技術・WCAG 2.1 の実践ガイド](https://qiita.com/tomokusaba/items/5603457cab9f2cbb1757)
