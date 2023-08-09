## Git Configuration
### Configuation File Location

1. System Wide Configuration
```bash
# Unix
/etc/gitconfig
# Windows
Program Files\Git\etc\gitconfig
```

2. User Configuration
```bash
# Unix
~/.gitconfig
# Windows
$HOME\.gitconfig
```

2. Project Configuration
```bash
my_project/.git/config
```

### Configuration Commands
1. System Wide Configuration
```bash
git config --system
```

2. User Configuration
```bash
git config --global
```

2. Project Configuration
```bash
git config
```

### Example
```bash
# Setting Configuration
chirag@ubuntu:~$ git config --global user.name "Chirag Singh"
chirag@ubuntu:~$ git config --global user.email "bharatsr1997@gmail.com"
chirag@ubuntu:~$ git config --global core.editor "nano"
chirag@ubuntu:~$ git config --global color.ui true
chirag@ubuntu:~/learning-git$ git config --global core.excludesfile ~/.gitignore_global

# To List All Configurations
chirag@ubuntu:~$ git config --list
user.name=Chirag Singh
user.email=bharatsr1997@gmail.com

# To View Specific Configuration
chirag@ubuntu:~$ git config user.name
Chirag Singh

# To View Config File
chirag@ubuntu:~$ cat ~/.gitconfig
[user]
        name = Chirag Singh
        email = bharatsr1997@gmail.com
[core]
        editor = nano
[color]
        ui = true
```
---
## Git Auto-Completion
### Script Link
https://github.com/git/git/blob/master/contrib/completion/git-completion.bash

### Steps
1. Save The File As _git-completion.bash_ In Home Directory
2. Add Following Lines In _~/.bashrc_:
```bash
if [ -f ~/.git-completion.bash ]
then
	source ~/.git-completion.bash
fi
```
----
## Git Help
```bash
chirag@ubuntu:~$ git help

chirag@ubuntu:~$ git help log
# Same As
chirag@ubuntu:~$ man git-log
```
---
## Initializing A Repository
```bash
# To Initialize A Empty Repository Use
chirag@ubuntu:~/learning-git$ git init
Initialized empty Git repository in /home/chirag/learning-git/.git/

# It Creates .git Directory
chirag@ubuntu:~/learning-git$ ls -la
total 12
drwxrwxr-x 3 chirag chirag 4096 Apr  5 11:43 .
drwxr-xr-x 4 chirag chirag 4096 Apr  5 11:43 ..
drwxrwxr-x 7 chirag chirag 4096 Apr  5 11:43 .git

# .git Directory Contains All The File That Git Needs To Keep Tracking Information
chirag@ubuntu:~/learning-git$ ls -la .git/
total 40
drwxrwxr-x 7 chirag chirag 4096 Apr  5 11:43 .
drwxrwxr-x 3 chirag chirag 4096 Apr  5 11:43 ..
drwxrwxr-x 2 chirag chirag 4096 Apr  5 11:43 branches
-rw-rw-r-- 1 chirag chirag   92 Apr  5 11:43 config
-rw-rw-r-- 1 chirag chirag   73 Apr  5 11:43 description
-rw-rw-r-- 1 chirag chirag   23 Apr  5 11:43 HEAD
drwxrwxr-x 2 chirag chirag 4096 Apr  5 11:43 hooks
drwxrwxr-x 2 chirag chirag 4096 Apr  5 11:43 info
drwxrwxr-x 4 chirag chirag 4096 Apr  5 11:43 objects
drwxrwxr-x 4 chirag chirag 4096 Apr  5 11:43 refs

# It Also Contains Project Wide Config File
chirag@ubuntu:~/learning-git$ cat .git/config
[core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
```
---
## Your First Commit
```bash
# Create A New File
chirag@ubuntu:~/learning-git$ nano first_file.txt
chirag@ubuntu:~/learning-git$ cat first_file.txt
This is my first file.

# Add All The Modified And Untracked Files In Current Director To Staging Area
chirag@ubuntu:~/learning-git$ git add .

# Create A Current Snapshot Of The Project Using Commit
# Save All The Staged Changes Along With A Brief Description In The Repository
chirag@ubuntu:~/learning-git$ git commit -m "Inital Commit"
[master (root-commit) 95497ff] Inital Commit
 1 file changed, 1 insertion(+)
 create mode 100644 first_file.txt
```
## A Note About Commit Messages
* A Short Single Line Summary (< 50 Characters).
* Optionally Followed By A Blank Line And A More Complete Description.
* Keep Each Line Less Than 72 Character.
* Write Commit Message In **Present Tense**.
  * Example: "Fix For A Bug", Instead Of "Fixed A Bug".
