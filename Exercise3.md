#### Exercise 3

- Complete Exercise 2
- Make a copy of exercise 2 folder
- Navigate to the new folder for exercise 3 and do not modify the folder of exercise 2.
- We have completed **A changes** and **B changes** and in the meantime we have made some additional changes on the `master` branch.
- Now we want to include all these changes in the `master` branch.
- Let's start with **A changes**. We need to merge the `a-changes` branch into the master.
- Ensure that you are on the `master` branch.
- Then use `git merge a-changes`
	```
	Merge made by the 'recursive' strategy.
	 FileWithAChanges | 1 +
	 file             | 1 +
	 2 files changed, 2 insertions(+)
	 create mode 100644 FileWithAChanges
	```
- Let's observe the graph for `master` branch only -> `git log --oneline --decorate --graph`
	```
	*   e515a66 (HEAD -> master) Merge branch 'a-changes'
	|\  
	| * 19f0265 (a-changes) added change log line in 'file'
	| * 2682a75 added A changes file
	* | 4a74bb9 added masterOnlyFile2
	* | 6420791 added masterOnlyFile
	|/  
	* 489be22 my second commit
	* 191fb85 my first commit
	```
- Now the master branch contains the changes that we did on `a-changes` branch
- You can delete `a-changes` branch if you want to keep a clean history. `git branch -d a-changes`
