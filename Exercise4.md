
#### Exercise 4

- Complete Exercise 3
- Make a copy of exercise 3 folder
- Navigate to the new folder for exercise 4 and do not modify the folder of exercise 3.
- We have merged `a-changes` and now we want to merge `b-changes`.
- Ensure that you are on master branch.
- Then try `git merge b-changes`
	```
	Auto-merging file
	CONFLICT (content): Merge conflict in file
	Automatic merge failed; fix conflicts and then commit the result.
	```
- Something has happened that caused a merge failure.
- Let's `git status`
	```
	On branch master
	You have unmerged paths.
	  (fix conflicts and run "git commit")
	  (use "git merge --abort" to abort the merge)

	Changes to be committed:

		new file:   FileWithBChanges

	Unmerged paths:
	  (use "git add <file>..." to mark resolution)

		both modified:   file
	```
- Something has happened with the `file`. Let's see its contents:
	```
	first
	second
	<<<<<<< HEAD
	Added A changes file
	=======
	Added B functionality file
	>>>>>>> b-changes
	```
- The contents of `file` contain the first two lines of the initial master branch. The rest of the contents does not seem correct. Let's remember the changes that we performed in this file.  On `a-changes` we added a third line and on `b-changes` we added a third line. We did the same thing on the same file but each line had different content. Git recognizes such changes and it does not merge automatically because without our instructions it doesn't know which changes to keep.
- We we know which changes we want to keep? Do we need only a-changes? Do we need only b-changes? Do we need both? Do we need none?
- If you observe the file it has a structure that show the two changes:
	```
	<<<<<<< HEAD
	
	=======
	
	>>>>>>> b-changes
	```
- This is the way git show you the changes that have conflicts and need resolving.
- In such cases we modify the file manually of with an IDE in order to select which changes we want to keep and then we save the file.
- Then we add the file `git add file`
- After adding the file the status has changed. `git status`
	```
	On branch master
	All conflicts fixed but you are still merging.
	  (use "git commit" to conclude merge)

	Changes to be committed:

		new file:   FileWithBChanges
		modified:   file
	```
- Now we can commit the merged changes. `git commit -m "merge branch 'b-changes'"`
- Let's observe the whole graph:
	```
	*   0e7aff1 (HEAD -> master) merge branch 'b-changes'
	|\  
	| * be7b050 (b-changes) added change log line in 'file'
	| * a9065fa added B changes file
	* |   e515a66 Merge branch 'a-changes'
	|\ \  
	| * | 19f0265 added change log line in 'file'
	| * | 2682a75 added A changes file
	* | | 4a74bb9 added masterOnlyFile2
	| |/  
	|/|   
	* | 6420791 added masterOnlyFile
	|/  
	* 489be22 my second commit
	* 191fb85 my first commit
	```
- You can delete `b-changes` branch if you want to a clean history.