* Add Bullet Points Using Asterisks Or Hyphens
* Can Add **Tracking Numbers** From Bug Or Support Request.
* Can Develop A Shorthand For Your Organization.
  * "[css,js]"
  * "bugfix:..."
  * "#3850 - ..."
* Be Clear And Descriptive.
  * "Add Missing Hyphen In Project Section Of HTML" Instead Of "Fixed Typo".
  * Change User Auth To Use oAuth" Instead Of "Update Login Code".

### Example
```text
ghi2325 - Fixes bug in admin logout

When an admin logged out of the admin area, they
could not log in to members area because their
session[:user_id] was still set to admin ID.
This patch fixes the bug by setting session[:user_id]
to nil when any user logs out of any area.
```
---
## Commit Log
```bash
# View All Commits
chirag@ubuntu:~/learning-git$ git log
commit 95497ff4f29728c61a302f6025e20dc433dd0858 (HEAD -> master)
Author: Chirag Singh <bharatsr1997@gmail.com>
Date:   Mon Apr 5 11:53:45 2021 +0530

    Inital Commit

# Display 5 Most Recent Commits
chirag@ubuntu:~/learning-git$ git log -n 5

# Display All Commit Since A Date
chirag@ubuntu:~/learning-git$ git log --since=2021-01-01

# Display All Commit Until A Date
chirag@ubuntu:~/learning-git$ git log --until=2021-01-01

# Display Commits By Author
# Can use Part Of Name
chirag@ubuntu:~/learning-git$ git log --author="Chirag"
chirag@ubuntu:~/learning-git$ git log --author="Singh"

# You Can Also Use Grep
chirag@ubuntu:~/learning-git$ git log --grep="Init"
```
---
## SHA-1 Checksum / Commit ID
* Git Uses SHA-1 Hash Algorithm To Create Checksums For Each Commit.
* This Insures Data Integrity.
* Hashes Are 40 Character Log Hexadecimal Strings.

