# Github Guide

## How to make a fork of an existing repo
If you are going to create a new feature, the approach is to fork the repository and create a branch that is for a single feature.
Create a fork of the project on github. Check under settings to make sure that the name of the main branch is set to main and not master

Clone fork locally with the following:
``` git clone <repo-url> ```

You then want to checkout the branch for the feature as follows. The convention is to name branches after a feature:
``` git checkout -b <branch-name> ```
Note: The "-b" flag generates a new branch. If you want to switch between branches in the future use git checkout <branch-name>

Now that you've created your branch, you can set it as the upstream origin, which pushes the change to github:
``` git push --set-upstream origin <branch-name> ```

Next, you want to bring in the base repository as a remote, to do this you do the following. Here by convention we set the local name for the name branch as "base":
``` git remote add base <original-repo-url> ```

Now if you need to update your branch with changes on the base repository you can type:
``` git fetch base ```
``` git rebase base/main ```

Now you want to bring a feature to main
If you have not already, install github CLI: 
​
Create a pull request by typing: GH PR Create
You can also use GH PR Create -d to share your code as a draft pull request (PR) with other people so they can review.
Potential Issues
If you have a conflict between your local branch and the master branch and you just want to reset your local branch to master branch do the following:
git rebase <local-name-for-main-branch>/main
If you get things really messed up type the following:
git reset --hard HEAD
git checkout <your-branch-name>
GH Workflows
Clone the root repository
Create a fork for yourself
add root repository as an additional remote
when you want to work on a feature bring main branch up to date (from upstream) and then create a local branch on that and then type GH PR Create.
GH PR Create




## Merging branches on two different forks

Start by cloning the first repo that you want to merge:<br>
``` git clone -o staging http://staging ```

This clones your staging repository. You will need to replace "http://staging" with the correct URL to your Staging/Support repository. You might also want to give a path where to clone the repository as another parameter. The parameter -o makes sure the remote repository is called "staging" which helps to distinguish it from the project repositories later on.

Next step is to add the remote repository to merge from (in this case "Sample Project 2")

``` git remote add project2 http://sampleproject2 ```

Again, replace "http://sampleproject2" with the URL of the repository "Sample Project 2". You can also change "project2", which is the name of the remote repository, to better fit your project.

After this type

``` git remote update ```

After doing that, git branch -r will show the branches from both staging and project2, like this:

$ git branch -r<br>
staging/Production<br>
staging/UAT<br>
project2/Master<br>
project2/QA<br>
project2/DEV<br>

Next checkout the branch you want to merge to, like this:

``` git checkout -b staging_UAT --track staging/UAT ```

This creates a new local branch called staging_UAT which tracks the remote branch UAT from the staging repository. The new branch will be checked out immediately.

Now you have a copy of the UAT branch from staging checked out. You can merge in the changes from project2:

``` git merge project2/Master ```

Now all changes from the branch Master of project2 are merged into the current branch (which is staging_UAT). You might want to have a look at git log to see the result. If it fits your expecations, you can push it to the Staging repository:

``` git push staging staging_UAT:UAT ```

Doing this you push the current state of your local branch staging_UAT to the branch UAT in the remote repository called staging.

You can handle the other projects equally and also add a branch like staging_Production to merge your changes into the Production branch of Staging.
