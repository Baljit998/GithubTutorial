# Version control with Git

## Introduction
Version control is the lab notebook of the digital world: it’s what professionals use to keep track of what they’ve done and to collaborate with other people. Every large software development project relies on it, and most programmers use it for their small jobs as well. And it isn’t just for software: books, papers, small data sets, and anything that changes over time or needs to be shared can and should be stored in a version control system.
A version control system is a tool that keeps track of these changes for us, effectively creating different versions of our files. It allows us to decide which changes will be made to the next version (each record of these changes is called a commit), and keeps useful metadata about them. The complete history of commits for a particular project and their metadata make up a repository. Repositories can be kept in sync across different computers, facilitating collaboration among different people.

KeyPoints
1. Version control is like an unlimited undo.
2. Version control also allows many people to work in parallel.


## Prerequisites
In this lesson we use Git from the Unix Shell. Some previous experience with the shell is expected, but isn’t mandatory.

## Table of Contents
- [Section 1: Getting Started](#section-1-getting-started)
- [Section 2: Intermediate Concepts](#section-2-intermediate-concepts)
- [Section 3: Advanced Techniques](#section-3-advanced-techniques)
- [Conclusion](#conclusion)

## Section 1: Getting Started
-Create Your Account On Github.
We need to setup the following configurations:
1. name and email address,
2. what our preferred text editor is,
3. and that we want to use these settings globally (i.e. for every project).

```
frappe@baljit-ThinkPad-T460:~$ cd Desktop
frappe@baljit-ThinkPad-T460:~/Desktop$ git config --global user.name "Baljit998"
frappe@baljit-ThinkPad-T460:~/Desktop$ git config --global user.email
"balsehra445@gmail.com"
frappe@baljit-ThinkPad-T460:~/Desktop$ git config --global core.autocrlf input
frappe@baljit-ThinkPad-T460:~/Desktop$ git config --list
user.email=balsehra445@gmail.com
user.name=Baljit998
core.autocrlf=input
frappe@baljit-ThinkPad-T460:~/Desktop$ cd ..
frappe@baljit-ThinkPad-T460:~$ git config --list
user.email=balsehra445@gmail.com
user.name=Baljit998
core.autocrlf=input
frappe@baljit-ThinkPad-T460:~$ git config --global init.defaultBranch main
frappe@baljit-ThinkPad-T460:~$ git config --global --edit
frappe@baljit-ThinkPad-T460:~$ git config --list
user.email=balsehra445@gmail.com
user.name=Baljit998
core.autocrlf=input
init.defaultbranch=main
frappe@baljit-ThinkPad-T460:~$ git help
usage: git [--version] [--help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           [--super-prefix=<path>] [--config-env=<name>=<envvar>]
           <command> [<args>]

These are common Git commands used in various situations:

start a working area (see also: git help tutorial)
   clone     Clone a repository into a new directory
   init      Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add       Add file contents to the index
   mv        Move or rename a file, a directory, or a symlink
   restore   Restore working tree files
   rm        Remove files from the working tree and from the index

examine the history and state (see also: git help revisions)
   bisect    Use binary search to find the commit that introduced a bug
   diff      Show changes between commits, commit and working tree, etc
   grep      Print lines matching a pattern
   log       Show commit logs
   show      Show various types of objects
   status    Show the working tree status

grow, mark and tweak your common history
   branch    List, create, or delete branches
   commit    Record changes to the repository
   merge     Join two or more development histories together
   rebase    Reapply commits on top of another base tip
   reset     Reset current HEAD to the specified state
   switch    Switch branches
   tag       Create, list, delete or verify a tag object signed with GPG

collaborate (see also: git help workflows)
   fetch     Download objects and refs from another repository
   pull      Fetch from and integrate with another repository or a local branch
   push      Update remote refs along with associated objects

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.
See 'git help git' for an overview of the system.
```
KeyPoints:
1. Use git config with the --global option to configure a user name.
2. email address, editor, and other preferences once per machine.


## Section 2: Create Directory
Create a directory inside the Desktop
```
frappe@baljit-ThinkPad-T460:~/Desktop$ mkdir planets
frappe@baljit-ThinkPad-T460:~/Desktop$ cd planets/

It is important to note that git init will create a repository that
can include subdirectories and their files—there is no need to create
separate repositories nested within the planets repository.
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git init
Initialized empty Git repository in /home/frappe/Desktop/planets/.git/
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ ls

-a flag show everything, we can see that Git has created a hidden
directory within planets called .git
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ ls -a
.  ..  .git
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git checkout -b main
Switched to a new branch 'main'
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git status
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)

```
KeyPoints:
1. git init initializes a repository.
2. Git stores all of its repository data in the .git directory.
3. It is not recommended to use git init inside an already initialized
repository because Git repositories can interfere with each other if
they are “nested”: the outer repository will try to version-control
the inner repository. Therefore, it’s best to create each new Git
repository in a separate directory.

## Section 3: Tracking Changes in Git

```
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ nano mars.txt
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ ls
mars.txt
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ cat mars.txt
Cold and dry, but everything is my favorite color
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
    mars.txt

nothing added to commit but untracked files present (use "git add" to track)
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git add mars.txt
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git status
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
    new file:   mars.txt

frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git commit -m "Start
notes on Mars"[main (root-commit) 912335a] Start notes on Mars
 1 file changed, 1 insertion(+)
 create mode 100644 mars.txt
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git status
On branch main
nothing to commit, working tree clean
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git log
commit 912335a3ac3f42a0b6bce83b0c830748a444dde0 (HEAD -> main)
Author: Baljit998 <balsehra445@gmail.com>
Date:   Mon Oct 9 12:15:18 2023 +0530

    Start notes on Mars
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ nano mars.txt
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ cat mars.txt
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
    modified:   mars.txt

no changes added to commit (use "git add" and/or "git commit -a")
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git diff
diff --git a/mars.txt b/mars.txt
index df0654a..315bf3a 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1 +1,2 @@
 Cold and dry, but everything is my favorite color
+The two moons may be a problem for Wolfman
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git add mars.txt
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git commit -m "Add
concerns about effexcts of Mars"
[main 7c6b2d7] Add concerns about effexcts of Mars
 1 file changed, 1 insertion(+)
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ nano mars.txt
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ cat mars.txt
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git diff
diff --git a/mars.txt b/mars.txt
index 315bf3a..b36abfd 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1,2 +1,3 @@
 Cold and dry, but everything is my favorite color
 The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git add mars.txt
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git diff --staged
diff --git a/mars.txt b/mars.txt
index 315bf3a..b36abfd 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1,2 +1,3 @@
 Cold and dry, but everything is my favorite color
 The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git commit -m "Discuss
concerns about Mars climate for Mummy"
[main de45b50] Discuss concerns about Mars climate for Mummy
 1 file changed, 1 insertion(+)
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git status
On branch main
nothing to commit, working tree clean
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git log
commit de45b5086a70e07e648555a243628c317ca979ca (HEAD -> main)
Author: Baljit998 <balsehra445@gmail.com>
Date:   Mon Oct 9 12:28:49 2023 +0530

    Discuss concerns about Mars climate for Mummy

commit 7c6b2d78ae5cd769a78f09795b638898c70d9583
Author: Baljit998 <balsehra445@gmail.com>
Date:   Mon Oct 9 12:23:56 2023 +0530

    Add concerns about effexcts of Mars

commit 912335a3ac3f42a0b6bce83b0c830748a444dde0
Author: Baljit998 <balsehra445@gmail.com>
Date:   Mon Oct 9 12:15:18 2023 +0530

    Start notes on Mars
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git log --oneline --graph
* de45b50 (HEAD -> main) Discuss concerns about Mars climate for Mummy
* 7c6b2d7 Add concerns about effexcts of Mars
* 912335a Start notes on Mars
frappe@baljit-ThinkPad-T460:~/Desktop/planets$
```
KeyPoints:
1. git status shows the status of a repository.
2. Files can be stored in a project’s working directory (which users
see), the staging area (where the next commit is being built up) and
the local repository (where commits are permanently recorded).
3. git add puts files in the staging area.
4. git commit saves the staged content as a new commit in the local repository.
5. Write a commit message that accurately describes your changes.

## Section 4: Exploring History in Git

```
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ nano mars.txt
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ cat mars.txt
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
An ill-considered change
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git diff HEAD mars.txt
diff --git a/mars.txt b/mars.txt
index b36abfd..93a3e13 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1,3 +1,4 @@
 Cold and dry, but everything is my favorite color
 The two moons may be a problem for Wolfman
 But the Mummy will appreciate the lack of humidity
+An ill-considered change
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git diff HEAD~3 mars.txt
fatal: ambiguous argument 'HEAD~3': unknown revision or path not in
the working tree.
Use '--' to separate paths from revisions, like this:
'git <command> [<revision>...] -- [<file>...]'
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git diff HEAD~1 mars.txt
diff --git a/mars.txt b/mars.txt
index 315bf3a..93a3e13 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1,2 +1,4 @@
 Cold and dry, but everything is my favorite color
 The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
+An ill-considered change
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git diff HEAD~3 mars.txt
fatal: ambiguous argument 'HEAD~3': unknown revision or path not in
the working tree.
Use '--' to separate paths from revisions, like this:
'git <command> [<revision>...] -- [<file>...]'
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git diff HEAD~2 mars.txt
diff --git a/mars.txt b/mars.txt
index df0654a..93a3e13 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1 +1,4 @@
 Cold and dry, but everything is my favorite color
+The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
+An ill-considered change
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git show HEAD~2 mars.txt
commit 912335a3ac3f42a0b6bce83b0c830748a444dde0
Author: Baljit998 <balsehra445@gmail.com>
Date:   Mon Oct 9 12:15:18 2023 +0530

    Start notes on Mars

diff --git a/mars.txt b/mars.txt
new file mode 100644
index 0000000..df0654a
--- /dev/null
+++ b/mars.txt
@@ -0,0 +1 @@
+Cold and dry, but everything is my favorite color
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git diff
912335a3ac3f42a0b6bce83b0c830748a444dde0 mars.txt
diff --git a/mars.txt b/mars.txt
index df0654a..93a3e13 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1 +1,4 @@
 Cold and dry, but everything is my favorite color
+The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
+An ill-considered change
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git diff 912335a mars.txt
diff --git a/mars.txt b/mars.txt
index df0654a..93a3e13 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1 +1,4 @@
 Cold and dry, but everything is my favorite color
+The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
+An ill-considered change
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
    modified:   mars.txt

no changes added to commit (use "git add" and/or "git commit -a")
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git checkout HEAD mars.txt
Updated 1 path from 6573bcb
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ cat mars.txt
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git checkout 912335a mars.txt
Updated 1 path from 12125a8
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ cat mars.txt
Cold and dry, but everything is my favorite color
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
    modified:   mars.txt

frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git checkout HEAD mars.txt
Updated 1 path from 6573bcb
```
KeyPoints:
1. git diff displays differences between commits.
2. git checkout recovers old versions of files.

## Section 4: Ignoring Things in Git
Configure Git to Ignore Some files which we don'd want git to track.
```
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ mkdir results
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ touch a.csv b.csv c.csv
results/a.out results/b.out
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git status
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
    a.csv
    b.csv
    c.csv
    results/

nothing added to commit but untracked files present (use "git add" to track)
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ nano .gitignore
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ cat .gitignore
*.csv
results/
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git status
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
    .gitignore

nothing added to commit but untracked files present (use "git add" to track)
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git add .gitignore
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git commit -m "Ignore
data files and the results folder"
[main 18d571c] Ignore data files and the results folder
 1 file changed, 2 insertions(+)
 create mode 100644 .gitignore
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git status
On branch main
nothing to commit, working tree clean
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git add a.csv
The following paths are ignored by one of your .gitignore files:
a.csv
hint: Use -f if you really want to add them.
hint: Turn this message off by running
hint: "git config advice.addIgnoredFile false"
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git status --ignored
On branch main
Ignored files:
  (use "git add -f <file>..." to include in what will be committed)
    a.csv
    b.csv
    c.csv
    results/

nothing to commit, working tree clean

```
KeyPoints:
1. The .gitignore file tells Git what files to ignore.

## Section 5: Remotes in Github

Log in to GitHub, then click on the icon in the top right corner to create a new repository called planets:

```
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git remote add origin
git@github.com:Baljit998/planets.git
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git remote -v
origin    git@github.com:Baljit998/planets.git (fetch)
origin    git@github.com:Baljit998/planets.git (push)
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ ls -al ~/.ssh
total 12
drwx------  2 frappe frappe 4096 Oct  3 13:47 .
drwxr-x--- 30 frappe frappe 4096 Oct  9 14:05 ..
-rw-r--r--  1 frappe frappe  142 Oct  3 13:47 known_hosts
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ ssh-keygen -t ed25519
-C "balsehra445@gmail.com"
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/frappe/.ssh/id_ed25519):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/frappe/.ssh/id_ed25519
Your public key has been saved in /home/frappe/.ssh/id_ed25519.pub
The key fingerprint is:
   <cut>
The key's randomart image is:
+--[ED25519 256]--+
   <cut>
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ ls -al ~/.ssh
total 20
drwx------  2 frappe frappe 4096 Oct  9 15:22 .
drwxr-x--- 30 frappe frappe 4096 Oct  9 14:05 ..
-rw-------  1 frappe frappe  464 Oct  9 15:22 id_ed25519
-rw-r--r--  1 frappe frappe  103 Oct  9 15:22 id_ed25519.pub
-rw-r--r--  1 frappe frappe  142 Oct  3 13:47 known_hosts
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ ssh -T git@github.com
git@github.com: Permission denied (publickey).
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ cat ~/.ssh/id_ed25519.pub
Put your ssh key
(Now, going to GitHub.com, click on your profile icon in the top right
corner to get the drop-down menu. Click “Settings,” then on the
settings page, click “SSH and GPG keys,” on the left side “Account
settings” menu. Click the “New SSH key” button on the right side. Now,
you can add the title (Dracula uses the title “Vlad’s Lab Laptop” so
he can remember where the original key pair files are located), paste
your SSH key into the field, and click the “Add SSH key” to complete
the setup.)

frappe@baljit-ThinkPad-T460:~/Desktop/planets$ ssh -T git@github.com
Hi Baljit998! You've successfully authenticated, but GitHub does not
provide shell access.
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git push origin main
Enumerating objects: 12, done.
Counting objects: 100% (12/12), done.
Delta compression using up to 4 threads
Compressing objects: 100% (8/8), done.
Writing objects: 100% (12/12), 1.06 KiB | 1.06 MiB/s, done.
Total 12 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), done.
To github.com:Baljit998/planets.git
 * [new branch]      main -> main
frappe@baljit-ThinkPad-T460:~/Desktop/planets$ git pull origin main
From github.com:Baljit998/planets
 * branch            main       -> FETCH_HEAD
Already up to date.
```

## Conclusion
Now repository is available at [Github](https://github.com/Baljit998/planets).

---
