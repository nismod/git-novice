---
# 4. Tracking Changes

Questions:
- How do I record changes in Git, and notes about my changes?
- How do I check the status of my version control repository?

Objectives:
- Explain where information is stored at each stage of Git commit workflow.

Keypoints:
- `git status` shows the status of a repository.
- Files can be stored in a project's working directory, the staging area and the local repository.
- `git add` puts files in the staging area.
- `git commit` saves the staged content as a new commit in the local repository.

---

## Here's what we are going to do...

![The Git Commit Workflow](../fig/git-staging-area.svg)

1.   Create a file
2.   `git add` to stage the file
3.   `git commit` to commit to the repository

---

## Let's do it...

Let's create a file called `mars.txt` that contains some notes
about the Red Planet's suitability as a base.

```bash
notepad mars.txt
```

Type the text below into the `mars.txt` file:

```
Cold and dry, but everything is my favorite colour
```

???

(We'll use `notepad` to edit the file;
you can use whatever editor you like.
In particular, this does not have to be the `core.editor` you set globally earlier.)

---


`mars.txt` now contains a single line, which we can see by running:

```bash
ls
```

--

```
mars.txt
```

--

```bash
cat mars.txt
```

--

```
Cold and dry, but everything is my favorite colour
```

---

If we check the status of our project again,
Git tells us that it's noticed the new file:

```bash
git status
```

--

```
On branch master

Initial commit

Untracked files:
   (use "git add <file>..." to include in what will be committed)

	mars.txt
nothing added to commit but untracked files present (use "git add" to track)
```

???

The "untracked files" message means that there's a file in the directory
that Git isn't keeping track of.

---

We can tell Git to track a file using `git add`:

```bash
git add mars.txt
```

and then check that the right thing happened:

```bash
git status
```

--

```
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   mars.txt

```

???

Git now knows that it's supposed to keep track of `mars.txt`,
but it hasn't recorded these changes as a commit yet.


---

Then we can record these changes as a commit:

```bash
git commit
```

This should open the text editor we configured earlier.

Type a commit message:

```
Start notes on Mars as a base
```


Then save it, and close the message file in the editor.

--

```
[master (root-commit) f22b25e] Start notes on Mars as a base
 1 file changed, 1 insertion(+)
 create mode 100644 mars.txt
```

--

If we run `git status` now:

```bash
git status
```

--

```
On branch master
nothing to commit, working directory clean
```

???
To get it to do that,
we need to run one more command, `git commit`.

