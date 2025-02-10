# Git commits to commit

## Within the work directory, establish a subdirectory named hello. Inside this directory, generate a file titled hello.sh and input the following content:
### echo "Hello, World"

1. Make dir work which include the hello directory :
    ```
   mkdir -p work/hello
    ```
2. Hello directory has a hello.sh file and the content is : echo "Hello, World" :
    ```
    cd work/hello
    ```
    ```
     echo 'echo "Hello, World"' > hello.sh
    ```
## Initialize the git repository in the hello directory.
3. Initialiaze the git repo in the hello directory :
    ```
     git init 
    ```
4. Add the hello.sh file to the git repository :
    ```
    git add hello.sh
    ```
5. Commit the file to the repo :
    ```
    git commit -m "Added hello.sh script"
    ```
## Check the status and act accordingly with the output of the executed command.

6. Check the git status :

    ```
    git status  
    ```

    6a. if the message is this :  
        On branch main
        nothing to commit, working tree clean
    This means everything is commited.

    6b. if you see untracked files (ex) :   
        Untracked files:  
            (use "git add <file>..." to include in what will be committed)
            hello.sh :
        add the file to staging :

    ```
    git add hello.sh
    ```
        
    6c. if you see that there are changes which are not staged for commit :
        Changes not staged for commit:
            (use "git add <file>..." to update what will be committed):
            stage the changes :
    ```
    git add hello.sh
    ```
        
    6d. if you see changes that are not committed :
        Changes to be committed:
            (use "git restore --staged <file>..." to unstage)
            commit the changes :
    ```
    git commit -m "Add some changes to the hello.sh script"
    ```
## Change the hello.sh content to the following:

7. Modify the hello.sh content :
    ```
    echo '#!bin/bash
        echo "Hello, $1"' > hello.sh
    ```
## Stage the changed file and commit the changes, the working tree should be clean.
8. Stage the changed file :
    ```
    git add hello.sh
    ```
9. Commit the changed file :
    ```
    git commit -m "Update hello.sh to the new greeting"
    ```

## Modify the hello.sh file to include comments and stage it.
#!/bin/bash

#Default is "World"
name=${1:-"World"}
echo "Hello, $name"

10. Modify the hello.sh file to include comments :
    ```
    echo '#!/bin/bash
        #comment"
        echo "Hello, $1"' > hello.sh
    ```
11. Stage the changed file :
    ```
    git add hello.sh
    ```

12. Commit the changed file :
    ```
    git commit -m "Update hello.sh to the new greeting"
    ```
## Make two separate commits:
### The first commit should be for the comment in line 3.
13. Modify the hello.sh file to include comment in the 3rd line :
    ```
    echo '#!/bin/bash
 
     #Default is "World"
    ```
14. Stage and commit hello.sh :
    ```
    git add hello.sh
    ```
    (to stage it)
    ```
    git commit -m "..."
    ```
    (to commit it)

### The second commit should include changes made to lines 4 and 5.
15. Modify the hello.sh file to include changes made to lines 4 and 5 :
    ```
    echo '#!/bin/bash

    #Default is "World"
    name=${1:-"World"}
    echo "Hello, $name"

    ```

16. Stage and commit hello.sh :
    ```
    git add hello.sh
    ```
    (to stage it)
    ```
    git commit -m "..."
    ```
    (to commit it)
# HISTORY

## Show the history of working directory :
1.
    ```
    git log
    ```


## Show One-Line History for a condensed view showing only commit hashes and messages :
2.  
    ```
     git log --oneline
    ```
## Controlled entries :
### You need to customize the log output by specifying the number of entries or a time range. Customize it to display the last 2 entries and to view the commits made within the last 5 minutes.
3.
    A. For the last 2 entries :
    ```
    git log -n 2
    ```
    B. For the commits made within the last 5 minutes :
    ```
    git log --since="5 minutes ago"
    ```
    C. For the last 2 entries and commits made within the last 5 minutes :
    ```
    git log -n 2 --since="5 minutes ago"
    ```
