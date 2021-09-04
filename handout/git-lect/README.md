# 工研雑講習 Git 編

## 事前準備編

### GitHub のアカウント作成

この講習では GitHub を使用するので GitHub のアカウントを作成してください。
淵野アタリさんが講習してくれたらしい…………

## Git とは

> Git（ギット）は、プログラムのソースコードなどの変更履歴を記録・追跡するための分散型バージョン管理システムである。
> (引用: https://ja.wikipedia.org/wiki/Git)

Wikipedia にはこのように記載されています。
しかしこのままではどのようなものなのか」良く分からないでしょう。
ですから補足説明をします。

ソースコードを書いたときに「昨日のコードではしっかり動いていたのに今は動かない」
なんてことを経験したことは無いでしょうか。

このときに役に立つのが Git です。

Git は変更履歴を記録します。
どのファイルにどのように変更をしたのかを記録するので正常に動作していたときのコードを引っ張ってくることが出来ます。

そして多くの場合、その変更履歴を大人数で共有します。
そのことにより同期を怠らなければ常に新しい変更をチーム全体で役立てることが出来ます。

## 何が嬉しいの

-   複数人で共同編集がしやすい
-   ファイルの状態を巻き戻せる
-   ブランチが作れる

### 複数人で共同編集がしやすい

共同編集がしやすいように設計されています。

共同編集に付きものの同じ所を別の人が同時に変更してしまったりブランチ（後述します）を作成することで作業内容が衝突しないように出来たりします。

### ファイルの状態を巻き戻せる

その通りです。

```bash
git checkout
```

コマンドを使います。

### ブランチが作れる

作業の枝分かれです。

ブランチを切って行った作業は他人に一切影響を与えないです。
これがとても素晴らしい。

## 実践 Git

### Git と GitHub の違い

GitHub は Git を活用したサービスです。

### git のはじめかた

#### ユーザ登録

git は変更履歴にユーザ名とメールアドレスを紐づけます。

そのときに使うアカウント情報です。

```bash
git config --global user.name "外部に公開される名前"
git config --global user.email "外部に公開されるメールアドレス"
```

[参考文献](https://docs.github.com/ja/github/setting-up-and-managing-your-github-user-account/managing-email-preferences/setting-your-commit-email-address)

## 実際に触る

### GitHub のアカウントを作成する

```bash
# sol にログインする
ssh X9999999@sol.edu.cc.uec.ac.jp

# git が使えるかを確認する
git --version
# git version 2.27.0

# もし使えないときは
echo 'module load git/2.27.0' >> ~/.tcshrc
exit

mkdir git_lect
cd git_lect

```

### `koken-lect-20210706`をフォークする。

フォークとは他人の Git リポジトリ（Git で変更履歴が保存されているディレクトリ）をコピーすることです。
GitHub 特有の作業です。

[ここから飛ぶ](https://github.com/Azuki-bar/koken-lect-20210706)

#### Git/ GitHub 講習の受講が初めての人

![GitHub-fork](./src/git_fork.png)

`https://github.com/<USER_NAME>/koken-lect-20210706`が存在することを確認する。

#### すでに fork したことがある人

下画像の緑色のボタンを押す。
![GitHub-forked](./src/fork-merged.png)

### 手元に最新のコードを取り寄せる。

#### Git/ GitHub 講習の受講が初めての人

```bash
git clone https://github.com/<USER_NAME>/koken-lect-20210706
cd koken-lect-20210706
```

#### すでに fork したことがある人

```bash
cd /path/to/koken-lect-20210706
git pull
```

### Git のありがたみを知ろう

`code`ディレクトリに移動し、中身を見る。

```bash
cd code
nano hello.rb
```

`hello.rb`の内部にある以下のコードを削除する。

```ruby
def hello()
  puts("Hello world!")
end

hello()
```

```bash
# hello.rb の変更を保存することを git に伝える
git add hello.rb

# 変更を保存する。
# ファイルの変更履歴をGitに保存する
git commit
# エディタが開く
# 1行目以降に変更の簡単な説明を書く（コミットメッセージと呼ばれています）
# もとからある部分は触らない
```

```bash
# git の保存履歴を確認する。
# commit ID と Author Date コミットメッセージが表示される
git log

#######
# 例
# commit 671e6b152c8ae0891e0c1591e997d86b0b8ce822 (HEAD -> master)
# Author: Azuki-bar <42642269+Azuki-bar@users.noreply.github.com>
# Date:   Sun Sep 5 01:15:54 2021 +0900
#
#     hello を削除しました。
#
# commit 92f1384a980748f1f4e47a60ab45ffbb67b0c7f4 (origin/master, origin/HEAD)
# Author: Azuki-bar <42642269+Azuki-bar@users.noreply.github.com>
# Date:   Sun Sep 5 00:45:02 2021 +0900
#
#     create other method
```

**間違えて**`hello`メソッドを削除してしまったので復旧させましょう。

```bash
git revert 671e6b152c8ae0891e0c1591e997d86b0b8ce822
# git revert は commit IDの変更を打ち消すコミットを保存する。
git revert 671e6b
# commit ID は先頭6桁くらいで問題ない
```

```bash
nano hello.rb
```

`hello`メソッドが復活していることを確認する。

### 手元の変更をみんなに知らせる

このようなタイトルを付けましたが、みんなに直接知らせることは出来ません。
あくまで全員が知ることの出来る環境にコードを置くだけです。

さて変更を他の人も見ることが出来るリモートリポジトリにアップロードしましょう。

ここでいうリモートリポジトリは GitHub 上にフォークした`<USER_NAME>/koken-lect-20210706`を指します。

```bash
git push
```

ブラウザで`https://github.com/<USER_NAME>/koken-lect-20210706`を確認しましょう。
変更が適用されていることが確認できれば OK です！

また、大元のディレクトリ（[Azuki-bar/koken-lect-20210706](https://github.com/Azuki-bar/koken-lect-20210706)）が変更されていないことも合わせて確認しましょう！

他人に影響を与えるのはそのような命令を明示的に書いたときだけ！！！！うれしい！！！！

ここまでが git を使う上でまず知っておきたい内容です！

### プルリクエストを出してみよう

自分が行なった変更で大元も変更したくなってきませんか？

その時に使用するのがプルリクエストです。
これは GitHub が提供している機能で、ここからの操作はブラウザを用いて行います。

![open PullRequest](./src/submit-PR.png)
![open PullRequest](./src/submit-PR-2.png)

この\[Create pull request]ボタンを押すと自分の手元で行なった変更が大元のリポジトリに提案されます。

<details>
<summary>厳密には</summary>
厳密に言うと fork は内部では`MY_USER_NAME/REPOGITORY_NAME/master/`のようなブランチを作成しており、
プルリクエストを発行し承認されることにより、このブランチでの変更が大元のmasterに反映されることとなっています。
</details>

### ブランチの説明

ブランチの説明したいけど難しいね。

ここで復習ですが、Fork した先の変更は Fork 元には影響を与えませんでした。

Fork はブランチの仕組みを活用したものです。

このようにして、変更を別の場所で行ない、
最後にレビュー（Review; Revue では無い）を受けることにより master という一番大切なところに変更が反映されるという
開発フローが最近主流になっていると言われています。

```bash
# ブランチを切るコマンド
git switch -c BRANCH_NAME
# 以降の変更は BRANCH_NAME上に保存される。

```

## <付録> Git コマンド集

### Git add

#### git add とは

`git add` とはファイルの変更を Git に教えてあげるコマンドです。

#### git add のつかいかた

```
git add <変更のあったファイル名>
```

### git commit

#### git commit とは

`git commit`とは`git add`で教えてあげたファイルの変更を保存することが出来るコマンドです。

#### git commit のつかいかた

```
git commit
```

これだけです。

### git push

#### git push とは

`git push`で`git commit`で保存した履歴をリモートに送れます。

#### git push のつかいかた

```
git push
```

これだけ

### git pull

#### git pull とは

`git pull`で GitHub などのリモート変更をダウンロードしてあげるコマンドです。（いろいろ省略した結果）

#### git pull のつかいかた

```
git pull
```

これだけです。

### git clone

#### git clone とは

リモートにある git 自体をコピーするコマンド

#### git clone の使い方

```
git clone https://github.com/<USER_NAME>/koken-lect-20210706.git
```