When we run `git commit`,
Git takes everything we have told it to save by using `git add`
and stores a copy permanently inside the special `.git` directory.
This permanent copy is called a [commit]({{ page.root }}/reference/#commit)
(or [revision]({{ page.root }}/reference/#revision)) and its short identifier is `f22b25e`
(Your commit may have another identifier.)

We use the `-m` flag (for "message")
to record a short, descriptive, and specific comment that will help us remember later on what we did and why.
If we just run `git commit` without the `-m` option,
Git will launch `notepad` (or whatever other editor we configured as `core.editor`)
so that we can write a longer message.

[Good commit messages][commit-messages] start with a brief (<50 characters) summary of
changes made in the commit.  If you want to go into more detail, add
a blank line between the summary line and your additional notes.

Then run git status again,
it tells us everything is up to date.

---

If we want to know what we've done recently,
we can ask Git to show us the project's history using `git log`:

```bash
git log
```

--

```
commit f22b25e3233b4645dabd0d81e651fe074bd8e73b
Author: Vlad Dracula <vlad@tran.sylvan.ia>
Date:   Thu Aug 22 09:51:46 2013 -0400

    Start notes on Mars as a base
```

???

`git log` lists all commits  made to a repository in reverse chronological order.
The listing for each commit includes
the commit's full identifier
(which starts with the same characters as
the short identifier printed by the `git commit` command earlier),
the commit's author,
when it was created,
and the log message Git was given when the commit was created.

## Where Are My Changes?

If we run `ls` at this point, we will still see just one file called `mars.txt`.
That's because Git saves information about files' history
in the special `.git` directory mentioned earlier
so that our filesystem doesn't become cluttered
(and so that we can't accidentally edit or delete an old version).

---

Now suppose Dracula adds more information to the file.

```bash
notepad mars.txt
cat mars.txt
```

--

```
Cold and dry, but everything is my favorite colour
The two moons may be a problem for werewolves
```

--

When we run `git status` now,
it tells us that a file it already knows about has been modified:

```bash
git status
```

--

```
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   mars.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

???

(Again, we'll edit with `notepad` and then `cat` the file to show its contents;
you may use a different editor, and don't need to `cat`.)

The last line is the key phrase:
"no changes added to commit".
We have changed this file,
but we haven't told Git we will want to save those changes
(which we do with `git add`)
nor have we saved them (which we do with `git commit`).
So let's do that now.

---

What changed?

```bash
git diff
```

--

```
diff --git a/mars.txt b/mars.txt
index df0654a..315bf3a 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1 +1,2 @@
 Cold and dry, but everything is my favorite colour
+The two moons may be a problem for Wolfman
```

???

It is good practice to always review
our changes before saving them. We do this using `git diff`.
This shows us the differences between the current state
of the file and the most recently saved version:


The output is cryptic because
it is actually a series of commands for tools like editors and `patch`
telling them how to reconstruct one file given the other.
If we break it down into pieces:

1.  The first line tells us that Git is producing output similar to the Unix `diff` command
    comparing the old and new versions of the file.
2.  The second line tells exactly which versions of the file
    Git is comparing;
    `df0654a` and `315bf3a` are unique computer-generated labels for those versions.
3.  The third and fourth lines once again show the name of the file being changed.
4.  The remaining lines are the most interesting, they show us the actual differences
    and the lines on which they occur.
    In particular,
    the `+` marker in the first column shows where we added a line.


---
After reviewing our change, it's time to commit it:

```bash
git commit -m "Add concerns about effects of Mars' moons on werewolves"
git status
```

Note: `git commit -m` lets us write a short message for the commit right on the
command line, without opening a separate text editor.

--

```
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   mars.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

--

Whoops! Git won't commit because we didn't use `git add` first.

--

```bash
git add mars.txt
git commit -m "Add concerns about effects of Mars' moons on werewolves"
```

--

```
[master 34961b1] Add concerns about effects of Mars' moons on werewolves
 1 file changed, 1 insertion(+)
```

???

Git insists that we add files to the set we want to commit
before actually committing anything. This allows us to commit our
changes in stages and capture changes in logical portions rather than
only large batches.
For example,
suppose we're adding a few citations to our supervisor's work
to our thesis.
We might want to commit those additions,
and the corresponding addition to the bibliography,
but *not* commit the work we're doing on the conclusion
(which we haven't finished yet).

To allow for this,
Git has a special *staging area*
where it keeps track of things that have been added to
the current [change set]({{ page.root }}/reference/#change-set)
but not yet committed.

---

Let's run through the process again, from (1) making a change in the working
directory to (2) the staging area, to (3) commiting.

```bash
notepad mars.txt
cat mars.txt
```

```
Cold and dry, but everything is my favorite colour
The two moons may be a problem for werewolves
But the Mummy will appreciate the lack of humidity
```

--

What changed?

```bash
git diff
```

--

```
diff --git a/mars.txt b/mars.txt
index 315bf3a..b36abfd 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1,2 +1,3 @@
 Cold and dry, but everything is my favorite colour
 The two moons may be a problem for werewolves
+But the Mummy will appreciate the lack of humidity
```

---

Add our change to the staging area:

```bash
git add mars.txt
git diff
```

--

(No output from `git diff`.)

--

What's the difference between the staging area and what has already been
committed?

```bash
git diff --staged
```

--

```
diff --git a/mars.txt b/mars.txt
index 315bf3a..b36abfd 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1,2 +1,3 @@
 Cold and dry, but everything is my favorite colour
 The two moons may be a problem for werewolves
+But the Mummy will appreciate the lack of humidity
```

???

There is no output:
as far as Git can tell,
there's no difference between what it's been asked to save permanently
and what's currently in the directory.
However, if we add the `--staged` flag...

So far, so good:
we've added one line to the end of the file
(shown with a `+` in the first column).
Now let's put that change in the staging area
and see what `git diff` reports:

## Staging Area

If you think of Git as taking snapshots of changes over the life of a project,
`git add` specifies *what* will go in a snapshot
(putting things in the staging area),
and `git commit` then *actually takes* the snapshot, and
makes a permanent record of it (as a commit).
If you don't have anything staged when you type `git commit`,
Git will prompt you to use `git commit -a` or `git commit --all`,
which is kind of like gathering *everyone* for the picture!
However, it's almost always better to
explicitly add things to the staging area, because you might
commit changes you forgot you made. (Going back to snapshots,
you might get the extra with incomplete makeup walking on
the stage for the snapshot because you used `-a`!)
Try to stage things manually,
or you might find yourself searching for "git undo commit" more
than you would like!

![The Git Staging Area](../fig/git-staging-area.svg)

Let's watch as our changes to a file move from our editor
to the staging area
and into long-term storage.
First,
we'll add another line to the file:

it shows us the difference between
the last committed change
and what's in the staging area.

---

And finally, committing:

```bash
git commit -m "Discuss concerns about Mars' climate for Mummy"
```

--

```
[master 005937f] Discuss concerns about Mars' climate for Mummy
 1 file changed, 1 insertion(+)
```

--

Check our status:

```bash
git status
```

--

```
On branch master
nothing to commit, working directory clean
```

--

All done!

---

To look at the history of what we've done so far:

```bash
git log
```

--

```
commit 005937fbe2a98fb83f0ade869025dc2636b4dad5
Author: Vlad Dracula <vlad@tran.sylvan.ia>
Date:   Thu Aug 22 10:14:07 2013 -0400

    Discuss concerns about Mars' climate for Mummy

commit 34961b159c27df3b475cfe4415d94a6d1fcd064d
Author: Vlad Dracula <vlad@tran.sylvan.ia>
Date:   Thu Aug 22 10:07:21 2013 -0400

    Add concerns about effects of Mars' moons on werewolves

commit f22b25e3233b4645dabd0d81e651fe074bd8e73b
Author: Vlad Dracula <vlad@tran.sylvan.ia>
Date:   Thu Aug 22 09:51:46 2013 -0400

    Start notes on Mars as a base
```

???

## Paging the Log

When the output of `git log` is too long to fit in your screen,
`git` uses a program to split it into pages of the size of your screen.
When this "pager" is called, you will notice that the last line in your
screen is a `:`, instead of your usual prompt.

*   To get out of the pager, press `q`.
*   To move to the next page, press the space bar.
*   To search for `some_word` in all pages, type `/some_word`
    and navigate throught matches pressing `n`.

---

To look at the latest commit:

```bash
git log -1
```

--

```
commit 005937fbe2a98fb83f0ade869025dc2636b4dad5
Author: Vlad Dracula <vlad@tran.sylvan.ia>
Date:   Thu Aug 22 10:14:07 2013 -0400

    Discuss concerns about Mars' climate for Mummy
```

???

## Limit Log Size

To avoid that `git log` cover all your terminal screen you can
limit the numbers of commit that Git will list by using `-N`
where `N` is the number of commits that you want to receive
the information. For example, if you only want the information
from the last commit you can use

--

Or ask for less information:

```bash
git log --oneline
```

--

```
* 005937f Thoughts about the climate
* 34961b1 Concerns about Mars's moons on my furry friend
* f22b25e Starting to think about Mars
```

???

Or try lots more options:

```bash
git log --oneline --graph --all --decorate
```

```
* 005937f Thoughts about the climate (HEAD, master)
* 34961b1 Concerns about Mars's moons on my furry friend
* f22b25e Starting to think about Mars
```

???

## Minimum info

 You can also reduce the quantity of information using the
`--oneline` option:

You can also combine the `--oneline` options with others. One useful
combination is

To recap, when we want to add changes to our repository,
we first need to add the changed files to the staging area
(`git add`) and then commit the staged changes to the
repository (`git commit`):

---

## Recap: Modify, Stage, Commit

![The Git Commit Workflow](../fig/git-committing.svg)

---

## Exercise: Choosing a Commit Message
Which of the following commit messages would be most appropriate for the
last commit made to `mars.txt`?

1. "Changes"
2. "Added line 'But the Mummy will appreciate the lack of humidity' to mars.txt"
3. "Discuss effects of Mars' climate on the Mummy"

--

## Suggested solution
Answer 1 is not descriptive enough,
and answer 2 is too descriptive and redundant,
but answer 3 is good: short but descriptive.

With larger changes, more detail might be helpful - commit messages
often have a short first line to summarise the change, and any further
details can be written as necessary.

---

## Exercise: Committing Changes to Git
Which command(s) below would save the changes of `myfile.txt`
to my local Git repository?
1. `git commit -m "my recent changes"`
2. `git init myfile.txt`<br>`git commit -m "my recent changes"`
3. `git add myfile.txt`<br>`git commit -m "my recent changes"`
4. `git commit -m myfile.txt "my recent changes"`

--

## Solution
1. Would only create a commit if files have already been staged.
2. Would try to create a new repository.
3. Is correct: first add the file to the staging area, then commit.
4. Would try to commit a file "my recent changes" with the message myfile.txt.

---

## Exercise: Committing Multiple Files
The staging area can hold changes from any number of files
that you want to commit as a single snapshot.

1. Add some text to `mars.txt` noting your decision
to consider Venus as a base
2. Create a new file `venus.txt` with your initial thoughts
about Venus as a base for you and your friends
3. Add changes from both files to the staging area,
and commit those changes.

---

## Solution

```bash
notepad mars.txt
cat mars.txt
```

```
Maybe I should start with a base on Venus.
```

```bash
notepad venus.txt
cat venus.txt
```

```
Venus is a nice planet and I definitely should consider it as a base.
```

---

Now you can add both files to the staging area. We can do that in one line:

```bash
git add mars.txt venus.txt
```

Or with multiple commands:

```bash
git add mars.txt
git add venus.txt
```

--

Now the files are ready to commit. You can check that using `git status`. If you are ready to commit use:

```bash
git commit -m "Wrote down my plans to start a base on Venus"
```

--

```
[master cc127c2]
Wrote down my plans to start a base on venus
2 files changed, 2 insertions(+)
```

???

`git commit --author="Vlad Dracula <vlad@tran.sylvan.ia>"`

For each of the commits you have done, Git stored your name twice.
You are named as the author and as the committer. You can observe
that by telling Git to show you more information about your last
commits:

[commit-messages]: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html

---

## Summary

- `git status` shows the status of a repository.
- Files can be stored in a project's working directory, the staging area and the local repository.
- `git add` puts files in the staging area.
- `git commit` saves the staged content as a new commit in the local repository.
