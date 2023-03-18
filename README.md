# submodule-main

Demo repository for submodule project. This is a workspace that contains submodules of repositores I've made as college projects. I have simplified the git documentation so you don't have to stare at the eye-sickening bright-themed documentation page. Thank me later~

## Creating a Repository With Submodules
To clone a repository as a submodule
```
git submodule add <repository-url>
```
For example,
```
git submodule add git@github.com:borednuna/CashierAppC.git

or

git submodule add https://github.com/borednuna/CashierAppC.git
```
After cloning a submodule, your root project will have a ```.gitmodule``` file contains informations about submodules inside the repository like these:
```
[submodule "CashierAppC"]
        path = CashierAppC
        url = git@github.com:borednuna/CashierAppC.git
[submodule "repository-name"]
        path = <repository-path>
        url = <repository-url>
...
```
Git sees your submodules as a commit of the main repository so it doesn't track the contents when you're not in that submodule directory.

To save the cloned repositories as submodules, push them to the main repository.
```
git add -A
git commit -m "feat: add submodule using git ssh"
git push
```

## Cloning A Repository with Submodules
To clone a repository with submodules, you can clone it like a common repositoy using
```
git clone <repository-url>
```
For example,
```
git clone git@github.com:borednuna/submodule-main.git
```
When the repository is cloned, the submodules directories will be empty. You will have to enter these commands.
```
git submodule init
```
That command will initialize your local configuration file. Then,
```
git submodule update
```
That command will fetch all the data of the submodules and checkout the appropriate commit of the submodule in the main repository.

Another way of cloning a repository with submodules is using the ```--recurse-submodules``` flag just like this.
```
git clone --recurse-submodules <repository-url>
```
For example,
```
git clone --recurse-submodules git@github.com:borednuna/submodule-main.git
```

## Working On Repositories With Submodules
### Pulling in Upstream Changes from Remote Repository
To pull changes made from the remote repository of the submodule directory,
```
cd <submodule-directory>
git fetch
```
then
```
git merge origin/master
```
or
```
git pull
```
You can also fetch the changes of a submodule from the root directory of the main repository using:
```
git submodule update --remote <submodule-directory>
```
To pull __all__ changes from all existing submodules' remote repository, you can just enter this command:
```
git submodule update --remote
```

Those commands works in the scope of the submodule directory so it's not aware of the changes made in the scope of the main repository. For example, it doesn't know if there is a new submodule added in the main repository. To fetch and sync all changes in the main repository,
```
git submodule update --init --recursive
```
The ```--init``` flag will help your local repository pull in case a new submodule is added in the remote repository. The ```--recursive``` flag helps updating recursively in case your submodule has submodules.

Another way of update submodules in your main repository is to use ```--recurse-submodules``` flag with ```git pull```. But this command will likely fail if the remote repository has changed its submodule url. So the best practice is to use
```
# copy the new URL to your local config
$ git submodule sync --recursive
# update the submodule from the new URL
$ git submodule update --init --recursive
```

### Publishing Local Changes to Remote Repository
The easiest way of publishing local changes to the remote repository is:
```
git push --recurse-submodules=on-demand
```
The ```--recurse-submodules``` flag will take an argument on how you want to push the changes. The ```on-demand``` argument will make git push the changes to the remote repository of the __submodule__ first before pushing it to the main repository. If somehow the pushing process in the submodule fails, git will cancel pushing to the main repository.

Another way of pushing changes in submodule is using the ```check``` argument. Git will push the changes directly to the main repository. It will fail if the changes hasn't been pushed to the submodule remote repository so you'll have to manually push the changes to the submodule remote first using ```git push``` in the submodule directory.

## Reference
[Git Documentation Page](https://git-scm.com/book/en/v2/Git-Tools-Submodules)