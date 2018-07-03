---
description: We use Git. Here's how to use it and what to do if you mess something up.
---

# Git Flight Rules

## Why Git is important

We version control our software using Git. It allows a sane way to update code, provides configuration management for servers and allows us to revert to known-good code when something breaks. It basically looks like this:

![Our Git workflow](https://documents.lucidchart.com/documents/cbc00276-f5dd-4454-a3ac-168d78e93029/pages/0_0?a=789&x=-45&y=248&w=1879&h=435&store=1&accept=image%2F*&auth=LCA%203b96d4a37bf6f6dbf3d6ed019817cbb6c77459c9-ts%3D1529638942)

### Our Git workflow

**MASTER branches are protected.** Not because we don't trust you...well, ok...kind of. Anything that merges to MASTER gets built into production. 

**DEV branches are for development.** Coding is done on the DEV branch, and any features or bug fixes on a NON-PRODUCTION system come off the DEV branch. Once the DEV branch is in a releasable state, a final merge request is approved and the code goes into production.

**FEATURE branches** **add functionality to an application**. A new page, a new button, a color update...all those kinds of changes are feature branches and merged back to DEV.

**FIX branches fix a bug we found in testing.** These are ideally caught in automatic testing and are very important. Fix branches merge do DEV, and are pushed to production when DEV is merged.

**HOTFIX branches mean we messed up.** We didn't test well enough and a bug made it into production. Generally these are usability breaking or security bugs. Other bugs, depending on severity, should be fixed in development and rolled into the next release.

### Git best practices

_**DON'T PANIC**_ - As long as you regularly commit your work, you probably won't ever lose any work unless you actively try to destroy it by running commands or physically destroy the hard drive the data is on.

_**COMMIT EARLY, COMMIT OFTEN -**_ Git only takes full responsibility for your data when you commit. If you fail to commit and then do something stu...poorly thought out, you can run into trouble. Additionally, having periodic checkpoints means that you can understand how you broke something.

_**MAKE COMMIT MESSAGES COUNT -**_ Creating insightful and descriptive commit messages is one of the best things you can do for others who use the repository. It lets people quickly understand changes without having to read code. When doing history archeology to answer some question, good commit messages likewise become very important. A great template for a commit message:

```text
Capitalized, short (50 chars or less) summary

Explain if you must. Tell what bug was squashed or feature was added.
Don't just say WHAT you did, say WHERE you did it.

- index.html
    added new header image
- index.html
    adjusted links in footer
- district.html
    fixed mispelling of 'SEPARATION'
```

_**HAVE STANDARDS -**_ Coding standards improve the quality of our commits, code-base and generally keep the nerds and the computers happy. Checks include regression tests, compilation tests, syntax/lint checkers, commit message analysis, etc. Deviations are sometimes, but rarely, necessary. We use stuff like commit hooks that can reject commits that don’t follow the standards.

_**AGREE ON A WORKFLOW -**_ When do we create a branch? How is it merged? How is it tested? These are important questions. In OTSS it can be summed up like this:

1. create an initial DEV branch
2. branch a DEV branch
3. branch feature and bug branches from DEV until DEV is an MVP
4. create MERGE request for DEV
5. the boss approves the MERGE request and DEV-&gt;MASTER-&gt;PRODUCTION
6. Profit?

## Terms

**Branch -** A version of the repository that diverges from the main working project...literally like a tree branch from a tree trunk. Branches can be a new version of a repository, experimental changes, or personal forks of a repository for users to alter and test changes.

**Checkout -** The `git checkout` command is used to switch branches in a repository. `git checkout testing-el` would take you to the _testing-el_ branch whereas `git checkout master` would drop you back into master. Be careful with your staged files and commits when switching between branches.

**Cherry-picking** - When cherry-picking a commit in Git, you are taking an older commit, and rerunning it at a defined location. Git copies the changes from the original commit, and then adds them to the current location.

**Clone** - A clone is a copy of a repository or the action of copying a repository. When cloning a repository into another branch, the new branch becomes a remote-tracking branch that can talk upstream to its origin branch \(via pushes, pulls, and fetches\).

**Fetch** - By performing a Git fetch, you are downloading and copying that branch’s files to your workstation. Multiple branches can be fetched at once, and you can rename the branches when running the command to suit your needs.

**Fork** - Creates a copy of a repository.

**HEAD** - HEAD is a reference variable used to denote the most current commit of the repository in which you are working. When you add a new commit, HEAD will then become that new commit.

**Index** - The working, or staging, area of Git. Files that have been changed, added and deleted will be staged within the index until you are ready to commit the files. To see what is set in your Git index, run `git status` within your repository. The green files are staged and ready to commit, whereas the red files have not yet been added to staging for the next commit.

**Master** - The primary branch of all repositories. All committed and accepted changes should be on the master branch. You can work directly from the master branch, or create other branches.

**Merge** - Taking the changes from one branch and adding them into another \(traditionally master\) branch. These commits are usually first requested via [pull request](https://linuxacademy.com/blog/linux/git-terms-explained/#pull) before being merged by a project maintainer.

**Origin** - The conventional name for the primary version of a repository. Git also uses `origin` as a system alias for pushing and fetching data to and from the primary branch. For example, `git push origin master`, when run on a remote, will push the changes to the master branch of the primary repository database.

**Pull/Pull Request** - If someone has changed code on a separate branch of a project and wants it to be reviewed to add to the master branch, that someone can put in a pull request. Pull requests ask the repo maintainers to review the commits made, and then, if acceptable, merge the changes upstream. A pull happens when adding the changes to the master branch.

**Push** - Updates a remote branch with the commits made to the current branch. You are literally “pushing” your changes onto the remote.

**Rebase** - When rebasing a git commit, you can split the commit, move it, squash it if unwanted, or effectively combine two branches that have diverged from one another.

**Remote** - A copy of the original branch. When you clone a branch, that new branch is a remote, or _clone_. Remotes can talk to the origin branch, as well as other remotes for the repository, to make communication between working branches easier.

**Repository \(“Repo”\)** - In many ways, you can think of a Git repository as a directory that stores all the files, folders, and content needed for your project. What it actually is, is the object database of the project, storing everything from the files themselves, to the versions of those files, commits, deletions, et cetera. Repositories are not limited by user, and can be shared and copied \(see: [fork](https://linuxacademy.com/blog/linux/git-terms-explained/#fork)\).

**Stash** - While working with Git, you may need to make multiple changes to files, but you may not want all changes to go in one commit. If you want to pause the changes you are working on now in favor of working on another issue or improvement, you can “stash” your changes, essentially clearing them from the staging area until the changes are called again. You can only stash one set of changes at a time. To stash your staging area use `git stash [files]`; to retrieve the stashed files, run `git stash pop`. You can also clear the stashed files with `git stash drop`.

**Tag** - Tags are used to define which portions of a project’s Git history is most important. Often this is used to note point releases of a project. Tags can be added to the commit you are working with or added after-the-fact when needed.

**Upstream** - While there is not necessarily a default “upstream” or “downstream” for Git projects, upstream can be considered where you _push_ your Git changes — this is often the master branch of the project within the origin.

## Repositories \(just use repo\)

Git puts an invisible `.git` folder inside your project folder. This tracks all of your local and remote changes, branches, commit messages and code. The `.git` folder also stores your configuration such as the location of the origin \(the remote, central repository\).

### I want to start a local repository

You have a folder with code already on your machine. To initialize an existing directory as a Git repository, open your command line and initialize your repo with:

```text
// change into your project folder
$ cd my-project-folder

// initialize the git repo
(my-project-folder) $ git init
```

_**THAT'S IT!**_  Your local folder is now a repo. You can commit changes into version control without ever accessing the central repository.

### I want to clone a remote repository

Let's say you're asked to work on a shared project. Instead of 'checking in' or 'checking out' code, you're going to _**clone**_ or _**copy**_  the code from the central repo on to your machine. _**You don't have to run `git init`**_ because the remote repo already has the .git folder!

To clone \(copy\) a remote repository, copy the url for the repository, and run:

```text
// to use the project/repo to a folder named 'awesome-project'
$ git clone https://code.mdek12.org/awesome-project

// to clone it into a folder named after your dog
$ git clone https://code.mdek12.org/awesome-project fluffy
```

## Committing code

The whole point of Git is to keep track of changes to the code. You do this by tracking and committing changes \(and pushing and pulling but that's later\).

### I want to tell Git what files to version control

You do this by _**tracking.**_

```text
// save your work first, then 'add' your files to track them
(awesome-project) $ git add . (or * in windows)

// to track a specific file
(awesome-project) $ git add specific-file-to-track.jpg
```

_**BUT WHAT ABOUT FILES I DON'T WANT TO TRACK?**_

That's what .gitignore files are for. Read that later when you're bored. Just use `git add .` or `git add file.txt` for now.

### I want to create a snapshot of my code

This is even easier, but there's one caveat..._**YOU HAVE TO TELL EVERYONE ELSE WHAT YOU DID!**_

```text
// make sure you add your files to tracking first
(awesome-project) $ git add .

// now commit your changes
(awesome-project) $ git commit -m "update the icon to corn-flower blue for my man"
```

## Editing Commits

### I forgot what I just committed

Let's say that you just blindly committed changes with `git commit -a` and you're not sure what the actual content of the commit you just made was. You can show the latest commit on your current HEAD with:

```text
(master)$ git show
```

Or

```text
$ git log -n1 -p
```

If you want to see a file at a specific commit, you can also do this \(where `<commitid>` is the commit you're interested in\):

```text
$ git show <commitid>:filename
```

### I wrote the wrong thing in a commit message

If you wrote the wrong thing and the commit has not yet been pushed, you can do the following to change the commit message:

```text
$ git commit --amend
```

This will open your default text editor, where you can edit the message. On the other hand, you can do this all in one command:

```text
$ git commit --amend -m 'xxxxxxx'
```

If you have already pushed the message, you can amend the commit and force push, but this is not recommended.

### I committed with the wrong name and email configured

If it's a single commit, amend it

```text
$ git commit --amend --no-edit --author "New Authorname <authoremail@mydomain.com>"
```

An alternative is to correctly configure your author settings in `git config --global author.(name|email)` and then use

```text
$ git commit --amend --reset-author --no-edit
```

If you need to change all of history, see the man page for `git filter-branch`.

### I want to remove a file from the previous commit

In order to remove changes for a file from the previous commit, do the following:

```text
$ git checkout HEAD^ myfile
$ git add myfile
$ git commit --amend --no-edit
```

In case the file was newly added to the commit and you want to remove it \(from Git alone\), do:

```text
$ git rm --cached myfile
$ git commit --amend --no-edit
```

This is particularly useful when you have an open patch and you have committed an unnecessary file, and need to force push to update the patch on a remote. The `--no-edit` option is used to keep the existing commit message.

### I want to delete or remove my last commit

If you need to delete pushed commits, you can use the following. However, it will irreversibly change your history, and mess up the history of anyone else who had already pulled from the repository. In short, if you're not sure, you should never do this, ever.

```text
$ git reset HEAD^ --hard
$ git push --force-with-lease [remote] [branch]
```

If you haven't pushed, to reset Git to the state it was in before you made your last commit \(while keeping your staged changes\):

```text
(my-branch*)$ git reset --soft HEAD@{1}

```

This only works if you haven't pushed. If you have pushed, the only truly safe thing to do is `git revert SHAofBadCommit`. That will create a new commit that undoes all the previous commit's changes. Or, if the branch you pushed to is rebase-safe \(ie. other devs aren't expected to pull from it\), you can just use `git push --force-with-lease`. For more, see [the above section](https://github.com/k88hudson/git-flight-rules#deleteremove-last-pushed-commit).

### Delete/remove arbitrary commit

The same warning applies as above. Never do this if possible.

```text
$ git rebase --onto SHA1_OF_BAD_COMMIT^ SHA1_OF_BAD_COMMIT
$ git push --force-with-lease [remote] [branch]
```

Or do an [interactive rebase](https://github.com/k88hudson/git-flight-rules#interactive-rebase) and remove the line\(s\) corresponding to commit\(s\) you want to see removed.

### I tried to push my amended commit to a remote, but I got an error message

```text
To https://github.com/yourusername/repo.git
! [rejected]        mybranch -> mybranch (non-fast-forward)
error: failed to push some refs to 'https://github.com/tanay1337/webmaker.org.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

Note that, as with rebasing \(see below\), amending **replaces the old commit with a new one**, so you must force push \(`--force-with-lease`\) your changes if you have already pushed the pre-amended commit to your remote. Be careful when you do this – _always_ make sure you specify a branch!

```text
(my-branch)$ git push origin mybranch --force-with-lease
```

In general, **avoid force pushing**. It is best to create and push a new commit rather than force-pushing the amended commit as it will cause conflicts in the source history for any other developer who has interacted with the branch in question or any child branches. `--force-with-lease` will still fail, if someone else was also working on the same branch as you, and your push would overwrite those changes.

If you are _absolutely_ sure that nobody is working on the same branch or you want to update the tip of the branch _unconditionally_, you can use `--force` \(`-f`\), but this should be avoided in general.

### I accidentally did a hard reset, and I want my changes back

If you accidentally do `git reset --hard`, you can normally still get your commit back, as git keeps a log of everything for a few days.

Note: This is only valid if your work is backed up, i.e., either committed or stashed. `git reset --hard` _will remove_uncommitted modifications, so use it with caution. \(A safer option is `git reset --keep`.\)

```text
(master)$ git reflog
```

You'll see a list of your past commits, and a commit for the reset. Choose the SHA of the commit you want to return to, and reset again:

```text
(master)$ git reset --hard SHA1234
```

Basta.

## Staging

### I need to add staged changes to the previous commit

```text
(my-branch*)$ git commit --amend
```

### I want to stage part of a new file, but not the whole file

Normally, if you want to stage part of a file, you run this:

```text
$ git add --patch filename.x
```

`-p` will work for short. This will open interactive mode. You would be able to use the `s` option to split the commit - however, if the file is new, you will not have this option. To add a new file, do this:

```text
$ git add -N filename.x
```

Then, you will need to use the `e` option to manually choose which lines to add. Running `git diff --cached` or `git diff --staged` will show you which lines you have staged compared to which are still saved locally.

### I want to add changes in one file to two different commits

`git add` will add the entire file to a commit. `git add -p` will allow to interactively select which changes you want to add.

### I want to stage my unstaged edits, and unstage my staged edits

This is tricky. The best I figure is that you should stash your unstaged edits. Then, reset. After that, pop your stashed edits back, and add them.

```text
$ git stash -k
$ git reset --hard
$ git stash pop
$ git add -A
```

## Unstaged Edits

### I want to move my unstaged edits to a new branch

```text
$ git checkout -b my-branch
```

### I want to move my unstaged edits to a different, existing branch

```text
$ git stash
$ git checkout my-branch
$ git stash pop
```

### I want to discard my local uncommitted changes \(staged and unstaged\)

If you want to discard all your local staged and unstaged changes, you can do this:

```text
(my-branch)$ git reset --hard
# or
(master)$ git checkout -f
```

This will unstage all files you might have staged with `git add`:

```text
$ git reset
```

This will revert all local uncommitted changes \(should be executed in repo root\):

```text
$ git checkout .
```

You can also revert uncommitted changes to a particular file or directory:

```text
$ git checkout [some_dir|file.txt]
```

Yet another way to revert all uncommitted changes \(longer to type, but works from any subdirectory\):

```text
$ git reset --hard HEAD
```

This will remove all local untracked files, so only files tracked by Git remain:

```text
$ git clean -fd
```

`-x` will also remove all ignored files.

### I want to discard specific unstaged changes

When you want to get rid of some, but not all changes in your working copy.

Checkout undesired changes, keep good changes.

```text
$ git checkout -p
# Answer y to all of the snippets you want to drop
```

Another strategy involves using `stash`. Stash all the good changes, reset working copy, and reapply good changes.

```text
$ git stash -p
# Select all of the snippets you want to save
$ git reset --hard
$ git stash pop
```

Alternatively, stash your undesired changes, and then drop stash.

```text
$ git stash -p
# Select all of the snippets you don't want to save
$ git stash drop
```

### I want to discard specific unstaged files

When you want to get rid of one specific file in your working copy.

```text
$ git checkout myFile
```

Alternatively, to discard multiple files in your working copy, list them all.

```text
$ git checkout myFirstFile mySecondFile
```

### I want to discard only my unstaged local changes

When you want to get rid of all of your unstaged local uncommitted changes

```text
$ git checkout .
```

### I want to discard all of my untracked files

When you want to get rid of all of your untracked files

```text
$ git clean -f
```

## Branches

### I want to list all branches

List local branches

```text
$ git branch
```

List remote branches

```text
$ git branch -r
```

List all branches \(both local and remote\)

```text
$ git branch -a
```

### Create a branch from a commit

```text
$ git checkout -b <branch> <SHA1_OF_COMMIT>
```

### I pulled from/into the wrong branch

This is another chance to use `git reflog` to see where your HEAD pointed before the bad pull.

```text
(master)$ git reflog
ab7555f HEAD@{0}: pull origin wrong-branch: Fast-forward
c5bc55a HEAD@{1}: checkout: checkout message goes here
```

Simply reset your branch back to the desired commit:

```text
$ git reset --hard c5bc55a
```

Done.

### I want to discard local commits so my branch is the same as one on the server

Confirm that you haven't pushed your changes to the server.

`git status` should show how many commits you are ahead of origin:

```text
(my-branch)$ git status
# On branch my-branch
# Your branch is ahead of 'origin/my-branch' by 2 commits.
#   (use "git push" to publish your local commits)
#
```

One way of resetting to match origin \(to have the same as what is on the remote\) is to do this:

```text
(master)$ git reset --hard origin/my-branch
```

### I committed to master instead of a new branch

Create the new branch while remaining on master:

```text
(master)$ git branch my-branch
```

Reset the branch master to the previous commit:

```text
(master)$ git reset --hard HEAD^
```

`HEAD^` is short for `HEAD^1`. This stands for the first parent of `HEAD`, similarly `HEAD^2` stands for the second parent of the commit \(merges can have 2 parents\).

Note that `HEAD^2` is **not** the same as `HEAD~2` \(see [this link](http://www.paulboxley.com/blog/2011/06/git-caret-and-tilde) for more information\).

Alternatively, if you don't want to use `HEAD^`, find out what the commit hash you want to set your master branch to \(`git log` should do the trick\). Then reset to that hash. `git push` will make sure that this change is reflected on your remote.

For example, if the hash of the commit that your master branch is supposed to be at is `a13b85e`:

```text
(master)$ git reset --hard a13b85e
HEAD is now at a13b85e
```

Checkout the new branch to continue working:

```text
(master)$ git checkout my-branch
```

### I want to keep the whole file from another ref-ish

Say you have a working spike \(see note\), with hundreds of changes. Everything is working. Now, you commit into another branch to save that work:

```text
(solution)$ git add -A && git commit -m "Adding all changes from this spike into one big commit."
```

When you want to put it into a branch \(maybe feature, maybe `develop`\), you're interested in keeping whole files. You want to split your big commit into smaller ones.

Say you have:

* branch `solution`, with the solution to your spike. One ahead of `develop`.
* branch `develop`, where you want to add your changes.

You can solve it bringing the contents to your branch:

```text
(develop)$ git checkout solution -- file1.txt
```

This will get the contents of that file in branch `solution` to your branch `develop`:

```text
# On branch develop
# Your branch is up-to-date with 'origin/develop'.
# Changes to be committed:
#  (use "git reset HEAD <file>..." to unstage)
#
#        modified:   file1.txt
```

Then, commit as usual.

Note: Spike solutions are made to analyze or solve the problem. These solutions are used for estimation and discarded once everyone gets clear visualization of the problem. ~ [Wikipedia](https://en.wikipedia.org/wiki/Extreme_programming_practices).

### I made several commits on a single branch that should be on different branches

Say you are on your master branch. Running `git log`, you see you have made two commits:

```text
(master)$ git log

commit e3851e817c451cc36f2e6f3049db528415e3c114
Author: Alex Lee <alexlee@example.com>
Date:   Tue Jul 22 15:39:27 2014 -0400

    Bug #21 - Added CSRF protection

commit 5ea51731d150f7ddc4a365437931cd8be3bf3131
Author: Alex Lee <alexlee@example.com>
Date:   Tue Jul 22 15:39:12 2014 -0400

    Bug #14 - Fixed spacing on title

commit a13b85e984171c6e2a1729bb061994525f626d14
Author: Aki Rose <akirose@example.com>
Date:   Tue Jul 21 01:12:48 2014 -0400

    First commit
```

Let's take note of our commit hashes for each bug \(`e3851e8` for \#21, `5ea5173` for \#14\).

First, let's reset our master branch to the correct commit \(`a13b85e`\):

```text
(master)$ git reset --hard a13b85e
HEAD is now at a13b85e
```

Now, we can create a fresh branch for our bug \#21:

```text
(master)$ git checkout -b 21
(21)$
```

Now, let's _cherry-pick_ the commit for bug \#21 on top of our branch. That means we will be applying that commit, and only that commit, directly on top of whatever our head is at.

```text
(21)$ git cherry-pick e3851e8
```

At this point, there is a possibility there might be conflicts. See the [**There were conflicts**](https://github.com/k88hudson/git-flight-rules#merge-conflict) section in the [interactive rebasing section above](https://github.com/k88hudson/git-flight-rules#interactive-rebase) for how to resolve conflicts.

Now let's create a new branch for bug \#14, also based on master

```text
(21)$ git checkout master
(master)$ git checkout -b 14
(14)$
```

And finally, let's cherry-pick the commit for bug \#14:

```text
(14)$ git cherry-pick 5ea5173
```

### I want to delete local branches that were deleted upstream

Once you merge a pull request on GitHub, it gives you the option to delete the merged branch in your fork. If you aren't planning to keep working on the branch, it's cleaner to delete the local copies of the branch so you don't end up cluttering up your working checkout with a lot of stale branches.

```text
$ git fetch -p upstream
```

where, `upstream` is the remote you want to fetch from.

### I accidentally deleted my branch

If you're regularly pushing to remote, you should be safe most of the time. But still sometimes you may end up deleting your branches. Let's say we create a branch and create a new file:

```text
(master)$ git checkout -b my-branch
(my-branch)$ git branch
(my-branch)$ touch foo.txt
(my-branch)$ ls
README.md foo.txt
```

Let's add it and commit.

```text
(my-branch)$ git add .
(my-branch)$ git commit -m 'foo.txt added'
(my-branch)$ foo.txt added
 1 files changed, 1 insertions(+)
 create mode 100644 foo.txt
(my-branch)$ git log

commit 4e3cd85a670ced7cc17a2b5d8d3d809ac88d5012
Author: siemiatj <siemiatj@example.com>
Date:   Wed Jul 30 00:34:10 2014 +0200

    foo.txt added

commit 69204cdf0acbab201619d95ad8295928e7f411d5
Author: Kate Hudson <katehudson@example.com>
Date:   Tue Jul 29 13:14:46 2014 -0400

    Fixes #6: Force pushing after amending commits
```

Now we're switching back to master and 'accidentally' removing our branch.

```text
(my-branch)$ git checkout master
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.
(master)$ git branch -D my-branch
Deleted branch my-branch (was 4e3cd85).
(master)$ echo oh noes, deleted my branch!
oh noes, deleted my branch!
```

At this point you should get familiar with 'reflog', an upgraded logger. It stores the history of all the action in the repo.

```text
(master)$ git reflog
69204cd HEAD@{0}: checkout: moving from my-branch to master
4e3cd85 HEAD@{1}: commit: foo.txt added
69204cd HEAD@{2}: checkout: moving from master to my-branch
```

As you can see we have commit hash from our deleted branch. Let's see if we can restore our deleted branch.

```text
(master)$ git checkout -b my-branch-help
Switched to a new branch 'my-branch-help'
(my-branch-help)$ git reset --hard 4e3cd85
HEAD is now at 4e3cd85 foo.txt added
(my-branch-help)$ ls
README.md foo.txt
```

Voila! We got our removed file back. `git reflog` is also useful when rebasing goes terribly wrong.

### I want to delete a branch

To delete a remote branch:

```text
(master)$ git push origin --delete my-branch
```

You can also do:

```text
(master)$ git push origin :my-branch
```

To delete a local branch:

```text
(master)$ git branch -d my-branch
```

To delete a local branch that _has not_ been merged to the current branch or an upstream:

```text
(master)$ git branch -D my-branch
```

### I want to delete multiple branches

Say you want to delete all branches that start with `fix/`:

```text
(master)$ git branch | grep 'fix/' | xargs git branch -d
```

### I want to rename a branch

To rename the current \(local\) branch:

```text
(master)$ git branch -m new-name
```

To rename a different \(local\) branch:

```text
(master)$ git branch -m old-name new-name
```

### I want to checkout to a remote branch that someone else is working on

First, fetch all branches from remote:

```text
(master)$ git fetch --all
```

Say you want to checkout to `daves` from the remote.

```text
(master)$ git checkout --track origin/daves
Branch daves set up to track remote branch daves from origin.
Switched to a new branch 'daves'
```

\(`--track` is shorthand for `git checkout -b [branch] [remotename]/[branch]`\)

This will give you a local copy of the branch `daves`, and any update that has been pushed will also show up remotely.

### I want to create a new remote branch from current local one

```text
$ git push <remote> HEAD
```

If you would also like to set that remote branch as upstream for the current one, use the following instead:

```text
$ git push -u <remote> HEAD
```

With the `upstream` mode and the `simple` \(default in Git 2.0\) mode of the `push.default` config, the following command will push the current branch with regards to the remote branch that has been registered previously with `-u`:

```text
$ git push
```

The behavior of the other modes of `git push` is described in the [doc of `push.default`](https://git-scm.com/docs/git-config#git-config-pushdefault).

### I want to set a remote branch as the upstream for a local branch

You can set a remote branch as the upstream for the current local branch using:

```text
$ git branch --set-upstream-to [remotename]/[branch]
# or, using the shorthand:
$ git branch -u [remotename]/[branch]
```

To set the upstream remote branch for another local branch:

```text
$ git branch -u [remotename]/[branch] [local-branch]
```

### I want to set my HEAD to track the default remote branch

By checking your remote branches, you can see which remote branch your HEAD is tracking. In some cases, this is not the desired branch.

```text
$ git branch -r
  origin/HEAD -> origin/gh-pages
  origin/master
```

To change `origin/HEAD` to track `origin/master`, you can run this command:

```text
$ git remote set-head origin --auto
origin/HEAD set to master
```

### I made changes on the wrong branch

You've made uncommitted changes and realise you're on the wrong branch. Stash changes and apply them to the branch you want:

```text
(wrong_branch)$ git stash
(wrong_branch)$ git checkout <correct_branch>
(correct_branch)$ git stash apply
```

## Rebasing and Merging

### I want to undo rebase/merge

You may have merged or rebased your current branch with a wrong branch, or you can't figure it out or finish the rebase/merge process. Git saves the original HEAD pointer in a variable called ORIG\_HEAD before doing dangerous operations, so it is simple to recover your branch at the state before the rebase/merge.

```text
(my-branch)$ git reset --hard ORIG_HEAD
```

### I rebased, but I don't want to force push

Unfortunately, you have to force push, if you want those changes to be reflected on the remote branch. This is because you have changed the history. The remote branch won't accept changes unless you force push. This is one of the main reasons many people use a merge workflow, instead of a rebasing workflow - large teams can get into trouble with developers force pushing. Use this with caution. A safer way to use rebase is not to reflect your changes on the remote branch at all, and instead to do the following:

```text
(master)$ git checkout my-branch
(my-branch)$ git rebase -i master
(my-branch)$ git checkout master
(master)$ git merge --ff-only my-branch
```

For more, see [this SO thread](https://stackoverflow.com/questions/11058312/how-can-i-use-git-rebase-without-requiring-a-forced-push).

### I need to combine commits

Let's suppose you are working in a branch that is/will become a pull-request against `master`. In the simplest case when all you want to do is to combine _all_ commits into a single one and you don't care about commit timestamps, you can reset and recommit. Make sure the master branch is up to date and all your changes committed, then:

```text
(my-branch)$ git reset --soft master
(my-branch)$ git commit -am "New awesome feature"
```

If you want more control, and also to preserve timestamps, you need to do something called an interactive rebase:

```text
(my-branch)$ git rebase -i master
```

If you aren't working against another branch you'll have to rebase relative to your `HEAD`. If you want to squash the last 2 commits, for example, you'll have to rebase against `HEAD~2`. For the last 3, `HEAD~3`, etc.

```text
(master)$ git rebase -i HEAD~2
```

After you run the interactive rebase command, you will see something like this in your text editor:

```text
pick a9c8a1d Some refactoring
pick 01b2fd8 New awesome feature
pick b729ad5 fixup
pick e3851e8 another fix

# Rebase 8074d12..b729ad5 onto 8074d12
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

All the lines beginning with a `#` are comments, they won't affect your rebase.

Then you replace `pick` commands with any in the list above, and you can also remove commits by removing corresponding lines.

For example, if you want to **leave the oldest \(first\) commit alone and combine all the following commits with the second oldest**, you should edit the letter next to each commit except the first and the second to say `f`:

```text
pick a9c8a1d Some refactoring
pick 01b2fd8 New awesome feature
f b729ad5 fixup
f e3851e8 another fix
```

If you want to combine these commits **and rename the commit**, you should additionally add an `r` next to the second commit or simply use `s` instead of `f`:

```text
pick a9c8a1d Some refactoring
pick 01b2fd8 New awesome feature
s b729ad5 fixup
s e3851e8 another fix
```

You can then rename the commit in the next text prompt that pops up.

```text
Newer, awesomer features

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# rebase in progress; onto 8074d12
# You are currently editing a commit while rebasing branch 'master' on '8074d12'.
#
# Changes to be committed:
#   modified:   README.md
#
```

If everything is successful, you should see something like this:

```text
(master)$ Successfully rebased and updated refs/heads/master.
```

### **Safe merging strategy**

`--no-commit` performs the merge but pretends the merge failed and does not autocommit, giving the user a chance to inspect and further tweak the merge result before committing. `no-ff` maintains evidence that a feature branch once existed, keeping project history consistent.

```text
(master)$ git merge --no-ff --no-commit my-branch
```

### **I need to merge a branch into a single commit**

```text
(master)$ git merge --squash my-branch
```

### **I want to combine only unpushed commits**

Sometimes you have several work in progress commits that you want to combine before you push them upstream. You don't want to accidentally combine any commits that have already been pushed upstream because someone else may have already made commits that reference them.

```text
(master)$ git rebase -i @{u}
```

This will do an interactive rebase that lists only the commits that you haven't already pushed, so it will be safe to reorder/fix/squash anything in the list.

### **I need to abort the merge**

Sometimes the merge can produce problems in certain files, in those cases we can use the option `abort` to abort the current conflict resolution process, and try to reconstruct the pre-merge state.

```text
(my-branch)$ git merge --abort
```

This command is available since Git version &gt;= 1.7.4

### Check if all commits on a branch are merged

To check if all commits on a branch are merged into another branch, you should diff between the heads \(or any commits\) of those branches:

```text
(master)$ git log --graph --left-right --cherry-pick --oneline HEAD...feature/120-on-scroll
```

This will tell you if any commits are in one but not the other, and will give you a list of any nonshared between the branches. Another option is to do this:

```text
(master)$ git log master ^feature/120-on-scroll --no-merges
```

## Possible issues with interactive rebases

### **The rebase editing screen says 'noop'**

If you're seeing this:

```text
noop
```

That means you are trying to rebase against a branch that is at an identical commit, or is _ahead_ of your current branch. You can try:

* making sure your master branch is where it should be
* rebase against `HEAD~2` or earlier instead

### **There were conflicts**

If you are unable to successfully complete the rebase, you may have to resolve conflicts.

First run `git status` to see which files have conflicts in them:

```text
(my-branch)$ git status
On branch my-branch
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

  both modified:   README.md
```

In this example, `README.md` has conflicts. Open that file and look for the following:

```text
   <<<<<<< HEAD
   some code
   =========
   some code
   >>>>>>> new-commit
```

You will need to resolve the differences between the code that was added in your new commit \(in the example, everything from the middle line to `new-commit`\) and your `HEAD`.

If you want to keep one branch's version of the code, you can use `--ours` or `--theirs`:

```text
(master*)$ git checkout --ours README.md
```

* When _merging_, use `--ours` to keep changes from the local branch, or `--theirs` to keep changes from the other branch.
* When _rebasing_, use `--theirs` to keep changes from the local branch, or `--ours` to keep changes from the other branch. For an explanation of this swap, see [this note in the Git documentation](https://git-scm.com/docs/git-rebase#git-rebase---merge).

If the merges are more complicated, you can use a visual diff editor:

```text
(master*)$ git mergetool -t opendiff
```

After you have resolved all conflicts and tested your code, `git add` the files you have changed, and then continue the rebase with `git rebase --continue`

```text
(my-branch)$ git add README.md
(my-branch)$ git rebase --continue
```

If after resolving all the conflicts you end up with an identical tree to what it was before the commit, you need to `git rebase --skip` instead.

If at any time you want to stop the entire rebase and go back to the original state of your branch, you can do so:

```text
(my-branch)$ git rebase --abort
```

## Stash

### Stash all edits

To stash all the edits in your working directory

```text
$ git stash
```

If you also want to stash untracked files, use `-u` option.

```text
$ git stash -u
```

### Stash specific files

To stash only one file from your working directory

```text
$ git stash push working-directory-path/filename.ext
```

To stash multiple files from your working directory

```text
$ git stash push working-directory-path/filename1.ext working-directory-path/filename2.ext
```

### Stash with message

```text
$ git stash save <message>
```

### Apply a specific stash from list

First check your list of stashes with message using

```text
$ git stash list
```

Then apply a specific stash from the list using

```text
$ git stash apply "stash@{n}"
```

Here, 'n' indicates the position of the stash in the stack. The topmost stash will be position 0.

## Finding

### I want to find a string in any commit

To find a certain string which was introduced in any commit, you can use the following structure:

```text
$ git log -S "string to find"
```

Commons parameters:

* `--source` means to show the ref name given on the command line by which each commit was reached.
* `--all` means to start from every branch.
* `--reverse` prints in reverse order, it means that will show the first commit that made the change.

### I want to find by author/committer

To find all commits by author/committer you can use:

```text
$ git log --author=<name or email>
$ git log --committer=<name or email>
```

Keep in mind that author and committer are not the same. The `--author` is the person who originally wrote the code; on the other hand, the `--committer`, is the person who committed the code on behalf of the original author.

### I want to list commits containing specific files

To find all commits containing a specific file you can use:

```text
$ git log -- <path to file>
```

You would usually specify an exact path, but you may also use wild cards in the path and file name:

```text
$ git log -- **/*.js
```

While using wildcards, it's useful to inform `--name-status` to see the list of committed files:

```text
$ git log --name-status -- **/*.js
```

### Find a tag where a commit is referenced

To find all tags containing a specific commit:

```text
$ git tag --contains <commitid>
```

## Submodules

### Clone all submodules

```text
$ git clone --recursive git://github.com/foo/bar.git
```

If already cloned:

```text
$ git submodule update --init --recursive
```

### Remove a submodule

Creating a submodule is pretty straight-forward, but deleting them less so. The commands you need are:

```text
$ git submodule deinit submodulename
$ git rm submodulename
$ git rm --cached submodulename
$ rm -rf .git/modules/submodulename
```

## Miscellaneous Objects

### Restore a deleted file

First find the commit when the file last existed:

```text
$ git rev-list -n 1 HEAD -- filename
```

Then checkout that file:

```text
git checkout deletingcommitid^ -- filename
```

### Delete tag

```text
$ git tag -d <tag_name>
$ git push <remote> :refs/tags/<tag_name>
```

### Recover a deleted tag

If you want to recover a tag that was already deleted, you can do so by following these steps: First, you need to find the unreachable tag:

```text
$ git fsck --unreachable | grep tag
```

Make a note of the tag's hash. Then, restore the deleted tag with following, making use of [`git update-ref`](https://git-scm.com/docs/git-update-ref):

```text
$ git update-ref refs/tags/<tag_name> <hash>
```

Your tag should now have been restored.

### Deleted Patch

If someone has sent you a pull request on GitHub, but then deleted their original fork, you will be unable to clone their repository or to use `git am` as the [.diff, .patch](https://github.com/blog/967-github-secrets) urls become unavailable. But you can checkout the PR itself using [GitHub's special refs](https://gist.github.com/piscisaureus/3342247). To fetch the content of PR\#1 into a new branch called pr\_1:

```text
$ git fetch origin refs/pull/1/head:pr_1
From github.com:foo/bar
 * [new ref]         refs/pull/1/head -> pr_1
```

### Exporting a repository as a Zip file

```text
$ git archive --format zip --output /full/path/to/zipfile.zip master
```

## Tracking Files

### I want to change a file name's capitalization, without changing the contents of the file

```text
(master)$ git mv --force myfile MyFile
```

### I want to overwrite local files when doing a git pull

```text
(master)$ git fetch --all
(master)$ git reset --hard origin/master
```

### I want to remove a file from Git but keep the file

```text
(master)$ git rm --cached log.txt
```

### I want to revert a file to a specific revision

Assuming the hash of the commit you want is c5f567:

```text
(master)$ git checkout c5f567 -- file1/to/restore file2/to/restore
```

If you want to revert to changes made just 1 commit before c5f567, pass the commit hash as c5f567~1:

```text
(master)$ git checkout c5f567~1 -- file1/to/restore file2/to/restore
```

### I want to list changes of a specific file between commits or branches

Assuming you want to compare last commit with file from commit c5f567:

```text
$ git diff HEAD:path_to_file/file c5f567:path_to_file/file
```

Same goes for branches:

```text
$ git diff master:path_to_file/file staging:path_to_file/file
```

## Configuration

### I want to add aliases for some Git commands

On OS X and Linux, your git configuration file is stored in `~/.gitconfig`. I've added some example aliases I use as shortcuts \(and some of my common typos\) in the `[alias]` section as shown below:

```text
[alias]
    a = add
    amend = commit --amend
    c = commit
    ca = commit --amend
    ci = commit -a
    co = checkout
    d = diff
    dc = diff --changed
    ds = diff --staged
    f = fetch
    loll = log --graph --decorate --pretty=oneline --abbrev-commit
    m = merge
    one = log --pretty=oneline
    outstanding = rebase -i @{u}
    s = status
    unpushed = log @{u}
    wc = whatchanged
    wip = rebase -i @{u}
    zap = fetch -p
```

### I want to add an empty directory to my repository

You can’t! Git doesn’t support this, but there’s a hack. You can create a .gitignore file in the directory with the following contents:

```text
 # Ignore everything in this directory
 *
 # Except this file
 !.gitignore
```

Another common convention is to make an empty file in the folder, titled .gitkeep.

```text
$ mkdir mydir
$ touch mydir/.gitkeep
```

You can also name the file as just .keep , in which case the second line above would be `touch mydir/.keep`

### I want to cache a username and password for a repository

You might have a repository that requires authentication. In which case you can cache a username and password so you don't have to enter it on every push / pull. Credential helper can do this for you.

```text
$ git config --global credential.helper cache
# Set git to use the credential memory cache
```

```text
$ git config --global credential.helper 'cache --timeout=3600'
# Set the cache to timeout after 1 hour (setting is in seconds)
```

### I want to make Git ignore permissions and filemode changes

```text
$ git config core.fileMode false
```

If you want to make this the default behaviour for logged-in users, then use:

```text
$ git config --global core.fileMode false
```

### I want to set a global user

To configure user information used across all local repositories, and to set a name that is identifiable for credit when review version history:

```text
$ git config --global user.name “[firstname lastname]”
```

To set an email address that will be associated with each history marker:

```text
git config --global user.email “[valid-email]”
```

### I want to add command line coloring for Git

To set automatic command line coloring for Git for easy reviewing:

```text
$ git config --global color.ui auto
```

## I've no idea what I did wrong

So, you're screwed - you `reset` something, or you merged the wrong branch, or you force pushed and now you can't find your commits. You know, at some point, you were doing alright, and you want to go back to some state you were at.

This is what `git reflog` is for. `reflog` keeps track of any changes to the tip of a branch, even if that tip isn't referenced by a branch or a tag. Basically, every time HEAD changes, a new entry is added to the reflog. This only works for local repositories, sadly, and it only tracks movements \(not changes to a file that weren't recorded anywhere, for instance\).

```text
(master)$ git reflog
0a2e358 HEAD@{0}: reset: moving to HEAD~2
0254ea7 HEAD@{1}: checkout: moving from 2.2 to master
c10f740 HEAD@{2}: checkout: moving from master to 2.2
```

The reflog above shows a checkout from master to the 2.2 branch and back. From there, there's a hard reset to an older commit. The latest activity is represented at the top labeled `HEAD@{0}`.

If it turns out that you accidentally moved back, the reflog will contain the commit master pointed to \(0254ea7\) before you accidentally dropped 2 commits.

```text
$ git reset --hard 0254ea7
```

Using `git reset` it is then possible to change master back to the commit it was before. This provides a safety net in case history was accidentally changed.

\(copied and edited from [Source](https://www.atlassian.com/git/tutorials/rewriting-history/git-reflog)\).

## Other Resources

### Books

* [Pro Git](https://git-scm.com/book/en/v2) - Scott Chacon and Ben Straub's excellent book about Git
* [Git Internals](https://github.com/pluralsight/git-internals-pdf) - Scott Chacon's other excellent book about Git

### Tutorials

* [Atlassian's Git tutorial](https://www.atlassian.com/git/tutorials) Get Git right with tutorials from beginner to advanced.
* [Learn Git branching](https://learngitbranching.js.org/) An interactive web based branching/merging/rebasing tutorial
* [Getting solid at Git rebase vs. merge](https://medium.com/@porteneuve/getting-solid-at-git-rebase-vs-merge-4fa1a48c53aa)
* [git-workflow](https://github.com/asmeurer/git-workflow) - [Aaron Meurer](https://github.com/asmeurer)'s howto on using Git to contribute to open source repositories
* [GitHub as a workflow](https://hugogiraudel.com/2015/08/13/github-as-a-workflow/) - An interesting take on using GitHub as a workflow, particularly with empty PRs
* [Githug](https://github.com/Gazler/githug) - A game to learn more common Git workflows

### Scripts and Tools

* [firstaidgit.io](http://firstaidgit.io/) A searchable selection of the most frequently asked Git questions
* [git-extra-commands](https://github.com/unixorn/git-extra-commands) - a collection of useful extra Git scripts
* [git-extras](https://github.com/tj/git-extras) - GIT utilities -- repo summary, repl, changelog population, author commit percentages and more
* [git-fire](https://github.com/qw3rtman/git-fire) - git-fire is a Git plugin that helps in the event of an emergency by adding all current files, committing, and pushing to a new branch \(to prevent merge conflicts\).
* [git-tips](https://github.com/git-tips/tips) - Small Git tips
* [git-town](https://github.com/Originate/git-town) - Generic, high-level Git workflow support! [http://www.git-town.com](http://www.git-town.com/)

### GUI Clients

You're better off using a CLI client, but if you HAVE to have it pretty, here's a list of GUIs.

* [GitKraken](https://www.gitkraken.com/) - The downright luxurious Git client,for Windows, Mac & Linux
* [git-cola](https://git-cola.github.io/) - another Git client for Windows and OS X
* [GitUp](https://github.com/git-up/GitUp) - A newish GUI that has some very opinionated ways of dealing with Git's complications
* [gitx-dev](https://rowanj.github.io/gitx/) - another graphical Git client for OS X
* [Sourcetree](https://www.sourcetreeapp.com/) - Simplicity meets power in a beautiful and free Git GUI. For Windows and Mac.
* [Tower](https://www.git-tower.com/) - graphical Git client for OS X \(paid\)
* [tig](https://jonas.github.io/tig/) - terminal text-mode interface for Git
* [Magit](https://magit.vc/) - Interface to Git implemented as an Emacs package.
* [GitExtensions](https://github.com/gitextensions/gitextensions) - a shell extension, a Visual Studio 2010-2015 plugin and a standalone Git repository tool.
* [Fork](https://git-fork.com/) - a fast and friendly Git client for Mac \(beta\)
* [gmaster](https://gmaster.io/) - a Git client for Windows that has 3-way merge, analyze refactors, semantic diff and merge \(beta\)
* [gitk](https://git-scm.com/docs/gitk) - a Git client for linux to allow simple view of repo state.

