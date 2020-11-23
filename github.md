# git
## Sample git configuration file
- set up your .gitconfig @ ~/ or project specific
```
[user]
name = Reinaldo Molina
email = rmolin88@gmail.com
[core]
editor = gvim
[remote "origin"]
url = http://github.com/rmolin88/vimrc.git
fetch = +refs/heads/*:refs/remotes/origin/*
					 [credential]
					 helper = wincred # for windows
#helper = cache --timeout 30000 # for unix 2 below
#helper = store --file /mnt/thumbdrive/.git-credentials
[diff]  
tool = gvim
[difftool "gvim"]  
cmd = "C:/Users/USER/Downloads/vim/complete-x86/gvim.exe -d \"$LOCAL\" \"$REMOTE\""
[merge]  
tool = gvim
[mergetool "gvim"]  
cmd = "C:/Users/USER/Downloads/vim/complete-x86/gvim.exe -d \"$BASE\" \"$LOCAL\" \"$REMOTE\" \"$MERGED\""
prompt = false
					*make sure you have internet
					git init
					git add remote origin
					this downloads your _vimrc
```

## Going back to old commit
  - 9/22/2016 12:19:34 PM
  - you can do this through the browser. Click on the repo number of commits.
  - There you can just copy or do anything you like and see the state of your
  repo through each commit 
  - Or you can create a branch `git checkout -b justin a9c146a09505837ec03b`
  - Checkout `.bash\_aliases` to get the SHA1 of each of your commits.
  Specifically the log commands.

## General good practices
  - 9/22/2016 12:18:37 PM 
  - Is always a good idea when messing with branches and with git 
  to clone your repo somewhere and mess with stuff there and never commit.
  - You can always delete that repo
