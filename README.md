## レポジトリの作成/クローン

###ローカルにレポを作る
git init

###clone
$ git clone https://github.com/schacon/ticgit


---
## コミット
### gitのcommitのやり直し(上書き)コマンド
$ git commit --amend

### amendの使い方
$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend


### addしてcommit
git commit -a -m 'added new benchmarks'

### 追跡対象から削除
git rm

### ファイルは残して追跡対処うから削除
$ git rm --cached README

## リモートの操作

## push 
$ git push origin master

---

## マージ/差分管理
GUIでdiff見る
$git difftool

difftoolは.gitconfigであらかじめ設定しておく

--- 
## ユーザー管理とパスワード

### 「資格情報マネージャ」の無効化
windows版gitは認証情報をwindowsの「資格情報マネージャ」で管理してしまう。
これが有効だと、.configのuser情報が無視されてしまうので、無効にする。
git config --system -e

https://qiita.com/tyori03/items/3cc2915f7429251eb908

### パスワードの保存
git config --global credential.helper store
