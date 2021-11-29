
#### Exercise 2

- Complete Exercise 1
- Type `git status`
	```
	On branch master
	
	nothing to commit, working tree clean
	```
- Observe the first line `On branch master` 
- Type `git branch`
	```
	* master
	```
	You have only one branch and it is called `master`. GitHub has switched the initial branch's name to `main`
- Suppose that we need to add two groups of changes to our software.

	**A Changes**
	```
	1. add new functionality in a new file. Let's say FileWithAChanges
	2. add a line in the `file` to show that you made changes in the software. 
	   Suppose that the `file` has the functionality of a change log. 
	   For example, add a third line "Added A functionality file"
	```
	**B Changes**
	```
	1. add new functionality in a new file. Let's say FileWithBChanges
	2. add a line in the `file` to show that you made changes in the software. 
	   Suppose that the `file` has the functionality of a change log. 
	   For example, add a third line "Added B functionality file"
	```
	We are going to assign these two tasks in two developers and they are going to work in parallel at the same project. Let's see how this problem can be simplified with git.
- The idea is to create two *"copies"* of the software that you already have and start applying the changes without losing the initial version or the changes from the two developers.
- Let's create one branch for the A Changes -> `git branch a-changes` 
- Now `git branch`
	```
	  a-changes
	* master
	```
	You have created the first branch.
- Let's navigate to the new branch -> `git checkout a-changes`
	```
	Switched to branch 'a-changes'
	```
-  Now `git branch`
	```
	* a-changes
	  master
	```
	You have moved to the new branch `a-changes`
-  Implement your changes. Add a new file named `FileWithAChanges`  with any content.
- Use `git status`
	```
	On branch a-changes
	Untracked files:
	  (use "git add <file>..." to include in what will be committed)

		FileWithAChanges

	nothing added to commit but untracked files present (use "git add" to track)
	```
- Start tracking the new file and commit. Commit message should be descriptive (e.g. "added A changes file")
- Let's observe the graph -> `git log  --oneline --graph --decorate`
	```
	* 2682a75 (HEAD -> a-changes) added A changes file
	* 489be22 (master) my second commit
	* 191fb85 my first commit
	```
	A third commit has been added but the `master` branch is at the second commit.
