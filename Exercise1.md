#### Exercise 1

- Open a terminal that has git available
- Create a folder for this exercise
- Navigate to the folder
- Type `git init`
   You should see the following
   ```
   Initialized empty Git repository in C:/Users/vasilis/Documents/GitHub/exercise1/.git/
   ```
- Type `git status`
   You should see the following
   ```
    On branch master

    No commits yet

    nothing to commit (create/copy files and use "git add" to track)
   ```
- Observe the folder of the project. A new hidden folder  `.git/` has been created. Git is saving the info inside this folder.
- Create a new file named `file` (without an extension .txt, .log etc.) and this file should have only one line as shown below
  ```
  first
  ```
  And save the file.
  
- Type `git status`
  ```
    On branch master

    No commits yet
    
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
            file
    
    nothing added to commit but untracked files present (use "git add" to track)
  ```
- Now you have created a new file but it is `untracked`. Type `git add file` to start tracking the file.
- Type `git status`.
  ```
    On branch master
    
    No commits yet
    
    Changes to be committed:
      (use "git rm --cached <file>..." to unstage)
            new file:   file
  ```
- You have started tracking the `file`. If you want to stop tracking it use `git reset file`.
- Use `git status` to ensure that the file is not tracked after using `git reset file`.
- Start again tracking the file. Use `git status` to check if it is tracked.
- It is time to do your first commit. Use `git commit -m "my first commit"`. Every commit needs a message. If not added with `-m` an editor will open for user to complete the message.
  ```
    [master (root-commit) e296fa6] my first commit
     1 file changed, 1 insertion(+)
     create mode 100644 file
  ```
- Type ` git log --graph --oneline --decorate`
    ```
    * e296fa6 (HEAD -> master) my first commit
    ```
- Add a second line to the `file`
  ```
  first
  second
  ```
  And save the file.
- Use `git status`
    ```
    On branch master
    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git restore <file>..." to discard changes in working directory)
            modified:   file
    
    no changes added to commit (use "git add" and/or "git commit -a")
    ```
    Now git has detected the change you performed on the `file` and its giving you the options to:
    1. stage your changes with `git add file`
    2. discard them with `git restore file`
- Stage your changes and commit them. 
  ` git commmit -m "my second commit"`
  ```
  [master 6a7830b] my second commit
  1 file changed, 2 insertions(+), 1 deletion(-)
  ```
- Type ` git log --graph --oneline --decorate`
  ```
    * 6a7830b (HEAD -> master) my second commit
    * e296fa6 my first commit
  ```
- **Soft Reset**
    - Now lets remove the second commit ->  `git reset --soft HEAD~1`
    - Type ` git log --graph --oneline --decorate`
      ```
        * e296fa6 (HEAD -> master) my first commit
      ```
      The commit has been removed
    - Let commit again ` git commmit -m "my second commit"`
    - Type ` git log --graph --oneline --decorate`
      ```
        * 185758e (HEAD -> master) my second commit
        * e296fa6 my first commit
  ```
  Commited again.
- **Hard reset**
    - Now lets remove the second commit with another way ->  `git reset --hard HEAD~1`. 
    - Observe that the second line has been completely removed from the file and from the unstaged changes.
    - Try to commit again
- **Simple reset**
    - Now lets remove the second commit with another way ->  `git reset HEAD~1`.
    - Observe that the second line is present but not staged and not commited.
    - Try to commit again

- Read [this article](https://www.datree.io/resources/git-unstage)
    
















