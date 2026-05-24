---
title: "アクセシブルなパッケージ設計から考える、インクルーシブデザインと Web への示唆"
tags:
  - アクセシビリティ
  - InclusiveDesign
  - Web
  - UX
  - Design
private: false
updated_at: ""
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
## はじめに

店頭や日常生活の中で商品を開けるとき、はさみやカッターがないと開封しづらいパッケージに出会うことがあります。一方で、特別な道具がなくても、つまみや切り口の工夫だけで自然に開けられるパッケージもあります。

私はこの違いを、単なる使いやすさの差ではなく、設計がどこまで人の多様な状況を想像しているかの差として受け取りました。握力が弱いとき、片手しか使えないとき、急いでいるとき、暗い場所にいるとき。そうした条件の違いは、Web アクセシビリティで考えていることと実はかなり近いように思えます。

そこで今回は、Microsoft の [Creating Accessible Packaging](https://inclusive.microsoft.design/articles/creating-accessible-packaging?WT.mc_id=DT-MVP-5004827) を読みながら、アクセシブルなパッケージ設計がなぜインクルーシブデザインの実践なのか、そしてそこから Web やソフトウェア設計にどんな示唆を受け取れるのかを整理してみます。身近な開けやすさの話からアクセシビリティを考え直したい方に向けた記事です。

## Microsoft がパッケージのアクセシビリティを語る意味

### ミッションと地続きのテーマだから

Microsoft は About ページで、次のミッションを掲げています。

> “Microsoft’s mission is to empower every person and every organization on the planet to achieve more.”
>
> — [Microsoft About](https://www.microsoft.com/en-us/about?WT.mc_id=DT-MVP-5004827)

この一文を読むと、パッケージのアクセシビリティを Microsoft が扱うのは自然だと分かります。ソフトウェアやクラウドだけが体験ではなく、製品と最初に接触する物理的な接点もまた体験の一部だからです。

もし中身の製品やサービスが優れていても、最初の開封の段階で人をふるい落としてしまうなら、「より多くを達成できるようにする」というミッションとは少しずれてしまいます。だからこそ、パッケージもまたインクルージョンの対象になります。

### Inclusive Design の原則にそのままつながっている

Microsoft の Inclusive Design では、次の 3 原則が示されています。

- **Recognize exclusion**
- **Learn from diversity**
- **Solve for one, extend to many**

— [Microsoft Inclusive Design](https://inclusive.microsoft.design/?WT.mc_id=DT-MVP-5004827)

私はこの 3 つが、パッケージの話に非常にきれいにつながっていると感じました。開けにくい包装は、誰かの身体条件や状況を暗黙に排除しているかもしれません。実際に困る人の声から学ばなければ、その排除には気づけません。そして、片手でも開けやすい、道具なしで扱いやすい設計は、結果として多くの人にとって便利になります。

Creating Accessible Packaging でも、inclusive design と accessibility の関係を次のように説明しています。

> “The best way to think of the relationship between inclusive design and accessibility is that inclusive design is a method and accessibility is an attribute.”
>
> — [Creating Accessible Packaging](https://inclusive.microsoft.design/articles/creating-accessible-packaging?WT.mc_id=DT-MVP-5004827)

つまり、アクセシビリティは最後のチェック項目ではなく、多様な人を起点に設計するプロセスの結果として現れるものだと捉えたほうがよさそうです。次は、その考え方がパッケージでどう見えるのかを見ていきます。

## パッケージから見えるインクルーシブデザイン

### 「道具が必要かどうか」は思った以上に大きい

Microsoft のガイドで、私がとても印象に残ったのは次の原則です。

> “No tools needed”
>
> — [Creating Accessible Packaging](https://inclusive.microsoft.design/articles/creating-accessible-packaging?WT.mc_id=DT-MVP-5004827)

ガイド本文では、これを「Design straightforward packaging that performs without the need for tools or external instruments.」と説明しています。つまり、外部の道具に依存しないで成立する開封体験を目指すということです。

これは単に親切な工夫というだけではありません。はさみが近くにない、握力が落ちている、片手がふさがっている、爪を使うのが難しい、といった状況では、道具前提の設計そのものが利用の壁になります。しかもその壁は、本人の能力だけでなく、そのときの環境や体調によっても簡単に現れます。

### 障害は一部の人だけの話ではない

同じガイドには、次の一文があります。

> “At some point in our lives, we will all experience or be impacted by disability.”
>
> — [Creating Accessible Packaging](https://inclusive.microsoft.design/articles/creating-accessible-packaging?WT.mc_id=DT-MVP-5004827)

私はこの視点がとても重要だと思っています。アクセシビリティを「特定の人向けの追加機能」と見ると、どうしても優先順位が下がります。しかし、障害や制約は常に固定された属性だけではありません。加齢、一時的な怪我、疲労、育児中の片手操作、暗所や騒音下の利用のように、誰でも制約のある側に回る可能性があります。

だからこそ、開けやすいパッケージは特別対応ではなく、人が現実に置かれる多様な状況を前提にした設計だと言えます。

### co-design は「想像する」だけでは足りないことを教えてくれる

このガイドは co-design の重要性も強調しています。障害のある当事者を後から評価者として呼ぶのではなく、最初から設計プロセスに含めるという考え方です。

パッケージでも Web でも、作り手だけで「きっとこうだろう」と考えると、気づけない摩擦が残りやすいです。Inclusive Design が求めているのは、想像力だけでなく、学び方そのものを変えることだと感じます。

ガイドでは、設計スプリントを開発プロセスの早い段階で行い、障害のある当事者や関連するステークホルダーと一緒に検討することを勧めています。これは Learn from diversity を実務に落とした姿そのものです。

### インクルーシブデザインは市場も広げる

ガイドには、次の表現もあります。

> “By the numbers, inclusive design expands the market for your product.”
>
> — [Creating Accessible Packaging](https://inclusive.microsoft.design/articles/creating-accessible-packaging?WT.mc_id=DT-MVP-5004827)

ここで大事なのは、「売上のためにアクセシビリティをやる」という単純な話ではないことです。より多くの人が無理なく使える設計は、結果として選ばれやすくなるという順番で理解したいです。

開けやすいパッケージのほうが好まれるのは、障害のある人に限りません。忙しい人、子どもを抱えている人、疲れている人、高齢の人、爪を傷めたくない人にも価値があります。ここに Solve for one, extend to many の実感があります。ここまで見えてくると、話は自然に Web やソフトウェア設計へつながります。

特に、日用品や食品のように毎日使うものでは、この価値がよりはっきり表れるように思います。1 回だけなら我慢できる開けにくさでも、それが毎日続くと小さな負担が積み重なります。もちろん、パッケージにはコストや製造上の制約もあるはずです。それでも、何かの制約があったり、忙しい日々を送っていたりする人にとって、開けやすさそのものが選ぶ理由の 1 つになるのだと感じます。

## Web やソフトウェア設計への示唆

### パッケージで起きることは、Web でも起きる

私は、パッケージを「最初のインターフェイス」として見ると、Web やソフトウェアとの共通点がかなり見えやすくなると感じました。

| 観点 | パッケージでの問い | Web / ソフトウェアでの問い |
|------|--------------------|-----------------------------|
| 道具への依存 | はさみやカッターがないと開けられないか | マウスがないと操作できないか |
| 次の行動の分かりやすさ | どこを持てばよいか直感的に分かるか | 次に押すべきボタンや入力項目が明確か |
| 身体的負荷 | 強い力や複雑な動作を要求していないか | 細かい操作、長い移動、時間制限を強いていないか |
| 多様な状況への配慮 | 片手利用や一時的な制約でも扱えるか | キーボード、スクリーンリーダー、拡大表示でも使えるか |
| 複数の到達経路 | 別の開け方が用意されているか | 複数の操作手段やナビゲーション経路があるか |

たとえば、パッケージにおける「No tools needed」は、Web で言えば「キーボードだけでも完結する」「音声読み上げでも意味が通る」「特定のデバイスや身体能力を前提にしない」に近い考え方です。

また、ガイドが挙げる low physical effort や ready access も、ソフトウェアに置き換えると示唆的です。クリック領域が小さすぎないか、モーダルから安全に抜けられるか、入力エラーの修正がしやすいか。こうした細部は、見た目以上にアクセシビリティを左右します。

### 開発者が持ち帰りたい視点

パッケージの話から、私は少なくとも次の 3 つを持ち帰りたいと思いました。

1. アクセシビリティは最後に足す属性ではなく、最初に置く前提条件であること
2. 制約のある人から学ぶことが、結果として全体の体験を押し上げること
3. 「使えるか」だけでなく、「無理なく使えるか」まで見ること

特に 3 つ目は見落としやすいです。形式的には操作できても、強い集中力や細かな器用さを要求する UI は、実質的には多くの人を遠ざけます。これは開けられるけれどかなり苦労するパッケージとよく似ています。

私は、アクセシビリティを考えるときに「この UI は開封に道具が必要なパッケージになっていないか」と自問すると、設計の見え方が少し変わるのではないかと思っています。抽象的な理念を、かなり日常的な感覚に引き寄せてくれるからです。最後に、この気づきをどう受け止めたいかをまとめます。

## おわりに

アクセシブルなパッケージ設計の話は、一見すると Web やソフトウェアから遠いテーマに見えます。しかし実際には、誰を前提に設計しているのかという意味で、かなり本質的に同じ問いを含んでいます。

Microsoft がパッケージのアクセシビリティを語るのは、製品体験をソフトウェアの画面だけで完結したものと見ていないからだと思います。そしてその背景には、Recognize exclusion、Learn from diversity、Solve for one, extend to many という Inclusive Design の原則があります。

私たちが Web やソフトウェアを設計するときも、見るべきなのは「仕様どおり動くか」だけではありません。道具を持っている人、十分に元気な人、慣れている人だけを暗黙に想定していないかを問い直すことが、インクルーシブデザインの入り口になるはずです。

身近なパッケージの開けやすさから考え始めると、アクセシビリティはぐっと具体的になります。開発者として、私もまずは「開けやすい体験」を Web の上でどう作るかを、もう一度見直していきたいです。

## 参考リンク

- [Creating Accessible Packaging](https://inclusive.microsoft.design/articles/creating-accessible-packaging?WT.mc_id=DT-MVP-5004827)
- [Microsoft Inclusive Design](https://inclusive.microsoft.design/?WT.mc_id=DT-MVP-5004827)
- [Microsoft About](https://www.microsoft.com/en-us/about?WT.mc_id=DT-MVP-5004827)
