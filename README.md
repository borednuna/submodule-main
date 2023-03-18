# submodule-main

Demo repository for submodule project. This is a workspace that contains submodules of repositores I've made as college projects.

## Starting with submodules
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

Git sees your submodules as a commit of the main repository so it doesn't track the contents when you're not in that submodule directory. The ```.git``` file in the submodule will contain this information :
```
gitdir: ../.git/modules/<submodule-repository-name>
```
