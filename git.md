
# git

An opinionated set of references.

## general

"I really never wanted to do source control management at all and felt that it was just about the least interesting thing in the computing world (with the possible exception of databases ;^), and I hated all SCM’s with a passion." -- Linus Torvalds, creator of git

* [git book, 2nd edition](https://git-scm.com/book/en/v2) -- git-scm.com
* [about git](https://git-scm.com/about) -- branching
* [an interview with Linus Torvalds](https://www.linuxfoundation.org/blog/blog/10-years-of-git-an-interview-with-git-creator-linus-torvalds/)

## install

* If you have a mac, you may already have a version of git in `/usr/bin/git` that works with mac's keychain.
* You can also [install git from conda-forge](https://anaconda.org/conda-forge/git)
  * I've started using this approach, but note that this version of git doesn't work with the keychain.
* Official ref: [1.4 Getting Started -- The Command Line](https://git-scm.com/book/en/v2/Getting-Started-The-Command-Line)
  * Other install options: [1.5 Installing git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) -- git-scm.com

## authenticating

* [Authentication on github](https://docs.github.com/en/authentication) -- github.com
  * In addition to using git, we'll use github. There are other services out there that use git.
  * Note: github is not git -- github uses git. So beware of becoming dependent on proprietary github stuff.
  * You have several options for authenticating on github.
  * I've used personal access tokens and stored passwords in the Mac keychain with `/usr/bin/git`
  * I've also used SSH.
* [generating ssh keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) -- github.com
  * this link has instructions for creating ssh keys
  * You can install open ssh with conda: `conda install -c conda-forge openssh` 
* HTTPS or SSH?
  ```
  git remote -v
  ```
  * [switching from https to ssh](https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories#switching-remote-urls-from-https-to-ssh) -- github.com

## tutorials

These tutorials are extensive. Some describe advanced usage of git and github that we'll use later in the course.

* [github starter course](https://github.com/education/github-starter-course)
* [atlassian git tutorials](https://www.atlassian.com/git) -- atlassian.com
  * These folks have some very good tutorials
  * [Beginner guide](https://www.atlassian.com/git/tutorials/what-is-version-control)
  * [Setting up a repository](https://www.atlassian.com/git/tutorials/setting-up-a-repository) -- pretty good
  * [Collaborating](https://www.atlassian.com/git/tutorials/syncing) -- later in the course
* [github cli](https://docs.github.com/en/github-cli) -- github.com
  * This -- the github CLI -- is NOT the same as "git" (I don't use it)

## cloning a repo

If you're authenticaing with personal access tokens, then cloning with HTTPS looks something like this...

```
$ git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
```

If you're authenticating with SSH then there's an alternate URL that looks like this...

```
$ git clone git@github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
```

Reference: [Clone a repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) -- github.com

## making changes

It's a good idea to make sure you're up to date with origin before you make local changes.
```
$ git pull
```
After you make a change in to your local repository, check to see what you changed
```
$ git status
```
Stage some or all of the changes (`git add .` stages all of them)
```
$ git add .
```
Then commit the staged changes with a message
```
$ git commit -m "I made a small but super-important change to such and such."
```
Verify things (you can do this a lot -- it's just a sanity check)
```
$ git status
```

References:

* [git tutorial](https://git-scm.com/docs/gittutorial/2.8.6) -- git-scm.com
* [about commits](https://docs.github.com/en/pull-requests/committing-changes-to-your-project/creating-and-editing-commits/about-commits) -- github.com

## .gitignore

List files and directories that you want to keep out of git in a `.gitignore` file.

If you forget to `.gitignore` a file and you want to remove it from git history, then it's a bit of a pain...

```
git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY
cd YOUR-REPOSITORY
git filter-repo --invert-paths --path PATH-TO-YOUR-FILE
git push origin --force --all
git push origin --force --tags
```

References:

* [To remove a file from a git history](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)
* [`git filter-repo` is recommended by the git community](https://git-scm.com/docs/git-filter-branch#_warning) -- git-scm.com
  * [it requires Python 3.5+ and git 2.22+](https://github.com/newren/git-filter-repo#prerequisites)
* Note: `git filter-repo` can be installed with `conda install -c conda-forge git-filter-repo`

## update github 

You can update the main branch on github by pushing to "origin main", **but** use pull requests if you're collaborating.

* If you've made a change, then check to see what you'll be committing
  ```
  git status
  ```
* Commit the changes locally
  ```
  $ git add .
  $ git commit -m "I've made a such-and-such a change"  
  $ git push origin main
  ```
  * Note: `git add .` will stage everything that changed, which may not be a good idea.

## reviewing things

To review the commit history
```
$ git log 
```
To checkout a previous commit
```
$ get checkout <tag/branch/commit id>
```
You can reset to a previous commit (but you'll lose everything you did since then!!)
```
$ get reset --hard <tag/branch/commit id>
```
Warning: `git reset` can get complicated quickly. That's one reason `git filter-repo` was created.

Reference: [git-reset](https://git-scm.com/docs/git-reset) -- git-scm.com

## accidental commits

* Common use case: You accidently commit a large data file or a file with sensitive info before you `.gitignore` it.
* There are [several recommended ways to deal with this problem.](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository) -- github.com
  * I use `git filter-repo`
  * You can [install git-filter-repo with conda from conda-forge](https://anaconda.org/conda-forge/git-filter-repo)
* Of course, the best way to deal with accidental commits is to [avoid them](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository) -- github.com

## branches

Branches allow you to develop outside the `main` branch.  This is good for experimenting and collaborating.

List branches, including current branch (which is preceded by an asterisk)
```
git branch
```
* default branch is usually "main", sometimes for older repos it's "master"
* if you haven't created any branches, that'll be the only one

Create a new branch called demo
```
git branch demo
```

Checkout the "demo" branch
```
git checkout demo
```

To merge changes made in a branch (an oversimplified example)
```
git checkout demo
...make changes...
git add .
git commit -m "I made some wicked cool changes that are ready to merge into the main branch"
git checkout main
git merge demo
```
* You need to specify the upstream for the branch before you can "push" or "pull"

References: 

* [git branch](https://git-scm.com/docs/git-branch) -- git-scm.com
* [Git branching](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging) -- git-scm.com
* [About branches](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-branches)
* [Working with branches](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-branches#working-with-branches)

## pull requests

[Creating a pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request) -- github.com
