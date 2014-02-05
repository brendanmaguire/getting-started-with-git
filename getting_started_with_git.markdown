# Getting Started With git

---
# What is version control?
* Version Control Systems refer to systems you can use to manage your source code
* It provides you with a history of the changes that have been made to a code repository
* Allows you to revert to a previous versions of your code (safety net)
* It allows many people to work on a code repository at the same time

---
# What is git?
* git is a Decentralised Version Control System
* Not necessary to have one central server
* You can make changes to the code and commit them even if you don't have access to a central server
* You only push these changes to other people when you want to
* You can view the history (and compare the files at different revisions) without needing access to a central server

---
# Installing git on Linux
On Debian based systems:

`
sudo apt-get install git
`

On RedHat based systems:

`
sudo yum install git
`

---
# Configuring your git user profile
Git must be configured so that your commits carry your information

`
git config --global user.email "johndoe@example.com"
`

`
git config --global user.name "John Doe"
`

Pick your favourite terminal based editor (if you don't know what your favourite is then nano is the path of least resistance)

Other options are vim, emacs, pico, gedit...

`
git config --global core.editor nano
`

Let's make things pretty!

`
git config --global color.ui true
`

***Note***: You can also edit the [configuration file](http://git-scm.com/book/ch7-1.html) directly if you wish. It is located at ~/.gitconfig

---
# Exercise - Set up your profile using git config

---
# git init - Creating a repository
Before you write any code you will need to create a repository

    !bash
    mkdir my-repo
    cd my-repo
    git init

This creates the hidden .git folder which git needs to keep track of the state of the repository.

***Note***: You *normally* shouldn't have to touch these files. Doing so usually leads to bad things

---
# git status - Viewing Repository Status
Use this to view the working tree status. This shows files that are in the following states:

* Modified
* Added
* Deleted
* Renamed
* Copied
* Untracked (not yet added to staging)

`
git status
`

---
# The staging area
* git is slightly different from most other version control systems in that it has a staging area
* The staging area is a temporary area to store your work before committing it
* It allows you to structure your commits in a way that suits you best

## A commit lifecycle
Locally Modified File(s) --&gt; Staging Area --&gt; Committed

---
# git add/rm - Adding and removing files
Add a specific file to the staging area

`
git add <file>...
`

Add all files to the staging area

`
git add .
`

You added a file by mistake. Remove a file from staging

`
git rm --cached <file>...
`

---
# git commit - Committing your changeset
Use git commit when you are happy with the changes to your files

`
git commit
`

This will open your editor so you can write a changeset message

Some useful commit options:

* ***-a | --all*** : Bypass the staging area process for files already under version control
* ***-m=&lt;msg&gt; | --message=&lt;msg&gt;*** : Specify your commit message
* ***--amend*** : Add the current changes in the staging area to the last commit in history

***Tip***: Commit often. It saves you from deleting work by mistake. You can always clean up your history if you want later

---
# git log - Viewing the repository history
Use git log to view the commits in a repository

`
git log
`

Some useful commit options:

* ***-&lt;number&gt; | -n &lt;number&gt;*** : Limit the number of commits to list
* ***--graph*** : A text based graph
* ***git log &lt;file&gt;...*** : Show commits that affected the specified file(s)

---
# Exercise - Create a repository and make a commit
* Initialise a repository
* Create a text file within
* Add the file to the staging area
* Commit the file
* View your history

---
# git diff - Viewing the changes to your tracked files
You will want to view the changes you have made before you commit

* View changes in your working directory

`
git diff
`

* View changes in your staging area

`
git diff --cached
`

---
# The GUI friendly way
* Now the *'easy'* way!
* There are many graphical tools for managing your git repositories
* My suggestions:
    - gitg : git GUI client (Built for GNOME but works \*everywhere)
    - tig : A ncurses based client
* An extensive list can be found [here](https://git.wiki.kernel.org/index.php/InterfacesFrontendsAndTools#Graphical_Interfaces)

---
# Exercise - Viewing changes to your repo
* Make some changes to the file(s) in your repo
* Create a new file
* View the diff for your working directory and staging area
* Add the new file and the changes to your existing file(s) to your staging area
* View the diff of your working directoy and staging area
* Install gitg and enjoy the GUI!
* Commit your changes (You can use gitg or the command line interface)

***Note***: During all of the above steps make lots of use of the *git status* command. It is very helpful for letting you know what is happening in your repo

---
# .gitignore - Ignoring files
* The gitignore file allows you to tell git to ignore certain files and not list them in your status output
* This is useful when you are building artifacts in the working directory that you don't want to be commited
* Examples are:
    - compiled files
    - binary executables
    - third party libraries

---
# Exercise - Add .javac files to your .gitignore
* Modify your .gitignore to tell git to ignore \*.javac files
* Create a file called prog.javac
* Use git status to see that it is correctly ignored
* .gitignore must be under version control also - Add it to staging and commit

---
# git checkout - Reverting changes to the working directory
Sometimes you realise that the changes you have made have actualy made the code worse and you want to revert to the last committed version of the files

git checkout will discard all changes you have made to the file. This will not affect files in the staging area

`
git checkout -- <file>...
`

---
# git reset - Reverting changes in the staging area
Remove the file(s) from the staging area but keep the changes in your working directory

`
git reset HEAD <file>...
`

Remove all files from the staging area and discard their changes totally
**Danger**: There is no coming back from this!

`
git reset HEAD --hard
`

---
# git branch - Working on multiple features at once
* You will often have situations where you will want to work on multiple seperate features at the same time
* Branching allows you to do this
* In this repository there are two live branches; new-secret-feature & big-bad-bug-fix
* Both can be worked on without affecting the other

* IMAGE FROM gitg goes here

* View branches as a pointer to a particular revision

---
# git branch - Creating a branch

`
git branch <branchname> [<start-point>]
`

* This will create a new branch
* You must supply a branch name
* If you do not supply a start point then the branch will 

***Note***: Creating a branch does not mean you are now on that branch automatically. It must be checked out

---
# git checkout - Going to a specific revision
Use *git checkout* if you would like to go to a specific revision in your repositories history

You can checkout a branch

`
git checkout <branchname>
`

or specify a revision using it's sha1 commit key

`
git checkout <sha1>
`
***Note***: The sha1 key can be found by using the git log command. It's the long string of hex characters

---
# git merge - Combining branches
* Use *git merge* to combine the code changes from two different branches

`
git checkout branch-1
git merge branch-2
`

---
# git branch - Deleting a branch
* When the changes on a branch have been merged back in, you will want to delete the branch pointer

`
git branch -d <branchname>
`
This will only work if the commits on this branch have been merged to another branch

The more terminal option is to use the *-D* option. This will delete the branch pointer even if this branch has not been merged
***Danger***: You will lose any commits on this branch that have not been merged

`
git branch -D <branchname>
`

---
# git rebase
* git rebase allows you to move your branches on top of each other
* Makes for a more sane history when many branches are live at the same time
* No merge commits left in the history
* Outside the scope of this presentation

---
# Exercise - Branching & Merging
* Create a new branch in your repository called branch1
* Check it out and commit some changes
* Create another new branch in your repository called branch2 - ensure you create it with a start point of master
* Check it out and commit some changes
* Merge the two branches
* Update your master (hint: merge master to the top most branch in your history)
* Delete your branches

---
# Working with remote repositories
* So far we have looked at managing our code locally
* This allows you to change your code and be safe in the knowledge that you can revert your changes if needs be
* It gives you a history of the changes you made and commit messages letting you know why you made those changes (provided you write good commit messages!)

---
# Working with remote repositories
* Another main benefit of version control is that it allows you to collaborate with others
* This is where remote repositories come in
* You and your co-workers can each clone a repository, work on it locally, commit your changes, and then contribute your changes back to the original repository

---
# git clone - Cloning an Existing Repository
Create your own working copy of an existing repository

* Cloning over ssh

`
    git clone <username>@<host>:/path/to/repo
`

* Cloning over http(s)

`
    git clone https://<host>/path/to/repo
`

---
# Exercise - Clone a repository from github
* The github page for this presentation can be found [here](http://github.com/brendanmaguire/???)
* Find the url you need to clone it over http
* Clone it

---
# ssh keys
* ssh keys are a way of authenicating automatically with a server running a sshd service
* Creating an ssh key

`
# Press enter for all defaults
ssh-keygen
`

* Viewing the public part of your ssh key

`
cat ~/.ssh/id_rsa.pub
`

---
# Exercise - Create a repository on github
* Create a github account
* Add your ssh key in the Account Setting -&gt; SSH Keys pages
* Create a repository
* DO NOT check the box for initialising the repo. You will be pushing the repository you created in the previous exercises

---
# Pushing to a remote repository
* To push to a remote repository, you must first add an entry for the remote server

`
git remote add origin git@github.com:<username>/<reponame>.git
`

* You can then push your master branch to the remote server

`
git push -u origin master
`

---
# Exercise - Push your local repo to your github repo
* Add the github repo as your remote origin
* Push your local commits

---
# [git pull](http://git-scm.com/docs/git-pull) - Pulling Updates
* Before you attempt to push your changes, you should perform a pull to ensure there are no new commits on the remote server
* If there are, then you should incoperate them into your local repo (and merge) before pushing

`
    git pull
`

---
# Exercise - Collaboration on github
* Pair up with the person beside you
* Add the other person as a collaborator on your github project
    - In the github UI: Your project -&gt; Setting -&gt; Collorators -&gt; Add

* Clone their repository
* Make some changes and commit
* Push to their repository

* Once they've pushed to your repo, make some changes to your own local repository and commit
* Try to push to your remote repository (hint: it should fail)
* pull the new changes your partner has made
* Merge and push

---
# Questions???
