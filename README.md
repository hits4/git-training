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
    $ git log --oneline


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
## HEADの操作
HEADとは現在のコミットへのポインタ。
言い換えれば作業中を示すためのもの。 HEADは任意のコミットに変更できる

### HEADを1つ前に戻す
    $ git checkout HEAD^
または
    $ git checkout HEAD~

### HEADを3つ前に戻す
    $ git checkout HEAD^^^
または
    $ git checkout HEAD~3

※厳密には
~(チルダ)を後ろに付け加えることで何世代前の親かを指定することができます。
^(キャレット)は、ブランチのマージで親が複数ある場合に、何番目の親かを指定することができます。

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

### リモートブランチの削除
    $ git push [remotename] --delete [branch-name]

----
## merge / fetch / pull
fetch : /origin/masterに情報を取得する。ローカルへのマージはしない。
merge : fetchした情報をマージする。マージ時はどうもcommitがされるようだ。

### origin/masterの内容をローカルmasterにマージ(ローカルの「origin/master」ブランチ → ローカルの「master」ブランチ)
    $ git merge origin/master    
上記のショートハンド
    $ git merge

リモートからフェッチ情報をローカルにマージする場合は次の手順となる。
    $ git fetch origin master
    $ git merge origin/master    

### リモートからのプル(== fetch + mergge)
    $ git pull 

参考: [fetch, merge, pullについて]https://qiita.com/wann/items/688bc17460a457104d7d

### マージ済みブランチの表示
    $ git branch --merged
    
### マージされていないブランチの表示
   $ git branch --no-merged

---
## rebase
マージと同等の事を行う方法としてrebaseがある。
マージとの違いはヒストリのラインが一本化されて美しく見える。変更履歴の直列化といえる。
rebaseは差分パッチを取得し、それを適用する。
https://git-scm.com/book/ja/v2/Git-%E3%81%AE%E3%83%96%E3%83%A9%E3%83%B3%E3%83%81%E6%A9%9F%E8%83%BD-%E3%83%AA%E3%83%99%E3%83%BC%E3%82%B9

rebaseはリモート(公開repo)に対して使わない方がいいっぽい。
プッシュする前の作業をきれいに整理する手段としてだけリベースを使い、まだ公開していないコミットだけをリベースすることを心がけていれば、何も問題はありません。

## リベース
ブランチの内容をmasterにリベースする場合    
    $ git checkout [branch-name]
    $ git rebase master

    $ git checkout master
    $ git merge [branch-name]

---
## tagの操作
*軽量タグ*
・名前を付けられる

*注釈付きタグ*
・名前を付けられる
・コメントを付けられる
・署名を付けられる

### tagの表示
    $ git tag

### tagを作る
    $ git tag -a [tag-name] -m [message]

### tagをpushする(要コミット)
    $ git push [remote-name]--tags
上記の省略形
    $ git push --tags

---
## いろいろなやり直し

### 直前のコミットを修正する
・直前のコミット漏れしたファイルを後から追加する
・直前のコミットコメントを修正する
    $ git commit --amend

### 任意のコミットの打ち消し
    revert

### コミットをresetする
・取り消したことはコミットログとして残らない。

soft : コミットだけを無かったことにする
mixed : 変更したインデックスの状態を元に戻す
hard : 最近のコミットを完全に無かったことにする

    $ git reset [--mixed | --soft | --hard]  [<commit>]

直前のコミットをリセット
    $ git reset --soft HEAD^

n個前のコミットをリセット
    $ git reset ---soft HEAD~n

### コミットをrevertする
・指定したコミットハッシュを打ち消すコミットを新たに行うこと。
・オプション-nを指定しない限り、自動的にコミットされる。
・「逆向きのコミット」と言われており、打ち消したこともコミットログとして残る。
    $ git revert [対象のコミットID] --no-edit

コミットを逐次行わなずまとめて行う場合
    $ git revert -n <対象のコミットID>
    $ git revert -n <対象のコミットID>
　　　　　　・
　　　　　　・
　　　　　　・
    $ git commit

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
