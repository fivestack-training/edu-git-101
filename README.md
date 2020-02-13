# Git 101

Learn the basics of git here. There are probably thousands of how-to's for git basics. I wrote this one primarily
for myself because I learn best by doing. If this helps you too, great! I'll also point out that many IDE's will do
a lot of this work for you via UIs. This can be very useful. But if you've ever had to unwind something that you
didn't intend to do, it can be very confusing and time-consuming. So I always think it's useful to know what's going
on behind the scenes with an IDE.

**_NOTE:_** The code snippets will assume that you're running this tutorial on Windows. But the vast majority of
the commands work in Bash or PowerShell as well. The exception will be when you're moving around the file system. All
of the git commands should be the same.

**_NOTE:_** I will capture all of the commands used in this tutorial at the bottom with a brief description of what
they do.

## What is a Code Repository?

If you're reading this file on a browser, you're likely looking at a code repository. You can think of a code
repository as being similar to a root folder on Google Drive &reg; or Dropbox &reg;. It's (generally) a remote
server that you can save files to and connect to from your computer. In particular, you can save all versions
of the files as you edit them over time. This is commonly referred to as "source control" or "version control".

As a point of clarification, there are many instances of the word "repository" in software development. Because developers
tend to think in terms of scope (context for newbies) we often leave off important qualifiers that are to be assumed.
You will almost always hear people refer to a code repository simply as a repository, or even shorter, as a repo.
In the context of this tutorial, I too will refer to it as a repository or a repo.

## What is Git?

For this particular repository, I use software called Git to manage code versioning as well as connecting from my
local computer to the remote repository. Git is an extremely common development tool. I would argue it's the
most common, but I'm too lazy to get statistics on that. Git also adds the concept of "branching", which becomes very
important when collaborating.

For the sake of completeness, I will mention that you can use Git with a local repository on your local machine
and never interact with a remote repository. And that is what happens for 80% to 90% of the time you use Git.
However, in most development, there is an implicit assumption that you will start by getting code from a remote 
repository and end by putting code back up on a remote repository. I will emphasize that in this tutorial because
my philosophy is that content, or "state" in developer-speak, (things like personal files, code, pictures, etc.)
should be separated from the environment doing work on the content, or "changing state" in developer-speak. If my
computer implodes right now, I lose three things: the computer parts, the time it will take to re-download my
software on a new computer (read as "games"), and the marginal work that I have done today. And let me emphasize,
it is marginal.

## How do I install Git?
 
I'm bought in, where do I get it? Go download Git from here:

https://git-scm.com/downloads

You'll get several questions in the dialog. The defaults should be fine for everything, at least for this tutorial.

## l33t h4ckz0r Command Line

For this tutorial, we're going to be real hackers and use the command line. In all seriousness, we're doing that
for three reasons:

1. Git is a command line tool, pure and simple
1. I can tell you exactly what to type instead of navigating your file system and various buttons and menus
1. You may find as you hone your development skills that it is actually easier to use the command line for
certain activities

So let's start the command line utility by pressing the Windows key + R to get the run dialog, typing "cmd.exe"
(without the quotes), and hitting run. You should get a black box that looks something like this:

```shell script
Microsoft Windows [Version 10.0]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Users\[your name]>
```

This is commonly referred to as the terminal or the command line. It is what your computer would look like if
it did not have all of the graphics and buttons and menus that you are used to using to (usually) make things
easier to do. You should have wound up in your user directory, but let's just make sure that you did, so that I
don't send you down the wrong road:

```shell script
C:\>cd %USERPROFILE%
```

## How do I create a repo?

Between corporate work and personal work, I use two remote code repository services: GitHub and Azure Dev Ops Repos
(ADO). These are both Git-compliant services, and either one will work for this tutorial. I tend to default to GitHub
for two reasons: it has been a staple among developers for a while, and there is far less overhead in managing a
basic GitHub repo than a basic ADO repo. For the purposes of this tutorial, I'll assume that you're using GitHub
as your remote code repository service.

###### Don't do this:

There are two ways to create a git repo. You could create a local repo on your machine and associate git with it.
This is as simple as running the following command:

```shell script
C:\Users\[your name]\Source>git init
```

While this will setup the local repo, it will do nothing with remotes. Also, doing this first tends to have the
effect of making you think of your local repo as the source of truth with the remote repo as a saved backup. Per
our philosophy of separating state from changing state, this is backwards.

###### Do this instead:

Instead, what we'll do is create an empty repo on GitHub first. If you haven't already, you should create a GitHub
account. It's free and there are instructions on the site of how to do so. Log in to GitHub and go to your
Repositories in the top right. Click the green "New" button to get to the create dialog. The only thing you're
required to do on this page is enter a name. But I would also go ahead and create a few files that this dialog
creates so that we have something to work with for this tutorial:

