
#### Exercise 5

- Complete Exercise 3
- Complete Exercise 4
- Make a copy of exercise 3 folder
- Navigate to the new folder for exercise 5 and do not modify the folder of exercise 3.
- We have merged `a-changes` and now we want to merge `b-changes`.
- As we saw in Exercise 4 when trying to merge changes there might be some conflicts and it is not that easy to resolve them and merge the changes.
- Before merging `b-changes` the graph is as shown below:
	```
	*   e515a66 (HEAD -> master) Merge branch 'a-changes'
	|\  
	| * 19f0265 added change log line in 'file'
	| * 2682a75 added A changes file
	* | 4a74bb9 added masterOnlyFile2
	| | * be7b050 (b-changes) added change log line in 'file'
	| | * a9065fa added B changes file
	| |/  
	|/|   
	* | 6420791 added masterOnlyFile
	|/  
	* 489be22 my second commit
	* 191fb85 my first commit
	```
- As we an see on the graph the `b-changes` is left behind in the change log. It would be better if we had a way to get the changes from `master` to `b-changes` branch. That way we will try to *"update"* the `b-changes` branch will the latest changes from the `master` branch.
- The first way to do achieve this *"update"*, is to merge `master` into `b-changes`. In exercise 4 we did the opposite. We merged `b-changes` into `master`. In this exercise we are going to use `rebase`. If you want to do the merge technique make another copy of exercise 3 and merge `master` into `b-changes`.
-  With rebase we are going to change the base of `b-branch`. Now the base of `b-changes` is commit 
	```
	6420791 added masterOnlyFile
	```
- We want to change its base so that it will be the latest commit on the `master` branch:
	```
	 e515a66 (HEAD -> master) Merge branch 'a-changes'
	```
- Ensure that you are on `b-changes` branch.
- Then `git rebase -i master`
	```
	pick a9065fa added B changes file
	pick be7b050 added change log line in 'file'
	```
	Save the file and exit for now. For this rebase we need `pick`. You can check `squash` and its functionality after this exercise.
	```
	Auto-merging file
	CONFLICT (content): Merge conflict in file
	error: could not apply be7b050... added change log line in 'file'

	Resolve all conflicts manually, mark them as resolved with
	"git add/rm <conflicted_files>", then run "git rebase --continue".
	You can instead skip this commit: run "git rebase --skip".
	To abort and get back to the state before "git rebase", run "git rebase --abort".

	Could not apply be7b050... added change log line in 'file'
	```
- Some problem occurred again. Let's see the status.
	```
	Last commands done (2 commands done):
	   pick a9065fa added B changes file
	   pick be7b050 added change log line in 'file'
	No commands remaining.
	You are currently rebasing branch 'b-changes' on 'e515a66'.
	  (fix conflicts and then run "git rebase --continue")
	  (use "git rebase --skip" to skip this patch)
	  (use "git rebase --abort" to check out the original branch)

	Unmerged paths:
	  (use "git reset HEAD <file>..." to unstage)
	  (use "git add <file>..." to mark resolution)

		both modified:   file

	no changes added to commit (use "git add" and/or "git commit -a")
	```
- You should think of `rebase -i` (-i interactive) as moving your commits one by one on the base that you have selected. The first commit has been rebased successfully but the second could not be rebase because of some conflicts. 
	```
	Last commands done (2 commands done):
	   pick a9065fa added B changes file
	   pick be7b050 added change log line in 'file'
	No commands remaining.
	```
	You can understand this from this part. `No commands remaining`. If we had more commits and an intermediate commit had conflicts with the new base then some commands would be remaining. That's the interactive (`-i`) mode that we added. Every time git picks a commit  to apply on the new base if something happens we stop and check the conflicts. We resolve the conflict and then we add them and finally we continue the rebase.
- Lets observe the whole graph
	```
	* a1be10b (HEAD) added B changes file
	*   e515a66 (master) Merge branch 'a-changes'
	|\  
	| * 19f0265 added change log line in 'file'
	| * 2682a75 added A changes file
	* | 4a74bb9 added masterOnlyFile2
	| | * be7b050 (b-changes) added change log line in 'file'
	| | * a9065fa added B changes file
	| |/  
	|/|   
	* | 6420791 added masterOnlyFile
	|/  
	* 489be22 my second commit
	* 191fb85 my first commit
	```
	git has moved the first commit of `b-changes` to the new base. `b-changes` is still at the old base until we complete the rebase.
- Let's resolve the conflicts as we did on Exercise 4. We need both changes. 
- After modifying the `file` to include both changes use `git add file` and the `git rebase --continue`
- Save the file and exit.
- Observe the whole graph
	```
	* 6452368 (HEAD -> b-changes) added change log line in 'file'
	* a1be10b added B changes file
	*   e515a66 (master) Merge branch 'a-changes'
	|\  
	| * 19f0265 added change log line in 'file'
	| * 2682a75 added A changes file
	* | 4a74bb9 added masterOnlyFile2
	* | 6420791 added masterOnlyFile
	|/  
	* 489be22 my second commit
	* 191fb85 my first commit
	```
- `b-changes` has been rebased and now it contains the latest changes and can be merged easily into master.
- Navigate to master branch and merge b-changes into master
	```
	* 6452368 (HEAD -> master, b-changes) added change log line in 'file'
	* a1be10b added B changes file
	*   e515a66 Merge branch 'a-changes'
	|\  
	| * 19f0265 added change log line in 'file'
	| * 2682a75 added A changes file
	* | 4a74bb9 added masterOnlyFile2
	* | 6420791 added masterOnlyFile
	|/  
	* 489be22 my second commit
	* 191fb85 my first commit
	```
- If you compare the project folder and its contents for Exercises 4 and 5 then the result is the same. We have included the changes from all the branch into master. Can you find any differences between the two trees?
- Can you find a way to start from exercise's 2 final result and get the following graph after merging everything ?
	```
	* ac75ada (HEAD -> master, b-changes) added change log line in 'file'
	* c89c98f added B changes file
	* 7901017 (a-changes) added change log line in 'file'
	* 322d28b added A changes file
	* 4a74bb9 added masterOnlyFile2
	* 6420791 added masterOnlyFile
	* 489be22 my second commit
	* 191fb85 my first commit
	```


