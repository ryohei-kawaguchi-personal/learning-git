# learning-git
git勉強用のリポジトリ

## [公式Book](https://git-scm.com/book/en/v2)
***
### 1章
SVNなどのVCS(Version Control System)はファイル毎に変更履歴を保持している。

<img src="readme_image/image.png" width="50%">

Gitはすべてのファイルの状態のスナップショットを撮り、そのスナップショットへの参照を格納している。

<img src="readme_image/image-1.png" width="50%">

Gitはコミットデータを削除しない

#### セットアップ
下の設定が優先的に設定されていく
- [path]/etc/gitconfig
  システム上のすべてのユーザーとそのすべてのリポジトリに適用される  
  `git config --system`
- ~/.gitconfig or ~/.config/git/config
  ユーザー固有の設定  
  `git config --global`
- [対象ディレクトリ]/.git/config
  ディレクトリ固有の設定  
  `git config --local`

※全ての設定を確認したいときは以下のコマンドを使う  
`git config --list --show-origin`
***
### 3章
### ブランチの概要
#### コミットとは何か？
コミットオブジェクト
- ステージしたコンテンツのスナップショット(treeオブジェクト)へのポインター
- 作成者
- メールアドレス
- コミットメッセージ
- 直前のコミットへのポインター

状態
- Modifired:ファイルは更新されているがコミットされていない状態
- Staged:
  次のコミットのスナップショットに入る更新されたファイルをマークしている状態
  各ファイルのチェックサム(ハッシュ値)が計算され、blobという単位でGit repositoryに保存する
- Committed:
  データがローカルデータベースに保存された状態
  各サブディレクトリ毎にチェックサムを計算し、treeオブジェクトとしてGit repositoryに保存する
  メタデータとルートプロジェクトのtreeオブジェクトへのポインターを持つCommitオブジェクトを作成する

<img src="readme_image/image-2.png" width="75%">
<img src="readme_image/image-3.png" width="75%">

#### 新しいブランチを作成する
`git branch hoge`  
現在実行しているのと同じコミットへの新しいポインターが作成される  
<img src="readme_image/image-4.png" width="25%">

#### 現在のブランチの切り替え
HEADが指すブランチへのポインターが切り替わる
`git branch hoge`コマンドでブランチを作成した直後は以下のようにHEADが指し示すブランチへのポインターは切り替わらない  
<img src="readme_image/image-5.png" width="25%">

ブランチを切り替えたい場合はcheckoutコマンドを実行する  
`git checkout hoge`  
するとHEADが切り替え先のブランチのポインターを持つようになる  
<img src="readme_image/image-6.png" width="25%">

ここで新しいコミットを実行すると次のようなイメージとなる  
<img src="readme_image/image-7.png" width="50%">

ブランチが分岐する場合は次のようなイメージ    
<img src="readme_image/image-8.png" width="50%">

### 基本的なBranchとMarge
**ストーリー**  
新しい機能を開発中、別の重要な問題が発生。hotfixが必要。次の流れで開発を行っていく。
1. 本番ブランチに切り替える  
   切り替えようとしているブランチと競合するコミットされていない変更がある場合、ブランチ切り替えはできない。  
   例：本番ブランチにREADME.mdがあり、featureブランチでREADME.mdを変更しているとき
   ```
    $ git status
    ブランチ feature
    Your branch is up to date with 'origin/feature'.

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git restore <file>..." to discard changes in working directory)
            modified:   README.md

    no changes added to commit (use "git add" and/or "git commit -a")

    $ git checkout main 
    error: Your local changes to the following files would be overwritten by checkout:
            README.md
    Please commit your changes or stash them before you switch branches.
    Aborting
   ```

2. hotfixブランチを作成する
3. hotfixブランチをマージする
4. 元の機能開発に戻る