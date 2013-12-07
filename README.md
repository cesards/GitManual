Git Manual (NOT FINISHED)
==========
Here is a small Git guide, created because we usually use prepared software for working with repositories, but after we should be able to know command line git instructions. It's much better than any other UI client! :-) 

Repository initialization
---------------------------
```
// Inside the project folder
touch README.md
git init
git add README.md
// Outside the project folder
git init <directory>
```
or, if you've already all your project initialized
```
git add . // Check all files to next commit
git commit -m COMMIT // It creates a new commit
git remote add origin URL // We add a remote, as https://github.com/m3n0R/GitManual.git
```
There is another way to initialize a repository
```
git clone <repo> // Clone the repository located at <repo> onto the local machine.
git clone <repo> <directory> // Clone the repository located at <repo> into the folder called <directory> on the local machine
// Example: git clone ssh://john@example.com/path/to/my-project.git 
// cd my-project
```

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

Branches
--------
There are different ways to create branches
```
git checkout -b BRANCH//new branch created and it points to this
```
or
```
git branch BRANCH /new branch created and it points to your current branch, not this
```
Other instructions
```
git branch -d BRANCH //it deletes a branch
git branch //it shows all branches
git branch -b BRANCH //new branch created and it points to this. You can do the same doing git checkout BRANCH after git branch
git branch BRANCH COMMIT //it creates a branch from the given commit
git branch -b BRANCH COMMIT //it creates a branch from the given commit and can do checkout to this (it points to this)
git branch -m CURRENT_BRANCH NEW_BRANCH //it renames current branch to new branch name 
git checkout BRANCH //it points to branch desired(HEAD)
git checkout COMMIT //it points to commit desired(HEAD)
git rebase BRANCH //it includes BRANCH commit logs to our current branch
git rebase CURRENT_BRANCH ANOTHER_BRANCH //we point the last commit to the desired branch
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
