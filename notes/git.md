#Version Control with Git

##What is git?

Git is a pretty standard version control system, similar to SVN and others.  Github took Git and ran with it, making it stupidly easy to collaborate on code.

##Guidelines

####Don't work on your local master branch

Working on your local master branch may seem easy, but it can complicate your workflow. To make a new branch and switch into it:

<pre>git checkout -b branch-name</pre>

####Keep branch names descriptive

It's a good idea to follow some sort of convention when naming your branches, so that people know what's going on when you push your code.

The convention most people use around Wistia is <code>initials-featurename</code>.  You'll see stuff like:

- jb-captions-api
- ms-rg-customize
- jv-more-preview-mailings

Looking at these branch names, you get a pretty good idea of who's working on what.  Cool, right?

####Rebase early and often

It takes **so** little effort to make sure you're always up to date with the codebase, so no excuses for slacking off!

To update your local <code>master</code>

<pre>
git checkout master
git fetch origin
git rebase origin/master
</pre>

Keeping your local master updated will help you avoid merge conflicts.  I'd recomment updating your local master at least once every day or so.

####No merge commits, anywhere, ever

Nobody likes merge commits!  The sneaky bastards pop up all kinds of places they don't belong (they don't belong anywhere) and they need to go.

Merge commits typically come from two actions:

1. *Using* <code>git pull</code> *to update your codebase*  
If you would rather pull than fetch and rebase, pull with the command <code>git pull --rebase</code> instead.  Is much better.
2. *Clicking the big green button*  
Don't ever merge a pull request by hitting that shiny green button in Github.  I know it's pretty, but it's a trap.


##Tips and Tricks

####Show the latest commits
<pre>git log</pre>

####Filter commits to ones containing seach-word in the commit message 
<pre>git log | grep search-word</pre>

####Display the diff for a commit
<pre>git show {hash}</pre>

####Regarding rebase conflicts
Rebase conflicts are the worst.  Somewhere in the middle of all the text that gets outputted when you encounter one of these monstrosities is useful information though, so don't panic too hard.

Open the conflicted files one at a time.  You'll see some arrows (>>>>>>>>>>>>>) indicating where the conflicts occured, with your version and the other branch separated by said crazy ass arrows.  

- Keep the lines you like
- Delete all the other crap
- Save the file
- Don't leave any extra whitespace

Boom!  When the files look good (I like to search for >>>), add your changes and continue the rebase.  Not bad, right?
<pre>
git add .
git reabse --continue
</pre>


####Rewriting history

You can rewrite history with an interactive rebase (but be careful with this one, **this is not a thing to do while sleepy**)

<pre>git rebase -i {reference branch}</pre>

If I type <code>git rebase -i origin/master</code>, it will pull up a window showing *all the commits I have on my local branch that differ from* <code>origin/master</code>.

From there, I can say which commits I want to keep as is ("pick"), which I want to reword the commit messages of, and which I want to squash into previous commits.  Doing this isn't necessary, but it's nice to be able to commit intermittently while working on a feature and ship the code as one commit when I'm ready.
