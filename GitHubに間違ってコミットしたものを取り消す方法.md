## GitHubに間違ってコミットしたものを取り消す方法
※作業前に必ずバックアップを取っておくこと！！<br>
vim操作について：https://qiita.com/one-a/items/a4e1d5a736d8408fd089<br>
<br>
### 「参考サイト.txt」を削除する場合（コミット履歴のdiffも見れなくする）
参考サイト1：https://qiita.com/go_astrayer/items/6e39d3ab16ae8094496c<br>
参考サイト2：https://am1tanaka.hatenablog.com/entry/2015/07/08/173643<br>
<br>
（例：AndroidManifest.xmlを削除する場合）<br>
```
git filter-branch -f --tree-filter "rm -f 'app\src\main\AndroidManifest.xml'" HEAD
```
<br>
（例：データフォルダーを削除する場合）<br>

```
git filter-branch -f --tree-filter "rm -rf 'データ'" HEAD
```

<br>
※-fオプションで強制削除<br>
※「Cannot rewrite branches: You have unstaged changes.」と表示される場合：<br>
　ローカルのディレクトリごと削除してからバージョン情報（GitHub）より新規で読み込んでからコマンドを実行する<br>
　または<br>
　一度コミットしてから再度実行する<br>
※「You need to run this command from the toplevel of the working tree.」と表示される場合：<br>
　cdコマンドでプロジェクトのトップディレクトリ（appディレクトリの上）に移動してから再度コマンドを実行する<br>
↓<br>

```
git gc --aggressive --prune=now
```
↓<br>

```
git push --force-with-lease
```

または<br>
Android Studioで「強制プッシュ」<br>
<br>
### 特定のコミット履歴を削除する（なかったことにする）
参考サイト：https://qiita.com/mikene_koko/items/d9c8e093b56648e569ad<br>
<br>

```
git log --oneline
```

↓<br>
削除したいコミットメッセージの行を探し、左に黄色で表示されている7桁の英数字をコピーする<br>
（すべて表示されていない場合は、スクロールではなく下キーで確認する）<br>
コピーしたら「:q」と入力して終了する<br>
↓<br>

```
git rebase -i ｛上でコピーした7桁｝
```

↓<br>
「i」キーを押して挿入モードにする<br>
↓<br>
取り消したいコミットの行を見つけたら、先頭の「pick」を「drop」に置き換える<br>
（他の行はそのままにしておく）<br>
↓<br>
Escキーを押してノーマルモード（コマンド入力）に切り替える<br>
↓<br>
「:wq」と入力し、保存して終了する<br>
※編集を間違えた場合は「:q!」と入力し、保存せずに終了する<br>
↓<br>
```
git push --force-with-lease
```
または<br>
Android Studioで「強制プッシュ」<br>
<br>
## リモートリポジトリ確認コマンド

```
git remote -v
```

<br>
