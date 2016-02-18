Git Manual
==========
Here is a small Git guide. Created to learn command line git instructions, rather than using GUI tools like SourceTree. There are only some basic and some interesting stuff we could use in our day to day codibg. Enjoy!

##### Sources worth to check

__Blogs__
- [__Thoughtbot Blog__](https://robots.thoughtbot.com/tags/git)

__Courses__
- [__Mastering Git__](https://upcase.com/mastering-git)

#### Table of Contents

- <a href="#repo_initialization">__Repository initialization__</a>
- <a href="#branches">__Branches__</a>
- <a href="#find_bug_navigating_through_commits">__Find bug navigationg through commits__</a>
- <a href="#git_ignore">__Git ignore__</a>
  - <a href="#global_git_ignore">__Global__</a>
  - <a href="#android">__Android__</a>
  - <a href="#intellij">__IntelliJ__</a>
  - <a href="#mac_os">__Mac OS__</a>
  - <a href="#windows">__Windows__</a>
- <a href="#tips">__Tips__</a>
<br>

<a name="repo_initialization">
### Repository initialization

__Locally__
```sh
# Inside the project folder
$ touch README.md
$ git init
$ git add README.md
# Outside the project folder
$ git init <directory>
# START HERE if you have already your project initialized
$ git add -A .
$ git commit -m COMMIT
$ git remote add origin <repo> # Where <repo> could be ssh://john@example.com/path/to/my-project.git 
```

From a __cloud__ repository
```sh
$ git clone <repo> # Where <repo> could be ssh://john@example.com/path/to/my-project.git 
$ git clone <repo> <directory> # Clone the repository located at <repo> into the folder called <directory> on the local machine
```

If we want to add a .gitignore to already initialized repo, we should do
```sh
$ git rm -r --cached . // This removes everything from the index
$ git add . 
$ git commit -m ".gitignore is now working"
```
<br>

<a name="branches">
### Branches








<br>

<a name="find_bug_navigating_through_commits">
### Find bug navigationg through commits

[__Sources__](http://linkbun.ch/03xl5)

Using __`git bisect`__ is a good idea. Is a tool that allows you to find an offending commit. Let’s say you’ve come across a bug in your codebase and you’re unsure of when it was introduced. If you can find a commit where the code works properly and a commit where it doesn’t, you don’t have to trace down the offending commit by hand (__find a particular regression__).

Imagine we have the following history

__`rev1 -- rev2 -- rev3 -- rev4 -- rev5 -- currentRev`__

We know that our program is not working properly at the __`currentRev`__ revision, and that it was working at the revision __`rev1`__. So the regression was introduced in one of the commits, __`rev2`__, __`rev3`__, __`rev4`__, __`rev5`__, __`currentRev`__.

__`git bisect`__ does a binary search. At each step it tries to reduce the number of revisiones that are potentially bad by half.

You can use the command the following way:
```sh
$ git stash save
$ git bisect start
$ git bisect bad
```

That will mark __`HEAD`__ as a bad commit. Alternatively, you could pass the sha of a specific commit like so:
```sh
$ git bisect bad <sha>
```

Then you'll to set a good commit. This will be the last known good commit. These two commands will set the outer bounds of the binary search. After:
```sh
$ git bisect good rev1
Bisecting: 2 revisions left to test after this (roughly 2 steps)
[< ... sha ... >] rev3
```

Git will split the revisions and load the first guess. In our case, it'll be commit __`rev3`__. You need to build your program, and check whether or not the regression is present. You'll also need to tell git the status of this revision with either git bisect bad if the regression is present, or git bisect good if it is not.

Let's suppose that the regression was introduced in commit __`rev4`__. Then the regression is not present in this revision, and we tell it to git.
```sh
$ git bisect good
Bisecting: 0 revisions left to test after this (roughly 1 step)
[< ... sha ... >] rev5
```

It will then checkout commit __`rev5`__. We need to check if regression is present:
```sh
$ git bisect bad
Bisecting: 0 revisions left to test after this (roughly 0 steps)
[< ... sha ... >] rev4
```
We test the last revision, __`rev4`__. And since it is the one that introduced the regression, we tell it to git:
```sh
$ git bisect bad
< ... sha ... > is the first bad commit
< ... commit message ... >
```

Over a larger range of commits this saving will be, obviously, greater. __(1 + log2 N)__.

More info:
- [__Debugging in Git with Blame and Bisect__](http://goo.gl/CJpZSA)

<br>

<a name="git_ignore">
### Git ignore

<a name="global_git_ignore">
#### Global

[__Source__](https://robots.thoughtbot.com/global-gitignore)

Set a __`.gitignore`__ file to apply across all projects on your local machine with:
```sh
$ git config --global core.excludesfile ~/.gitignore
```

It can be useful to ignore files in each project you work on but not every of your teammates on the project necessary need them.

<br>

<a name="android">
#### Android
```sh
# built application files
*.apk
*.ap_

# files for the dex VM
*.dex

# Java class files
*.class

# generated files
bin/
gen/

# Local configuration file (sdk path, etc)
local.properties
project.properties
*.DS_Store
tmp

## Proguard folder generated by Eclipse
proguard/

# Android studio
.idea/
*.iml

## Intellij project files
*.ipr
*.iws
*.idea
*/target

#Gradle
build/
.gradle/

#Maven
target
release.properties
pom.xml.*
```

<br>

<a name="intellij">
#### InbtelliJ

```sh
*.iml
*.ipr
*.iws
.idea/
```

<br>

<a name="mac_os">
#### Mac OS

```sh
.DS_Store
.AppleDouble
.LSOverride
Icon


# Thumbnails
._*

# Files that might appear on external disk
.Spotlight-V100
.Trashes
```

<br>

<a name="windows">
#### Windows

```sh
# Windows image file caches
Thumbs.db
ehthumbs.db

# Folder config file
Desktop.ini

# Recycle Bin used on file shares
$RECYCLE.BIN/
```

<br>

<a name="tips">
### Tips

__Use `.gitconfig` to save some important changes and aliases__

[__Source__](https://robots.thoughtbot.com/push-the-current-git-branch-even-if-youve-never)

The first time you push a git branch to a remote, you have to be explicit the first time:
```sh
$ git push origin my-branch-name
```

Every time after that, a simple git push will work fine. But there’s a setting for __`.gitconfig`__  that will let you just push without needing that initial explicitness:

```sh
[push]
  # Push current branch even if you've never pushed it before
	default = current
```

We can also play with commit messages automation, setting a template using __`.gitmessage`__.
```sh
[commit]
  template = ~/.gitmessage
```

Then create the template using __`*`__ for gaps.
```
Commit Title

Related issue:
*
Related feature:
*
```

There are other options worth se checking:
```sh
[core]
	excludesfile = /Users/user/.gitignore_global
[difftool "sourcetree"]
	cmd = opendiff \"$LOCAL\" \"$REMOTE\"
	path = 
[mergetool "sourcetree"]
	cmd = /Applications/SourceTree.app/Contents/Resources/opendiff-w.sh \"$LOCAL\" \"$REMOTE\" -ancestor \"$BASE\" -merge \"$MERGED\"
	trustExitCode = true
[user]
	name = User
	email = user@mail.com
[filter "lfs"]
	clean = git-lfs clean %f
	smudge = git-lfs smudge %f
	required = true
```

<br>















































git mergetool -t meld


Normal merge conflict for 'README':
  {local}: modified
  {remote}: modified

Hit return to start merge resolution tool (meld):
You would then see:


Configure Git For Your Mergetool Of Choice

To configure git to remember which merge tool you want, type git config –global merge.tool [tool]. For example, if you want git mergetool to automatically use kdiff3 as our mergetool, we would type:

$ git config --global merge.tool kdiff3





ADD A REMOTE (original copy from the project)

You probably have a "remote" for each repository. You need to pull from the one remote and push to the other.

If you originally cloned from your fork, that remote will be called "origin". If you haven't added it already, you'll need to add the first guy's repository as another remote:

git remote add firstguy git://github.com/firstguy/repo.git
After that's all set up, you should indeed be able to

git pull firstguy master
git push origin

OR

git fetch upstream
git checkout master

Merge the changes from upstream/master into your local master branch. This brings your fork's master branch into sync with the upstream repository, without losing your local changes.
git merge upstream/master
































Work flow
---------
Your local repository is composed by three "trees", managed by git. The first one is your "Working folder" that contains all files. The second one is the "Index" which plays a middle area rol, and finally "HEAD" wich points to last commit released

![Flow](https://raw.github.com/m3n0r/gitManual/master/resources/flow.png)


Basic actions
-------------
We can propose changes to "Index" using
```
git add FILE_NAME
```
or
```
git add *
```
After that, we can commit our changes
```
git commit -m COMMIT
```
Now the file is included in HEAD, but it's not in the repository yet. To send data to repository execute
```
git push REMOTE BRANCH
```
To refresh your local repository to newest commit, execute
```
git pull
```
To merge another branch to your current active branch (for example master), do
```
git merge BRANCH
```
If there are conflicts, you have to solve them manually edditing thos files. After that, you should check them as merged, with
```
git add FILENAME
```
Before merging changes, you could also review them using
```
git diff SOURCE_BRANCH TARGET_BRANCH
```
If we want to fetch data and merge after that, we could use
```
git pull --rebase
```

Tags
----
It's recommended to create tags for every software published version, using
```
git tag 1.0.0 * COMMIT_ID * //where *COMMIT_ID* is 10 chars of the commit id which you want to refer with your tag, for example 1b2e1d63ff
```
You can get commit id with the following instruction
```
git log
```

Replace local changes
---------------------
You can replace local changes using
```
git checkout -- FILENAME
```
This command replace changes in your current folder with the last work of HEAD. Both changes and files already added to Index will be without changes. If you want to undo local changes and commits, you can bring las server version and point to your main copy
```
git fetch origin
git reset --hard origin/master
```

Useful data
-----------
UI by default
```
gitk
```
Special colors for console
```
git config color.ui true
```
Show only a line for every commit in the trace
```
git config format.pretty oneline
```
Add files in interactive way
```
git add -i
```

Examples
-----------
#### Example 1

```
git commit
git commit
git checkout -b bugFix C1
git commit
git commit
git merge master
git checkout master
git commit
git commit
```
![Example 1 Flow](https://raw.github.com/m3n0r/gitManual/master/resources/example_1.png)
```
git rebase bugFix
git commit
```

#### Example 2
__Description__
_We want the commits to all be in sequential order. So this means that our final tree should have C7' at the bottom, C6' above that, etc etc, etc all in order_
```
git commit
git checkout -b bugFix C1
git commit
git checkout -b side C0
git commit
git commit
git commit
git checkout -b another C5
git commit
git checkout master
```
![Example 2 Solution 1](https://raw.github.com/m3n0r/gitManual/master/resources/example_2_solution_1.png)

__Solution__
```
git checkout bugFix
git rebase master
```
![Example 2 Solution 2](https://raw.github.com/m3n0r/gitManual/master/resources/example_2_solution_2.png)
```
git checkout side    
git rebase bugFix 
git checkout another    
git rebase side    
git rebase another master
```
![Example 2 Solution 3](https://raw.github.com/m3n0r/gitManual/master/resources/example_2_solution_3.png)   


***
***
***

This manual could not be possible withou the help of the following pages:
* [Learn Git Branching][page_1]
* [Git guida rápida][page_2]
* [Git - la guía sencilla][page_3]

[page_1]: http://pcottle.github.io/learnGitBranching
[page_2]: http://www.edy.es/dev/docs/git-guia-rapida
[page_3]: http://rogerdudler.github.io/git-guide/index.es.html