- Check the box next to "Initialize this repository with a README". This will create a short default version of the
file that you're reading right now.
- Under "Add a license:", select MIT. If you're interested, this license allows readers to reuse the code in this
repo however they see fit. You can read more about software licenses here: https://choosealicense.com

Once you click "Create repository", you should be handed a page that has a file list with two files in it and a
green button near the top right that says "Clone or download". That means you're good to go.

## How do I get a local copy of my repo?

To edit the code in your repository, you'll need to get a local copy on your machine. First, we need to create a
place to put all of your repos. Let's do that by making a new directory in our home directory and then going into it:

```shell script
C:\>cd %USERPROFILE%

C:\Users\[your name]>mkdir Source

C:\Users\[your name]>cd Source
```

**_NOTE:_** I chose to name my directory "Source" because it is where I put repos from source control. You can use
whatever name you like. But if you don't use Source, remember to swap that out for what you used through this tutorial.

Now let's get the clone url from GitHub and use Git to pull it down. Click on the green "Clone or download" button
on your repo. It will display a url that looks something like `https://github.com/[your name]/[repo name].git`. Use
`git clone` to pull down a copy in your new directory:

```shell script
C:\Users\[your name]\Source>git clone
```

Confirm that you now have a new directory that's name the same as the repo by using the `dir` command:

```shell script
C:\Users\[your name]\Source>dir
...

 Directory of C:\Users\[your name]\Source

[timestamp] <DIR> .
[timestamp] <DIR> ..
[timestamp] <DIR> [repo name]
          0 File(s)            0 bytes
          # Dir(s)   ###,###,### bytes free

```

Let's go to our new local repo and see what's there:

```shell script
C:\Users\[your name]\Source>cd [repo name]

C:\Users\[your name]\Source\[repo name]>dir
...

 Directory of C:\Users\[your name]\Source\[repo name]

[timestamp] <DIR> .
[timestamp] <DIR> ..
[timestamp]       #,### LICENSE
[timestamp]          ## README.md
          2 File(s)        #,### bytes
          # Dir(s)   ###,###,### bytes free

```

Great! Our new repo came down with our license file and our readme markdown file.

## What is this branching thing you mentioned earlier?

At this point, you can add, change, or delete pretty much anything in this directory as if it's any other directory.
There is one exception. If you have "View -> Hidden Items" checked, you'll also notice there is a directory called
".git" in this directory. That is what Git is using to track changes you make. If you delete or change that directory,
you're on your own. The only time I touch that directory is when I am deleting the entire local repo because I'm no
longer working on it. In other words, don't touch it.

While you could just edit files as you wish, I recommend using branches to make your changes. This will make it
easier to clean up any issues that you may create as you go. It also makes it much easier to collaborate on code
with other developers. Whereas I think of traditional versioning of code as a serial concept (one change happens
after another), I think of branches as parallel versions of the code (changes can happen in multiple branches at
the same time). With the help of Git, you will ultimately merge all of these changes back together at some point.
But this flexibility is incredibly useful, even when working on a solo project.

If you look at your remote repo on GitHub, you'll see that you have one branch called `master`. This is the default
name that GitHub gives your first branch. You can see it on your local machine as well:

```shell script
C:\Users\[your name]\Source\[repo name]>git branch
* master
```
 
In a simple repo, most people will understand the master branch to be the 'real' branch. It should always have
working code. And it is usually the most recent working version of the code. This is one reason to create another
branch, so that we can save partially working code that is in progress. So let's create a new branch, switch to it,
verify that we can see it, and verify that it has a copy of the original files:

```shell script
C:\Users\[your name]\Source\[repo name]>git checkout -b my_new_branch

C:\Users\[your name]\Source\[repo name]>git branch
  master
* my_new_branch

C:\Users\[your name]\Source\[repo name]>dir
...

 Directory of C:\Users\[your name]\Source\[repo name]

[timestamp] <DIR> .
[timestamp] <DIR> ..
[timestamp]       #,### LICENSE
[timestamp]          ## README.md
          2 File(s)        #,### bytes
          2 Dir(s)   ###,###,### bytes free

```

## How do I add a new file to my repo?

Setting up new repos, configuring things, and learning some basic command line stuff is fun and all, but let's actually
create some code. Or at least let's create a text file. I'm going to give a few commands that I won't explain here in
the interest of minimizing the scope of the tutorial. Let's create a new file called "new_file.txt" that has a line
of text in it reading "this is a new file" and verify that this all worked:

