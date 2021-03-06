Git
================

### 1.git commands(build and edit git files)

#### git init

cd any folder you want to track history, use git init to build a empty Git repository

> **git can not track the word document**

#### git commit

git commit -m "with the message you want to keep up with"
once it has been saved, it will show (1) file changed, and (2) insertions(how many lines)

#### git commit & git add

1.  the difference between git add and git commit is that the git add is just temportary save the changes while the git commit will save the changes eventually.

2.  we can add several files to be commited

> 1.  git track the changes not the files. if you dont add changes to the stage, when you commit the file, it will not change anything.

#### git status and git diff

use git status to check what has been modified and use git diff to see the difference

> use git diff HEAD -- readme.txt to the the difference between the wd ver and new ver.

#### git log

1.use git log to check all commit

2.can add --pretty=oneline to see simpler version.(has commit id before, HEAD -&gt; master is the current version)

#### git reset

1.the last ver. is HEAD^, last 100 is HEAD~100

2.git reset --hard HEAD^

3.**use cat to see the contents**

4.one more time to go back the previous one(not reset):git reset --hard (commit id)

#### git reflog

to see every command(check to see which ver. we need to go back)

#### git checkout --file(luck) and (unluck) git reset HEAD <file>;git checkout --file

delete all the chages made in wd.(**note that the --**)

1.(LUCKY) hasnt added to the stage, it will look exactly like in the file.

2.(UNLUCKY) has added to the stage, look same in the stage. use git reset HEAD <file> will unstage.

1.  already commit, use the reset one(only works when you not yet upload to remote)

#### git branch

git branch to check the current branch, and git branch a will set a new branch a , but a is subbranch the master branch, if you want the develop based on a, you need to change to a branch, git checkout a. (**make two steps in one git checkout -b a**)

#### git merge

1.first step is to change to master branch and use git merge a 2.delete used branch a use git branch -d a(use branch -D a to force delete a)

#### git tag

to check if v1.0 has the same bug as v1.1(new version)

1.  just use git tag v1.0 or v1.1
2.  use git tag to see the tag history
3.  if want to change to a certain tag, use git checkout v1.0

### 2. working directory concept

wd -&gt;(add) stage(after add, where to store the files temporary) -&gt;(commit) current branch

### Delete git files

In git, deleting is also a editing action

after rm test.txt, git knows that you had deleted the file, two options:

1.  use git rm test.txt and commit -m "remove" to delete

2.  use git checkout -- test.txt to restore.(use the brunch version to substitute the wd ver.)

### remote

1.first time to add remote with github repo, use git remote add origin <git@server-name>:path/repo.git;

2.then, git push -u origin master to push everthing the first time;

3.after the first time, use git push origin master to push the new ver.

### clone from the repo

1.build a repo in github

1.  git clone <git@github.com>:renyugt/gitskills.git

### branches

#### fast-forward

we can save in different branches to make sure not commit something incompelte and not afraid to lose any tracks.

1.  HEAD is not point to new commit but point to the master, master(a line(point-timeline)) is point to the new commit, so the HEAD is point to the current branch.

2.  when add a new branch, the HEAD will always follows the current branch, and the master will not change the pointer, and the HEAD move forwardly(point-timeline).

3.git branch to check the current branch, and git branch a will set a new branch a , but a is subbranch the master branch, if you want the develop based on a, you need to change to a branch, git checkout a. (**make two steps in one git checkout -b a**) (only checkout means switch)

1.  merge the new branch with master: git merge dev.(show the fast-forward:change the pointer)

2.  git branch -d dev

3.  check:git branch

#### can not be done with fast forward

1.  both add something new in master and new branch

2.use cat to see again, will show &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;(directly in the txt)

1.  edit in file, add and commit again.

2.  git log --graph --pretty=online --abbrev-commit will show the garph

#### stratgies

1.git will auto use fast forward, under this, after deleting the branch, it will lose the track of info on branch.

1.  use git merge --no-ff -m "merge with no-ff" dev to leave a message to see the history.

2.  git log --graph --pretty=online --abbrev-commit to see

> we need to confirm this thing: the master should be really stable, used to release new versions, and use dev(new branch) to do everybody's own job.

> When merge, add "no-ff" will show the normal mode, the history will show has done the merge; while the ff will not show any history.

#### bug

1.every bug could be resolved by any new branch, after resolving, merge, delete the branch

2.when you need to debug issue101, while you are on branch dev, use git stash to store the wd and index state.

3.make sure where to debug, suppose is master, build branch from master, fix, git commit -m "fix bug 101"

4.git checkout master to switch to master and merge --no-ff -m "merged bug fix 101" issue-101.

5.back to current work, checkout dev, use git stash list to check the work; restore has two ways: a.git stash apply, (wont delete stash), use git stash drop to delete;
b.git stash pop(do both)

6.check with git stash list, you can even stash multiple times, when come back, use git stash list to check and restore the one that you want, git stash apply <stash@%7B0>}

#### feature

1.  when add some new feature to the ver., add a feature branch to develop, then merge, delete.

2.  has to delete the branch, use git branch -D <name> to force delete some new feature when not merged yet.

### multi-people coorperation

1.  when clone from the repo, git link the local master with the remote master, and make default name: origin; use git remote to check the info, git remote -v show more

2.  push is that pushing everything on that branch to corresponding remote branch, git push origin dev

3.  master and dev need to stay sync, so always push these two, bug does not to be pushed.

#### capture branches

1.  under coorperation, everyone push there own update, when they clone the source, use git clone <git remote -v>

2.  they can only seen master branch in default, if they want to develop, they need to add a branch, git checkout -b dev origin/dev, then they can add and edit on dev, and push to remote.(git push origin dev)

3.  if you and your pal edit the same file on dev,when you push, it will show rejected, first, git pull the new ver. then fix the conflit, last push.

4.  git pull will show error, you need to specify the local dev and the remote origin/dev: git branch --set-upstream-to=origin/dev dev(when show no tracking information; git 'dev' set up to track remote branch 'dev' from 'origin')

5.  git pull, and manully fix the conflit.

6.  push

### rebase

1.  git rebase make everything before local not yet pushed to be a line.

2.  the purpose for rebase is to easy track the history commit, since needed third party to checked.

### git tag(again)

easy to find out the old ver.

1.  git branch, git checkout master. change to the one need to be tagged.

2.  add tag. git tag v1.0; can use git tag to see all tags.

3.  if we forgot to tag something, use git log --pretty=online --abbrev-commit to see the commit id, then git tag v0.9 <id>

4.  use git tag to see all tags, and the tag is ordered by the abbr., so we can use git show <tag name> to see the tag info.

5.  we can also add tag with some notes, git tag -a v0.1 -m "version 0.1 released" <commit id>

6.  if we tag something wrong, use git tag -d v1.0 to delete the tag, since the tag wont be seen in remote, easy to delete or edit.

7.  if we need to push the tag to the remote, use git push origin <tagname>, or we can push all , use git push origin --tags

8.  if we already pushed to the remote, when we want to delete the tag, delete local first, git tag -d v0.9; then delete from the remote, (the command is push), git push origin :refs/tags/v0.9

github
------

1.  use fork to clone the repo, and clone from own account. git clone <git@github.com>:renyugt/bootstrap.git

2.  fix the bug or edit anything, and push to your own repo.

3.  if we want to be accepted by the offical, ask a pull request

gitee.com
---------

### self-edit git

1.  git config --global color.ui trus to add colour