### What Goes In Hashing Algorithm?
* The Source Tree Of The Commit.
* The Parent Commit SHA-1.
* The Author Info.
* The Committer Info (Rights).
* The Commit Message.
---
### HEAD
* Pointer To Tip Of Current Branch If The Repository.
```bash
chirag@ubuntu:~/learning-git$ cat .git/HEAD
ref: refs/heads/master
chirag@ubuntu:~/learning-git$ cat .git/refs/heads/master
95497ff4f29728c61a302f6025e20dc433dd0858
```
---
## Git Status
The git status command displays the state of the working directory and the staging area. It lets you see which changes have been staged, which haven't, and which files aren't being tracked by Git. 
```bash
# See The Status Of The Branch
chirag@ubuntu:~/learning-git$ git status
On branch master
nothing to commit, working tree clean

# Create Some New Files
chirag@ubuntu:~/learning-git$ nano second_file.txt
chirag@ubuntu:~/learning-git$ nano third_file.txt

# Now Git Status Displays 2 Untracked Files
chirag@ubuntu:~/learning-git$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

        second_file.txt
        third_file.txt

nothing added to commit but untracked files present (use "git add" to track)

# Add second_file.txt To Staging Tree
chirag@ubuntu:~/learning-git$ git add second_file.txt

# Now If We Check The Status We Can See second_file.txt In Stating Tree
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   second_file.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        third_file.txt

# Commit The Changes
chirag@ubuntu:~/learning-git$ git commit -m "Add Second File To Project"
[master 934f989] Add Second File To Project
 1 file changed, 1 insertion(+)
 create mode 100644 second_file.txt

 # We Can See Our Two Commits Using git log
 # Notice That HEAD Pointer Is Pointing To Commit Just Made
chirag@ubuntu:~/learning-git$ git log
commit 934f98949e6033c2cc8deb6132787c81f68f74c8 (HEAD -> master)
Author: Chirag Singh <bharatsr1997@gmail.com>
Date:   Mon Apr 5 13:05:10 2021 +0530

    Add Second File To Project

commit 95497ff4f29728c61a302f6025e20dc433dd0858
Author: Chirag Singh <bharatsr1997@gmail.com>
Date:   Mon Apr 5 11:53:45 2021 +0530

    Inital Commit

# Similarly Adding Third File
chirag@ubuntu:~/learning-git$ git add third_file.txt
chirag@ubuntu:~/learning-git$ git commit -m "Add Third File To The Project"
[master d410d4b] Add Third File To The Project
 1 file changed, 1 insertion(+)
 create mode 100644 third_file.txt
chirag@ubuntu:~/learning-git$ git log
commit d410d4b373235a45af1db4b1446e07bb0bf51a6f (HEAD -> master)
Author: Chirag Singh <bharatsr1997@gmail.com>
Date:   Mon Apr 5 13:10:48 2021 +0530

    Add Third File To The Project
...
```
---
## Editing Tracked Files
```bash
# Edit first_file.txt
chirag@ubuntu:~/learning-git$ nano first_file.txt

# Git Noticed The File Is Modified In The Working Tree Since It Was Tracked Already
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   first_file.txt

no changes added to commit (use "git add" and/or "git commit -a")

# Add The Changes Of first_file.txt To Staging Tree
chirag@ubuntu:~/learning-git$ git add first_file.txt

# Modification Added To Staging Tree
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   first_file.txt

# Similarly Edit second_file.txt And third_file.txt
chirag@ubuntu:~/learning-git$ nano second_file.txt
chirag@ubuntu:~/learning-git$ nano third_file.txt
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   first_file.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   second_file.txt
        modified:   third_file.txt

chirag@ubuntu:~/learning-git$ git add second_file.txt
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   first_file.txt
        modified:   second_file.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   third_file.txt

# Commit The Change In Each File And See The Status
chirag@ubuntu:~/learning-git$ git commit -m "Made Changes To First And Second File"
[master 3a09c77] Made Changes To First And Second File
 2 files changed, 2 insertions(+), 2 deletions(-)
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   third_file.txt

no changes added to commit (use "git add" and/or "git commit -a")
chirag@ubuntu:~/learning-git$ git add third_file.txt
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   third_file.txt

chirag@ubuntu:~/learning-git$ git commit -m "Modified The Text Of The Third File"
[master fde7f45] Modified The Text Of The Third File
 1 file changed, 1 insertion(+), 1 deletion(-)

# Add The Changes Were Commited To The Repository
chirag@ubuntu:~/learning-git$ git status
On branch master
nothing to commit, working tree clean
```
---
## Viewing Changes With Diff
* Use git diff --color-words To Make Changes Easier To Spot.
* 
```bash
# Changes The Contents Of first_file.txt
chirag@ubuntu:~/learning-git$ nano first_file.txt
chirag@ubuntu:~/learning-git$ cat first_file.txt
This is the first file I added to the project.


This file comes before the others.
Git is tracking my changes.

# We Can See That The File Has Been Modified But Cannot See The Actual Chanegs
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   first_file.txt

no changes added to commit (use "git add" and/or "git commit -a")

# To See Actual Changes Use git diff
# 'a' Is The Version In The Repository
# 'b' Is The Version In The Working Directory
# The Output Of Diff Shows We Have Added 4 Lines
chirag@ubuntu:~/learning-git$ git diff
diff --git a/first_file.txt b/first_file.txt
index bdde579..f6f3fca 100644
--- a/first_file.txt
+++ b/first_file.txt
@@ -1 +1,5 @@
 This is the first file I added to the project.
+
+
+This file comes before the others.
+Git is tracking my changes.

# We Changed An Existing Line
chirag@ubuntu:~/learning-git$ nano first_file.txt

# The Output Of Diff Shows We Have Deleted One Line And Added Another
chirag@ubuntu:~/learning-git$ git diff
diff --git a/first_file.txt b/first_file.txt
index bdde579..9878a76 100644
--- a/first_file.txt
+++ b/first_file.txt
@@ -1 +1,5 @@
-This is the first file I added to the project.
+This is the first file I added to my project.
+
+
+This file comes before the others.
+Git is tracking my changes.
```
---
## Viewing Changes With Diff In Staging Tree

