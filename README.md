# Tutorial Title

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

### Subsection 2.1: Intermediate Topic
Explain intermediate concepts, techniques, or features. Use code samples, diagrams, or any relevant media.

### Subsection 2.2: Another Intermediate Topic
Continue exploring intermediate concepts, providing examples and explanations.

## Section 3: Advanced Techniques
Go deeper into the subject, covering advanced techniques, tips, and best practices.

### Subsection 3.1: Advanced Topic
Explain advanced topics, methodologies, or techniques, and include more complex code examples.

### Subsection 3.2: Another Advanced Topic
Continue with additional advanced content, guiding the reader through advanced scenarios.

## Conclusion
Summarize what the reader has learned in the tutorial. Highlight key takeaways and encourage them to explore further.

## Additional Resources
Provide links to external resources, related tutorials, books, or documentation for readers who want to learn more.

## Feedback
Encourage readers to provide feedback, report issues, or ask questions. Provide contact information or links to a community forum or support channel.

## License
Specify the licensing information for your tutorial if applicable.

---

**Note**: Customize this structure to suit your specific tutorial's needs. Markdown allows for flexibility in formatting, so you can use headings, lists, code blocks, and more to create a well-organized and visually appealing tutorial.
