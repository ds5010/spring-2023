# install

Instructions to set up a Python development environment for data science -- some opinionated recommendations

There are many ways to set things up. If you have something that works, stay with it. These are my choices w/references.

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

VScode is a free visual text editor and an IDE (integrated dev environment) from microsoft.

* https://code.visualstudio.com/download
* it has issues, but they can usually be resolved

## Why miniconda?

* Recommended by Jake VanderPlas, the author of [Python Data Science Handbook (PDS)](https://github.com/jakevdp/PythonDataScienceHandbook/blob/master/notebooks/00.00-Preface.ipynb)
  * [This link](https://jakevdp.github.io/PythonDataScienceHandbook/00.00-preface.html#Installation-Considerations) points to a Jupyter notebook on github, where you'll see a recommendation to use miniconda.
  * It's the first edition of the book, which was updated in 2022.  The more recent edition makes the same recommendation.
* Recommended by Wes McKinney lead developer of Pandas and author or [Python for Data Analysis, 3rd Ed (2022)](https://wesmckinney.com)
  * Section 1.4 of [Python for Data Analysis, 3rd Ed (2022)](https://wesmckinney.com/book/preliminaries.html#installation_and_setup) has the recommendation
* [Conda myths and misconceptions](https://jakevdp.github.io/blog/2016/08/25/conda-myths-and-misconceptions/)
  * This blog post by Jake VanderPlas comparing pip & conda is a bit old (2016) but still interesting/relevant
* Don't use pip. Or at least be careful about it.
  * See: [Using pip in an environment](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#using-pip-in-an-environment) -- conda.io
  * It discusses best practices for using conda and pip
  * Another discussion of [conda and pip](https://www.anaconda.com/blog/understanding-conda-and-pip) -- anaconda.com

## Create an environment that has Python

Create an environment with a specific version of python
```
conda create -n myenv python=3.9
```
Activate the environment and verify
```
conda activate myenv
python --version
```
Deactivate the environment
```
conda deactivate
```

* [Manage environments](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) -- conda.io
  * [Creating an environment with commands](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-with-commands)

## Conda basics

You can use conda to create multiple environments with various installed libraries.

* create a new environment called "myenv" and install the latest seaborn and friends from conda-forge
```
conda create --name myenv
conda activate myenv
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

* [conda docs](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)
* [conda cheatsheet](https://docs.conda.io/projects/conda/en/latest/_downloads/843d9e0198f2a193a3484886fa28163c/conda-cheatsheet.pdf)

## Remove an environment

```
conda remove --name myenv --all
```

* [Remove an environment](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#removing-an-environment) -- conda.io

## Share an environment

If you're using special software, or you need a specific version, then use 
[conda](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) 
and provide instructions with an `environment.yml` file.
I created an environment.yml for this repo by first running this command
```
conda env export > environment.yml
```
Then I used the `--from-history` option to get hints on editing/trimming the file into something nice and short.
```
conda env export --from-history
```
I settled on this for my environment.yml...
```
channels:
  - conda-forge
  - defaults
dependencies:
  - seaborn=0.11.2
  - pyqt
```
Ref: [Sharing an environment](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#sharing-an-environment)

## Create an environment from a yml file

You can create an environment from a .yml file as follows:
```
conda env create --name myenv -f environment.yml
```
Remove an environment with:
```
conda env remove --name myenv
```
* Ref: [Creating an environment from an enviroment.yml file](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file) -- conda.io

## channels -- conda vs conda-forge

* geospatial software has dependencies that can cause problems if you mix channels
* see: [geopandas install](https://geopandas.org/en/stable/getting_started/install.html)
* see also: [using multiple channels](https://conda-forge.org/docs/user/tipsandtricks.html#using-multiple-channels)
* I use conda-forge, and this is an ENV.yml created from my base install...
```
$ conda env export --from-history>ENV.yml
$ cat ENV.yml
name: base
channels:
  - conda-forge
  - defaults
dependencies:
  - python=3.10
  - conda==22.11.1
  - setuptools
  - pip
  - wheel
  - conda-content-trust
  - python.app
  - geopandas
  - contextily
  - pyqt
prefix: /Users/pbogden/miniconda3
```

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
    * Download the installer for your architecture (I had to use the nonstandard "Miniconda Linux-aarch64 64-bit")
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
  * Be patient! Don't just hit return or you may respond incorrectly to the prompts...
  * Follow the instructions and accept all the defaults, including default activation
  * When it's done, you can verify that you have python with...
  ```
  which python
  ```
  this command should return something like `/home/yourname/miniconda3/bin/python`
  * Verify that it works with
  ```
  python --version
  ```
  which should return something like `Python 3.9.12`

## My experience on a mac

* For my old Intel Mac, I downloaded "Miniconda3 macOS Intel x86 64-bit bash"
* Checked the hash with `shasum -a 256 ~/Downloads/Miniconda3-latest-MacOSX-x86_64.sh`
* Followed the regular installation [here](https://conda.io/projects/conda/en/stable/user-guide/install/macos.html)
* With the command: `bash Miniconda3-latest-MacOSX-x86_64.sh`
  * When prompted with the following question:
  ```
  Do you wish the installer to initialize Miniconda3
  by running conda init? [yes|no]
  ```
  * I responded with "yes" -- don't get impatient, because the default response is no
* I opened a new terminal shell and my prompt began with "(base)" -- so the base environment was running
* And I had python installed. `which python` returns `/Users/pbogden/miniconda3/bin/python`
* And `python --version` returns `Python 3.10.8`

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

* Problem: My terminal would occasionally hang on my laptop using an old version of the MacOS
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

### seaborn issue

I encountered an issue on my older Mac.
For some reason (python not installed as a framework?), plt.show() with seaborn hangs my terminal.
Fix this by turning off interactive mode:
```
plt.ioff()
```
You can also fix this by using a different backend:
```
matplotlib.use('TkAgg')
```
List all the backends and the current backend with:
```
print(plt.get_backend())
print(matplotlib.rcsetup.all_backends)
```
Or, to avoid using matplotlib, add the following to `~/.zprofile`:
```
# Avoids seaborn hang on my old macbook pro
export MPLBACKEND=qtagg
```
