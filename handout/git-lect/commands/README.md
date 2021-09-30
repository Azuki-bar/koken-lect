# <付録> Git コマンド集

-   [<付録> Git コマンド集](#付録-git-コマンド集)
    -   [はじめに](#はじめに)
    -   [コマンド集](#コマンド集)
        -   [Git add](#git-add)
            -   [git add とは](#git-add-とは)
            -   [git add のつかいかた](#git-add-のつかいかた)
        -   [git commit](#git-commit)
            -   [git commit とは](#git-commit-とは)
            -   [git commit のつかいかた](#git-commit-のつかいかた)
        -   [git push](#git-push)
            -   [git push とは](#git-push-とは)
            -   [git push のつかいかた](#git-push-のつかいかた)
        -   [git pull](#git-pull)
            -   [git pull とは](#git-pull-とは)
            -   [git pull のつかいかた](#git-pull-のつかいかた)
        -   [git clone](#git-clone)
            -   [git clone とは](#git-clone-とは)
            -   [git clone の使い方](#git-clone-の使い方)

## はじめに

Git のコマンド群は`git SOME_COMMAND --help`でヘルプページを読むことが出来ます。

このページの内容はどこよりも信頼出来るものですから、分からないことがあったら一読することを強くおすすめします。

## コマンド集

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

`git push`を使うと`git commit`で保存した履歴をリモートに送れます。

#### git push のつかいかた

```
git push
```

これだけです。

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

リモートにある git 自体をコピーするコマンドです。

#### git clone の使い方

```
git clone https://github.com/<USER_NAME>/koken-lect-20210706.git
```
