---
title: "眠れるWiiバランスボードよ、Raspberry Pi 4で目覚めよ！ 自宅でスマートトレーニングのススメ"
date: 2026-06-28 07:00:31 
description: "WiiバランスボードをRaspberry Pi 4とBluetoothで接続し、自宅で手軽に体幹トレーニングを行う方法を解説します。眠っていたバランスボードを再活用し、Pythonを使って計測データを可視化。初心者でも安心のセットアップ手順も網羅し、パーソナルな健康管理システムを構築しましょう。"
categories:
  - 技術
  - ガジェット
  - GitHub
tags:
  - 技術
  - ガジェット
  - GitHub
---
# {{ page.title }}
<p>{{ page.date }}</p>
![アイキャッチ画像](https://images.pexels.com/photos/17122728/pexels-photo-17122728.jpeg?auto=compress&cs=tinysrgb&h=350)


皆さん、こんにちは！独楽鼠吾郎です。

Wii Fitで一世を風靡したWiiバランスボード。かつてはリビングの主役だったこのガジェット、今や押し入れの奥で眠っていませんか？ 独楽鼠吾郎は、そんな眠れるバランスボードに**Raspberry Pi 4**という新しい心臓を注入し、自宅で手軽にパーソナルトレーニングを実現する方法をご紹介します。

### なぜ今、WiiバランスボードとRaspberry Pi 4なのか？

「スマートな体幹トレーニングツールが欲しいけれど、市販品は高価だ…」と感じている方も多いのではないでしょうか。実は、中古のWiiバランスボードは手軽に入手可能で、そこにRaspberry Pi 4を組み合わせることで、高機能な計測デバイスに早変わりさせることができるのです。

この組み合わせの最大のメリットは、その**カスタマイズ性と拡張性**にあります。Pythonを使ってプログラマブルに制御できるため、ただ体重を測るだけでなく、重心移動のリアルタイムな可視化、トレーニングメニューとの連携、さらには長期的な健康データログの構築まで、皆さんのアイデア次第で無限の可能性が広がります。

### 準備するもの

今回のプロジェクトに必要な主なアイテムは以下の通りです。

*   **Raspberry Pi 4** (メモリ4GB以上推奨)
*   **Wiiバランスボード** (Wii Fit同梱品でOK)
*   **microSDカード** (16GB以上、高速なものが望ましい)
*   **Raspberry Pi用電源** (公式推奨品が安定します)
*   **HDMIケーブル、モニター、USBキーボード/マウス** (初回セットアップ時のみ)
*   **インターネット接続環境** (Wi-Fiまたは有線LAN)

### Raspberry Pi 4 セットアップ手順

まずはRaspberry Pi 4を動かすための基本的なセットアップから始めましょう。今回は、コマンドライン操作がメインとなるため、軽量な**Raspberry Pi OS Lite**（64-bit）を使用します。

#### 1. Raspberry Pi OSのインストール

PCにRaspberry Pi Imagerをダウンロードし、以下の手順でmicroSDカードにOSを書き込みます。

1.  Raspberry Pi Imagerを起動します。
2.  「OSを選ぶ」で「Raspberry Pi OS (other)」から「**Raspberry Pi OS Lite (64-bit)**」を選択します。
3.  「ストレージを選ぶ」で、用意したmicroSDカードを選択します。
4.  **重要！** 書き込み前に設定アイコン（歯車マーク）をクリックし、SSHを有効にし、ユーザー名とパスワードを設定しておくことを強くお勧めします。Wi-Fiもここで設定しておけば、モニターやキーボードなしでSSH接続が可能になり、その後の作業が格段に楽になります。
5.  「書き込む」をクリックし、指示に従って書き込みを完了させます。

書き込みが完了したら、microSDカードをRaspberry Pi 4に挿入し、電源を投入してください。

#### 2. 初期設定とシステムのアップデート

SSHでRaspberry Piに接続するか、モニター・キーボードを接続してターミナルを開き、以下のコマンドを実行します。システムのパッケージリストを更新し、インストールされているソフトウェアを最新の状態にします。

```bash
sudo apt update
sudo apt upgrade -y
```

#### 3. 必要なパッケージのインストール

WiiバランスボードとBluetooth接続を行うために、いくつかのパッケージとPythonライブラリをインストールします。

まず、Bluetooth関連のツールとPythonのpipをインストールします。

```bash
sudo apt install bluetooth bluez python3-bluez python3-pip -y
```

### WiiバランスボードとRaspberry Pi 4をBluetoothで接続する

ここが今回のプロジェクトの核心となる部分です。Wiiバランスボードは、Bluetooth LEではなく、レガシーなBluetooth Classic接続を使用します。

#### 1. Bluetoothサービスの確認

BluetoothサービスがRaspberry Pi上で正しく動作していることを確認します。

```bash
sudo systemctl status bluetooth
```

もし「inactive (dead)」と表示される場合は、以下のコマンドでサービスを開始・有効化してください。

```bash
sudo systemctl start bluetooth
sudo systemctl enable bluetooth
```

#### 2. Bluetoothctlでのペアリング

`bluetoothctl`ツールを使って、Wiiバランスボードをペアリングします。

```bash
bluetoothctl
```

`[bluetooth]#`というプロンプトが表示されたら、以下のコマンドを順に実行します。

```bluetoothctl
agent on
default-agent
scan on
```

ここで、Wiiバランスボードの電源ボタン（電池ボックスの中にある赤いボタン）を押し、検出モードに入れます。数秒待つと、`[NEW] Device XX:XX:XX:XX:XX:XX Nintendo RVL-WBC-01` のようにWiiバランスボードが検出されるはずです。表示されたMACアドレス（`XX:XX:XX:XX:XX:XX`の部分）をメモしておきましょう。

検出されたら、`scan off`でスキャンを停止し、以下のコマンドでペアリング、信頼設定、接続を行います。

```bluetoothctl
scan off
pair [WiiバランスボードのMACアドレス]
# パスキーの入力を求められたら '0000' を入力してください（一部のWiiリモコン/ボードで必要）
trust [WiiバランスボードのMACアドレス]
connect [WiiバランスボードのMACアドレス]
```

接続に成功すると、「Connection successful」のようなメッセージが表示されます。これで物理的なBluetooth接続は完了です。`quit`と入力して`bluetoothctl`を終了します。

#### 3. Pythonスクリプトの導入と実行

Bluetooth接続が確立されたところで、Wiiバランスボードからデータを取得するためのPythonスクリプトを導入しましょう。

独楽鼠吾郎のGitHubリポジトリでは、WiiバランスボードとRaspberry Pi 4をBluetoothで接続し、データを取得・活用するためのPythonスクリプトを公開しています。

{% include link-card.html url="https://github.com/komasn/wiiboard_trainer" title="wiiバランスボードとRaspberrypi4でトレーニング（関連アイテム）" context="wiiバランスボードとRaspberrypi4をBluetoothで接続した" %}

このリポジトリをRaspberry Piにクローンし、必要なPythonライブラリをインストールします。

```bash
git clone https://github.com/komasn/wiiboard_trainer.git
cd wiiboard_trainer
pip install -r requirements.txt
```

これで準備は万端です。リポジトリ内のサンプルスクリプト（例えば`main.py`や`wiiboard_logger.py`など）を実行することで、Wiiバランスボードからリアルタイムで体重や重心移動のデータが取得できるようになります。

```bash
python3 main.py
# または
python3 wiiboard_logger.py
```

### トレーニングデータの取得と活用

スクリプトを実行すると、Wiiバランスボードの各センサーからのデータがリアルタイムで表示されます。得られる主なデータは以下の通りです。

*   **左上前方 (TL)**: 左足前方センサーの荷重
*   **右上前方 (TR)**: 右足前方センサーの荷重
*   **左下後方 (BL)**: 左足後方センサーの荷重
*   **右下後方 (BR)**: 右足後方センサーの荷重
*   **合計体重 (Total Weight)**: 4つのセンサーの合計荷重
*   **重心位置 (Center of Pressure - CoP)**: 体重の重心位置 (X, Y座標)

これらのデータをCSVファイルに保存したり、Pythonの`matplotlib`ライブラリなどを使ってグラフで可視化したりすることで、自分の重心移動の癖や体幹の安定性を客観的に把握できます。例えば、片足立ちのトレーニング中にCoPの動きを記録すれば、バランス能力の向上を数値で確認できるでしょう。

さらに、これらのデータをWebインターフェース（FlaskやDjangoなど）を構築してブラウザからリアルタイムで確認したり、データベース（SQLiteなど）に保存して長期的なトレーニングログとして活用することも可能です。

### さらなる高みへ！カスタマイズと応用

今回ご紹介したシステムは、あくまでWiiバランスボードをRaspberry Pi 4で動かすための基盤です。皆さんのアイデア次第で、様々な応用が考えられます。

*   **特定のトレーニングメニューとの連動**: スクワットの深さやプランクの姿勢維持時間など、特定のトレーニングと連携させてフィードバックを与える。
*   **日々の重心データの記録と分析**: 毎日の重心移動データを記録し、専用の健康アプリと連携させて、体の変化や歪みを早期に発見する。
*   **ゲーム化**: バランスボードを使ったオリジナルのミニゲームを作成し、楽しく運動を継続する。
*   **高齢者の転倒予防トレーニング**: 重心移動の癖を検出し、転倒リスクを低減するためのトレーニングプログラムを支援する。

### まとめ

独楽鼠吾郎が今回ご紹介したWiiバランスボードとRaspberry Pi 4を組み合わせたDIYトレーニングシステムは、手軽に始められ、かつ高いカスタマイズ性を持っています。押し入れに眠っていたガジェットが、皆さんの健康的な生活をサポートする強力なツールへと生まれ変わる可能性を秘めているのです。

ぜひこの機会に、ご自身のWiiバランスボードとRaspberry Pi 4を活用して、スマートな体幹トレーニングを始めてみませんか？ きっと新しい発見があるはずです。それでは、また次回の記事でお会いしましょう！