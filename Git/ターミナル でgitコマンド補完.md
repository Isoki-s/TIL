# Git-Completionをインストールする

- gitのタブ補完ツール。特にブランチ名補完が便利。 



# Code

Check brew list

```
$ brew list
```

bash-completionがなければ以下を実行してインストール。

```
$ brew install bash-completion
```

~/.bash_profile に以下を追記する。

```
# bash completion
if [ -f $(brew --prefix)/etc/bash_completion ]; then
  . $(brew --prefix)/etc/bash_completion
fi
```

# Git Completion の有効化

git-comletion.bash というファイルを探す。


```
$ mdfind -name git-completion.bash
```

git-completion.bash のフルパスが出力されるのでそれをコピピピ。

```
$ cp [コピーしたパスをここにうぇーーい] /usr/local/etc/bash_completion.d/git
```

再起動して、try