If We Make Changes To File And Add Those Changes To Staging Directory, ```git diff``` No Longer Show Those Changes.

To View Changes Made In The Files In Staging Area We Ues ```git diff --staged``` OR ```git diff --cached```.

* ```git diff```: Differences Between Staging And Working Area.

* ```git diff --statged```: Differences Between Staging And Repository.

```bash
## Changes Not Yet Added To Staging Area
chirag@ubuntu:~/learning-git$ git diff
diff --git a/first_file.txt b/first_file.txt
index bdde579..9878a76 100644
--- a/first_file.txt
+++ b/first_file.txt
@@ -1 +1,5 @@
-This is the first file I added to the project.
+This is the first file I added to my project.
+
+
+This file comes before the others.
+Git is tracking my changes.

## Add The Changes To Staging Area
chirag@ubuntu:~/learning-git$ git add first_file.txt

## git diff Doesn't Show Differences Since Working Area And Staging Are In Sync Now
chirag@ubuntu:~/learning-git$ git diff

# git diff --statged shows ifferences Between Staging And Repository
chirag@ubuntu:~/learning-git$ git diff --staged
diff --git a/first_file.txt b/first_file.txt
index bdde579..9878a76 100644
--- a/first_file.txt
+++ b/first_file.txt
@@ -1 +1,5 @@
-This is the first file I added to the project.
+This is the first file I added to my project.
+
+
+This file comes before the others.
+Git is tracking my changes.

## Commit And Check Again
chirag@ubuntu:~/learning-git$ git commit -m "Minor Text Edits"
[master d8bad57] Minor Text Edits
 1 file changed, 5 insertions(+), 1 deletion(-)
chirag@ubuntu:~/learning-git$ git diff
chirag@ubuntu:~/learning-git$ git diff --cached
chirag@ubuntu:~/learning-git$ git diff --staged
```
---
## Deleting Files
```bash
## Add Some To Files To Delete
chirag@ubuntu:~/learning-git$ touch file_to_delete1.txt
chirag@ubuntu:~/learning-git$ touch file_to_delete2.txt

# If We Delete Untracked File There If No Effect On Repository
chirag@ubuntu:~/learning-git$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

        file_to_delete1.txt
        file_to_delete2.txt

nothing added to commit but untracked files present (use "git add" to track)

# Commit And Commit Changes
chirag@ubuntu:~/learning-git$ git add .
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   file_to_delete1.txt
        new file:   file_to_delete2.txt
chirag@ubuntu:~/learning-git$ git commit -m "Add Files To Delete Soon"
[master f93a8cc] Add Files To Delete Soon
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file_to_delete1.txt
 create mode 100644 file_to_delete2.txt

# Method 1: Deleting Files Directly Using File Explorer/CMD
# Remove The File Using rm Command
chirag@ubuntu:~/learning-git$ rm file_to_delete1.txt

# Git Status Show file_to_delete1.txt Has Been Deleted From The Working Tree
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        deleted:    file_to_delete1.txt

no changes added to commit (use "git add" and/or "git commit -a")

# Use git rm To Remove A File And Move The Changes To Staging Area
chirag@ubuntu:~/learning-git$ git rm file_to_delete1.txt
rm 'file_to_delete1.txt'
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        deleted:    file_to_delete1.txt

# Commit The Changes To Repository
chirag@ubuntu:~/learning-git$ git commit -m "Delete First File"
[master b25d614] Delete First File
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 file_to_delete1.txt
chirag@ubuntu:~/learning-git$ git status
On branch master
nothing to commit, working tree clean

# Method 2: Using Git To Remove The File
# Using git rm Directly Will Remove The File From The Working Area And Also Add Those Changes To Staging Area
chirag@ubuntu:~/learning-git$ git rm file_to_delete2.txt
rm 'file_to_delete2.txt'
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        deleted:    file_to_delete2.txt

chirag@ubuntu:~/learning-git$ git commit -m "Delete Second File"
[master 1a94eec] Delete Second File
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 file_to_delete2.txt
```
---
## Moving And Renaming Files
```bash
# Method 1: Renaming Using File Explorer/CMD
chirag@ubuntu:~/learning-git$ mv first_file.txt primary_file.txt

# git status Recognizes This Operation As Deleting One File And Adding Another Untracked File
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        deleted:    first_file.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        primary_file.txt

no changes added to commit (use "git add" and/or "git commit -a")

# If We Add These Changes To Staging Git Recognizes The File Is Actually Being Renamed
chirag@ubuntu:~/learning-git$ git add primary_file.txt
chirag@ubuntu:~/learning-git$ git rm first_file.txt
rm 'first_file.txt'
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        renamed:    first_file.txt -> primary_file.txt

# Method 1: Renaming Using Git
chirag@ubuntu:~/learning-git$ git mv second_file.txt secondary_file.txt

# git mv Renames/Moves The File And Directly Adds It To Staging Area
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        renamed:    first_file.txt -> primary_file.txt
        renamed:    second_file.txt -> secondary_file.txt

# Commit Changes
chirag@ubuntu:~/learning-git$ git commit -m "Renamed Files"
[master c741986] Renamed Files
 2 files changed, 0 insertions(+), 0 deletions(-)
 rename first_file.txt => primary_file.txt (100%)
 rename second_file.txt => secondary_file.txt (100%)
```
---
## Commiting Changes Directly From Working Tree
* git commit -a
* git commit --all
* Stages And Commit All Changes To Tracked Files
* Does Not Include Untracked Files
```bash
chirag@ubuntu:~/learning-git$ git status
On branch master
nothing to commit, working tree clean
chirag@ubuntu:~/learning-git$ nano primary_file.txt
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   primary_file.txt

no changes added to commit (use "git add" and/or "git commit -a")

# Use git commit -a/--all To Skip The Staging Step
chirag@ubuntu:~/learning-git$ git commit -a -m "Edit First File"
[master eb9e668] Edit First File
 1 file changed, 1 insertion(+), 1 deletion(-)
chirag@ubuntu:~/learning-git$ git status
On branch master
nothing to commit, working tree clean
```
---
## Viewing The Details Of A Previous Commit
```bash
# Get SHA-1 Of The Commit You Want To View
chirag@ubuntu:~/learning-git$ git log -n 2
commit eb9e668f31dcd8b92268cb0a2107e17499ba32b0 (HEAD -> master)
Author: Chirag Singh <bharatsr1997@gmail.com>
Date:   Mon Apr 5 14:25:26 2021 +0530

    Edit First File

commit c7419861f4eda694ea78efed14bde4cbfbc9fb03
Author: Chirag Singh <bharatsr1997@gmail.com>
Date:   Mon Apr 5 14:15:33 2021 +0530

    Renamed Files

# View The Details Of The Commit Using git show
chirag@ubuntu:~/learning-git$ git show eb9e668f31dcd8b92268cb0a2107e17499ba32b0
commit eb9e668f31dcd8b92268cb0a2107e17499ba32b0 (HEAD -> master)
Author: Chirag Singh <bharatsr1997@gmail.com>
Date:   Mon Apr 5 14:25:26 2021 +0530

    Edit First File

diff --git a/primary_file.txt b/primary_file.txt
index 9878a76..26c51c2 100644
--- a/primary_file.txt
+++ b/primary_file.txt
@@ -1,4 +1,4 @@
-This is the first file I added to my project.
+This is the primary file I added to my project.


 This file comes before the others.
```
---
## Comparing Two Commits
```bash
# Use git diff SHA..SHA To View Differences Between Two Commits
chirag@ubuntu:~/learning-git$ git diff eb9e668..1a94eecc --color-words
diff --git a/primary_file.txt b/first_file.txt
similarity index 57%
rename from primary_file.txt
rename to first_file.txt
index 26c51c2..9878a76 100644
--- a/primary_file.txt
+++ b/first_file.txt
@@ -1,4 +1,4 @@
This is the primaryfirst file I added to my project.


This file comes before the others.
diff --git a/secondary_file.txt b/second_file.txt
similarity index 100%
rename from secondary_file.txt
rename to second_file.txt
```
---
## Multi-Line Commit Messages
```bash
chirag@ubuntu:~/learning-git$ nano primary_file.txt
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   primary_file.txt

no changes added to commit (use "git add" and/or "git commit -a")

# Git Will Open Editor And Waits For You To Add The Commit Message
chirag@ubuntu:~/learning-git$ git commit -a
[master 50dddfd] Minor Text Edits
 1 file changed, 1 insertion(+)

 # We Can See The Multi-Line Commit Message Here
chirag@ubuntu:~/learning-git$ git log -n 1
commit 50dddfde96aa81c5ba2c3b4b1c1199b8953f2282 (HEAD -> master)
Author: Chirag Singh <bharatsr1997@gmail.com>
Date:   Mon Apr 5 14:44:12 2021 +0530

    Minor Text Edits

    Added A Line In Primary File To Demonstrate The
    Usage Of Multi-Line Commit Messages.
# Use git log --oneline To Display Only First Line Of The Commit Message
chirag@ubuntu:~/learning-git$ git log -n 1 --oneline
50dddfd (HEAD -> master) Minor Text Edits
```
---
## Undo Chanegs
### Undo Changes Im Working Directory
```bash
# Suppose We Accidently Deleted The Contents Of A File
chirag@ubuntu:~/learning-git$ nano primary_file.txt
chirag@ubuntu:~/learning-git$ cat primary_file.txt
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   primary_file.txt

no changes added to commit (use "git add" and/or "git commit -a")

# Git Knows Our File Has Been Changed
# We Can Restore The Contents Of The File Using git checkout Command
# The -- Means Current Branch
chirag@ubuntu:~/learning-git$ git checkout -- primary_file.txt
chirag@ubuntu:~/learning-git$ cat primary_file.txt
This is the primary file I added to my project.


This file comes before the others.
Git is tracking my changes.
Git Is Awesome.
chirag@ubuntu:~/learning-git$ git status
On branch master
nothing to commit, working tree clean
```
### Unstage A File
```bash
chirag@ubuntu:~/learning-git$ nano primary_file.txt
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   primary_file.txt

no changes added to commit (use "git add" and/or "git commit -a")
chirag@ubuntu:~/learning-git$ git add primary_file.txt

# primary_file.txt Is Now Added To Staging Index
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   primary_file.txt

# Use git reset HEAD To Unstage A File
chirag@ubuntu:~/learning-git$ git reset HEAD primary_file.txt
Unstaged changes after reset:
M       primary_file.txt
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   primary_file.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
### Amend Commits
* We Can Edit The Most Recent Commit.
```bash
chirag@ubuntu:~/learning-git$ nano primary_file.txt
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   primary_file.txt

