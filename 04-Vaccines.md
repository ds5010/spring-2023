
# 04-Vaccines

* Review the vaccines project and github-pages site
* Clone the vaccines repo and investigate how it works (end-to-end processing)
* Update the repo and the data products with new data (dig into code and documentation)

## Links

* Polleverywhere: https://PollEv.com/pbogden
* [scratch-notebook.ipynb](https://colab.research.google.com/drive/1CIJAMn73A8ZvxzCgyjN7MGXT0W2BqUTq)

## Reading (for next week)

* TBD

## Homework

* Review solution

## Vaccines

* repo -- https://github.com/ds5010/vaccines
* gh-pages -- https://ds5010.github.io/vaccines
* [vaccines.md](vaccines.md)

## Basic elements

#### README.md

* audience: 6-month rule, collaborators
  * quickstart -- new users with requisite skills
* contents (for us)
  * primary results
  * documentation
* reproducibility -- critically important
  * README.md is the starting point for instructions & requirements
  * instructions should be platform independent (unless you're working privately)
* attribution -- critically important
  * without it, consequences could be worth than plagiarism
  * cite original sources (only)
  * review [iris_dataset.md](iris_dataset.md) -- not covered in first class
* examples
  * [palmerpenguins](https://allisonhorst.github.io/palmerpenguins/) -- dataset
  * Observable [Plot](https://github.com/observablehq/plot) includes API reference docs -- software

#### LICENSE

* [Licensing a repository](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository)
  * github document with links for more detail
* [Introduction to licenses](https://observablehq.com/@observablehq/licenses) -- observable notebook
  * short read with nice overview

#### .gitignore

Don't put these files in version control (and keep them off of github)
```
#File extensions to ignore
*.csv
*.gz

#Mac clean-up
*.ds_store
```
* Note: files already in version control will continue to be tracked
* relevant [sfo exchange](https://stackoverflow.com/questions/1274057/how-do-i-make-git-forget-about-a-file-that-was-tracked-but-is-now-in-gitignore)

#### Makefile

* [make](https://www.gnu.org/software/make/manual/make.html) -- gnu.org
* ideally, the Makefile documents the entire data-processing pipeline
* `.PHONY` -- avoids conflicts when make commands (keywords) are the same file/directory names
* `make` without an argument runs the first keyword in the Makefile

#### data, docs, img, src, tests

* Data is in data
* The github-pages site is in docs
* Figures are in img
* Code is src
* Unit tests are in tests

# vaccines

Get a copy of the vaccines repo, review the workflow, update the result.

### fork or clone?

* Fork if you want your own private copy and don't intend to collaborate directly.
  * In other words, you can choose a different path (fork in the road) and go your own way.
  * Browse to http://github.com/ds5010/vaccines
  * Click on "fork"
  * The GUI automatically offers to create a new fork in your personal account by the same name
  * Just press "Create fork" (green button) and it's done
* Clone if you want to collaborate actively.
  * ...or if it's a repo that was assigned to you by github-classroom.
  * If you're collaborating with others, you'll need to worry about branches, pull requests, etc.
* Community discussions
  * [What's the difference between forking and cloning on github?](https://stackoverflow.com/questions/7057194/what-is-the-difference-between-forking-and-cloning-on-github)
    * Q/A ranks -- 213/123 (highest ranking response isn't checked as the answer)
    * Answer doesn't link to documentation
    * 11 years old and 130k views
    * Reputation 10-100k
  * [Are git forks actually git clones?](https://stackoverflow.com/questions/6286571/are-git-forks-actually-git-clones)
    * Q/A ranks -- 860/967
    * Answer links to documentation and includes an informative figure
    * 11 years old and 300k views
    * Reputation 1k/1m
    * Discussions point to documentation, e.g.:
    * [What happens to forks when a repository is deleted or changes visibility](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/what-happens-to-forks-when-a-repository-is-deleted-or-changes-visibility)
  * [What's the difference between git pull and git fetch?](https://stackoverflow.com/questions/292357/what-is-the-difference-between-git-pull-and-git-fetch?rq=1)
    * Answer links to documentation on git-scm.com
    * Q/A ranks -- 13k/11k
    * 14 years old and 3.3m views
    * Reputation 0.3-1m
  * [How do I delete a git branch locally and remotely?](https://stackoverflow.com/questions/2003505/how-do-i-delete-a-git-branch-locally-and-remotely?rq=1)
    * Q/A ranks -- 20k/25k
    * Answer links to documentation
    * 13 years old and 11m views
    * Reputation 450k -- person who asked it at 1:12 also answered it at 1:13

### clone the repo and get the data

* clone the repo to get an idea of how it works
```
git clone https://github.com/ds5010/vaccines.git
```
* download the data -- figure this out by looking at the Makefile
* curl downloads CSV (as of 16 Sep 2022), which is 395M
* gzip asks if you want to overwrite existing .gz file -- I responded yes
```
make data
make cdc
```
* this creates a gzip data file in data, which is 144M (as of 16 Sep 2022)
* you won't be allowed to push files bigger than 100M to github.com 
* `.gitignore` will ignore new files added to the repo...along with some other things
* BUT -- and this is IMPORTANT -- the pre-existing .gz file is already in the git history, so it won't be .gitignored
* If you update the .gz file and it's bigger than 100M, then you'll have problems.
* You'll be able to commit the change locally, but you won't be able to push to github.
* You'll have to revert the commit, and that's a non-trivial task!
```
#File extensions to ignore
*.csv
*.gz

#Mac clean-up
*.ds_store
```

## In-class exercise

* Recreate the data products
* Update the data products with new data
