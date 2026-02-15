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

実施した方法は以下の２つです
- AndroidのUserLand上にcode-serverをインストールしてChromeからアクセスして使う
- Codespace を使う  

code-serverを使った開発環境の良いところは、端末内で完結するので通信環境に影響されないところです  
操作感もネイティブのVScodeアプリと良く似ているので、ストレスなく文章作成する事ができます  

もう一つのCodespaceを使うとGitHub Copilot も利用できるようになります  
大変便利で楽しいです

作業環境を充実させるため、格安のモバイルノートパソコンが欲しいと思っているのですが、理想としてはスマホでいろいろな事が出来るようにしたいです  

GitHub Copilotはproプランを契約しているものの、もうすぐ上限に達しそうです