no changes added to commit (use "git add" and/or "git commit -a")
chirag@ubuntu:~/learning-git$ git add primary_file.txt

# Notice We Made A Typo In The Commit Message
chirag@ubuntu:~/learning-git$ git commit -m "Added Nwe Line To First File"
[master e044dfe] Added Nwe Line To First File
 1 file changed, 1 insertion(+)
chirag@ubuntu:~/learning-git$ git log -n 2
commit e044dfe582c49a601540a57279ec0ef16fc92b48 (HEAD -> master)
Author: Chirag Singh <bharatsr1997@gmail.com>
Date:   Mon Apr 5 15:46:07 2021 +0530

    Added Nwe Line To First File

commit fdfd939cb3f9b8260a82915602025cebc67c9736
Author: Chirag Singh <bharatsr1997@gmail.com>
Date:   Mon Apr 5 15:42:42 2021 +0530

    Added New Line To The First File

# git commit --amend Allows You To Modify The Most Recent Commit
# Notice How SHA-1 Value Is Also Modified
chirag@ubuntu:~/learning-git$ git commit --amend -m "Added New Line To First File"
[master dc83547] Added New Line To First File
 Date: Mon Apr 5 15:46:07 2021 +0530
 1 file changed, 1 insertion(+)
chirag@ubuntu:~/learning-git$ git log -n 2
commit dc835471f94695092072df203573da1df47b5002 (HEAD -> master)
Author: Chirag Singh <bharatsr1997@gmail.com>
Date:   Mon Apr 5 15:46:07 2021 +0530

    Added New Line To First File

