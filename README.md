# learning-git
git勉強用のリポジトリ

## [公式Book](https://git-scm.com/book/en/v2)
### 1章
SVNなどのVCS(Version Control System)はファイル毎に変更履歴を保持している。
<img src="image.png" width="50%">

Gitはすべてのファイルの状態のスナップショットを撮り、そのスナップショットへの参照を格納している。
<img src="image-1.png" width="50%">
***
Gitはコミットデータを削除しない
### セットアップ
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

### 2章
###
`git branch`