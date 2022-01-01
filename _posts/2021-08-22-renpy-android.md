---
layout: post
title: Ren'PyでのAndroid開発
author: "komasn"
date: 2021-08-22 13:00
categories: BLOG Ubuntu
---  
## Androidデベロッパーアカウントが停止される
私のAndroidデベロッパーアカウントが2021年10月13日に削除されそうです。  
<BR>
アカウント取得から９年間まったく利用しなかったので当然ですが、いざなくなると思うと回避したい。  
## 回避する方法
とにかくAndroidアプリを作ることです。  
以前[Ren'Py](https://ja.renpy.org/doc/html/#)を使って作った紙芝居があったので、それをAndroidアプリにすることで回避したいと思いました。  
<BR>
Googleからのアカウント停止通知のメールに
>アプリを公開する準備ができていない場合は、内部アプリ共有、内部テスト、またはクローズドテストを利用して、一般提供することなく安全にアップロードしていただけます

とありましたでの、なんとか管理サイトに上げるところまで行きたいと思っています。  
Ren'pyには[Androidアプリとして成果物をビルドする機能](https://ja.renpy.org/doc/html/android.html)があるようなので、それを使いたいと思います。
<BR>
## うまくいかない
Ren'pyで作成したプロジェクト「TwoMOuse」を選択して、画面右下のAndroidをクリックします。  
<BR>
![image1](/assets/images/Screenshot from 2021-08-22 13-47-17.png)  
<BR>
SDKのインストールキー&キーの作成をクリックします。  
![image2](/assets/images/Screenshot from 2021-08-22 14-02-32.png)  
<BR>
すると以下のエラーメッセージが吐き出されました。  
![image3](/assets/images/Screenshot from 2021-08-22 14-05-58.png)

>Ren'Py 7.4.8.1895  
>  
>小さなテストプログラムをコンパイルして、あなたのシステムで JDK が動作するか確認しています。  
>  
>Traceback (most recent call last):  
>  File "game/mobilebuild.rpy", line 195, in call  
>  File "/home/tom/ab/renpy-build/tmp/install.linux-x86_64/lib/python2.7/subprocess.py", line 325, in __init__  
>  File "/home/tom/ab/renpy-build/tmp/install.linux-x86_64/lib/python2.7/subprocess.py", line 978, in _execute_child  
>OSError: [Errno 2] No such file or directory  
>  
>I was unable to use javac to compile a test file. If you haven't installed the Java Development Kit yet, please download it from:  
>  
>https://adoptopenjdk.net/?variant=openjdk8&jvmVariant=hotspot  
>  
>The JDK is different from the JRE, so it's possible you have Java without having the JDK. Without a working JDK, I can't continue.  

このエラーを解決する方法がわかりません。  
JDKの問題かと思い[Ren'Py公式で案内されたOracleのJDK](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html)をインストールしました。  
<BR>
インストールしたJDKは  
Linux x64 Compressed Archive です  
<BR>
次のページを参考にインストールしました。  
[DebianまたはUbuntuシステムでのOracleJREまたはJDKのインストール](https://docs.datastax.com/ja/install/6.0/install/installJdkDeb.html)

<BR>
$ java -version  

>java version "1.8.0_301"  
>Java(TM) SE Runtime Environment (build 1.8.0_301-b09)  
>Java HotSpot(TM) 64-Bit Server VM (build 25.301-b09, mixed mode)  

<BR>
$ javac -version  

>コマンド 'javac' が見つかりません。次の方法でインストールできます:  
>sudo apt install openjdk-11-jdk-headless  
>sudo apt install default-jdk  
>sudo apt install openjdk-13-jdk-headless  
>sudo apt install openjdk-16-jdk-headless  
>sudo apt install openjdk-8-jdk-headless  
>sudo apt install openjdk-14-jdk-headless  
>sudo apt install ecj  

$ echo $JAVA_HOME
>/usr/lib/jvm/jdk1.8.0_301/bin

Ren'Pyのエラーコードから[OpenJDKのURL](https://adoptopenjdk.net/?variant=openjdk8&jvmVariant=hotspot)にアクセスしてOpenJDK8をダウンロード
して設定しても同様の状態になります。  
<BR>
javac のパスが通ってないことが原因なのでしょうか。  
javacのパスを通す手順を追加してみます。  
<BR>
$ sudo update-alternatives --install "/usr/bin/javac" "javac" "/usr/lib/jvm/jdk1.8.0_301/bin/javac" 1  
>update-alternatives: /usr/bin/javac (javac) を提供するために自動モードで /usr/lib/jvm/jdk1.8.0_301/bin/javac を使います  

$ javac -version
>javac 1.8.0_301

<BR>
<BR>
javacのパスを通してもRenPyから吐き出されるエラーメッセージは変わりません。。。  
<BR>
<BR>
完全に行き詰まってしまったので、作業内容を忘れないようにまとめてみました。
<BR>
<BR>
アカウント停止までに解決できない気がします。。。