## Personalized format :
### Show logs in a personalized format, including the commit hash, date, message, branch information, and author name, resembling * e4e3645 2023-06-10 | Added a comment (HEAD -> main) [John Doe] .
4. 
    ```
    git log --pretty=format:"* %h %ad | %s (%d) [%an]" --date=short
    ```
    
    - %h: Commit hash (abbreviated)
    
    - %ad: Author date (formatted as YYYY-MM-DD using the --date=short option)
    - %s: Commit message
    - %d: Ref names (e.g., branch or tag information, such as HEAD -> main)
    - %an: Author name


              
              
# CHECK IT OUT
## Restore first snapshot :
### Revert the working tree to its initial state, as captured in the first snapshot, and then print the content of the hello.sh file.
1.  Identify the first commit :
    ```
    git rev-list --max-parents=0 HEAD
    ```

2. Restore the working tree to the first commit :
    ```
    git checkout <hash_of_the_1st_commit>
    ```
3. Print the content of the hello.sh file :
    ```
    cat hello.sh
    ```

4. Go back to the last snapshot :
    ```
    git checkout main
    ```

## Restore the second recent snapshot :
### Revert the working tree to the second most recent snapshot and print the content of the hello.sh file.
5. Identify the second commit :
    ```
    git log --oneline (list the recent commits)
    ```
    ```
    git checkout <hash_of_the_2nd_recent_commit>
    ```
6. Print the content of the hello.sh file :
    ```
    cat hello.sh
    ```
## Return to latest version :
### Ensure that the working directory reflects the latest version of the hello.sh file present in the main branch, without referring to specific commit hashes.
7. Return to the main branch :
    ```
    git checkout main
    ```
8. Update the working directory :
    ```
    git pull origin main
    ```
9. Restore the hello.sh file to the lastest version :
    ```
    git checkout main -- hello.sh
    ```
10. Print the content of the hello.sh file :
    ```
    cat hello.sh
    ```

# TAG ME
## Referencing Current Version :
### Tag the current version of the repository as v1.
1. Ensure that we are in the root directory of the repository :
    ```
    ls -a 
    ```
    (if there is a .git directory, we are in the root directory)

2. Tag the current version :
    ```
    git tag v1
    ```
3. Push the tag (optional) :
    ```
    git push origin v1
    ```
## Tagging Previous Version :
### Tag the version immediately prior to the current version as v1-beta, without relying on commit hashes to navigate through the history.
4. Find the previous commit (HEAD^ is the parent of the current HEAD) :
    ```
    git log --oneline HEAD^..
    ```
5. Create the tag for the previous version :
    ```
    git tag v1-beta HEAD^
    ```
6. Push the tag (optional) :
    ```
    git push origin v1-beta
    ```
## Navigating Tagged Versions :
### Move back and forth between the two tagged versions, v1 and v1-beta.
7. Move to v1 :
    ```
    git checkout v1 
    ```
8. Move to v1-beta :
    ```
    git checkout v1-beta
    ```
9. Return to the current branch :
    ```
    git checkout main(or master)
    ```
## Listing Tags :
### Display a list of all tags present in the repository to verify successful tagging.
10.
    ```
    git tag
    ```

# CHANGING YOUR MIND

## Reverting Changes:
### Modify the latest version of the file with unwanted comments, then revert it back to its original state before staging using a Git command.
#!/bin/bash

#This is a bad comment. We want to revert it.
name=${1:-"World"}

echo "Hello, $name"
1. Add the comments.

2. Check the current status :
    ```
    git status
    ```
3. Revert the changes :
    ```
    git checkout -- hello.sh (Discard and restore to the last commit)
    ```

## Staging and Cleaning
### Introduce unwanted changes to the file, stage them, then clean the staging area to discard the changes.
#!/bin/bash

#This is an unwanted but staged comment
name=${1:-"World"}

echo "Hello, $name"

