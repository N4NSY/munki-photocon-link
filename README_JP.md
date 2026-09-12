# むんきちゃんフォトコン 固定リンク運用セット

## 目的

VRChatワールド内の告知ポスターに、まだ存在しないXの告知ポストURLを直接入れず、
先に固定URL・固定QRコードだけを配置しておくためのセットです。

固定URL（このREADMEでは以下を前提）:

https://n4nsy.github.io/munki-photocon-link/

公開前:
QR → 固定ページ → 「まだ公開前です」

告知ポスト公開後:
QR → 固定ページ → Xの告知ポストへ自動転送

Unity/VRChatワールドの再アップロードは不要です。


# 1. GitHubリポジトリを作る

GitHubで新しいPublicリポジトリを作成します。

Repository name:
munki-photocon-link

Owner:
N4NSY

Publicを選択してください。

※ リポジトリ名を変える場合は、
index.html 内の GITHUB_REPO とQRコードのURLも変更してください。


# 2. このフォルダのファイルをアップロード

最低限、以下をリポジトリ直下へ入れます。

- index.html
- config.json
- .nojekyll

README_JP.md はGitHub上に置いても置かなくても構いません。


# 3. GitHub Pagesを有効化

GitHubのリポジトリを開く

Settings
→ Pages
→ Build and deployment
→ Source: Deploy from a branch
→ Branch: main
→ Folder: /(root)
→ Save

公開URL:

https://n4nsy.github.io/munki-photocon-link/

最初だけGitHub Pagesの公開処理を待ちます。


# 4. QRコードをポスターへ載せる

同梱の

qr_munki_photocon.png

を告知ポスターに貼ってください。

できればQRの近くに文字でも

n4nsy.github.io/munki-photocon-link/

と書いておくと、QRが読めない場合の保険になります。

重要:
ポスターにはXのstatus URLを直接入れません。
この固定URLだけを使います。


# 5. 集会前

config.json はこの状態にしておきます。

{
  "released": false,
  "tweetUrl": "",
  "message": "フォトコンの詳細は集会終了後に公開します。"
}

この状態では固定ページを開いてもXへ飛びません。


# 6. 集会終了時の実際の操作

1. Xでフォトコン告知を投稿
2. 投稿したポストのURLをコピー

例:
https://x.com/N4NSY/status/1234567890123456789

3. GitHubの munki-photocon-link リポジトリを開く
4. config.json を開く
5. 鉛筆アイコン Edit this file
6. 下記のように変更

{
  "released": true,
  "tweetUrl": "https://x.com/N4NSY/status/1234567890123456789",
  "message": "フォトコンの詳細は集会終了後に公開します。"
}

7. Commit changes

これで完了です。

固定ページはGitHub Pages上の古いconfig.jsonだけに依存せず、
GitHub APIからmainブランチの最新config.jsonを直接確認するようにしています。

そのため、Pages側の再デプロイ完了を待たずに、
最新のtweetUrlを取得できる設計です。

ページを既に開いている人も65秒ごとに再確認します。
「今すぐ再確認」ボタンを押せばその場で再確認できます。


# 7. 次回また使う場合

イベント終了後や次回の準備時に config.json を

{
  "released": false,
  "tweetUrl": "",
  "message": "フォトコンの詳細は集会終了後に公開します。"
}

へ戻すだけです。

固定URLとQRコードは変わりません。


# VRChat側について

通常の一般ワールドでは、任意のWeb URLをブラウザで直接開くボタンは基本的に使えないため、
QRコードを入口にする運用を推奨します。

この構成ならUnity側にUdonSharpスクリプトを追加する必要はありません。

ポスターをPlane等へ貼り、
QRコードが十分な大きさで読めるように配置してください。


# QRコード運用の注意

- QRの周囲に余白を残す
- 極端に小さくしない
- Emissionを強くしすぎない
- lilToonの場合、照明で黒白が潰れない設定にする
- VR内で実機スマホから一度読み取り確認する
- URL文字列も併記する


# ファイル

index.html
  待機ページ + GitHubのconfig.json確認 + Xへの転送

config.json
  公開状態とX URLだけを管理するファイル

.nojekyll
  GitHub Pagesでそのまま静的ファイルを配信するための空ファイル

qr_munki_photocon.png
  固定URL用QRコード

qr_munki_photocon.svg
  ベクター版QRコード
