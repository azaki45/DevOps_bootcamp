# Notes from pro-git book

## Getting started:

* Git has integrity : Git stores everything after checksumming it using SHA-1 hash mechanism. This is a 40 character string composed of hexadecimal characters (0-9 nad a-f) and calculated based on the contents of a file or directory structure in Git.
* An example of a SHA-1 hash : '''24b9da6552252987aa493b52f8696cd6d3b00373'''

### The Three States:
* Git has three main states that files can reside in: modified, staged, committed.
* Modified means that you have changed the file but have not committed it to your database yet.
* Staged means that you have marked a modified file in its current version to go into your next commit snapshot.
* Committed means that the data is safely stored in your local database.
* The three main sections of a Git project are: Working tree, the staging area, and the Git directory. ![git](https://user-images.githubusercontent.com/95584904/237024966-6e4e52c7-e2c6-43fc-b242-7dbefc27a037.png)
* The working tree : A single checkout of one version of the project. These files are pulled out of the compressed database in the Git directory and placed on disk for us to use or 
mosify.
* The staging area is a file, generally contained in our Git directory, that sotres information about what will go into our next commit. Its technical name in Git parlance is "index".
* The Git directory is where Git stores the metadata and obejct database for a project. This is the most important part of Git, and it is what is copied when we clone a repo form another computer.

### First-time Git Setup:
* Git comes with a tool called git config that lets us get and set configuration variables that control all aspect of how Git looks and operates. These variable can be stored in three different places:
  1. ```[path]/etc/gitconfig``` file: Contains values applied to every user on the system and all their repositories. If passed the option ```--system``` to ```git config```, it reads and writes from this file specifically. Because this is a system configuration file, one would need admin or superuser priviledge to make changes to it.
  2. ```~/.gitconfig``` or ```~/.config/git/config``` file: Values specific personnaly to the user. One can make Git read and write to this file specifically by passing the '''--global''' option, and this effects all of the repositoris we work on our system.
  3. ```config``` file in the Git directory (that is, .git/config) of whatever repo we're currently using: Specific to that single repo. We can force Git to read from and write to this file with the ```--local``` option, but that is in fact tbe default.

* Each level overrides values in the prev level, so values in ```.git/config``` trump those in ```[path]/etc/gitconfig```.
* To view the origin of the config settings : ```$ git config --list --show-origin```
* -h as help.

## Git Basics

### Important commands:
* ```$ git init``` : This creates a new subdirectory named .git that contains all of our necessary repo files.
* ```$ git add <file>```: Specifies the file that we want to keep a track of. This command takes a path name for either a file or a directory, if a directory, the command adds all th efiles in that directory recursively.
* ```$ git commit``` : Commits the changes.
* ```$ git status``` : The main tool used to determine which files are in which state.
* git add is a multilpurpose command. It is used to begin tracking new files, to stage modified files, and to marking merge-conflicted files as resolved.
* For viewing a shorter status, we use ```$ git status -s```.
    Sample output : ```                      
                     $ git status -s
                     M README
                     MM Rakefile
                     A lib/git.rb
                     M lib/simple git.rb
                     ?? LICENSE.txt
                     ```
    New files that aren’t tracked have a ?? next to them, new files that have been added to the staging
    area have an A, modified files have an M and so on. There are two columns to the output — the left-
    hand column indicates the status of the staging area and the right-hand column indicates the status
    of the working tree. So for example in that output, the README file is modified in the working
    directory but not yet staged, while the lib/simplegit.rb file is modified and staged. The Rakefile
    was modified, staged and then modified again, so there are changes to it that are both staged and
    unstaged.
  
### Ignoring Files:
  * Create a .gitignore file within which we decide which file types or directories to ignore while tracking     them.
  * Refer pro-git page 32.
  * [.gitignore file examples](https://github.com/github/gitignore)
  * use ```man gitignore``` for more details if needed.
 
### Viewing our staged and unstaged changes:
  * ```git diff``` this command is used to answer two questions:
      1. What have we changes but nit staged yet?
      2. What have we staged that we are about to commit?
      git diff shows the exact lines added and removed. This is what makes it different form git status.
  * Note: git diff by itself doesn't show all changes made since your last commit, only changes that are still unstaged. If you've staged all of your changes, git diff will give us no output.
  * ```git diff --staged``` : This command compares our staged changes to our last commit. This helps us to see what have we staged that will go into our next commit.
  * Read on git difftool. Run ```git difftool --tool-help```.
  
### Committing our changes:
  * ```git commit```: The simplest way to commit. Any file modification not sent to the staging area using ```git add``` will not be included in the snapshot.
  * On typing ```git commit```, an editor is launched. We can set it to be of our choice using ```git config --global core.editor```. The editor will hold the latest output of the ```git status``` command as the default commit message. We can add our own commit message.
  * For an even more explicit reminder use ```git commit -v```. This puts the diff of our change in the editor so we can see exactly what changes we're committing.
  * All this can be done in a single line using ```git commit -m "commit message"```.

### Skipping the Staging Area:
* We can skip the staging are by using ```git commit -a```. This makes Git automatically stage every file that is already tracked before doing th ecommit, letting us skip the ```git add``` part.

### Removing Files:
* To remove a file from Git, we remove it from our staging area and then commit.
* ```git rm``` command does that, it also removes it from our working directory so we don't see it as an untracked file next time around.
* A simple ```rm``` command will remove it from the working directory and this deletion will be present in the unstages area, whereas using ```git rm``` also adds the deletion to the staged area and is ready for commit.
* If we accidently missed some file in .gitignore: Use the cache option, ```$ git rm --cached <file/directory names/file-glob patterns>```.
  ![git1](https://github.com/azaki45/DevOps_bootcamp/assets/95584904/7d518f68-f22c-44c0-b54e-cd2263f943b3)

### Moving Files:
* ```git mv file_form file_to```: This is equivalent to renaming the file and will be recorded by git as a rename.
* It is equivalent to :
```
$ mv README.md README
$ git rm README.md
$ git add README
```

### Viewing the Commit History:
The most basic and powerfull command to look back and see what has happened is ```git log```. There are a bunch of variations of this command that can be used.
![git1](https://github.com/azaki45/DevOps_bootcamp/assets/95584904/65c111b2-d54a-422c-89c7-3e9b005f3a85)

![git2](https://github.com/azaki45/DevOps_bootcamp/assets/95584904/fe71fad7-83c0-4474-acd5-4d513c301a04)


### Limitting Log Output:
* ```git log --since=2.weeks``` : This outputs the list of commits made in the last two weeks.
* To prevent the display of merge commits whcih typically are'nt very informative, use ```--no-merges```.

![git1](https://github.com/azaki45/DevOps_bootcamp/assets/95584904/019e19e1-5d00-432f-81d5-9c346329ce0f)

### Undoing Things:
To redo a commit, we make the additional changes, stage them and then commit again using ```git commit --ammend```. This commmand uses the staging area for the commit. This overwrites the previous commit.
* git reset and git restore: Proceed with caution.

### Working with remotes:



## Git Branching:
A branch is a pointer to a certain commit. It is a 41 bytes file (40 characters and 1 new line) SHA-1 checksum.
## Creating a branch:
* ```git branch <branch name>``` : Cretes a branch with the given name.
* ```git checkout <branch name>``` : This moves the HEAD pointer to the newly created branch and we can now work in the new branch and merge our work later when it is the right time.
