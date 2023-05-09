# Notes from pro-git book

## Getting started:

* Git has integrity : Git stores everything after checksumming it using SHA-1 hash mechanism. This is a 40 character string composed of hexadecimal characters (0-9 nad a-f) and calculated based on the contents of a file or directory structure in Git.
* An example of a SHA-1 hash : '''24b9da6552252987aa493b52f8696cd6d3b00373'''

### The Three States:
* Git has three main states that files can reside in: modified, staged, committed.
* Modified means that you have changed the file but have not committed it to your database yet.
* Staged means that you have marked a modified file in its current version to go into your next commit snapshot.
* Committed means that the data is safely stored in your local database.
* The three main sections of a Git project are: Working tree, the staging area, and the Git directory. ![git](/home/azaki45/Pictures/git.png)
* The working tree : A single checkout of one version of the project. These files are pulled out of the compressed database in the Git directory and placed on disk for us to use or mosify.
* The staging area is a file, generally contained in our Git directory, that sotres information about what will go into our next commit. Its technical name in Git parlance is "index".
* The Git directory is where Git stores the metadata and obejct database for a project. This is the most important part of Git, and it is what is copied when we clone a repo form another computer.

### First-time Git Setup:
* Git comes with a tool called git config that lets us get and set configuration variables that control all aspect of how Git looks and operates. These variable can be stored in three different places:
  1. '''[path]/etc/gitconfig''' file: Contains values applied to every user on the system and all their repositories. If passed the option '''--system''' to '''git config''', it reads and writes from this file specifically. Because this is a system configuration file, one would need admin or superuser priviledge to make changes to it.
  2. '''~/.gitconfig''' or '''~/.config/git/config file: Values specific personnaly to the user. One can make Git read and write to this file specifically by passing the '''--global''' option, and this effects all of the repositoris we work on our system.
  3. '''config''' file in the Git directory (that is, .git/config) of whatever repo we're currently using: Specific to that single repo. We can force Git to read from and write to this file with the '''--local''' option, but that is in fact tbe default.

* Each level overrides values in the prev level, so values in '''.git/config''' trump those in '''[path]/etc/gitconfig'''.
* To view the origin of the config settings : '''$ git config --list --show-origin'''
* -h as help.

## Git Basics

### Important commands:
* '''$ git init''' : This creates a new subdirectory named .git that contains all of our necessary repo files.
* '''$ git add <file>''' : Specifies the file that we want to keep a track of. This command takes a path name for either a file or a directory, if a directory, the command adds all th efiles in that directory recursively.
* '''$ git commit''' : Commits the changes.
* '''$ git status''' : The main tool used to determine which files are in which state.
* git add is a multilpurpose command. It is used to begin tracking new files, to stage modified files, and to marking merge-conflicted files as resolved.
  
  
