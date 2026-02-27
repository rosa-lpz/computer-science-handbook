# Git
Repository for Git

# Status

```bash
git status
```
# Starting a project


```cmd
git init                        # Initialize a new repo in the current folder
git clone <repo-url>            # Clone an existing repo
```
# Branches

```bash
git branch                      # List branches
git branch <branch-name>        # Create a new branch
git checkout <branch-name>      # Switch to a branch
git checkout -b <branch-name>   # Create and switch to a new branch
git branch -d <branch-name>     # Delete a local branch

# to make sure your local branch has a [remote tracking # branch]
git push -u origin branchname

```

**Clone in an specific branch**

```bash
# Clone the specific branch using git clone with the -b flag
git clone -b branch_name https://github.com/username/repository
```

**Push to a branch created in local**
To push the current branch and set the remote as upstream, use
```bash
git push --set-upstream origin <branch_name>
```

# Git Log

```bash
git log
```

# Add / remove file or folder

```bash
# add file/folder
git add <file_name> or <folder> 

# remove file/folder
git rm <file_name> or <folder> 
```
# Restore

```bash
# to discard changes in working directory
git restore <file>
```



# Commits

## Create commit
```bash
# add file/folder
git commit -m "insert_comment"
```
## Remove a git commit that has not been pushed
I did a `git commit` but I have not pushed it to the repository yet. So when I do `git status`, I get '# Your branch is ahead of 'master' by 1 commit.

So if I want to roll back my top commit, can I just do:

```bash
 git reset --hard 6f1bfa856866809287a95d28a5f6f1a36d8a0201
 git reset --hard HEAD~1
```


Reference
* https://stackoverflow.com/questions/1611215/remove-a-git-commit-which-has-not-been-pushed
## Viewing the Commit History

```bash
git log
```


```bash
git log --pretty="%h - %s" --author='Junio C Hamano' --since="2008-10-01" \
   --before="2008-11-01" --no-merges -- t/
5610e3b - Fix testcase failure when extended attributes are in use
acd3b9e - Enhance hold_lock_file_for_{update,append}() API
f563754 - demonstrate breakage of detached checkout with symbolic link HEAD
d1a43f2 - reset --hard/read-tree --reset -u: remove unmerged new paths
51a94af - Fix "checkout --track -b newbranch" on detached HEAD
b0ad11e - pull: allow "git pull origin $something:$current_branch" into an unborn branch
```

# Push
Push commits to branch

```bash
git push
```


# Tracking Git ignore



## Stop tracking - Using git rm -cached

**File**

```bash
git rm --cached file.zip
git commit -m "Stop tracking data.zip"
git push
```

Now, `data.zip` will be ignored by Git.



**Folder**

```bash
git rm --cached data/
git commit -m "Stop tracking data.zip"
git push
```

Now, `data.zip` will be ignored by Git.



## Stop tracking - Modifying gitignore file

Another effective way to untrack a folder is to modify your `.gitignore` file. This file tells Git which files or folders to ignore when tracking changes. Here’s how to do it:

1. Open or create the `.gitignore` file in the root of your repository.
2. Add the folder name you want to untrack.

```bash
echo "folder_name/" >> .gitignore
```

Output:

```text
folder_name/
```

After adding the folder to the `.gitignore` file, you need to untrack it using the `git rm --cached` command:

```bash
git rm -r --cached folder_name
```

Output:

```text
Unstaged changes after reset:
M   folder_name/file1.txt
D   folder_name/file2.txt
```

By adding the folder to the `.gitignore` file, you ensure that Git will ignore any future changes to that  folder. This is particularly useful for folders that contain temporary  files or build artifacts that you don’t want to include in your version  history.

Once you’ve made these changes, remember to commit your updates:

```bash
git commit -m "Add folder_name to .gitignore and untrack it"
```

This will finalize the untracking process and ensure that your repository remains clean and organized.



https://www.delftstack.com/howto/git/git-untrack-folder/

# User
```bash
git config --global user.email "you@exmaple.com"
git config --global user.name "Your name"
```

# References

* https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History
* https://www.ivanontiveros.com/git-cheat-sheet/
* https://stackoverflow.com/questions/1611215/remove-a-git-commit-which-has-not-been-pushed
* https://www.delftstack.com/howto/git/git-untrack-folder/