4. Add the comments.

5. Check the current status :
    ```
    git status
    ```

6. Stage the changes :
    ```
    git add hello.sh
    ```
7. Check the current status :
    ```
    git status
    ```
8. Cleaning :
    ```
    git restore --staged hello.sh
    ```
    (to remove from the staging area)
    
    ```
    git restore hello.sh
    ```
    (to discard the changes)

## Committing and Reverting :
### Add the following unwanted changes again, stage the file, commit the changes, then revert them back to their original state.
#!/bin/bash

#This is an unwanted but committed change
name=${1:-"World"}

echo "Hello, $name"

9. Make the changes

10. Check the current status :
    ```
    git status
    ```
11. Stage the changes :
    ```
    git add hello.sh
    ```
12. Check the current status :
    ```
    git status
    ```
13. Commit the changes :
    ```
    git commit -m "add changes"
    ```
14. Revert the commit :
    ```
    git revert HEAD
    ```

## Tagging and removing commits :
### Tag the latest commit with oops, then remove commits made after the v1 version. Ensure that the HEAD points to v1.
15. Tag oops :
    ```
    git tag -a oops HEAD -m "Tagging the latset commit as oops"
    ```
    (tag the last commit with the name oops and i put a message)

16. List all tags to find the commit hash associated with v1 :
    ```
    git show-ref --tags
    ```
17. Reset HEAD to v1 :
    ```
    git reset --hard v1
    ```

## Displaying Logs with Deleted Commits :
### Show the logs with the deleted commits displayed, particularly focusing on the commit tagged oops.
18. List the deleted commits :

    ```
    git reflog
    ```

19. View the details of the commit tagged as oops :
    ```
    git show oops
    ```

## Cleaning Unreferenced Commits :
### Ensure that unreferenced commits are deleted from the history, meaning there should be no logs for these deleted commits.
20. Expire unreachable entries in the reflog :
    ```
    git reflog expire --expire-unreachable=now --all
    ```
21. Perform garbage collection:
    ```
    git gc --prune=now
    ```
22. Verify the cleanup :
    ```
    git fsck --unreachable
    ```
    ```
    git reflog
    ```

## Author Information :
### Add an author comment to the file and commit the changes.
#!/bin/bash

#Default is World
#Author: Jim Weirich
name=${1:-"World"}

echo "Hello, $name"

23. Modify the file :
    ```
    echo '#!/bin/bash

    #Default is World
    #Author: Jim Weirich
    name=${1:-"World"}

    echo "Hello, $name"
    ```
24. Stage the changes :
    ```
    git add hello.sh
    ```
25. Commit the changes with an author:
    ```
    git commit -m "Add author comment" --author="Jim Weirich"
    ```

26. Verify the changes :
    ```
    git show -s --format=fuller
    ```
27. Amend the last commit with author information:
    ```
    git commit --amend --author="Jim Weirich <jim.weirich@example.com>"
    ```



# MOVE IT
## Moving hello.sh :
### Using Git commands, move the program hello.sh into a lib/ directory, and then commit the move.
1. Create a lib directory :
    ```
    cd ../
    ```
    (go to work directory)
    ```
    mkdir -p lib
    ```
2. Move the hello.sh file :
    ```
    git mv hello/hello.sh lib/hello.sh
    ```
3. Stage it :
    ```
    cd lib
    ```
    ```
    git add hello.sh
    ```
4. Commit it :
    ```
    git commit -m "Move it to lib"
    ```

### Create a Makefile in the root directory of the repository with the provided content and commit it to the repository. 
TARGET="lib/hello.sh"

run:
	bash ${TARGET}

5. Make a Makefile :
    ```
    cd ../
    ```
    (go to work directory)
    ```
    code Makefile
    ```
6. Add the content and commit it :
    ```
    Add content
    ```
    ```
    git add Makefile
    ```
    ```
    git commit -m "Make a Makefile"
    ```
# BLOBS, TREES AND COMMITS

