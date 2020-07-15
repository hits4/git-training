## gitチートシート
https://qiita.com/TaaaZyyy/items/b2b68aec99789374a204


## レポジトリの作成/クローン

### ローカルにレポを作る
    git init

### 既にあるレポをcloneする
    $ git clone [URL]

### ローカルに作ったレポをremoteにプッシュする一連の操作
    $ git init
    $ git add -A
    $ git commit -m "init"
    $ git remote add origin [url]
    $ git push -u origin master

---
## add

・一度addしたものを取り消す。
git reset HEAD ファイル名


・ファイルへの変更の取り消し
git checkout -- ファイル名


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

# リモートの操作

## リモートレポジトリの追加
$ git remote add [remote-name] URL

## リモートレポジトリの削除
$ git remote rm [remote-name]

## リモートレポジトリのリネーム
$ git remote rename [old-remote-name] [new-remote-name]

## リモートからのフェッチ(マージしない)
$ git fetch [remote-name]

## リモートからのプル(マージする)
$ git pull 

## push 
$ git push origin master
上記の省略形として
$ git push

---

# tagの操作

## tagの表示
$ git tag

## tagを作る
$ git tag -a [tag-name] -m [message]

## tagをpushする(要コミット)
$ git push [remote-name]--tags
上記の省略形
$ git push --tags

---

## マージ/差分管理
GUIでdiff見る
$ git difftool

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
