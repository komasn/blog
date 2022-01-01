---
title: "GoogleDomainによる独自ドメイン運用"
author: "komasn"
date: 2021-08-09 18:00
categories: GitHub Ubuntu jekyll
---
GoogleDomainで独自ドメインを取得しました😘
これからはconoha vps上のWEBサイトにドメインでアクセスできるようになりました🤗💕！
ブログっぽくなってきて嬉しいです。  
  
github.io上のサイトは不要になったので削除する予定です😮‍💨サミシー
  
jekyll new  
で新しいサイトを作ったので、テーマとしてMinimaが適用されています。  
少しレイアウトをしようとしたら、_layoutsフォルダが見つからずに一瞬焦りました、が、

公式サイトに書いてある通り、デフォルトの_layoutsを上書きすることでレイアウトの修正できました‼️←初めから見たらいいのに、公式サイト😇

<br>
<br>
↓↓やり方書いておきますね↓↓
  
[http://jekyllrb-ja.github.io/docs/themes/](http://jekyllrb-ja.github.io/docs/themes/)  
  
bundle path --info minima  


で場所と内容を確認し、それをプロジェクトの_includeフォルダに上書きしてから修正することで解決🐇🐇
<br>
<br>
レイアウトを継承して別の名前をつけて、というのも良いかと思います。