---
title: "jekyllでのヘッダー編集方法"
date: 2022-01-10 18:00
categories: ["技術", "Jekyll", "テーマ"]
---  
<p>このブログはGitHubPagesのjekyllテンプレートを使って更新しています😃</p>  


<br>
使っているテーマはarchitectです。   
ヘッダー行を編集する方法が分からなかったのですが、architectの公式githubリポジトリに記述がありました。  
<br>
[architect公式](https://github.com/pages-themes/architect)  
<br>
readmeに書いてある通りですが、_includesのhead-custom.htmlに追記すれば良いようです。  
<br>

- 公式のリポジトリから_includesディレクトリをコピーする　　
- 自分のjekyllリポジトリに配置する  
- head-custom.htmlを編集する  

<br>
という流れになります  
ずっとjekyllの公式リファレンスばかり探していてつまづいていました💦  
<br>
テーマの公式を見れば良かったのか😇😇  
<br>
layoutsの編集なども色々出来そうなので、少しずつ試していこうと思います🏹　　
<br>
やっぱりjekyllは楽しいなあ😄  
<br>
<p>{{ page.title }}</p>
<p>{{ page.date }}</p>