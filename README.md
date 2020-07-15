## gitチートシート
https://qiita.com/TaaaZyyy/items/b2b68aec99789374a204


## 状態の確認

### staged / modified / untracked の一覧	
    $ git status

### ローカルブランチの一覧	
    $ git branch

### ローカルブランチとリモート追跡ブランチの一覧	
    $ git branch -a

### [履歴] 現在のブランチの履歴	
    $ git log


---

## マージ/差分管理

### [差分] ワーキングディレクトリ と ステージングエリア の差分を表示
    $ git diff

### GUIでdiff見る
    $ git difftool

※difftoolは.gitconfigであらかじめ設定しておく

---- 
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

## ステージング

### add 
    $ git add [file]

### すべてのmodifiedをadd
    $ git add -u

### すべてのファイルをadd
    $ git add -A

### カレントディレクトリをすべてadd
    $ git add .

### stagedからmodifiedに戻す
    $ git reset [file]

### 一度stagedしたものをHEADの状態に戻す
    $ git reset HEAD [file]

### 追跡対象(tracked)から削除(ファイルも削除)
    $ git rm [file]

### 追跡対象(tracked)から削除(ファイルは残る)
    $ git rm --cached [file]

---

## コミット

### addしてcommit
git commit -a -m [message]

### gitのcommitのやり直し(上書き)コマンド
    $ git commit --amend

### amendの一連の使い方
    $ git commit -m 'initial commit'
    $ git add forgotten_file
    $ git commit --amend -m [new-message]

---

## チェックアウト

### チェックアウト
    $ git checkout [branchname]

### ブランチ作成 + チェックアウト
    $ git checkout -b [branchname]

### 特定のコミットからブランチ作成 + チェックアウト
    $ git checkout -b [branchname] [commit-id]

### 任意のファイルを指定してチェックアウト(ファイルへの変更を戻す)
    $ git checkout -- [file]

---

## リモートの操作

### リモートレポジトリの一覧
    $ git remote

### リモートレポジトリの追加
    $ git remote add [remote-name] URL

### リモートレポジトリの削除
    $ git remote rm [remote-name]

### リモートレポジトリのリネーム
    $ git remote rename [old-remote-name] [new-remote-name]

### リモートからのフェッチ(リモートの「master」ブランチ → ローカルの「origin/master」ブランチ)
    $ git fetch [remote-name]

### origin/masterの内容をローカルmasterにマージ(ローカルの「origin/master」ブランチ → ローカルの「master」ブランチ)
    $ git merge
フェッチとマージの一連の流れ
    $ git fetch origin master
    $ git merge origin/master    

### リモートからのプル(== fetch + mergge)
    $ git pull 

参考: [fetch, merge, pullについて]https://qiita.com/wann/items/688bc17460a457104d7d

### push 
    $ git push origin master

上記の省略形として
    $ git push

---
## branch

brachとはコミットに対するポインタである。初期状態で作られるmasterもbranchである。
また、 HEADは現在のワーキングディレクトリを指すためのbranchへのポインタといえる。
(HEAD == 現在の作業ブランチ == 現在のコミット)

### ローカルレポジトリにbranchを作成する
    $ git branch [branch-name]

### ワーキングディレクトリを任意のbranchに切り替える
    $ git checkout [branch-name]

### ブランチを作成 + 作成したブランチに切り替える(ショートハンド)
上記2つをまとめて実行してくれるショートハンド。
    $ git checkout -b [branch-name] 

### リモートのブランチを作成 + 作成したブランチに切り替える
    $ git checkout -b [branch-name] [remotename]/[branch-name] 

上記のショートハンド
    $ git checkout --track [remotename]/[branch-name] 

上記のさらにショートハンド。ローカルにない場合自動でチェックアウト
    $ git checkout [branch-name]

### 既に手元にあるローカルブランチを、リモートブランチにも作成
    $ git branch -u [remotename]/[branch-name] 
または
    $ git branch --set-upstream-to [remotename]/[branch-name] 

### ブランチの削除
    $ git branch -d [branch-name]

### マージ済みブランチの表示
    $ git branch --merged
    
### マージされていないブランチの表示
   $ git branch --no-merged

---
## tagの操作

### tagの表示
    $ git tag

### tagを作る
    $ git tag -a [tag-name] -m [message]

### tagをpushする(要コミット)
    $ git push [remote-name]--tags
上記の省略形
    $ git push --tags


--- 
## ユーザー管理とパスワード

### ユーザー名、emailなどの設定
$ git config --[system/global/local] user.name ["ユーザー名"]
$ git config --[system/global/local] user.email ["ユーザー名"]

### git configをコマンドラインで編集
$ git config --[system/global/local] -e

### 「資格情報マネージャ」の無効化
windows版gitは認証情報をwindowsの「資格情報マネージャ」で管理してしまう。
これが有効だと、.configのuser情報が無視されてしまうので、無効にする。
$ git config --system -e

https://qiita.com/tyori03/items/3cc2915f7429251eb908

### パスワードの保存
$ git config --global credential.helper store

---

## KEYWORDS/用語

### masterとは
デフォルトのブランチ名

### originとは
リモートサーバー名のデフォルト名

すなわちorigin/masterとはデフォルトのリモートサーバー名のデフォルトブランチを指している。