commit fdfd939cb3f9b8260a82915602025cebc67c9736
Author: Chirag Singh <bharatsr1997@gmail.com>
Date:   Mon Apr 5 15:42:42 2021 +0530

    Added New Line To The First File
```
### Retrieve Old Versions
```bash
# Suppose We Want To Retrieve The Version Of The File As It Looked Like In Commit SHA fdfd939cb3f9b8260...
chirag@ubuntu:~/learning-git$ git log -n 2
commit dc835471f94695092072df203573da1df47b5002 (HEAD -> master)
Author: Chirag Singh <bharatsr1997@gmail.com>
Date:   Mon Apr 5 15:46:07 2021 +0530

    Added New Line To First File

commit fdfd939cb3f9b8260a82915602025cebc67c9736
Author: Chirag Singh <bharatsr1997@gmail.com>
Date:   Mon Apr 5 15:42:42 2021 +0530

    Added New Line To The First File

# View The Changes Happend In The Commit
chirag@ubuntu:~/learning-git$ git show fdfd939cb3f9b8260a82915602025cebc67c9736
commit fdfd939cb3f9b8260a82915602025cebc67c9736
Author: Chirag Singh <bharatsr1997@gmail.com>
Date:   Mon Apr 5 15:42:42 2021 +0530

    Added New Line To The First File

