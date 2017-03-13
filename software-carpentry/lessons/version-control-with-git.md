# Version Control with Git

{% hint style='info' %}
You can find the Software Carpentry lesson at: https://swcarpentry.github.io/git-novice/.
{% endhint %}

## Instructor notes

The big picture:

- Nothing that is committed is lost
- Possible to go back in time
- Exact record of who made what changes when
- Conflict management
- It is easy to set up
- Every copy of a Git repository is a full backup of a project and its history
- A few easy-to-remember commands are all you need for most day-to-day version control tasks
- The GitHub hosting service provides a web-based collaboration service

### Automated version control

Explain how it can be used to keep track of what one person did and when.

**Action:** show PhD Comics picture

Changes separated from the document itself --> playing back different sets of changes.

A version control system is a tool that keeps track of these changes and help version and merge files.

**Question:** Who uses `undo` in their editor? `Undo` is the simplest form of version control.

### Setting up Git

```
$ git config --global user.name "Your name here"
$ git config --global user.email "name@example.org"
$ git config --global color.ui "auto"
$ git config --global core.editor "nano -w"
$ git config --list
```

### Creating a repository

```
$ cd ~
$ mkdir planets
$ cd planets
$ git init
$ ls
$ ls -a
$ git status
```

### Tracking changes

```
$ nano mars.txt
	Cold and dry, but everything is my favorite color
$ ls
$ cat mars.txt
$ git status
$ git add mars.txt
$ git status
$ git commit -m "Start notes on Mars as a base"
```

Explain the notion of commit and commit identifier.
You should write good commit messages.

```
$ git status
$ git log
```

```
$ nano mars.txt
	The two moons may be a problem for Wolfman
$ cat mars.txt
$ git status
$ git diff # important to review the changes before saving them --> cryptic output (explain each row)
```

```
$ git commit -m "Add concerns about effects on Mars' moons on Wolfman"
$ git status
```

```
$ git add mars.txt
$ git commit -m "Add concerns about effects on Mars' moons on Wolfman"
```

**Action:** explain the staging area with a drawing

```
$ nano mars.txt
	But the Mummy will appreciate the lack of humidity
$ cat mars.txt
$ git diff
$ git add mars.txt
$ git diff
$ git diff --staged
$ git commit -m "Discuss concerns about Mars' climate for Mummy"
$ git status
$ git log
```

Directories are not seen by Git, only files (actually contents) within them.

**Action:** recap of the `init`, `add`, `commit`, `log`, `status` and `diff` commands.

**Exercise ideas:**

- Choosing a commit message
- Committing changes to Git
- Committing multiple files

### Exploring history

Reference to a commit: identifiers.
Most recent commit is: `HEAD`.

```
$ nano mars.txt
	An ill-considered change
$ cat mars.txt
$ git diff HEAD mars.txt
$ git diff HEAD~1 mars.txt
$ git diff HEAD~2 mars.txt
$ git show HEAD~2 mars.txt
```

```
$ git log
$ git diff <long_id> mars.txt # at least 4 chars
$ git diff <short_id> mars.txt
```

```
$ nano mars.txt
	We will need to manufacture our own oxygen
$ cat mars.txt
$ git status
$ git checkout HEAD mars.txt
$ cat mars.txt
$ git checkout <short_id> marst.txt
$ cat mars.txt
$ git status
```
```
$ git checkout -f master mars.txt # put things back the way they were
```
Use the commit number that identifies the state of the repository before the change we are trying to undo.

**Action:** enhance scheme to show how to switch states (unmodified, modified, staging area, commit).

**Exercise ideas:**

- Recovering Older Versions of a File
- Understanding Workflow and History

### Ignoring things

```
$ mkdir results
$ touch a.dat b.dat c.dat results/a.out results/b.out
$ git status
```

```
$ nano .gitignore
	*.dat
	results/
$ cat .gitignore
$ git status
$ git add .gitignore
$ git commit -m "Add the ignore file"
```

```
$ git add a.dat
$ git status --ignored
```

It is possible to use wildcards.

**Exercise ideas:**

- Ignoring nested files
- Including Specific Files
- Ignoring all data Files in a Directory

### Remotes in GitHub

Only thing missing: copy changes from one repository to another.

Hosting services: GitHub, BitBucket, GitLab, etc.

Make clear that Git and GitHub are not the same thing.

**Action:** create a repo on GitHub, explain everyting.

Setup a remote:

```
$ git remote add origin https://github.com/<username>/planets.git
$ git remote -v
$ git push origin master
```

Fetch + merge changes:

```
$ git pull origin master
```

Be sure to explain the difference between Push and Commit.

### Collaborating

Pushing to `master` is a privilege.

Branches to the rescue!

**Action:**

1. create a branch (and switch)
2. show in Finder the state of the repo
3. add a file with some content, commit it
4. switch to `master` (or previous branch)
5. show in Finder
6. push branch to github
7. create a Pull Request
8. merge PR
9. retrieve branch
10. delete branch