```shell script
C:\Users\[your name]\Source\[repo name]>echo this is a new file > new_file.txt

C:\Users\[your name]\Source\[repo name]>dir
...

 Directory of C:\Users\[your name]\Source\[repo name]

[timestamp] <DIR> .
[timestamp] <DIR> ..
[timestamp]       #,### LICENSE
[timestamp]          ## new_file.txt
[timestamp]          ## README.md
          3 File(s)        #,### bytes
          2 Dir(s)   ###,###,### bytes free

C:\Users\[your name]\Source\[repo name]>more new_file.txt
this is a new file

```

So we have our new file, but Git knows nothing about it. We can confirm that with `git status`:

```shell script
C:\Users\[your name]\Source\[repo name]>git status
On branch my_new_branch
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        new_file.txt

nothing added to commit but untracked files present (use "git add" to track)

```

With coding in general, you want to be more explicit than implicit. So Git is not going to assume that you want to
save every single file that you create in your repo. We need to tell Git to add the new file to be tracked:

```shell script
C:\Users\[your name]\Source\[repo name]>git add new_file.txt

C:\Users\[your name]\Source\[repo name]>git status
On branch my_new_branch
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   new_file.txt

```

At this point, our new file is saved to the local file system and it's added to Git tracking on the my_new_branch
branch in the local repo.

## How do I save my changes to my local repo?

There are several phases of "saved" in Git. And it takes a little bit to understand why we would need all of
these levels of saved. For small solo projects, this is going to seem like overkill, but it is a good practice to get
into. This is a bit to read through, but I think it's required before moving on. The levels of "saved" look like this:

| Phase | Name | Action |
|---|:---|:---|
| 0 | File Save          | save the file to the local file system |
| 1 | Commit             | save the changes to the file in the current branch in the local repo |
| 2 | Push               | save the changes to the file in the current branch in the remote repo |
| 3 | Merge Pull Request | save the changes to the file to the master branch in the remote repo |

The first step of saving a file means almost nothing to me. I actually have my IDE set to auto-save as I go so that as
I open and close files, they look like how I last left them.
 
I think of committing my changes as saving my work. Another way to put that is, if Git does not know that I saved my
changes, then they are not saved. I commit very often, multiple times per day. It allows me to add commit messages
that describe what I did and maybe even why I did it. GitHub will track these messages and display the most current
one, from the file's perspective and not the repo's perspective, in the file details. So while it may seem like
you're setting a message at the commit level, over time you will wind up with a different commit message next
to every file.

I think of pushing my changes as sharing my work with others or calling it a day. I will push at least every day, at
the end of the day, but not as often as I commit. If I am not actively working on something, and I've reached a good
stopping point, that's usually a good time to push. I will push code if others need to incorporate it into their
changes. It's the first point where they can do that. I will also push code if I'm done for the day. Following the
philosophy of separating state from changing state, I don't want my state to be stuck on a particular machine. Between
corporate work, personal work, personal work on the couch, etc. I actually develop on no less than three machines. If
I leave my code on any one of those machines without pushing it, I could easily start making changes on another
machine that now conflict with my original changes. Pushing makes it so that the remote is the single source of truth.

I think of merging a pull request as completing the work. I submit a pull request when I'm reasonably confident that
people who rely on the code to work, but don't work on the code themselves, would be able to use the code with
minimal negative effects. Depending on the feature you're trying to add, this can be anywhere from a day to a few
weeks. You don't want this to go on too long because you risk running into conflicts with other people have branched
off of master to build something out. You also run the risk of building a giant piece of code that doesn't work and
you don't know why. You want small pieces that you can verify work correctly.

Now, having said all of that, let's commit our changes to Git, remind our future selves what we did, and verify that
our changes have been committed:

```shell script
C:\Users\[your name]\Source\[repo name]>git commit -m "I added a new file"

C:\Users\[your name]\Source\[repo name]>git status
On branch my_new_branch
nothing to commit, working tree clean

```

## How do save my changes to my remote repo?

We saved the new file to the file system, and we updated our local git repo to commit the changes. But to the outside
world we have yet to do anything. So let's get our changes up on the remote repo so that others can see it and we can
call it a day. Remember that we created our new branch locally. So we also need to tell our remote repo that we are
sending a new branch:

```shell script
C:\Users\[your name]\Source\[repo name]>git push --set-upstream origin my_new_branch

```

This will likely give you a log in screen for GitHub. The reason you get this is because you still have to authenticate
to make changes on GitHub. By default, GitHub is readable by the public. But for obvious reasons, it is not editable by
the public. Even if you're logged in on your browser, it's a separate session as far as GitHub is concerned. Once
you have done this the first time, Git will remember your credentials. However, if you've setup 2FA, you may need to
authenticate every time.

