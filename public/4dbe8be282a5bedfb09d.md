---
title: Fluent UI 2 の Popover を理解する — Fluent UI Blazor 5 との比較と Tooltip / Dialog の使い分け
tags:
  - UI
  - React
  - アクセシビリティ
  - Blazor
  - fluentui
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---

## はじめに 🌟

Fluent UI 2 の Popover は、画面の文脈を保ったまま補足情報を出すための小さなサーフェスです。Dialog のように作業を止めず、Tooltip よりは構造化された内容や軽い操作を置けるのが特徴です。

この記事では、まず Fluent UI 2 の位置づけを短く整理し、これまでの Fluent UI 2 シリーズをすべて紹介します。そのうえで、Fluent UI 2 の Popover usage と Fluent UI Blazor 5 の `FluentPopover` を比較し、**使用法**、**機能差**、**使い分け**、**ガイドライン**、**レイアウト**、**アクセシビリティ**、**コンテンツ設計**を整理します。特にガイドラインとコンテンツは重点的に扱います。

参照した一次情報:

- [Fluent UI 2 Popover usage](https://fluent2.microsoft.design/components/web/react/core/popover/usage)
- [Fluent UI Blazor 5 Popover](https://fluentui-blazor-v5.azurewebsites.net/Popover)
- [Fluent UI 2 Tooltip usage](https://fluent2.microsoft.design/components/web/react/core/tooltip/usage)
- [Fluent UI 2 Dialog usage](https://fluent2.microsoft.design/components/web/react/core/dialog/usage)

## Fluent UI 2 とは

Fluent UI 2 は、Microsoft Fluent 2 デザインシステムに沿って UI を設計・実装するための指針とコンポーネント群です。見た目の統一だけではなく、情報の優先順位、操作の一貫性、アクセシビリティ、コンテンツ表現まで含めて設計する点が核になります。

Popover もこの文脈で捉えると分かりやすいです。Popover は単なる「吹き出し」ではなく、必要十分な文脈情報を、作業フローを壊さずに渡すための設計要素です。

## これまでの Fluent UI 2 シリーズ（公開済み）📚

1. [Fluent UI 2 のアクセシビリティを色から読む ─ WCAG 2.1 と対比しながら整理する](https://qiita.com/tomokusaba/items/c1c5d0faed184fb27da4)
2. [Fluent UI 2 で始めるアクセシビリティ実装 — キーボード操作・支援技術・WCAG 2.1 の実践ガイド](https://qiita.com/tomokusaba/items/5603457cab9f2cbb1757)
3. [Fluent UI 2 の Accordion を理解する — 情報設計・アクセシビリティ・React 実装](https://qiita.com/tomokusaba/items/6a9a8bd2eb278cffb83b)
4. [Fluent UI 2 の Avatar を整理しつつ Fluent UI Blazor 5 でどう実装するか](https://qiita.com/tomokusaba/items/db6f552e0e853d0ce0f2)
5. [Fluent UI 2 の Badge を理解する — Fluent UI Blazor 5 との比較と実装ポイント](https://qiita.com/tomokusaba/items/1b334d303ed207f956c6)
6. [Fluent UI 2 の Breadcrumb を理解する — Fluent UI Blazor 5 との対応とアクセシビリティ](https://qiita.com/tomokusaba/items/337b0de5fb5bd238c2a8)
7. [Fluent UI 2 の Button を理解する — 種類・レイアウト・アクセシビリティ・Blazor 5 比較](https://qiita.com/tomokusaba/items/14928a4a52850c4eb09f)
8. [Fluent UI 2 の Card を理解する — React と Fluent UI Blazor の違い](https://qiita.com/tomokusaba/items/d9b72ccddacd948aaec4)
9. [Fluent UI 2 の Checkbox を理解する — React と Fluent UI Blazor v5 の違い](https://qiita.com/tomokusaba/items/6b43dddf9803786f01ed)
10. [Fluent UI 2 の Combobox を理解する — Fluent UI Blazor 5 との比較と使い分け](https://qiita.com/tomokusaba/items/af200d11891210cfc03b)
11. [Fluent UI 2 の Dialog を理解する — React と Fluent UI Blazor 5 の違いと使い分け](https://qiita.com/tomokusaba/items/5dcfce6246b5f5017bec)
12. [Fluent UI 2 の Divider を理解する — Fluent UI Blazor 5 との比較](https://qiita.com/tomokusaba/items/fd3a94940a76a3a08498)
13. [Fluent UI 2 の Drawer を理解する — Tooltip / Popover / Dialog との使い分けと Fluent UI Blazor 5 比較](https://qiita.com/tomokusaba/items/0ea1e4cdea16dcaaf97c)
14. [Fluent UI 2 の Dropdown を理解する — Fluent UI Blazor 5 の近縁コンポーネント比較とアクセシビリティ](https://qiita.com/tomokusaba/items/7f92dfabf9b32967b2f1)
15. [Fluent UI 2 の Field を理解する — Fluent UI Blazor 5 と比較する入力設計の基礎](https://qiita.com/tomokusaba/items/f8adff1e4bdff753a8e4)
16. [Fluent UI 2 の Icon を理解する — Fluent UI Blazor の FluentIcon 比較とアクセシビリティ](https://qiita.com/tomokusaba/items/4446e4ab89b5eaa55987)
17. [Fluent UI 2 の Image を理解する — Fluent UI Blazor 5 と比較しながらレイアウトとアクセシビリティを整理する](https://qiita.com/tomokusaba/items/6f522ad550c6a853e623)
18. [Fluent UI 2 の Input を理解する — Textarea・Fluent UI Blazor TextInput / Number 比較とアクセシビリティ](https://qiita.com/tomokusaba/items/0e2f80eff7e8afbb51ee)
19. [Fluent UI 2 の Label を理解する — Fluent UI Blazor 5 と比較するラベル設計の基礎](https://qiita.com/tomokusaba/items/5fb6729fb6caa207f335)
20. [Fluent UI 2 の Link を理解する — Fluent UI Blazor 5 と比較するリンク設計とアクセシビリティ](https://qiita.com/tomokusaba/items/bf6f2d4d6cd875042d2a)
21. [Fluent UI 2 の Menu を理解する — Fluent UI Blazor 5 と比較するガイダンス・動作・アクセシビリティ](https://qiita.com/tomokusaba/items/f2e681262a8e304981c8)
22. [Fluent UI 2 の MessageBar を理解する — Fluent UI Blazor 5 と比較する機能・使用方法・アクセシビリティ](https://qiita.com/tomokusaba/items/7152b61fdf418239bbb8)
23. [Fluent UI 2 の Nav を理解する — ガイダンス・動作・レイアウト・アクセシビリティと Fluent UI Blazor 5 比較](https://qiita.com/tomokusaba/items/c323de23e753455eeb7c)
24. [Fluent UI 2 の Persona を理解する — ガイダンス・レイアウト・アクセシビリティ・Fluent UI Blazor 5 比較](https://qiita.com/tomokusaba/items/5ca07275ad4a3a685aee)
25. [Fluent UI / Fluent 2 で raw 値より alias token を使うべき理由 ─ アクセシビリティ運用を強くする設計](https://qiita.com/tomokusaba/items/c6d6c248fc3030d63f50)

## 今回のゴール ✅

- ✅ Popover を Tooltip / Dialog とどう切り分けるか理解する
- ✅ Fluent UI 2 と Fluent UI Blazor 5 の使用法と機能差を整理する
- ✅ ガイドライン、レイアウト、アクセシビリティ、コンテンツ設計の要点を実装へ落とし込めるようにする

## Fluent UI 2 Popover と Fluent UI Blazor 5 `FluentPopover` の比較

結論として、Fluent UI 2 側は「いつ Popover を使うか」という設計判断のガイドが中心で、Fluent UI Blazor 5 側は「どう表示・制御するか」という API 提供が中心です。

| 観点 | Fluent UI 2 Popover (React / Usage) | Fluent UI Blazor 5 `FluentPopover` |
|---|---|---|
| 🧭 主眼 | 非必須の文脈情報をどう提示するか | `AnchorId` と `Opened` を軸に UI をどう実装するか |
| 🧩 情報の性質 | 構造化コンテンツ・軽い操作まで許容 | `ChildContent` で自由に配置可能 |
| 🪟 表示制御 | 設計ガイド中心（実装詳細は別） | `@bind-Opened` / `OpenedChanged` で制御 |
| 📍 位置決め | `positioning` を使うことを案内 | アンカー基準で自動配置（下優先、足りなければ上/左） |
| ↕️ オフセット | ガイドで相対位置の考え方を提示 | `OffsetVertical` / `OffsetHorizontal` を提供 |
| 📐 サイズ | 既定制約なし。必要に応じて制限し overflow を扱う | `Width` / `Height` を指定可能 |
| ⌨️ キー操作 | 文脈ごとに適切なアクセシビリティ設計を求める | `Esc` でクローズ可能 |
| ♿ フォーカス | `trapFocus` 利用時の挙動を明示 | フォーカス管理の方針は利用側設計に委ねられる |
| 🪆 ネスト | **ネストしない**方針を明示 | `Nested` パラメーターあり（最大 2 階層を推奨） |

特に実務で重要なのは、**Fluent UI 2 の「使うべき場面」判断を先に行い、その後に Blazor API で実装する**順序です。API が書けることと、Popover を使うべき文脈であることは別問題です。

## 類似コンポーネント（Tooltip / Dialog）との使い分け

| コンポーネント | 目的 | 向いている内容 | 向いていない内容 |
|---|---|---|---|
| 🏷️ Tooltip | 最小限の補足 | 非必須のプレーンテキスト | 構造化情報、複雑な説明 |
| 🪟 Popover | 文脈付き補足 | 非必須の構造化情報、軽い操作 | タスク完了に必須な情報 |
| 🚨 Dialog | 中断して判断させる | 重要確認、破壊的操作、未保存確認 | ただの補足説明 |

Fluent UI 2 の文脈では、本文に影響しない補足は Tooltip/Popover、操作を止めて判断が必要な場面は Dialog です。Popover に「必須情報」を載せると、見落としがそのまま失敗に直結するので避けるべきです。

## Popover のガイドライン（最重要）🧭

ここがいちばん重要です。Popover の guidance は、UI 部品の API ではなく、使い方の境界線を定義しています。

1. **非必須情報に限定する**  
   Popover の内容は、タスク完了に必須であってはいけません。
2. **主 UI の重要情報を隠さない**  
   関連対象が分かる位置に置きつつ、同時に見たい主要情報を覆わない配置にします。
3. **サイズを必要最小限にする**  
   既定でサイズ制約はないため、レイアウト要件に応じて幅・高さを制限します。
4. **overflow を意図的に扱う**  
   はみ出る内容は `overflow: scroll` でアクセス可能にし、スクロール軸は原則 1 軸に寄せます（ただし、意味や操作上 2 次元レイアウトが必要なコンテンツは除きます）。
5. **用途を逸脱したら別サーフェスへ移す**  
   情報が本質的/重いなら、メイン画面や Dialog/Panel へ移す判断を優先します。

:::message alert
Popover に「読まないと進めない説明」や「重要な警告」を入れるのは避けるべきです。  
その時点で Popover ではなく Dialog やメインコンテンツに昇格させるのが正解です。
:::

## レイアウト 📐

Popover のレイアウトは「小さいこと」より「関係が分かること」が優先です。

- 対象コンポーネントとの関連が一目で分かる位置に置く
- 主情報を隠さない
- 必要ならサイズ制限を設定する
- 長文を入れすぎない

Blazor 側では次のように実装すると、設計意図を反映しやすいです。

```razor
<FluentButton Id="help-popover-button" OnClick="@(() => isOpen = !isOpen)">
    表示条件
</FluentButton>

<FluentPopover AnchorId="help-popover-button"
               @bind-Opened="isOpen"
               Width="320px"
               Height="220px"
               OffsetVertical="8">
    <div style="overflow-y: auto; max-height: 180px;">
        ここに補足説明を置きます（非必須情報）。
    </div>
</FluentPopover>

@code {
    private bool isOpen;
}
```

## アクセシビリティ ♿

Popover で重要なのは、**補助情報であること**と**フォーカス設計**です。

- キーボード利用者が開閉できる導線を用意する
- 必要に応じて `trapFocus` の影響を理解して使う
- 閉じた後のフォーカス遷移先を意識する
- 過剰なネストで操作文脈を壊さない

Fluent UI 2 の usage では「Popover をネストしない」を強く推奨しています。`trapFocus` を使う場合は、Popover オープン中に親要素へ `aria-hidden="true"` が設定される点も理解しておく必要があります。  
Fluent UI Blazor は `Nested` を提供しますが、公式ドキュメント側でも 2 階層を超えるネストは非推奨です。つまり両者とも、ネストは抑制的に扱うのが基本です。

## コンテンツ設計（最重要）✍️

Popover の価値は、内容が短く、重複せず、行動を邪魔しないことです。ここを外すと、Popover はただの読みにくい小窓になります。

> Content in popovers should never be essential for someone to complete a task. It also shouldn’t repeat information that’s available in the main UI.  
> — [Fluent UI 2 Popover usage](https://fluent2.microsoft.design/components/web/react/core/popover/usage)

実務で守りたいポイント:

| 観点 | 推奨 | 避けたい書き方 |
|---|---|---|
| 🧠 必須性 | 補助情報に限定 | 読まないと操作できない説明 |
| ✂️ 長さ | 短文・短句中心 | 長い段落、手順の羅列 |
| 🔁 重複 | 主 UI と内容を重複させない | 見えている文言の焼き直し |
| 🛟 追加導線 | 必要なら `Learn more` を下部に置き、新しいウィンドウまたはパネルで開く | Popover 内にすべて詰め込む |
| 🧭 文脈 | 何に対する補足かを明確にする | 対象が不明な一般論 |

Popover のテキストは「説明の完全版」ではなく「次の判断を助ける最小単位」として書くと安定します。詳細が必要な場合は、Popover を肥大化させるより、別面へ誘導したほうが読みやすくなります。

## まとめ ✅

Popover は「情報を出せる小窓」ではなく、**非必須の文脈情報を作業を止めずに渡す設計コンポーネント**です。Fluent UI 2 はその判断基準を与え、Fluent UI Blazor 5 は `FluentPopover` で実装手段を提供します。

最終的に押さえるべき点は次の 4 つです。

1. Popover は必須情報に使わない
2. Tooltip / Popover / Dialog の境界を先に決める
3. レイアウトは「関連性」と「主情報を隠さないこと」を優先する
4. コンテンツは短く、重複させず、必要なら別導線へ分離する

## 出典

- [Fluent UI 2 Popover usage](https://fluent2.microsoft.design/components/web/react/core/popover/usage)
- [Fluent UI Blazor 5 Popover](https://fluentui-blazor-v5.azurewebsites.net/Popover)
- [Fluent UI 2 Tooltip usage](https://fluent2.microsoft.design/components/web/react/core/tooltip/usage)
- [Fluent UI 2 Dialog usage](https://fluent2.microsoft.design/components/web/react/core/dialog/usage)
