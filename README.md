= How to Git

This assumes you are comfortable using the OSX terminal to change directories and look at their contents using the 'cd' and 'ls' commands.

There is a difference between using Github and using git. "git" in lowercase is the general name of the version control system software. "Github" is a website where many millions of git repositories are mirrored and there are graphical tools for looking at them and sharing them. 

Let's say my goal is to add my name to the contributors listed in a README file for a  project that I am helping with. 

0. Start with a Github account. Make sure you know your username and password.
1. Go to a directory on your computer where you'd like to maintain projects. I have a /Users/ari/Projects directory where all my random project repos live. Inside that, do not create a directory just for your new project, because "git clone" will create it for you.
2. Clone the repository. In your terminal window, type "git clone " with a space after the word 'clone' but do not press Enter yet. 

Click the "HTTP" button on the repo's page. Copy the repository URL (it starts with https and ends with .git) to the clipboard and paste it after "git clone ". Now you can press Enter.

For my repo on Github named "Treasury" this looks like:
`$ git clone https://github.com/tensory/Face.git`

3. Go into the newly created repo directory. For me this would be `/Users/ari/Projects/Treasury/`.

4. Create a branch.* A branch is a version of the repository where you can make changes without messing up the main version (called "master"). If you're ever unhappy with how the changes are going in your branch, you can just delete the whole thing and start fresh, without messing up master.

Think of a name for your new branch that will help you remember what you intend to do with it. It's best to make a new branch any time you have a specific task in mind. Use the "git checkout" command to set up the branch.

`$ git checkout -b edit-readme-file master`

In English this would mean "Check out a new branch from 'master' and call it 'edit-readme-file'". However, for the git checkout command, the new branch name comes before the origin name.

Checking out a branch is kind of like changing a TV channel. Once you enter a "git checkout" command, you would say you are "on that branch". If you were to type "git checkout master" you would be back on the "master" branch.

5. Start making changes. Here I would look for a file called README.md in my project and edit it in a text editor to add my name. 

6. Once done making a change, you need to tell git about the changed file so that it knows you are done. This is done in two steps, called 'add' and 'commit'.

First, type git status:
$ git status

I would see a list of "unstaged" changes with one entry, README.md, which is the same file as I just edited.

So I tell git to "add" the changes:

$ git add README.md

Now if I type "git status" again, README.md has been upgraded to "staged" status, and I have no other unstaged changes. The git add command expects you to add files one by one. This means that if you make several changes, you can save just certain ones without being stuck with every change all at once. (You can also "git add" with multiple file names on the same line. Or you could just type "git add ." to add everything, but I feel that tends to cause more mistakes.)

7. Commit your changes. "git commit" only works on whatever changes have been staged. If I hadn't done the "git add" step, git commit would do nothing. But I did add the file, so when I type:

`$ git commit -m "Added my name to README"`

git goes ahead and commits the README.md edit, with a log message that says "Added my name to README". 

Now I could, if I wanted to, type "git log" and see a record of that change. git log  shows the most recent change at the top.

At this point, the edit-readme-file branch on my own computer knows that I made the change to README.md. But, the "master" branch doesn't know about that change yet, and neither does Github. If my computer hard drive died right now, my work would not be on Github anywhere.

So what now? I'm at a fork in the road. I have a choice of ways I could get the work onto Github. My method depends on whether I am working with other people.

If I am working with others, we all make a rule that nobody commits code to "master" without allowing someone else to take a look and approve it. Not all working groups do this, but it's considered a best practice for code quality and general politeness. Going this route, I would merge through a Github pull request. 

If I'm just working by myself, I can merge my changes directly into my local "master" and then push "master" to Github.

Let's look at it both ways. Skip to method 2 if you're working without collaborators.

== Merge Method 1: Collaborative Merging Through Github ==

Github has a very nice graphical UI that makes it easy to see what changes someone is proposing to push into a branch.  So first I check that I am ready to push. If "git log" shows the commit message that I care about, I'm ready to push the branch.

I type:

`$ git push origin edit-readme-file`

This is the point where the git program on my computer will try talking to Github's servers. This is where I need to know my username and password. If that works (if I got my password right, and if Github already thinks my account is a contributor to the repo) then Github will receive the command from my computer and create an "edit-readme-file" branch on its own servers, containing everything I did on my edit-readme-file.

This is really exciting. It means that I can ask to get my changes merged into the shared master, and it also means that anyone working with me is able to check out that branch (just the branch!) to add more work to it, again without messing up anyone's master.

So, now that I have pushed, I go to the project repository page on Github and click the button near the page top that says "Pull Request".

A pull request is like a "proposed merge" of one branch into another branch. Typically you want to merge your working branch into master. It's called a pull request because from Github's point of view, you are creating a request to pull the working branch into the intended target (master.)  

In the dropdown on the LEFT hand side, make sure master is selected. 

In the dropdown on the RIGHT hand side, make sure your working branch is selected.

Note the little tiny left-pointing arrow between the two columns, which is supposed to indicate the movement "into" master.

You can optionally fill out the form that appears on the "Write" tab to help explain the intent of the changes you hope to merge. 

When you're happy with the description, click "Send pull request". The resulting page can be shared with someone else, who has the opportunity to read and comment on your code. If you make more pushes to the same branch (perhaps in response to review comments), the pull request will automatically be updated with changes.

When you are totally happy, and so is your collaborator, one of you can hit the "Merge" button at the very bottom of the pull request page. By convention, you (and not the reviewer) would get to hit merge, as a little reward for all your hard work. :) 


== Merge Method 2: Local Merging

Use this method if you're developing by yourself and you're only interested in getting your branch changes into master, without a review step.

Once you feel you are done with your working branch, do a "git status":

$ git status

If you see any files that are STAGED (added) but NOT COMMITTED, git will not let you continue with this process. Unstaged files will be ignored, committed files will be included, but staged files stand in the way.

If you want to unstage anything, you can do it with git reset (you can google it for the exact process.) Now's the time to do one last "git commit -m" if you see any stragglers. But let's assume that all the files you wanted to commit are committed.

OKAY. Now, remember your working branch name (git status will tell you if you forgot). Now change to master:

$ git checkout master

Ok, you're on master. Now's a good time to do a git pull on master to make very sure that's up to date: (Do it anyway, even if you're the sole contributor, to get in the habit)

$ git pull origin master

Assuming that all went fine, do your merge!

$ git merge edit-readme-file
 
By default, git will automatically commit your merged branch. You can disable that, but it's fine most of the time. So, you've "added" and "committed" the branch files by doing the merge, so we come to the final step:

$ git push origin master

THAT WAS EASY.

Go to Github and admire your freshly merged master branch. Back on the command line, you can delete your finished branch with:

$ git branch -D edit-readme-file

---

Thanks for reading! Please direct comments/improvements to me at alacenski@gmail.com


* Most git tutorials do not start with branching. I think everyone should do this right away. It will save you a lot of time untangling problems on master.


