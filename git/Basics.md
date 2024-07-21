# Git basics
- Version control system
- Versioning system
- [Reference](https://git-scm.com/docs)
- Git is not delta based. At every commit or state changes, a snapshot of the files will be done.
- Everything is checksummend in Git and be then refered by this checksum.
- working copy $\hat{=}$ checkout
- A file can have 3 main states:
  - **Modified** means that you have changed the file but have not committed it to your database yet.
  - **Staged** means that you have marked a modified file in its current version to go into your next commit snapshot.
  - **Committed** means that the data is safely stored in your local database.

~~~mermaid
sequenceDiagram
    participant W as Working directory <br> (Working tree)
    participant S as Staging area(index)
    participant L as Local repository(.git)
    L ->> W: checkout
    W ->> S: add
    S ->> L: commit
~~~

## Initialisation
### installation
~~~
sudo apt install git
git --version
~~~
### track folder
In the folder to be tracked(working directory). <br>
Create `.git` file:
~~~
git init
~~~
### settings
Show all information:
~~~
git config --list --show-origin
~~~
Set personal information:
~~~
git config [scope] user.name "<name>"
git config [scope] user.email "<email>"
~~~
scope:
- --global &rarr; ~/.gitconfig
- --local &rarr; .git/config (default)
- --system &rarr; /etc/gitconfig

## Files status
Show status of the files:
~~~
git status
~~~
A file can have one of four different status:
- **untracked**: files in the working directory that were not in the last snapshot and are not in the staging area.
- **unmodified**: tracked files that match those in the repository.
- **modified**: tracked files that doesnt math those in the repository.
- **staged**: files that are added to the staging area(Changes to be committed).
~~~mermaid
sequenceDiagram
    participant UT as untracked
    participant UM as unmodified
    participant M as modified
    participant S as staged
    UT ->> S: add the file
    UM ->> M: edit the file
    M ->> S: stage the file
    UM ->> UT: remove the file
    S ->> UM: commit
~~~
