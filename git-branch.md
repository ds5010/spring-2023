
# git branch

* Step 1 -- create a branch
```
git branch pbdemo
git checkout pbdemo
```
* Add/edit a file
```
vi test.txt
```
* commit the change
* compare to main
```
git diff main
```
* merge from branch into main
```
git checkout main
git pull origin main
git merge pbdemo
git push origin main
```
* keep branch in sync with main (requires adding a merge message)
```
git checkout main
git pull
git checkout pbdev
git diff main
git merge main
```
* push branch to github (you'll be able to make a pull request)
```
git checkput pbdev
git push origin pbdev
```
* delete remote branch (on origin)
```
git push -d origin pbdemo
```
* delete local branch
```
git checkout main
git branch -D pbdemo
```
