## What is Git ?

Git is a version control system that tracks every change made to your files, allowing you to "time travel" to previous versions if things break.

It enables multiple developers to work on the same project simultaneously through branching, merging their individual contributions into a single, organized history.

## Why Git Matters ?

Collaboration: Multiple developers can work on the same project without overwriting each other’s work.

History: Every change is tracked, so you can roll back if needed.

Experimentation: Branching allows safe testing of new ideas.

Open Source: Most modern open-source projects rely on Git.

## github vs git

GitHub is not the same thing as “git”.

    Git: Open source VCS software.

    GitHub:Company that operates a service for hosting files on the internet that are managed using git.

●Git is the open source software that actually manages the git commands as a VCS. We will call it at the command line with commands such as: git push

●GitHub is the online hosting provider, that can act as a machine connected to our local machine via the internet and host code in a repository for us.


## Important GIT Commands

**--Config Commands--**

git config --global user.name "Aditya Avi"

git config --global core.editor "c:/windows/notepad.exe -multiinst -nosession"

------------------------------------------------
**git init** - initialize git in a repository

**git clone <url>** - Copy a remote repo locally

**git status**	-	Show current changes and branch info

**git add <file>** -		Stage changes for commit

**git commit -m "message"** -	Save staged changes with a message

**git log**		-	View commit history

**git branch**	-	List or create branches

**git checkout <branch>**	- Switch branches

**git merge <branch>**	- Merge another branch into current

**git push**	-	Upload local commits to remote

**git pull** -		Fetch and merge changes from remote

**git branch -d xyz** -	Delete branch

**git branch -M xyz** -	Rename branch

**git log --oneline** -   Provides logs of commits

## Example Flow for new branch creation

&nbsp;  60  git clone https://github.com/xyz/pandas

&nbsp;  61  cd pandas

&nbsp;  62  echo "Hello Pandas" > hello.txt

&nbsp;  63  git checkout -b practice-branch

&nbsp;  64  git add hello.txt

&nbsp;  65  git status

&nbsp;  66  git commit -m "hello.txt added"

&nbsp;  67  git push origin practice-branch

## git fetch vs. git pull

**git fetch:** "Go see what's new." It downloads the latest data from the remote server but does not change your local files. It’s a passive check. Logs of commits can be seen and this helps avoid merge conflicts.

    git fetch origin: Downloads all updates from the remote "origin" but keeps your local code exactly as it is.

**git pull:** "Get the new stuff and put it in my files right now." It is essentially a git fetch followed immediately by a git merge. It updates your code to match the server.

    git pull origin main: Grabs the latest code from the remote main branch and merges it into your current branch immediately.

This distinction is important in collaborative projects: fetch is safer when you want to review changes first, while pull is faster when you trust the remote updates.

*Tip: Many professional developers prefer git fetch followed by git rebase instead of git pull. This keeps the history cleaner!*

## git reset

**git reset** moves your current branch pointer backward to a specific previous commit. It’s like hitting Undo on a grand scale.

    options:

    --soft: Moves the pointer but keeps your changes staged (ready to commit again).

    --mixed (Default): Moves the pointer and keeps changes in your folder, but unstages them.

    --hard: DANGER. Wipes everything out. Your work-in-progress is gone.

    cmd:
    
    git reset --soft HEAD~1 — Undoes the last commit but keeps your changes staged.
    
    git reset --mixed HEAD~1 — Undoes the last commit and unstages changes, but keeps files in your folder.
    
    git reset --hard HEAD~1 — Completely deletes the last commit and all uncommitted changes.

## git revert

**git revert** is the safest way to undo a change, especially if you've already pushed your code to a shared server (like GitHub).

    --Instead of deleting a bad commit, Git creates a brand new commit that does the exact opposite of the one you want to get rid of. If you added a line in Commit B, revert creates Commit C that deletes that line.

    --It preserves history. Everyone can see exactly what went wrong and how it was fixed. It doesn't "break" the timeline for your teammates.

    Example scenrio: You need to fix the site immediately. You can't use reset because other developers have already pulled your broken code; if you "delete" the history, their computers will get confused.

    cmd:
    
    --git revert <commit-id> — Creates a new commit that introduces the exact opposite changes of the specified commit.

## git rebase

**git rebase** is about moving a sequence of commits to a new base commit. It’s the "make it look pretty" tool.

    --Imagine you branched off main a week ago. Since then, main has moved forward. rebase takes your work, lifts it up, and sticks it onto the very end of the current main branch.

    --A perfectly straight line of history without "merge commits" cluttering things up.
    --Interactive Rebase (-i): This lets you "squash" five tiny, messy commits into one clean, professional-looking commit.

    --Git virtually "lifts" your feature-auth branch, sets it aside, updates your branch to include all the new work from main, and then "replays" your commits one by one on top of the fresh code.

    cmd:
    
    --git rebase main — Moves your current branch's commits to the tip of the main branch.
    
    --git rebase -i HEAD~3 — Opens an interactive list of the last 3 commits to squash, edit, or delete them.

## git tag

**git tag** is used to capture a point in history as being important. Most people use it to mark Release Points (e.g., v1.0, v2.1.4).A tag is a pointer to a specific commit that doesn't move. Unlike a branch (which moves every time you add a new commit), a tag stays exactly where you put it.

    cmd:
    
    --git tag -a v1.0 -m "Version 1.0 release" — Creates a permanent, annotated label for the current commit.
    
    --git push origin v1.0 — Explicitly sends a specific tag to the remote server.

## git stash

**git stash** is your "I'm not done yet, but I need to switch tasks" button. It’s a way to temporarily shelf your uncommitted changes so you can work on something else.Git takes your modified files (both staged and unstaged) and saves them in a secret internal stack. Your working directory then becomes "clean" (matching the last commit). When you’re ready, you "pop" the changes back out.

    cmd:
    --git stash — Hides your uncommitted changes and reverts your folder to a clean state.
    
    --git stash list — Shows all the "shelved" sets of changes you currently have saved.
    
    --git stash pop — Re-applies the most recently stashed changes and removes them from the stash list.
    
    --git stash apply — Re-applies stashed changes but keeps them saved in the stash list for later use.

