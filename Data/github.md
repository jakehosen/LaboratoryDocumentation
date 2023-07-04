# Github Guide

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
