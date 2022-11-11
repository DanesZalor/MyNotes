### git

is a Version Control System
- software designed to record changes made to files over time
- ability to revert back to a previous file version or project version
- compare changes made to files form one version on to another

#### 3 stages of a file
1. **`Commited`** - are files with no change and already in the repo.
2. **`Modified`** - When files are edited they are modified. New files are also `Modified` because it changes the state of the branch. 
3. Staged - Are modified files or changes that are tracked

### 3 states of a Git project
- **.git directory (repository)** 
    - origin of data and is pulled down from the remote server where git stores the metadata and object database for your project.
    - Files in this state are committed and recorded to the project as version snapshots
- Working Directory
    - single copy, aka a *"checkout"* of one version of the project. Pulled from the .git directory. 
    - Files in this state have been modified and added to be staged in the next commit snapshot
- Staging Area 
    - where the changes are stored


## CLI Commands
```
pwd -
cd -
ls -
mkdir -

git config --global // for all git repo in your machine
git config // for only the current
git config --list // print the config
```

## Git repository hosting services
are online servers that offer git repository hosting services (lmao) like git and bitbucket