diff --git a/primary_file.txt b/primary_file.txt
index cf0a43d..3b92788 100644
--- a/primary_file.txt
+++ b/primary_file.txt
@@ -3,4 +3,5 @@ This is the primary file I added to my project.

 This file comes before the others.
 Git is tracking my changes.
-Git Is Awesome.
+Git Is Awesome. Git Is Free.
+
chirag@ubuntu:~/learning-git$ cat primary_file.txt
This is the primary file I added to my project.


This file comes before the others.
Git is tracking my changes.
Git Is Awesome. Git Is Free.
Git Is Open Source.

# Retrieve The Old Version Of The File Using Command
# git checkout <SHA> <branch> <file_name>
chirag@ubuntu:~/learning-git$ git checkout fdfd939cb3f9b8 -- primary_file.txt
chirag@ubuntu:~/learning-git$ cat primary_file.txt
This is the primary file I added to my project.


This file comes before the others.
Git is tracking my changes.
Git Is Awesome. Git Is Free.

# The Old Version Is In Working As Well As Staging Index
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   primary_file.txt

# We Can See The Changes Needed To Be Done In Order To Revert To Old Version
chirag@ubuntu:~/learning-git$ git diff --staged
diff --git a/primary_file.txt b/primary_file.txt
index 619eb7a..3b92788 100644
--- a/primary_file.txt
+++ b/primary_file.txt
@@ -4,5 +4,4 @@ This is the primary file I added to my project.
 This file comes before the others.
 Git is tracking my changes.
 Git Is Awesome. Git Is Free.
