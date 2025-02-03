echo "# devopsnotes" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:bionicnate/devopsnotes.git
git push -u origin main

Now, it's time to commit our  change! A commit records the change in the repository compared to its  previous state. But before that we must configure the git user who will be the owner of the commit.
Set git username as sarah and user email as sarah@example.com using the below commands. 
git config user.email sarah@example.com 
git config user.name sarah

It is good that the file is  untracked. But it is still under GIT's radar. If you run the "git add ."  command accidentally git will start to track this file.
Let's configure git to ignore this file permanently.
Add the file to a .gitignore file. echo notes.txt >> .gitignore

How many branches does the repository currently have?
Run git branch

Checkout branch feature/signout and then use the command git log --graph --decorate to see previous commit history along with the branch they were committed on.

While in the master branch merge the story/frogs-and-ox branch. If prompted for a commit message leave it to the default and quit the editor.
Run git merge story/frogs-and-ox
Check git log now and it should show commit message as Merge branch 'story/frogs-and-ox'

Let's now configure the remote repository for the local repository at /home/sarah/story-blog
Target remote repo URL : http://git.example.com/sarah/story-blog.git 
remote repo alias : origin 
Run cd /home/sarah/story-blog; git remote add origin http://git.example.com/sarah/story-blog.git

Which command can be used to push data to our remote repo?
Syntax: git push <remote repo alias> <remote branch>
Now push our current stories to the remote git repository we created
Simply run git push origin master to push and input login credentials

max needs to download the current code (stories) uploaded by Sarah in remote repository. As user Max, clone the remote repo to his home directory - /home/max
cd /home/max; git clone http://git.example.com/sarah/story-blog.git

Instead commit it to a new branch named story/fox-and-grapes with the commit message 'Added fox-and-grapes story'
Run git checkout -b story/fox-and-grapes; git add .; git commit -m 'Added fox-and-grapes story'

Run git checkout master; git fetch origin master to fetch remote changes
Now that we’ve fetched the origin master branch, we can update our local master branch with the latest changes made on origin/master branch.
 Merge the remote master branch to local master
Syntax: git merge <other-branch>

Run: git rebase -i HEAD~3 command after that it will open with the default editor. Change the second and third lines to use squash instead of pick. 
In next, add new commit message Add hare-and-tortoise story and save it. 
To see the changes run the git log --oneline command.

undo all the changes made in the previous commit. Note that the changes must be retained in the commit history. Use the default revert commit message.
Use git revert HEAD~0 command or git revert <commit id> 

revert the last commit but retain the unfinished changes. The last commit must not be part of the GIT history.
Use git reset --soft HEAD~1 command

reset her story to the previous good version of the story and remove all commits and changes she made since the commit 
Run git reset --hard HEAD~3 

git stash show stash@{0} ; git stash show stash@{1}; git stash show stash@{2}




