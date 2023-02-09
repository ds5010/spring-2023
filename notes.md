
# hw-vaccines3-solution

## Create the github-classroom assignment

* use the github-classroom invitation link to create a new repo, for me: https://github.com/ds5010/hw2-vaccines3-pbnu
* it took 1-2 minutes to complete (the big gz file) -- it makes an independent copy of ds5010/vaccines-2
* it's not a fork, it's a new repo created from a templte, it's independent of the original

## Step 1 -- clone and clean

* Immediately after cloning the repo, use `git filter-repo` to clean out the .gz file
  * it needs to be removed from the git history, otherwise it won't be ".gitignore"ed
  * the original https://github.com/ds5010/vaccines repo has a copy if you want it (e.g., to verify reproducibility)
```
git clone git@github.com:ds5010/hw2-vaccines3-pbnu.git
cd hw2-vaccines3-pbnu
git filter-repo --invert-paths --path data/COVID-19_Vaccinations_in_the_United_States_County.csv.gz
git status
```
The command `git status` returns...
```
On branch main
nothing to commit, working tree clean
```
* The .gz file is gone
* Note -- I did not create a fork
* Note -- I did not push any changes back to the original github URL
* Class notes on [.gitignore and filter-repo](https://github.com/ds5010/spring-2023/blob/main/git.md#gitignore)
* Reference: [git filter-repo](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository) -- githu.com

## Step 2 -- Reproduce previous results

* Read the Makefile to find out what needs to happen and in what order
```
make clean
make data
make cdc
make vaccines
make deaths
```
* `make data` downloads a CSV that's ~430M, then compresses it with gzip to ~140M
* `make vaccines` takes quite a while to run (couple minutes)
  * `vaccines.py` -- creates intermediate files from cdc data
  * This takes a while, and intermediate printout isn't very informative (just printing dataframe shapes)
  * TODO: Could improve on this by speeding things up and providing a more informative progress message
* continuing...
```
make merge
```
* This command throws an error...
```
FileNotFoundError: [Errno 2] No such file or directory: 'data/JHU/deaths-05-01-2021-to-05-31-2021.csv'
```
* It's looking for a file that should have been created by `make deaths`
* I updated `months.csv` to include "05-01-2021"
* I then tried 
```
make deaths
make merge
```
* Then `make merge` threw an error
```
FileNotFoundError: [Errno 2] No such file or directory: 'data/CDC/vaccinations-05-01-2021.csv'
```
* It's looking for a file that should have been created by `make vaccines`, so I ran
```
make vaccines
make deaths
make merge
```
* These ran to completion without throwing an error, so continuing the pipeline
```
make scatters
make animation
```
* animation.py throws an error -- I need imagio -- there's no requirements.txt
  * I added to my base install: `conda install -c conda-forge imageio`
  * I then shared the environment with this ENV.yml
* For discussion of conda environments, see: https://github.com/ds5010/spring-2023/install.md
```
channels:
  - conda-forge
  - defaults
dependencies:
  - python=3.10
  - pyqt=5.15
  - imageio=2.25
  - pandas=1.5.3
  - matplotlib=3.6.3
```
* Then a deprecation warning in animation.py forced me to change import to: `import imageio.v2 as iio`
  * Note: Deprecation Warning comes with imageio v2.25 (didn't appear with v2.9)
```
DeprecationWarning: Starting with ImageIO v3 the behavior of this function will switch to that of iio.v3.imread. To keep the current behavior (and make this warning disappear) use `import imageio.v2 as imageio` or call `imageio.v2.imread` directly.
  im = iio.imread(f)
```
* So followed the recommendation and changed `animation.py` to import as follows: `import imageio.v2 as iio`
* Then the two final steps run to completion and reproduce original results
```
make animation
make comparison
```

## Step 3 -- Add a couple new dates

* Edit "months.csv" -- this is a configuration file added in vaccines-2 with dates to be used in the analysis
* I added a few months to the original, which ended Nov 2021
```
date
05-01-2021
05-31-2021
06-30-2021
07-31-2021
08-31-2021
09-30-2021
10-31-2021
11-30-2021
12-31-2021
01-31-2022
```
Then upates things (`make cdc` isn't necessary)
```
make vaccines
make deaths
make merge
make scatters
make comparison
```
Everything seems to work fine

## Step 4 -- Add all dates through Jan 2023

* Change `months.csv` to...
```
date
05-01-2021
05-31-2021
06-30-2021
07-31-2021
08-31-2021
09-30-2021
10-31-2021
11-30-2021
12-31-2021
01-31-2022
02-28-2022
03-31-2022
04-30-2022
05-31-2022
06-30-2022
07-31-2022
08-31-2022
09-30-2022
10-31-2022
11-30-2022
12-31-2022
01-31-2023
```
Then `vaccines.py` indicates that some of the dataframes are empty -- no data!?!
```
make vaccines
```
After digging in, seems that missing vaccine data starts 06-30-2022 -- what's going on here?!

## Step 5: What's up with the missing data?

* There's a link to the CDC site, but nothing on the background of what's going on or the data model
* Poking around the CDC site, I found background, data dictionary, etc...
  * https://data.cdc.gov/Vaccinations/COVID-19-Vaccinations-in-the-United-States-County/8xkx-amqh
  * This page has a link to the entire CSV
  * [Data definitions)](https://www.cdc.gov/coronavirus/2019-ncov/vaccines/reporting-vaccinations.html?CDC_AA_refVal=https%3A%2F%2Fwww.cdc.gov%2Fcoronavirus%2F2019-ncov%2Fvaccines%2Fdistributing%2Fabout-vaccine-data.html)
  * Beginning June 2022, reports changed to weekly...https://data.cdc.gov/stories/s/u99h-6e3k
* Inspecting the data -- there seem to be plenty of reports on Wednesdays -- so I switched to last Wed of the month
  * Here's the code I worked with in Colab to perform a little EDA
  * Learning goals: DataFrame.apply(), string manipulation, dates vs strings in pandas
  ```
  def get_month(x, mon='07', year='2022'):
      return (x[0:2] == mon) and (x[6:10] == year)

  df['Date'].apply(get_month).sum()# returns 100k in Jul 2021, 60k in Jun 2022, 13k in Jul 2022
  ```
* Change months.py as follows: Starting Jun 2022, use last Wednesday of the month, starting in June 2022
```
06-29-2022
07-27-2022
08-31-2022
09-28-2022
10-26-2022
11-30-2022
12-28-2022
01-25-2023
```

## Step 6: Update the products

```
make vaccines
make deaths
make merge
make scatters
make animation
make comparison
```
* "make scatters" generates a matplotlib warning about using too much memory
```
python -B src/scatters.py
/Users/pbogden/Sites/ds5010/homework/vaccines3/hw-vaccines3-solution/hw2-vaccines3-pbnu/src/scatters.py:20: 
RuntimeWarning: More than 20 figures have been opened. 
Figures created through the pyplot interface (`matplotlib.pyplot.figure`) are 
retained until explicitly closed and may consume too much memory. 
(To control this warning, see the rcParam `figure.max_open_warning`).
  fig, ax = plt.subplots()
```

## Tasks for hw2-vaccines3

* Fix vaccines.py
* Fix comparison.py (use https://seaborn.pydata.org/generated/seaborn.barplot.html)