-Git Is Open Source.
```
### Revert Commits
```bash
chirag@ubuntu:~/learning-git$ git log -n 1
commit dc835471f94695092072df203573da1df47b5002 (HEAD -> master)
Author: Chirag Singh <bharatsr1997@gmail.com>
Date:   Mon Apr 5 15:46:07 2021 +0530

    Added New Line To First File

# Use git revert <SHA> To Revert Changes To Any Previous Commit
chirag@ubuntu:~/learning-git$ git revert dc835471f94695092072df203573da1df47b5002
[master 90de4b2] Revert "Added New Line To First File"
 1 file changed, 1 deletion(-)
chirag@ubuntu:~/learning-git$ cat primary_file.txt
This is the primary file I added to my project.


This file comes before the others.
Git is tracking my changes.
Git Is Awesome. Git Is Free.

chirag@ubuntu:~/learning-git$ git log -n 1
commit 90de4b278086b515b6527f6f00f3620c2f8e42f9 (HEAD -> master)
Author: Chirag Singh <bharatsr1997@gmail.com>
Date:   Mon Apr 5 16:08:39 2021 +0530

    Revert "Added New Line To First File"

    This reverts commit dc835471f94695092072df203573da1df47b5002.
```
### Remove Untracked Files
```bash
chirag@ubuntu:~/learning-git$ touch junk1.txt
chirag@ubuntu:~/learning-git$ touch junk2.txt
chirag@ubuntu:~/learning-git$ touch junk3.txt
chirag@ubuntu:~/learning-git$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

        junk1.txt
        junk2.txt
        junk3.txt

nothing added to commit but untracked files present (use "git add" to track)

# git clean -n Allow You See Which Files Will Be Deleted
chirag@ubuntu:~/learning-git$ git clean -n
Would remove junk1.txt
Would remove junk2.txt
Would remove junk3.txt

# git clean -f Deletes All Untracked Files
# You Can Use -i Option To Delete Files Interactively
chirag@ubuntu:~/learning-git$ git clean -f
Removing junk1.txt
Removing junk2.txt
Removing junk3.txt
```
---
## .gitignore
* Regex

		*?[aeiou][0-9] 
		logs/*.txt
* All php Files Except Index.php

		.php
		!index.php
* All Files In Folder
  
		assets/videos/
---
## Ignore Tracked Files
```bash
# Suppose We Have A File Which Is Being Tracked
chirag@ubuntu:~/learning-git$ cat secret_file.txt
Password=1234

# Add It To .gitignore
chirag@ubuntu:~/learning-git$ echo "secret_file.txt" > .gitignore

# Remove It From The Cache
chirag@ubuntu:~/learning-git$ git rm --cached secret_file.txt
rm 'secret_file.txt'

# Commit The Changes
chirag@ubuntu:~/learning-git$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        deleted:    secret_file.txt

chirag@ubuntu:~/learning-git$ git commit -m "Untrack Secret File"
[master 2323e51] Untrack Secret File
 1 file changed, 1 deletion(-)
 delete mode 100644 secret_file.txt

# Confirm It Is No Longer Being Tracked
chirag@ubuntu:~/learning-git$ git status
On branch master
nothing to commit, working tree clean
chirag@ubuntu:~/learning-git$ ls
primary_file.txt  secondary_file.txt  secret_file.txt  third_file.txt
chirag@ubuntu:~/learning-git$ echo "UserName=Ninja" >> secret_file.txt
chirag@ubuntu:~/learning-git$ cat secret_file.txt
Password=1234
UserName=Ninja
chirag@ubuntu:~/learning-git$ git status
On branch master
nothing to commit, working tree clean
```
---
## Tracking Empty Directories
Just Add ```.gitkeep``` To The Empty Directory To 
Keep It Tracked.
---
