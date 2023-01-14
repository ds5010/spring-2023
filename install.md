# Install

Setting up a Python development environment for data science -- some opinionated recommendations

There are many ways to set things up. These are my choices along with some references.

## 1. Install miniconda

Install miniconda on some version of Linux.

* Miniconda is a minimal distribution of Python and friends, and it includes conda
  * conda is the package manager that comes with miniconda
  * conda also comes with anaconda -- anaconda is a distribution
  * you can install miniconda or anaconda, the references below mention the differences
* If you have Mac or you're using Linux on a PC then you're in good shape.
* If you're using Windows, then consider first installing WSL, Windows Subsystem for Linux (see below).
* Ref: [miniconda](https://docs.conda.io/projects/conda/en/stable/user-guide/install/index.html)

## 2. Install vscode

This is a visual text editor (for starters) and an IDE (integrated dev environment) with some configuration

* https://code.visualstudio.com/download

## Why miniconda?

* Preface of [Python Data Science Handbook](https://github.com/jakevdp/PythonDataScienceHandbook/blob/master/notebooks/00.00-Preface.ipynb) by Jake VanderPlas
  * This link points to a Jupyter notebook on github, where you'll see a recommendation to use miniconda.
  * The entire 1st edition (published in 2017) is available as Jupyter notebooks in this github repo.
  * The 2nd edition (published in Dec 2022) has been modernized, but it's not freely available.
  * In my opinion, the freely available github notebooks are still the preferred the way to go. Changes aren't big.
* Section 1.4 of [Python for Data Analysis, 3rd Ed (2022)](https://wesmckinney.com/book/preliminaries.html#installation_and_setup) by Wes McKinney
  * The author of Pandas also recommends miniconda
* [Conda myths and misconceptions](https://jakevdp.github.io/blog/2016/08/25/conda-myths-and-misconceptions/)
  * This blog post by Jake VanderPlas comparing pip & conda is a bit old (2016) but still interesting/relevant
* [using pip in an environment](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#using-pip-in-an-environment) -- conda.io
  * best practices for using conda and pip
* [managing conda environments](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) -- conda.io
* [conda and pip](https://www.anaconda.com/blog/understanding-conda-and-pip) -- anaconda.com

## conda basics

You can use conda to create multiple environments with various installed libraries.

* create a new environment called "myenv" and install the latest seaborn and friends from conda-forge
```
conda create --name myenv
conda install -c conda-forge seaborn
conda install -c conda-forge python
conda install -c conda-forge pandas
conda install -c conda-forge matplotlib
conda install -c conda-forge 
```

* deactivate an environment
```
conda deactivate
```

* activate the "myenv" environment
```
conda activate myenv
```

* list all environments
```
conda env list
```

* create a new environment called "newenv" from requirements.txt
```
conda create --name newenv --file requirements.txt --channel conda-forge
conda activate newenv
```

* save an environment to ENV.yml
```
conda env export --from-history>ENV.yml
```

* [conda docs](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)
* [conda cheatsheet](https://docs.conda.io/projects/conda/en/latest/_downloads/843d9e0198f2a193a3484886fa28163c/conda-cheatsheet.pdf)

## WSL

Detailed instructions for installing WSL and some other useful things...

* [Install WSL](https://learn.microsoft.com/en-us/windows/wsl/install)
  * Very easy. Open powershell/command prompt (windows jargon for the built-in terminal)
  ```
  wsl --install
  ```
* Verify that you're using Linux...
  ```
  which curl
  ```
  should return: `/usr/bin/curl`
* Install make
  ```
  sudo apt-get install make
  ```
  Verify that it worked...
  ```
  which make
  ```
  should return: `/usr/bin/make`
* Enable copy/paste into the terminal from the clipboard
  * [Copy and Paste Arrives for Linux/WSL Consoles](https://devblogs.microsoft.com/commandline/copy-and-paste-arrives-for-linuxwsl-consoles/) -- microsoft.com
* Install miniconda
  * Use the directions for [Installing on Linux](https://docs.conda.io/projects/conda/en/stable/user-guide/install/linux.html)
  * Download the miniconda installer
    * Go to: https://docs.conda.io/en/latest/miniconda.html
    * Download the installer for your architecture (I used the nonstandard "Miniconda Linux-aarch64 64-bit")
    * The browser will download the file to your windows C drive
* Where's the C drive?
  * The C drive is available in Linux as `/mnt/c`
* Use the built-in Linux `sha256sum` command for [cryptographic hash verification](https://docs.conda.io/projects/conda/en/stable/user-guide/install/download.html#cryptographic-hash-verification)
  * On the command line, it'll be something like...
  ```
  sha256sum /mnt/c/Documents\ and\ Settings/your.name/Downloads/Miniconda3-latest-Linux-X86_64.sh
  ```
* Install miniconda from the command line with something like...
  ```
  bash /mnt/c/Documents\ and\ Settings/your.name/Downloads/Miniconda3-latest-Linux-X86_64.sh
  ```
  * Follow the instructions and accept all the defaults, including default activation
  * When it's done, you can verify that you have python with...
  ```
  which python
  ```
  which should return something like `/home/yourname/miniconda3/bin/python`
  * Verify that it works with
  ```
  python --version
  ```
  which should return something like `Python 3.9.12`

## vscode terminal on Mac

* The problem: vscode's integrated terminal wasn't using my conda environment
  * Why? Because Microsoft still doesn't play real well with Mac
* The solution:
  * In vscode, navigate to `code->preference->setting->Features->Terminal->Integrated>Env:Osx` 
  * Choose `edit in settings.json`
  * Add the following
```
"terminal.integrated.env.osx": {  
          "PATH": null
 }
```
* Restart vscode (e.g., from the command line: `vscode .`)
  * Then `which python` will point to python in the conda environment
* Ref: [sfo hint](https://stackoverflow.com/questions/72908232/vs-code-terminal-not-recognising-conda-environment)

## matplotlib on an old Mac

* Problem: My terminal would occasionally on my laptop using an old version of the MacOS
* Solution: Add the following to `~/.zprofile` to avoid a hang with default backend

```
# Avoids matplotlib hang on my old macbook pro
export MPLBACKEND=qtagg
```
Or you can put the following in your code
```
# This uses a different backend (needed for my old Mac, so it doesn't hang on the command line)
import matplotlib
matplotlib.use('QtAgg')
matplotlib.use('TkAgg')
```

* [matplotlib backends](https://matplotlib.org/stable/users/explain/backends.html)
