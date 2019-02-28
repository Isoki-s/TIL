# macのターミナルにgitのブランチ名を表示するやつ

ターミナルで[git-completion.bash]をファイル検索
 
```
$ mdfind git-completion.bash
```

以下のように出てくるのでどちらかをコピーしてエディタに貼り付け。  
一つしか出ない場合もある。 gitのインストール方法によって違う。  
verによってもソースが違う。違う 違う そうじゃ そうじゃない。

 ```
/Library/Developer/CommandLineTools/usr/share/git-core/git-completion.bash
/usr/local/Cellar/git/2.15.1/share/zsh/site-functions/git-completion.bash
 ```
 
ターミナルで[git-prompt.sh]をファイルを森田健作

$ mdfind git-prompt.sh

複数ある場合は使用するパスをコピーーーーーー

 ```
/Library/Developer/CommandLineTools/usr/share/git-core/git-prompt.sh
/usr/local/Cellar/git/2.15.1/etc/bash_completion.d/git-prompt.sh
 ```

## .bashrc
`~/.bashrc `に以下を追記する。ファイルがなければつくればいいじゃない。

```
# git settings
# 1,ここにコピーしたディレクトリ貼り付け
source /Library/Developer/CommandLineTools/usr/share/git-core/git-completion.bash
# 2,ここにコピーしたディレクトリ貼り付け
source /Library/Developer/CommandLineTools/usr/share/git-core/git-prompt.sh
GIT_PS1_SHOWDIRTYSTATE=true
export PS1='\[\033[32m\]\u@\h\[\033[00m\]:\[\033[34m\]\w\[\033[31m\]$(__git_ps1)\[\033[00m\]\$ '
```

## .bash_profile
`~/.bash_profile`に以下を追記する。パンがなければお菓子を食べればいいじゃない。

.bash_profileに.bashrcを読みに行く設定を追記。すでに記述済みであれば不要。

```
$ vi ~/.bash_profile

if [ -f ~/.bashrc ] ; then
. ~/.bashrc
fi
```

ターミナルを再起動してgit管理下のディレククトリに移動すれば、You can see it

# こんなに簡単な方法があった

`~/.bash_profile` に以下を記載するだけでいいそうだ。まだやっていない。

```
# Git branch in prompt.

parse_git_branch() {
  git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}

export PS1="\u@\h \W\[\033[32m\]\$(parse_git_branch)\[\033[00m\] $ "
```

By MARTIN FITZPATRICK at
https://www.mfitzp.com/article/add-git-branch-name-to-terminal-prompt-mac/
