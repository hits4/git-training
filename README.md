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

任意のコミットまでマージしたい場合は
    $ git merge [commid-id]

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

### tagの表示
    $ git tag

### tagを作る
    $ git tag -a [tag-name] -m [message]

### tagをpushする(要コミット)
    $ git push [remote-name]--tags
上記の省略形
    $ git push --tags

---
## コミット(history)の操作
いろいろとやり直ししたい場合、このセクションの操作をする。

### 直前のコミットを修正する
・直前のコミット漏れしたファイルを後から追加する
・直前のコミットコメントを修正する
    $ git commit --amend

### 任意のコミットの打ち消し(revert)
・指定したコミットハッシュを打ち消すコミットを新たに行うこと。
・オプション-nを指定しない限り、自動的にコミットされる。
・あくまでコミットを消すだけで、ワーキングディレクトリの中身は変わらない。
・既に公開してしまったremoteレポのコミットをやり直したいときとかに使う。
・localのやり直しであればぶっちゃけresetやamendの方がhistoryキレイになるのでそちらを使うべき。
・「逆向きのコミット」と言われており、打ち消したこともコミットログとして残る。
    $ git revert [対象のコミットID] --no-edit

コミットを逐次行わなずまとめて行う場合
    $ git revert -n <対象のコミットID>
    $ git revert -n <対象のコミットID>
　　　　　　・
　　　　　　・
　　　　　　・
    $ git commit

### コミットをresetする
・取り消したことはコミットログとして残らない。
・公開済みのremoteレポに対しては行うべきではない。

soft : コミットだけを無かったことにする
mixed : 変更したインデックスの状態を元に戻す
hard : 最近のコミットを完全に無かったことにする

    $ git reset [--mixed | --soft | --hard]  [<commit>]

直前のコミットをリセット
    $ git reset --soft HEAD^

n個前のコミットをリセット
    $ git reset ---soft HEAD~n

### コミット履歴を書き換える(書き換え、統合)
・pushする前にコミットコメントをきれいに書きなおす
・意味的に同じ内容のコミットをわかりやすいように一つにまとめる
・コミット漏れしたファイルを後から追加する

    $ git rebase -i [修正する範囲]
    $ git rebase -i HEAD~~

### merge時にコミットをひとつにまとめる(squash)
・トピックブランチ中のコミットを一つにまとめて統合ブランチに統合する時などに使う。

    $ git merge --squash [branch-name]


## Githubとの接続設定
githubとの接続にはhttpsとssh接続(git@)が選べる。
githubの推奨はhttps

### 現在の接続設定を確認する
    $ git remote -v

### sshとhttpsを切り替える
    $ git remote set-url HTTPSかSSHのURL

### httpsでRepository not found.が出る場合
結論 : 認証が通っていないから。以下のいずれかの形式にする必要がある。

    https://{ユーザ名}:{パスワード}@github.com/ponsuke/repository.git

二段階認証している場合

    https://{ユーザ名}:{トークン}@github.com/ponsuke/repository.git

トークンの取得方法等はこちらを参照
https://qiita.com/ponsuke0531/items/4fe191b7bed03342cff2

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

## Github Desktopとgit bashについて
sshを使っている場合、レポの場所は以下のようの記法になる。
git@github.com:sdtechinc/sam-comperio.git

configのurlが上記のようだと、 コンソールからは正しくアクセスできる。
しかし、github desktopからはアクセスできない。
github desktopからアクセスするにはURLをhttpsにしなくてはいけない。
https://github.com/sdtechinc/sam-comperio.git

つまり、今のところSSH利用前提であれば、
両方を同時に使う事ができない。

## KEYWORDS/用語

### masterとは
デフォルトのブランチ名

### originとは
リモートサーバー名のデフォルト名

すなわちorigin/masterとはデフォルトのリモートサーバー名のデフォルトブランチを指している。
