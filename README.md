## 0. 事前準備

1. IBM Cloud ライトアカウント作成
2. GitHub アカウント作成

### OpenShift へのいろいろな入力パターン

![](./images/001.png)

本ハンズオンワークショップではこの中から Source to Image (S2I) を試します。
![](./images/002.png)

### ハンズオンワークショップの流れ

1. OpenShift 環境の準備
2. ソースコードの Fork
3. アプリケーションの Deploy
4. Webhook の設定
5. ソースコードの修正及び Deploy(⾃動）

## 1. OpenShift 環境の準備

ワークショップ⽤の IBM Cloud 環境にご⾃⾝の IBM Cloud ID を関連付けます。

注意事項

```
・ブラウザはFirefox, Chromeをご利⽤ください
・本ワークショップ⽤のIBM Cloud環境はセミナー開催時から24時間限定でお使いいただけます
```

### 1.1 指定 URL に Firefox ブラウザでアクセス

ワークショップの場合、講師よりアクセス先をご案内いたします。下記はサンプル URL となります。
https://openshiftdojo.mybluemix.net/

### 1.2 ハンズオン環境へ Submit

[Lab Key] 、[Your IBMid]にご⾃⾝の ID を⼊⼒し、チェックボックスにチェックを⼊れて[Submit]をクリックします。
![](./images/003.png)

### 1.3 IBM Cloud ダッシュボードの起動

Congratulations! が表⽰されたら[1. Log in IBM Cloud]リンクをクリックします。
![](./images/004.png)

### 1.4 アカウントの切り替え

IBM Cloud ダッシュボードの右上のアカウント情報の右横の「v」をクリックして、ワークショップ用のアカウントへ切り替えます。<br>
[1840867 – Advowork] のような「数字の羅列 - Advowork」がワークショップ用に準備されたアカウントです。 (数字部分は自動的に割り当てられます)<br>
※このアカウントは 1 日程度で無効になる一時的なアカウントです。
![](./images/005.png)

### 1.5 OpenShift クラスタへのアクセス

IBM Cloud ダッシュボードの右上のアカウント情報が変更されたことを確認し、[リソースの要約]の[Clusters]をクリックします。
![](./images/006.png)

Clusters の下のクラスター名をクリックします。 (クラスター名は⾃動的に割り当てられます)
![](./images/007.png)

### 1.6 OpenShift Web コンソールの起動

[OpenShift Web コンソール]ボタンをクリックします。<br>
※ポップアップが制御されていると動作しませんので解除してください。
![](./images/008.png)

新しいウィンドウ（またはタブ）で OpenShift のコンソールが開けば OK です。アクセスする URL はポート 30000 番台（⾃動で割り当てられます）を使っているので、社内プロキシなどで制限している場合はポートを開いておいてください。<br>
Web コンソールは、通常以下のような URL でリダイレクトされます。
`https://c100-e.jp-tok.containers.cloud.ibm.com:31379/`
![](./images/009.png)

これで OpenShift ワークショップの環境準備は完了です。

## 2. ソースコードの Fork

ここからは GitHub へアクセスして自分のリポジトリへサンプルソースコードを Fork していきます。

### 2.1 GitHub へのサインイン

GitHub にサインイン(Sign in)してください。まだアカウント登録されていない方は[こちら](https://github.com/)からサインアップ(Sign up)してください。<br>
![](./images/010.png)

### 2.2 リポジトリーの Fork

ブラウザーで[https://github.com/osonoi/node-build-config-openshift](https://github.com/osonoi/node-build-config-openshift)を開いてください。<br>
[Fork]ボタンをクリックして、自分のアカウントを選択してください。
![](./images/011.png)

### 2.3 自分のリポジトリーの確認

Fork する際に指定した自分のリポジトリーへ、対象のプロジェクトが Fork されたことを確認します。<br>
リポジトリーのパスの最初の部分が自分の GitHub アカウントになっていれば OK です。
![](./images/012.png)

## 3. アプリケーションの Deploy

ここからは、先程用意した OpenShift の環境へ、自分の GitHub リポジトリーにあるアプリケーションをデプロイします。

### 3.1 OpenShift Project の作成

OpenShift の Web コンソールへ戻り、[Project]ボタンをクリックします。<br>
その後[Create Project]ボタンをクリックすると Create Project 画面が開きますので、任意のプロジェクト名を入力してください。例では「Dojo」としています。
![](./images/013.png)

### 3.2 OpenShift ユーザータイプの切り替え

左上のメニューにて、[Administrator]から[Developer]に切り替えます。<br>
切り替えたら[From Git]をクリックしてください。
![](./images/014.png)

### 3.3 デプロイするアプリケーションのソースコードを指定

先ほどコピーした、自分の GitHub リポジトリーの URL を[Git Repo URL]に入力します。<br>
下の[Show Advanced Git Option]をクリックすると入力エリアが展開するので、[Content Dir]に「/site」と入力してください。
![](./images/015.png)

### 3.4 デプロイするアプリケーションのタイプを選択

言語やタイプの一覧がタイルで表示されるので、Node.js を選択します。今回 GitHub リポジトリーへ Fork したプロジェクトは Node.js アプリケーションだからです。<br>
選択したら[Create]ボタンをクリックしてください。
![](./images/016.png)

### 3.5 アプリケーションのデプロイ

アプリケーションのデプロイが始まります。1 分弱お待ちください。中の丸が青くなったら完成です。丸の中をクリックすると右側にメニューが出てくるので[Routes]の下の URL をクリックすると Web へ公開されたアプリケーションへアクセスできます。
![](./images/017.png)

### 3.6 アプリケーションへのアクセス

デプロイされ、Web へ公開されたアプリケーションへアクセスできました。<br>
実際にこのアプリケーションへログインしてみましょう。ID,Password ともに「test」と入れてログインしてください。<br>
医療関連のデータを管理するサンプルアプリケーションへログインできたかと思います。
![](./images/018.png)

ここまでで、GitHub 上のソースコードをダイレクトに OpenShift へデプロイする方法を学びました。

## 4. Webhook の設定

ここでは、GitHub 上のソースコードが変更された際に、自動的に OpenShift へデプロイされるように Webhook を GitHub 上へ設定していきたいと思います。

### 4.1 OpenShift の Webhook URL の取得

OpenShift の Web コンソールへアクセスします。左側のメニューから[Build]を選択し、右側のワークスペースに表示される[node-build-config-openshift]をクリックします。
![](./images/019.png)

下にスクロールして一番右の[Copy URL with Secret]をクリックして Webhook の URL と Secret をクリップボードにコピーしてください。
![](./images/020.png)

### 4.2 GitHub に Webhook を設定

GitHub の自分のリポジトリーへ戻り、[Settings] -> [Webhooks] -> [Add webhook]を選択します。
![](./images/021.png)

先ほどクリップボードにコピーした URL+secret を[Payload URL]に貼り付けてください。[Control type]は[application/json]を選択してください。
![](./images/022.png)

入力後、以下の図の様に緑のチェックマークが付いたら設定成功です。
![](./images/023.png)

これで webhook の設定は完了です。後はソースコードの修正で自動的にアプリケーションがデプロイされます。

## 5. ソースコードの修正及び Deploy(自動)

最後に、GitHub 上のソースコードを修正し、それが自動で OpenShift へ反映されることを試していきます。

### 5.1 ソースコードの修正

GitHub の自分のリポジトリ画面から[Site]フォルダーを選択します。
![](./images/024.png)

[public]フォルダ配下の[index.html]を選択しペンのアイコンをクリックして編集モードにします。<br>
ここでは、GitHub の GUI から編集を行いますが、ローカルに clone して編集したファイルを commit、push しても OK です。
![](./images/025.png)

変更点をクイックに確認するために、ここでは 23 行目の英文「Example Health」を日本語の「医療管理」に変更してみます。<br>
変更したらコミットしてください。自分所有のリポジトリーなので、そのまま反映されます。
![](./images/026.png)

OpenShift の Web コンソールへ戻り、左側の[Topology]を確認すると、再度デプロイがおこなわれていることが分かります。
![](./images/027.png)

再デプロイが完了したらデプロイしたアプリケーションを起動し直してください。（既に表示されている場合はリロードしてください）<br>
アプリケーション内にある見出しが「Example Health」から「医療管理」に変更されたことが確認できました。
![](./images/028.png)

お疲れさまでした！これで、OpenShift の S2I を使ったハンズオンワークショップは完了です。

## その他のアプリケーション

もし、PHP のサンプルアプリケーションで試してみたい方は下記のリポジトリーのソースコードを試してみてください。
[https://github.com/osonoi/php-s2i-openshift](https://github.com/osonoi/php-s2i-openshift)
![](./images/029.png)