## Exploring .git/ Directory :
### Navigate to the .git/ directory in your project and examine its contents.You will have to explain the purpose of each subdirectory, including objects/, config, refs, and HEAD in the audit.
1. objects (directory) :
    ```
    This directory stores all the content of your files, commits, trees, and tags in the form of Git objects.

    Structure: Objects are stored in subdirectories named after the first two characters of their SHA-1 hash,with the remaining characters as the filename.This structure ensures efficient storage and retrieval. 
    ```

    Contents:
    ```
    Blobs: Store file data.
    Trees: Represent directory structures.
    Commits: Record snapshots of the repository at specific points in time.
    Tags: Mark specific commits as important.
    ```
2. config File :
    ```
    This file contains repository-specific configuration settings, such as user information,
    remote repository URLs, and other preferences.
    It's essential for defining how Git operates within this repository.
    ```
3. refs/ Directory :
    ```
    This directory holds references to commit objects, effectively pointing to various branches, tags, and remote references.

    Subdirectories:

    heads/: Contains files that represent local branches,each file named after a branch and containing the SHA-1 hash of the latest commit on that branch.

    tags/: Stores pointers to specific commits, often used to mark release points. 

    remotes/: Holds references to branches in remote repositories, organized by remote name. 
    ```
4. HEAD File :
    ```
    The HEAD file is a symbolic reference to the current branch or commit checked out in your working directory.

    Contents: Typically, it contains a reference like ref: 
    refs/heads/main, indicating that the current working directory is aligned with the main branch.
    In a detached HEAD state, it contains the SHA-1 hash of a specific commit.
    ```
  ------ ews edw -----
  
## Latest Object Hash :
### Find the latest object hash within the .git/objects/ directory using Git commands and print the type and content of this object using Git commands.
5. Identify the latest commit hash :
    ```
    git log -n 1
    ```
    (if you want only the commit hash you can use :
        ```
        git log -n 1 --format="%H"
        ```
        )

6. Determine the object's type :
    ```
    git cat-file -t <commit hash>
    ```
7. View the object's content :
    ```
    git cat-file -p <commit hash>
    ```

    (#optional#
        View the tree object :
        ```
        git cat-file -p <tree hash>
        ```

    View the content (inspect blob objects) :
        ```
        git cat-file -p <blob hash>
        ```)

## Dumping Directory Tree :
### Use Git commands to dump the directory tree referenced by this commit.
8. Identify the latest commit :
    ```
    git log -n 1 --format="%H"
    ```

9. Display the directory tree :
    ```
    git ls-tree -r <commit hash>
    ```
### Dump the contents of the lib/ directory and the hello.sh file using Git commands.
10. List the content of the lib directory :
    ```
    git ls-files lib/ (list all files under lib directory which are tracked by Git)
    ```
11. View the content of hello.sh :
    ```
    cat lib/hello.sh
    ```
    #optional#
            
    if you want to view the content of a specific commit :
    ```
    git show <commit hash>:lib/hello.sh
    ```
    



# BRANCHING
It’s time to do a major rewrite of the hello world functionality. Since this might take a while, you’ll want to put these changes into a separate branch to isolate them from changes in the main branch.
## Create and Switch to New Branch: :
### Create a local branch named greet and switch to it.
1. Create the branch :

    ```
    git branch greet
    ```
(if you want to view the local branches :
    ```
    git branch
    ```
(the branch with the * is currently active branch))

2. Switch to the greet branch :
    ```
    git checkout greet
    ```
### In the lib directory, create a new file named greeter.sh and add the provided code to it.Commit these changes.
#!/bin/bash

Greeter() {

who="$1"

echo "Hello, $who"

}

3. Navigate to the lib directory :
    ```
    cd lib
    ```
4. Create the greeter.sh file :
    ```
    code greeter.sh
    ```
5. Stage the new file :
    ```
     git add greeter.sh
    ```
6. Commit the new file :
    ```
    git commit -m "Add greeter.sh with a greeter function"
    ```
    