Once you've successfully pushed your changes, you should be able to see the new branch on GitHub. Go to your repo and
look along the top. You should see that you have 2 branches. You should also be able to select your new branch from
the "Branch:" drop-down menu. You can see that you now have a new file on the my_new_branch branch, but if you switch
back over to master, this file is not there.

## How do I make master look like my new branch?

We have one last phase in our saving hierarchy. We're happy with our new file, as simple as it may be. If we want our
master branch to reflect this, all we need to do is merge our development branch, my_new_branch, into our master branch.
Luckily, GitHub is usually smart enough to realize that you just pushed a branch and may want to merge it to master.
If that's the case, you'll see an alert along the top with a green button that says "Compare & pull request". Click
on that to get the dialog. If not, click on "Pull requests on the top" and click the green "New pull request" button.
On this page, you want to merge the "compare" branch into the "base" branch. For some reason GitHub makes this read
right to left. Perhaps they want to indicate that the base branch is fixed by making it left aligned. Whatever the
case may be, leave "base:" as master and change "compare:" to my_new_branch. You should get a comparison on the bottom
that shows that you have a new file called "new_file.txt" and that the new file has a line in it that reads "this is
a new file". This is very useful because it's a quick way to determine if you are merging the changes that you intend
to merge. Once you're happy that you have things in the right order, click the green "New Pull Request" button and
you'll be taken to the pull request conversation stream. When working on a team, this could turn into a long
discussion about whether code is suitable to be merged into master, whether it is written in an optimal way, etc.
Since we are a team of one, we can just click the "Merge pull request" button in the middle of the screen. This
will complete the pull request and merge our changes into master.

At this point, you may want to delete your development branch on GitHub. I generally do that because I don't like
having several active branches. And if there is a branch out there, it looks as if someone is working on it whereas
it may just be a stale branch that was merged months ago. And if you delete your remote branch and don't intend on
continuing it locally, which is usually the case, then you should definitely delete the local branch:

```shell script
C:\Users\[your name]\Source\[repo name]>git checkout master

C:\Users\[your name]\Source\[repo name]>git branch -d my_new_branch

C:\Users\[your name]\Source\[repo name]>git branch
* master

```

## How do I continue working on my project?

You finally come back to your project months later and want to continue working on it. You have a few options. If you
don't have the local repo anymore, or you simply want to start fresh, you can clone the repo the way we did at the
beginning. However, if you have the local repo, and you just want to make sure you pick up all changes that have
happened since you last cloned the repo, just pull down the repo from within your local repo:

```shell script
C:\Users\[your name]\Source\[repo name]>git pull
```

And that completes the circle of coding.

# Appendix - Command Summary

## Git

| Command | Action | Example |
|:---|:---|:---|
| `init` | initializes a local repo | C:\Source>git init |
| `clone` | initializes a local repo and pulls the remote repo into it | C:\Source>git clone |
| `branch` | gives a list of all branches in the local and indicates which is current | C:\Source>git branch |
| `branch -d <branch>` | deletes the branch | C:\Source>git branch -d my_new_branch |
| `status` | gives a status on what is committed, staged, etc. | C:\Source>git status |
| `checkout <branch>` | makes the named branch the current branch | C:\Source>git checkout master |
| `checkout -b <branch>` | creates a new branch and makes it the current branch | C:\Source>git checkout -b my_new_branch |
| `add <file>` | stages changes for the file | C:\Source>git add new_file.txt |
| `commit -m <message>` | commits all staged changes with a commit message | C:\Source>git commit -m "I added a new file" |
| `push <remote> <branch>` | pushes the local branch to the remote repo | C:\Source>git push origin my_new_branch |
| `push --set-upstream <remote> <branch>` | pushes a new local branch to the remote repo | C:\Source>git push --set-upstream origin my_new_branch |
| `pull` | pulls down the remote changes to the local repo, equivalent to `fetch` plus `merge` | C:\Source>git pull |

## Windows Command Line

| Command | Action | Example |
|:---|:---|:---|
| `cd <directory>` | changes directory | C:\Users>cd Source |
| `mkdir <directory>` | creates a new directory | C:\Users>mkdir Source |
| `dir` | lists everything in a directory | C:\Users>dir |
| `echo <message>` | prints what you type to standard out | C:\Users>echo hello world |
| `echo <message> > <file>` | writes what you type to a file, and creates it if it doesn't exist | C:\Users>echo hello world > hello_world.txt|
| `more <file>` | prints the contents of the file to standard out | C:\Users>more hello_world.txt |