- Let's add in `file` the change that we just implemented. Open `file` and add a third line  "Added A functionality file".
- Add your changes and commit them. Commit message should always be descriptive (e.g. "added change log line in 'file'"
- Let's observe the graph -> `git log  --oneline --graph --decorate`
	```
	* 19f0265 (HEAD -> a-changes) added change log line in 'file'
	* 2682a75 added A changes file
	* 489be22 (master) my second commit
	* 191fb85 my first commit
	```
	A fourth commit has been added. `master` has not changed at all. The commit has been added on the `a-changes` branch
- We have completed **A changes**. Let's go to `master` again to see what is going on.
- Observe the contents of the project folder.
- Now use `git checkout master` and observe again the contents of the project folder.
- `FileWithAChanges` disappeared and if you open the `file` , you'll see that the third line is no longer there.
- Now `git log  --oneline --graph --decorate`
	```
	* 489be22 (HEAD -> master) my second commit
	* 191fb85 my first commit
  ```
  We lost the changes :fearful:
- Let's try `git log --oneline --graph --decorate --all`
	```
	* 19f0265 (a-changes) added change log line in 'file'
	* 2682a75 added A changes file
	* 489be22 (HEAD -> master) my second commit
	* 191fb85 my first commit
	```
	No we didn't lost our changes :sunglasses: :trollface:
	Git is showing the changes (set of commits) that our branch contains, if we don't add `--all`.
	When adding `--all` we can see all the commits from all the branches, but how can we undestand in which branch we are ???
	Until now, we were adding commits at the top of the *"chain"*, but now we are at the `master branch but we are seeing all the commits. It is the **HEAD** that shows us where we are currently.
- Let's focus in our branch again (remove `--all`) -> `git log  --oneline --graph --decorate` 
	```
	* 489be22 (HEAD -> master) my second commit
	* 191fb85 my first commit
	```
- Let's add a new file named `masterOnlyFile` with any content.
- Start tracking the new file and commit. Remember, descriptive commit messages (e.g. "added masterOnlyFile")
- Let's observe the `master` branch -> `git log  --oneline --graph --decorate` 
	```
	* 6420791 (HEAD -> master) added masterOnlyFile
	* 489be22 my second commit
	* 191fb85 my first commit
	```
	We have added a file that is *"branch specific"* or *"branch agnostic"* ???
- Lets observe the whole graph -> `git log  --oneline --graph --decorate --all`
	```
	* 6420791 (HEAD -> master) added masterOnlyFile
	| * 19f0265 (a-changes) added change log line in 'file'
	| * 2682a75 added A changes file
	|/  
	* 489be22 my second commit
	* 191fb85 my first commit
	```
	We have created divergence between the two branches. 
	1. `a-changes` branch contains changes that the `master` does not have 
	2. `master` branch contains changes that `a-changes` does not have.
- Let's go back to the initial problem. We still need to add **B changes** in the project
- Let's create a new branch. Previously we used 
	```
	git branch a-changes
	git checkout a-changes 
	```
	Usually, we use `git checkout -b b-changes` which is the same with the above.
- After `git checkout -b b-changes` 
   ```
   Switched to a new branch 'b-changes'
  ```
  If you want to see your branch in your terminal without using `git branch` or `git status` you can customize your terminal 
  and the branch will be displayed in the terminal prompt.
  ```
  ~/Documents/gitexamples/exercise2 (b-changes)$ ls -la
	total 20
	drwxr-xr-x 3 vasilis domain users 4096 Nov 25 19:29 .
	drwxr-xr-x 3 vasilis domain users 4096 Nov 25 18:17 ..
	-rw-r--r-- 1 vasilis domain users   13 Nov 25 19:12 file
	drwxr-xr-x 8 vasilis domain users 4096 Nov 25 19:42 .git
	-rw-r--r-- 1 vasilis domain users    5 Nov 25 19:29 masterOnlyFile
  ```
	 You can see the branch in the first line after `~/Documents/gitexamples/exercise2`.
-  Let's create the functionality file with name `FileWithBChanges`.
- Start tracking and commit. Again, descriptive commit messages (e.g. "added B changes file")
Let's observe the graph -> `git log  --oneline --graph --decorate`
	```
	* a9065fa (HEAD -> b-changes) added B changes file
	* 6420791 (master) added masterOnlyFile
	* 489be22 my second commit
	* 191fb85 my first commit
	```
	A fourth commit has been added but the `master` branch is at the third commit.
- Let's add in `file` the change that we just implemented. Open `file` and add a third line  "Added B functionality file".
- Add your changes and commit them. Commit message should always be descriptive (e.g. "added change log line in 'file'"
- Let's observe the graph -> `git log  --oneline --graph --decorate`
	```
	* be7b050 (HEAD -> b-changes) added change log line in 'file'
	* a9065fa added B changes file
	* 6420791 (master) added masterOnlyFile
	* 489be22 my second commit
	* 191fb85 my first commit
	```
	A fifth commit has been added. `master` has not changed at all. The commit has been added on the `b-changes` branch
- Now let's observe the whole project graph -> `git log  --oneline --graph --decorate --all`
	```
	* be7b050 (HEAD -> b-changes) added change log line in 'file'
	* a9065fa added B changes file
	* 6420791 (master) added masterOnlyFile
	| * 19f0265 (a-changes) added change log line in 'file'
	| * 2682a75 added A changes file
	|/  
	* 489be22 my second commit
	* 191fb85 my first commit
	```
- Let's create some divergence between `b-changes` and `master`. Navigate to the `master `branch, add a new file named `masterOnlyFile2`, start tracking it and commit with *descriptive* message.
-   Let's observe the whole project graph -> `git log  --oneline --graph --decorate --all`
	```
	* 4a74bb9 (HEAD -> master) added masterOnlyFile2
	| * be7b050 (b-changes) added change log line in 'file'
	| * a9065fa added B changes file
	|/  
	* 6420791 added masterOnlyFile
	| * 19f0265 (a-changes) added change log line in 'file'
	| * 2682a75 added A changes file
	|/  
	* 489be22 my second commit
	* 191fb85 my first commit
	``` 
- Jump from branch to branch and check that the **HEAD** is showing the correct location.
- Can you move the HEAD to a commit that is not the latest commit of any branch?
- You can download a git visualization tool in you want to see the graph without using `git log  --oneline --graph --decorate --all` or `git log  --oneline --graph --decorate`. I prefer using SourceTree for Mac and Windows and gitg for Ubuntu. GitHub desktop is very good but it cannot be set up easily for other git repositories like gitlab or bitbucket.