## Update the lib/hello.sh file by adding the content below, stage and commit the changes.
#!/bin/bash

source lib/greeter.sh

name="$1"

if [ -z "$name" ]; then

name="World"

fi

Greeter "$name" :

7. Change the content.
8. Stage the changes :
    ```
    git add hello.sh
    ```
9. Commit them :
    ```
    git commit -m "Make changes in the hello.sh file"
    ```

## Update the Makefile with the following comment and commit the changes.
# Ensure it runs the updated lib/hello.sh file
TARGET="lib/hello.sh"

run:

bash ${TARGET} :

10. Add comments
11. Stage the updated file :
    ```
    git add Makefile
    ```
12. Commit this file :
    ```
    git commit -m "Add comments in the Makefile"
    ```
## Switch back to the main branch, compare and show the differences between the main and greet branches for Makefile, hello.sh, and greeter.sh files.
13. Switch to the main branch :
    ```
    git checkout main
    ```    
14. Compare the difference :
    ```
    git diff main..greet -- Makefile lib/hello.sh lib/greeter.sh
    ```
## Generate a README.md file for the project with the provided content. Commit this file.
This is the Hello World example from the git project.

15. Make the file :
    ```
    code README.md
    ```
16. Stage it :
    ```
    git add README.md
    ```
17. Commit it :
    ```
    git commit -m "Add README.md file"
    ```
## Draw a commit tree diagram illustrating the diverging changes between all branches to demonstrate the branch history.
18. Generating the commit tree diagram :
    ```
    git log --all --decorate --oneline --graph
    ```
    - --all : includes all branches in the log
    - --decorate : adds names of brances or tags of commits shown
    - --oneline : displays each commit in a single line
    - --graph : shown an ASCII graph of the branch and merge history







# Conflicts, merging and rebasing

## Merge Main into Greet Branch :
### Start by merging the changes from the main branch into the greet branch.
1. Verify the remote configuration :
    ```
    git remote -v 
    ```
    if return no output or does not list 'origin' means the remote repo is not configure
        so follow the next steps :
    
    a.  Add remote repository :
    ```
    git remote add origin <repo's url>
    ``` 
    b. Verify again :
    ```
    git remote -v 
    ```
2. Fetch and Merge changes :
    ```
    git fetch origin
    ```
    ```
    git checkout greet
    ```
    ```
    git merge origin/main
    ```
    if you see fatal : refusing to merge unrelated histories :
    ```
    git fetch origin
    ```
    ```
    git merge origin/main --allow-unrelated-histories
    ```
    ```
    git add <file>
    ```
    ```
    git commit -m "Merge origin/main into current branch, allowing unrelated histories"
    ```
    


### Switch to main branch and make the changes below to the hello.sh file, save and commit the changes.

#!/bin/bash

echo "What's your name"
read my_name

echo "Hello, $my_name" :

3. Switch branch :
    ```
    git switch main
    ```
4. Make changes .
5. Stage it :
    ```
    cd lib
    ```
    ```
    git add hello.sh
    ```
6. Commit it :
    ```
    git commit -m "Update hello.sh to prompt user's name"
    ```

## Merging Main into Greet Branch (Conflict):
### Attempt to merge the main branch into greet. Bingooo! There you have it, a conflict.
7. Go to the greet branch :
    ```
    git switch greet
    ```
8. Merge the main branch into greet :
    ```
    git merge main
    ```
### Resolve the conflict (manually or using graphical merge tools), accept changes from main branch, then commit the conflict resolution.
9. Identify conflicted files :
    ```
    git status 
    ```
#### Resolve the conflicts :
    
10. Open the file which you should modify
    ```
    (cmd + click)
    ```

11. Remove everything between:
    ```
    <<<<<<< HEAD and ======= 
    ```
12. Stage the resolve file :
    ```
    git add <file name>
    ```
13. Commit it :
    ```
    git commit -m "Resolved merge conflict by accepting changes from main branch"
    ```


