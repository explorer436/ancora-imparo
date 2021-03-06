Git power user tips:

Are some of you guys power users of GIT? Are you someone who at some point had to fix an issue relating to git? 

This one isn�t a git command, but another tool you can tell git to use to render diffs:
https://github.com/so-fancy/diff-so-fancy
It makes git diff alot easier to read on the command line.



git pull origin master --ff-only
Pulls the latest changes into your branch without creating an extra merge commit. I run this command multiple times a day when I am working to avoid merge conficts.
If there is a merge conflict, I may drop the --ff-only flag to deal with the conflict asap. This avoids nasty merge conflicts later.
Fun fact - git pull is an alias for git fetch && git merge

You can also configure git to only allow fast forwards on pulls without having to set it everytime:
git config --global pull.rebase true
https://spin.atomicobject.com/2020/05/05/git-configurations-default/


Squashing commits is a great way to reduce the history. Especially if you have a long running branch that may have a bunch of merges in there
git checkout master
git checkout -b feature/my-branch-2
git merge --squash feature/my-branch
This command creates a new branch (my-branch-2) off of master, and merges in the changes from another branch. Squashing the commits along the way


If you have a file that you want to add to the .gitignore file, but is already in the git index, you will notice it can be a pain to remove it as git will ignore your ignore command for this file.
To work around this, you can re-index the repo
git rm -r --cached .
git add .
git commit -m "re-indexed"
This may look scary at first as it kicks every single file out of the repo and restages them. But dont worry, your change set will only show the files you are now not indexing


Renaming files can be a bit of a pain as git, by default, is not case sensitive. So if you rename a file you need to run the following command to ensure any case-sensitive changes are picked up
git mv -f test/postman/Pagro-Home-API.postman_collection.json test/postman/pagro-home-api.postman.collection.json


Another command I found helpful in the past was migrating code from an old repository to a new repository. I wanted to retain history along the way; to make it easier to pull changes over later. We did this recently with the migration of renters from docker to ocf
> git remote add original ssh://git@git.forge.lmig.com:7999/pagro/renters-api-sb2.git
> git pull original feature/migrate-to-ocf --allow-unrelated-histories

What this does is adds another remote (which I called original) to your repository. We prepped a branch over in the old application with the changes we thought may need to be pulled (feature/migrate-to-ocf).
We then pulled those changes over to the OCF application with the format git pull <remote name> <branch name>
This command is very similar to git pull origin master but with a different remote and branch.
The flag --allow-unrelated-histories was used as the new application had some baseline files/commits that the cloudforge market place already commited. This allowed us to work through the problem.
As changes were done in renters, instead of having to manually make the changes in two places; now the team can manually run git pull original develop to continue pulling in the latest changes with minimal merge conflicts and manual intervention


Git has an alias command built in that is cross platform.  https://www.git-scm.com/book/en/v2/Git-Basics-Git-Aliases (edited) 


git add .
git add -A
Both are very similar commands that read "add all files to the commit".
But did you know that . is used to add all files from your current location and its child directories; where -A is for all files in the git repository (including parent directories).


git bisect is a pretty powerful tool as well. Say you know there was a bug introduced between 2 commits, you can give it the known good commit and the known bad commit and step through the commits one at a time, running each one against a test script. For example, a jest suite.  It is very useful if you don�t know when a bug was introduced and need to identify the commit.
https://makandracards.com/makandra/17477-automated-git-bisect-will-make-your-day (edited) 

Anecdote about how much time bisect could save you:
At my old job, we were building mainline Linux kernels for specific pieces of hardware we supported. There was a bug in the linux kernels intel graphics stack that would occasionally prevent our hardware from booting.
I setup a test script that would run during a bisect, that would build to the device over SSH and reboot it N number of times. If the script was unable to establish an ssh connection within N seconds after a reboot, I had it throw an error.
Using that method I was able to let git bisect  run automatically and eventually we found the commit in the linux kernel that broke our hardware and were able to report the bug. (edited) 



git commit --amend allows you to re-write the last commit message


You can also use git commit --amend to add more changes to your last commit, if you forgot to stage a file(s) or need to tweak what you comitted without adding a second commit.


