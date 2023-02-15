
# vaccines-3 setup

Setting up to collaborat on [vaccines-3](https://github.com/ds5010/vaccines-3) with pull requests

### Clone and clean the vaccines-3 repo

```
git clone git@github.com:ds5010/vaccines-3.git
cd vaccines-3
git filter-repo --invert-paths --path data/COVID-19_Vaccinations_in_the_United_States_County.csv.gz
```
* git filter-repo rewrites history -- and removes origin configuration to force you to think about it!
  * [git issues discussion](https://github.com/newren/git-filter-repo/issues/46) has links to more docs
* So I need to reset origin (locally) to the original repo on github.com
```
git remote add origin git@github.com:ds5010/vaccines-3.git
```
Push all the changes to origin -- warning: this is a destructive "force" push!
```
git push origin --force --all
```
Reset the upstream for the local main branch main on origin
```
git branch --set-upstream-to=origin/main main
```
Note: I previously removed all the branches with the following sequence...
```
# Delete all local branches except main
git branch | grep -v main | xargs git branch -D
# Delete all remote branches on origin except main
git branch -r | awk -F/ '/origin/{print $2}' | grep -v main | xargs git push -d origin
```
* Note: I've configured things so updates to origin/main now require a pull request!
* Ref: [Managing a branch-protection rule](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/defining-the-mergeability-of-pull-requests/managing-a-branch-protection-rule) -- github.com

## To revert to previous commit

For example, say you accidentally committed on the local main branch, by-passing pull request on main
```
git reset --hard 0d1d7fc32
```
or, to revert one commit
```
git reset --hard HEAD~1
```

## Collaborating with pull requests

Workflow example: [git-demo.md](https://github.com/ds5010/spring-2023/blob/main/git-branch.md)