## Rebasing Greet Branch :
### Go back to the point before the initial merge between main and greet.
14. Identify the commit before the merge :
    ```
    git log --oneline
    ```
15. Reset the greet branch :
    ```
    git reset --hard <commit hash>
    ```
### Rebase the greet branch on top of the latest changes in the main branch.

16. Ensure your local repo is up to date :
    ```
    git fetch origin 
    ```
17. Switch to the greet branch :
    ```
    git switch greet
    ```
18. Rebase the greet branch onto main :
    ```
    git rebase origin/main
    ```


## Merging Greet into Main :
### Merge the changes from the greet branch into the main branch.
19. Switch to main branch :
    ```
    git switch main
    ```
20. Merge greet into main (with the --allow-unrelated-histories flag):
    ```
    git merge greet (--allow-unrelated-histories)
    ```
21. Resolve any merge conflicts (if u see conflicts):
    ```
    git status
    ```
    a. Open and resolve the modified files
    
    b. Stage them :
    ```
    git add <file name>
    ```
    
    c. Commit them :
    ```
    git commit -m "Merge greet into main"
    ```

## Understanding Fast-Forwarding and Differences :
### Explain fast-forwarding and the difference between merging and rebasing.
#### A. Fast-Forwarding

- Happens when the branch being merged has no new commits diverging from the main branch.
- Git simply moves the branch pointer forward to the latest commit.
- No merge commit is created.
- Example: 
    ```
    git checkout main
    git merge feature-branch
    ```
- Works if feature-branch is ahead of main without divergence.

#### B. Merging

- Combines changes from one branch into another.
- If branches have diverged, Git creates a merge commit.
- Retains full commit history, including branch structure.
- Example:
    ``` 
    git checkout main
    git merge feature-branch
    ```
- Pros: Preserves history, clear branch structure.
- Cons: Can create unnecessary merge commits.

#### C. Rebasing

- Moves (reapplies) commits from one branch onto another, rewriting history.
- Makes it seem like all changes were made sequentially.
- Example:
    ```
    git checkout feature-branch
    git rebase main
    ```
- Pros: Cleaner linear history.
- Cons: Can cause issues if used on shared branches (rewrites history).


##### When to Use Which?
- Use Merge for keeping history intact, especially in shared repositories.
- Use Rebase for a clean, linear history, particularly in personal feature branches.

# Local and remote repositories

## In the work/ directory, make a clone of the repository hello as cloned_hello. (Do not use copy command) :
1. Navigate to work directory :
    ```
    cd /path/to/work/
    ```
2. Use git clone , to clone hello into a new directory named cloned_hello :
    ```
    git clone /path/to/hello/cloned_hello
    ```


## Show the logs for the cloned repository. :
3. Navigate to the cloned_hello directory :
    ```
    cd cloned_hello
    ```
4. View the commit history :
    ```
    git log
    ```
        
    
## Display the name of the remote repository and provide more information about it. :
5. List the remote repo :
    ```
    git remote -v
    ```
6. Show detailed information about the remote repo :
    ```
    git remote show origin
    ```

## List all remote and local branches in the cloned_hello repository.
7. List all branches :
    ```
    git branch -a 
    ```
    
    ##### List only local branches :
    - git branch

    ##### List only remote branches :
    - git branch -r 
    


## Make changes to the original repository, update the README.md file with the provided content, and commit the changes.

This is the Hello World example from the git project.
(changed in the original)

8. Navigate to work directory :
    ```
    cd ../
    ```
    
9. Check your branch :
    ```
    git status
    ```
10. Update the content of README.md file .

11. Stage the difference :
    ```
    git add README.md 
    ```
12. Commit them :
    ```
    git commit -m "Update README.md with new content"
    ```


## Inside the cloned repository (cloned_hello), fetch the changes from the remote repository and display the logs. Ensure that commits from the hello repository are included in the logs.
13. Go to cloned_hello :
    ```
    cd cloned_hello
    ```
