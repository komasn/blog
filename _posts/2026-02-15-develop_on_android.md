---
title: "AndroidでVScodeを試してみました。code-serverかcodespaceで実行します"
date: 2026-02-15
categories: ["技術", "Android", "開発", "GitHub"]
description: "Android上でVSCodeを動かす方法を比較・検証します。code-serverとCodespacesの利点・注意点、実際の利用感をまとめた実践レポート。"
tags: [GitHub, Android, develop, code-server, codespace]
---
# {{ page.title }}
<p>{{ page.date }}</p>

私はスマホでGitHubのリポジトリを修正する時はGitHubの公式アプリのほか、Spck Editor というアプリを使っています  

[AndroidにおけるGitHubクライアントの決定版](https://note.com/lively_quince256/n/nb78cdd7cc10a)  

非常に便利なアプリなのですが、AndroidでもVScodeを使いたいという気持ちが大きくなってきました

パソコンでGitHubと連携させたVScodeを使ってコーディングしていると、「これが外出先でも出来れば良いのに」と感じてしまいます  

外出先やスキマ時間でのコーディングのために安いノートブックPCを買おうか迷いながら、スマホでの開発環境が便利になれば解決するのではないかと思いいろいろと試しています  

スマホでVScodeを使うために、２つの方法を試して見ました

- GitHub の Codespaces を使う  
- AndroidのUserLand上にcode-serverをインストールしてChromeからアクセスして使う

結論からいえば、どちらの方法でもスマホ上でVSCodeを使うことができました

## GitHub の Codespaces を使う  

まずはじめに、GitHubのCodespacesを使ってみました。

[Codespaces](https://github.co.jp/features/codespaces)

GitHub Codespacesとは、クラウド上でVSCodeを中心とした開発環境の利用が可能になるものです。

|機能|vscode.dev (github.dev)|GitHub Codespaces|
|---|---|---|
|正体|ブラウザ上で動く「エディタ」|クラウド上の「仮想PC（Linux）」|
|起動方法|URLを入力するか、リポジトリで . を押す|緑の [Code] ボタンから作成|
|コードの実行|不可（ターミナルがない）|可能（本物のターミナルがある）|
|Copilot|基本不可（一部機能制限あり）|フル機能利用可能|
|料金|完全に無料|無料枠あり（月60〜120時間など）|
|スマホとの相性|軽い（ブラウザだけ）|少し重い（サーバーと通信する）|

単なるEditorであるvscode.devとは違い、VScodeのほぼ完全な機能を有しています
GitHub Copilot も利用できるようになります  

有料である点と、起動に少し時間がかかる点が気になりました

## AndroidのUserLand上にcode-serverをインストールしてChromeからアクセスして使う

AndroidにUserLandというアプリをインストールし、Ubuntu上にcode-server をインストールした上でChromeからアクセスして使います。code-serverを使った開発環境の良いところは、端末内で完結するので通信環境に影響されないところです  
操作感もネイティブのVScodeアプリと良く似ているので、ストレスなく文章作成する事ができます  

作業環境を充実させるため、格安のモバイルノートパソコンが欲しいと思っているのですが、理想としてはスマホでいろいろな事が出来るようにしたいです  

vscode.dev（github.dev）によるコーディングも意外と快適です

現在は、code-serverを使ったコーディングをためしています

通信環境に操作感が依存せず、安定してコーディングが出来るのは非常に快適です

AIとの連携や安定性など、自分にあった方法を探していこうと思います

いろいろな実現方法がありますが、スマホの開発環境も本当にリッチになってきたものだと改めて感じます  

