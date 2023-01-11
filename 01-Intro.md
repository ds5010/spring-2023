
# 01 -- Intro

## Goals for today

* Introductions
* Course overview
* Colab intro

## Links

* [01-Intro.ipynb](https://colab.research.google.com/drive/1OPNRI-kujEq1SpU4J9CZfFyHF9lVjk18)
  * We'll start next week by working on the exercise in this notebook...
* Polleverywhere: https://PollEv.com/pbogden
* [Scratch notebook](https://colab.research.google.com/drive/1CIJAMn73A8ZvxzCgyjN7MGXT0W2BqUTq)

## Intros

## Syllabus

* Syllabus (in Canvas) -- review the content in detail

## Colab

* Colab access (authenticate using your husky.neu.edu email)

## Student responsibilities (for next week)

Make sure you have your local environment set up...

* python & miniconda -- the latest release installed locally (look at Section 1.4 of McKinney)
* text editor -- vscode or others (e.g., vim) -- not atom, which is deprecated as of summer 2022:-(
* Command line (terminal/REPL=read-eval-print-loop) -- make sure you can run code from the command line
  * Note: [vscode + vim](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim) works well
* [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) -- install command-line git

## Reading (for next week)

* [Python for Data Analysis, 3rd Ed](https://wesmckinney.com/book/) (2022) by Wes McKinney
  * [Chapter 1, Preminaries](https://wesmckinney.com/book/preliminaries.html)
    * This is important
    * You should follow the instructions for installing a Python environment with miniconda
* [How to ask a good question](https://stackoverflow.com/help/how-to-ask) -- stackoverflow.com
  * This was mentioned in class -- it's here as a reference

## Looking ahead

Next week we'll be using...

* [built-in functions](https://docs.python.org/3/library/functions.html),
* [I/O methods](https://docs.python.org/3/tutorial/inputoutput.html)
* [string methods](https://docs.python.org/3/library/stdtypes.html)
* [matplotlib](https://matplotlib.org/)

## Reading (looking ahead)

* There's a lot of content and a lot of detail. Some or all of it may be review.
  * We'll be applying techniques described in these references.
  * Open Colab (or a Jupyter notebook) to practice working with examples if it's new or if you want a refesher.
* [Chapter 2. Python language basics, ipython & jupyter](https://wesmckinney.com/book/python-basics.html)
  * This chapter has a lot of detail.
* [Chapter 3. Built-in data structures, functions and files](https://wesmckinney.com/book/python-basics.html)
  * We'll be applying techniques in this chapter.
* [Whirlwind Tour of Python](https://jakevdp.github.io/WhirlwindTourOfPython/) (2016) by Jake VanderPlas
  * This is a collection of notebooks on github that you can execute in Colab or Jupyter.
  * This is optional reading that you may find helpful -- much of if may be review, but it's still a good reference.

## Projects

* http://ds5010.github.io/vaccines
* http://ds5010.github.io/broadband
* git & github for version control and collaboration
* branches/pull requests/merging for communication & development (later this semester)
* project management -- planning and modularizing (a key to success)
* communication/documentation for 2 audiences:
  * developers (6-month rule)
  * stakeholders/general public (gh-pages)

## Attribution

* [Northeastern academic integrity policy](https://osccr.sites.northeastern.edu/academic-integrity-policy/)
  * Copy and paste could have legal implications that extend beyond academic integrity (unlikely for us right now).
* [Introduction to licenses](https://observablehq.com/@observablehq/licenses) -- observablehq.com
  * reusing published work, attribution, copyright
* [CapitalOne perspective](https://www.capitalone.com/tech/open-source/open-source-licenses-explained-2021/)
  * An open source lawyer explains code use under various open source licenses

## Iris dataset

* [iris_dataset.md](iris_dataset.md)

## In-class exercise -- colab intro

* Colab -- https://colab.research.google.com/
  * Colab is Jupyter as a service, with GUI improvements & GPU access (and an underlying business model)
  * Authenticate with your husky.neu.edu
  * Colab and jupyter are for prototyping and in-class exercises, but NOT for code submission.
  * You can share Jupyter notebooks, but editing is not synchronous.  You need to "save" explicitly.
* Verify that students can access their github accounts
  * Show how to "share" a notebook with someone else
  * Practice with markdown and tex
* Accessing the iris dataset
  * Look here: https://github.com/mwaskom/seaborn-data/blob/master/iris.csv
  * Use the "raw" link
  * `!curl -O "https://raw.githubusercontent.com/mwaskom/seaborn-data/master/iris.csv"`
* [colab.md](colab.md) -- look here for additional hints on using colab
