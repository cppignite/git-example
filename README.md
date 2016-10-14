# Let's Talk About Git
This repo was created to demonstrate some of the key features of Git and GitHub for the Outreach Program at Cal Poly Pomona.
## Topics Covered
- The Basic Commands of Git including: git clone, git add, git status, git commit, and git push
- Advanced topics including: merge conflicts, cherry-picking, branching, rebasing, blaming, and reverting vs reseting
- Features offered from GitHub: Logs, Pull Requests, and Code Review Tools

## Important Note
This lesson will only cover topics relating to the command-line tools for git. I will not be covering the techniques for using the GUI version of git. Feel free to do independent research on this topic but in general I would discourage you from using this tool. Using the command-line tool forces us to understand our interactions with git, which means less merge conflicts (and angry managers :D).

## What is git? What is GitHub?
A common misconception of these two is that git and GitHub are a single entity. The truth is that git is a version control tool and GitHub is just a website which allows us to interact with git in a visual context and provides us with several social programming tools (we'll see these later).

## The Basics
I'm going to write this introduction with the assumption that you've never used git before so if the words clone, add, commit, and push mean anything to you can skip this section.

### Cloning
`git clone https://github.com/cppignite/git-example`

This is the first command you will ever type with git. git clone downloads the repo to your local directory. Enter this command into your

### Status
`git status`

This command allows us to see our progress as we use git. Files in git are in one of 5 states. 

1. Untracked files are files that are in our repo's directory but we haven't told git to track. (git status will show these in red)
2. Tracked and unmodified files that git is tracking, but they are exactly as they appear in your current version of the repo. (git status won't show these)
3. Unstaged changes are files which we've made changes to but haven't used git add to stage them for a commit. (git status will show these in red)
4. Staged changes are unstaged changes that have been staged with git add. (git status will show these in green)

### Adding
`git add my/local/file/or/folder/`

This command serves as your main tool for queuing files to be changed. When you add a file using git add you adding it to a set of files which have changes you would like to submit to the remote repo. 

Many StackOverflow pages will list the command `git add .` what this command is actually doing is adding all files in your current directory (this is because . is used to represent the present directory in most command-line interfaces). I would generally discourage this unless you know exactly what files were changed. Using this generalized statement makes it easy to add unintentional files to your repo.

### Commits
`git commit`

So once you run this command a text editor will open and you will have to type a commit message. In most cases this will open a vi based editor. If you've never used one of these tools before use [this link](http://www.openvim.com/) to get an idea of how to start editing and how to save your edits once you’re done.

Let's go over the difference between using adding and committing. Using git add allows us to add to a set of changes on our repo, while committing allows us to put our changes in logical groups. For instances if you are working on your personal website and you want to add new features like a toolbar, a sidebar, and a picture of yourself. It makes sense to implement your toolbar in one commit, sidebar in another, and so on...Obviously different companies will have different policies on commits, but the general rule of thumb I follow is to use commits should implement something. Just one thing. No more, no less.

#### Commit Naming Conventions
We've all been there...Its the end of the day...You just pushed a new version of code only to go back to your IDE and find a bug. What do you do? Quickly fix the change, add your file, and commit...."Fixed Bug".... anddd push. 

This is fine for small projects and you'll see this all over several of my personal repos. But its bad practice. One of the main points of version control is to provide context to history of code. So when we write "Fixed Bug" we can't really understand much from this commit other than it fixed...some bug. Here are some good rules to follow for writing commit messages:

1. Always describe your commit with a subject line (Fixed Bug, afdafsaddas, Removes dumbass mistake)
2. Separate subject from body with a blank line (If you want to use a body)
3. Aim for a 50 character limit for the subject line (To avoid trunca...) 
4. Only capitalize the first word of the subject line
5. No periods in the subject line
6. Use the imperative mood in the subject line: "Clean your room", "Wash a dish". Generally this is done by starting the sentence with a verb and phrasing it as an order.

These rules will vary depending on where you work, but maintaining consistency is a good way to keep your public repos looking clean. 
[Here's my source for this list](http://chris.beams.io/posts/git-commit/)

### Push
`git push`

This command is simply used to push any local commits you've made to the remote repository (in most cases this will be on GitHub). Keep in mind, any changes you've made up to this point are purely local. Why is this important? If you fuck up and create some bug. You can fix it, WITHOUT ANYONE SEEING YOUR MISTAKE. However, once you run this command you're changes are made public and will be available to anyone who can see your repo. Push with care!

## Advanced Topics
This section will cover the more difficult features of git which, although unnecessary, allow us to fully take advantage of git instead of just using it as Google Drive for programmers.
### Merge and Merge Conflicts
`git merge`

If you've ever worked with a team of people of a git project you've had to deal with merging. A merge is simply taking your local changes and applying them to a code base which has commits which were made after your initial pull. At first you will use this command to merge your local changes with the master branch on your repo. However, as time goes on this will become more relevant in merging some other branch with your master branch. But we will cover branches later in this tutorial.

Merge conflicts are when you try to push your code and your change conflicts with a change someone else had made.  Git will not let you push this code until you resolve the conflict. Here are the steps you should take to resolving merge conflicts.

1. `git status` to see which files were changed in both commits that you were trying to merge. These files should appear in red and should be labeled as such.
2. Edit each of these files and resolve each conflict. git will show you both versions of the code you changed you will see something like 
~~~~
<<<<<<<<<<<< HEAD
//some code
================== 
//some other code
>>>>>>>>>>>> 2dd2112d 
~~~~
3. Remove all the lines git added and try to merge the two version of the code into their correct form.

### Diff
`git diff file-name` 

Use this command to see the actual changes you've made to a file in a line by line presentation of which lines were removed, changed, or unchanged. 
### Log
`git log`

This command is so simple but it is absolutely crucial to my day to day use of git. This command is very important when using the rest of the advanced commands, as we will use it to access the commit hashes. A commit SHA is the long string of characters under each commit when you run git log. These are unique identifiers that git automatically generates for each commit in your repo.

#### Referencing Commits
As stated above we can use git log to get the SHA for each commit in our repo, but git also provides us with some handy shortcuts in order so we don't need to check the log every time we want to reference a commit. Using the keyword `head` in place of any commit hash will reference the last commit in your log. You can also add carets to reference a specific number of commits before your commit. `head^^^` will reference three commits behind your current commit. 

### Checkout
`git checkout`

There are a couple of powerful use cases for git checkout. The first involves a file which you've made changes to locally but haven't added it yet. You can revert this change with `git checkout file-name`. The second use for git checkout is to navigate between commits and branches. We'll cover branches below, but you can navigate between commits with `git checkout commitSHA`.

### Reset
`git reset`

Reset is used to restore a file or a set of files to a previous state in your commit tree. You can use it to remove a commit or a series of commits made to your local. There are several types of commit resets in git, but the two most important types are --hard and --soft. `git reset --soft commitSHA` update all differences between your current commit and the commitSHA you specify to unstaged changes. This means your changes will still be visible in the files, but git will act like you just made them. This is very useful for applying quick fixes to your commits. `git reset --hard commitSHA` is only for those brave souls who want to destroy all work done between HEAD and your commitSHA. All commits and changes will be removed and your files will be reset to the state of that commitSHA.

### Stashing
`git stash`

This one is really quick but really useful. Stash acts as temporary storage for any unstaged changes on your repo. Typing it once will remove all changes. Typing it again will bring them all back.

### Branching
`git branch`

Branching is an important part of git because it allows multiple programmers to work on different projects in the same code base at the same time. Whenever you see the word `master` in git, it is referring to the master branch. This is the main strain of code in the repo. In a university setting it is common practice to simply use the commands listed in the basics section to work solely off the master branch of a repo. In general, this is bad practice as it will slow down your development cycle.

To start branching first use the command `git checkout -b branch-name`. This command will allow you to create a new branch with the given name. 

#### Branch Naming Conventions
I would like to briefly go over some common naming conventions. 

1. Use the tags of your repo. For instance, bug/feat/wip at the start of your name.
2. Use slashes to separate parts.
3. Be descriptive but concise.

Example: "bug/wip/fix-save-button"

Once we have our branch created we can use git as normal using add, commit, and push. You will need to specify a new upstream, but git will tell you how to do this when you `git push`. If you think you are done with your changes on your branch there are a couple of ways to apply it back to master. We'll go over the merge method here.

1. Checkout the master branch
2. `git merge branch-name`
3. Then write a commit message for your merge. 

Merge will add a new commit into your master branch with the changes you applied to your personal branch.

### Rebasing

Rebasing is probably one of the most complicated components of git. It allows us to modify order and the logical composition of your commits. The first thing rebasing allows us to do is to rebase our current branch/working directory to the top of another commit chain. For instance if I clone from a repo on Monday, create a new branch, and work on it till I might go to push only to find 72 commits ahead of my own on master. Now I can merge my branch with these changes or I can use rebase to move all my commits to the top of the other 72. `git rebase master` allows us to copy all new files/changes in master then apply our branch's commits on top of them.

One of the more interesting concepts of rebase is `git rebase -i commitSHA` for interactive. This allows us to pick, delete, or modify all commits between HEAD and our specified commitSHA. With this command rebase becomes a very powerful tool for rewriting history. This command will open a vi editor and allow you to choose what action to take with each commit. The editor will explain what each option means but here are some of the more important ones.

1. Pick allows us to keep the commit as is 
2. Reword allows us to reword the commit message
3. Edit will stage our changes for commit but will not apply the commit (We can use this to edit changes inside commits)
4. Squash will apply all changes of this commit into the previous commit. This is particularly import for cleaning your commit logs as you can take a group of commits and merge them all into one coherent change.

### Cherry Picking
`git cherry-pick commitSHA`

We use this command to apply commits from other branches individually. This is accomplished without merging or rebasing. Use this as a 'quick fix' for moving commits around your repo. 

### Blame
`git blame file-name`

This command will show you who last changed each line of a file. This is useful for witch hunts where you found a bug in the code and want to find the person responsible. It is also useful when work with large teams of programmers as you can use it to find out who will know and be able to explain the code you have to edit.

### Bisect
`git bisect commitSHA`

Another useful command for witch hunts, you can use bisect to do a binary search through a commit log. Bisect will walk you back and forth checking out commits through the history of your repo having you label them as good or bad until you find the changes that introduced the bug.

