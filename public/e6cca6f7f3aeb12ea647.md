---
title: GitHub CopilotのAgentモードでASP.NET Coreアプリケーションを作る
tags:
  - VisualStudio
  - ASP.NET_Core
  - GitHubCopilot
private: false
updated_at: '2026-06-22T19:13:29+09:00'
id: e6cca6f7f3aeb12ea647
organization_url_name: FutureOne
slide: false
ignorePublish: false
---
# 事前準備
Visual StudioのAgentモードを有効にしよう。
6/17現在、Visual Studioをインストールした時点でのデフォルトではAgentモードが無効になっています。
Agentモードを有効にしましょう。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3951664/4ba18a27-c5f6-4873-a97c-8621b2fc1a65.png)

# コンソールアプリケーションを作る
.NET 8あたりでコンソールアプリケーションを作成していきます。
今回の、Webアプリケーションの元ネタになるものです。

たとえば、GitHub Copilot Chatをエージェントモードにして以下のようにします。

```
1から100までの偶数を表示する
```
すると、以下のようにコードが生成されました。

```csharp
// 1から100までの偶数を表示
for (int i = 2; i <= 100; i += 2)
{
    Console.WriteLine(i);
}

```

ではこれをWebアプリケーションにしていきます。

# ASP.NET Coreアプリケーションにする

GitHub Copilot Chatに以下のように入力していきます。

```
Webアプリケーションにしてください
```

すると、プロジェクトファイルを以下のように書き換えASP.NET Coreアプリケーションにするなどの変更をしていきます。

```
<Project Sdk="Microsoft.NET.Sdk.Web">
```

Program.csは以下のようになりました。

```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.MapGet("/", () =>
{
    var evenNumbers = Enumerable.Range(1, 100).Where(x => x % 2 == 0);
    return string.Join("<br>", evenNumbers);
});

app.Run();
```
実行結果が以下のようになりました。
改行のHTMLマークアップが邪魔です。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3951664/8987bd81-985c-4179-8d06-c35d05c7b8f7.png)

ですので、再びGitHub Copilot Chatに以下のようにお願いします。

```
改行のマークアップは不要です
```

良い感じになりました。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3951664/2c6f4f4a-8001-46fa-99ce-881b30c54c30.png)

さらに、データとして読みやすいようにJSON形式で返してもらうようにお願いしてみます。

```
JSON形式で返却するようにしてください
```

コードが以下のように最終的になりました。

```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.MapGet("/", () =>
{
    var evenNumbers = Enumerable.Range(1, 100).Where(x => x % 2 == 0).ToArray();
    return Results.Json(evenNumbers);
});

app.Run();
```
JSON形式で返却されていることを確認できます。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3951664/3441f2b7-f822-455a-86f7-5af3e4a67680.png)

さらに、Blazor WebAssemblyでこれを表示するフロントエンドを作ってもらいましょう

# フロントエンドの作成
同じようにGitHub Copilot Chatにお願いしていきます。
```
今あるAPIのデータを表示するフロントエンドをBlazor WebAssemblyで作ってください。
```

同様に何回かエラーの末、GitHub Copilot Chatとのやり取りの末以下のようになりました。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3951664/6a790059-9fa6-4f91-92e7-72b1eb8833ff.png)

# 結論

コードを1行も書かなくても簡単なものならCopilotで作れる！