14. Fetch changes from the remote repo :
    ```
    git fetch origin 
    ```
15. View the commit history :
    ```
    git log --oneline --graph --all
    ```
16. Compare local and remote branches :
    ```
    git log HEAD..origin/main 
    ```

## Merge the changes from the remote main branch into the local main branch.
17. Check that you are on the main branch :
    ```
    git checkout main 
    ```
18. Fetch the latest changes from the remote repo :
    ```
    git fetch origin
    ```
19. Merge the remote main branch into local main branch  :
    ```
    git merge origin/main
    ```

## Add a local branch named greet tracking the remote origin/greet branch.
20. Verify the existence of the greet branch on the remote :
    ```
    git branch -r 
    ```
21. Create and switch to the local greet branch :
    ```
    git ckeckout -b greet 
    ```
22. Verify the tracking relationship :
    ```
    git branch -vv
    ```

## Add a remote to your Git repository and push the main and greet branches to the remote.
23. Add the remote repository :
    ```
    git remote add origin <remote URL>
    ```
24. Verify the remote repo :
    ```
    git remote -v 
    ```
25. Push the main branch to the remote repository :
    ```
    git push -u origin main 
    ```
26. Push the greet branch to the remote repository :
    ```
    git push -u origin greet
    ```
## Be ready for this question in the audit!
### "What is the single git command equivalent to what you did before to bring changes from remote to local main branch?
```
git pull origin main
```

#### This command performs two actions:

- Fetches the latest changes from the remote repository named origin.

- Merges those changes into your local main branch.



# Bare repositories

## What is a bare repository and why is it needed?
- A bare repository in Git is a version of a repository that lacks a working directory,meaning it doesn't contain the actual files of the project but only the Git metadata,such as branches, tags, and commit history.This structure is achieved by omitting the working tree,which is the directory where the project's files reside in a non-bare repository. 

    Key characteristics of a bare repository include:

    1. Absence of a Working Directory: Unlike standard repositories,
    bare repositories do not have a working tree,
    so you cannot edit files or perform typical development tasks within them. 


    2. Storage of Git Metadata: They contain all the version control information,
    such as commit objects, branches, and tags, but do not include the actual files from the project. 


- Why are bare repositories needed?

    Bare repositories are primarily used as central repositories to facilitate collaboration among multiple developers.
    Since they don't have a working directory, there's no risk of conflicts arising from uncommitted changes in the repository itself.
    This makes them ideal for serving as remote repositories where team members can push their changes and pull updates from others. 


    In essence, a bare repository acts as a centralized storage for the project's history
    and facilitates collaboration by serving as a common point for synchronizing changes among team members.


## Create a bare repository named hello.git from the existing hello repository.
1. Navigate to hello repository:
    ```
    cd hello
    ```
2. Create a bare clone of the repo :
    ```
    git clone --bare . ../hello.git
    ```
    
## Add the bare hello.git repository as a remote to the original repository hello.
3. Navigate to hello repository :
    ```
    cd hello
    ```
4. Add the bare repository as a remote :
    ```
    git remote add origin path/to/hello.git
    ```
5. Verify the remote adition :
   ```
   git remote -v
    ```
## Change the README.md file in the original repository with the provided content:
This is the Hello World example from the git project.
(Changed in the original and pushed to shared)

6. Navigate to work directory :
    ```
    cd ../
    ```
7. Modify the content of the README.md file.

## Commit the changes and push them to the shared repository.
8. Stage the changes :
    ```
    git add README.md
    ```
9. Commit them :
    ```
    git commit -m "Update the README.md file again"
    ```
10. Push them to the shared repository :
    ```
    git push origin main 
    ```
## Switch to the cloned repository cloned_hello and pull down the changes just pushed to the shared repository.
11. Navigate to the cloned_hello repository :
    ```
    cd cloned_hello
    ```
12. Pull the latest changes from the shared repository :
    ```
    git pull origin main
    ```



