---
# 5. Exploring History

Questions:
- How can I identify old versions of files?
- How do I review my changes?
- How can I recover old versions of files?

Objectives:
- Explain what the HEAD of a repository is and how to use it.
- Compare various versions of tracked files.
- Restore old versions of files.

Keypoints:
- `git diff` displays differences between commits.
- `git checkout` recovers old versions of files.

---

Let's make another small change:

```bash
notepad mars.txt
cat mars.txt
```

```
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
An ill-considered change
```

--

What changed?

```bash
git diff HEAD mars.txt
```

--

```
diff --git a/mars.txt b/mars.txt
index b36abfd..0848c8d 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1,3 +1,4 @@
 Cold and dry, but everything is my favorite color
 The two moons may be a problem for Wolfman
 But the Mummy will appreciate the lack of humidity
+An ill-considered change.
```

???

As we saw in the previous lesson, we can refer to commits by their
identifiers.  You can refer to the _most recent commit_ of the working
directory by using the identifier `HEAD`.

We've been adding one line at a time to `mars.txt`, so it's easy to track our
progress by looking, so let's do that using our `HEAD`s.  Before we start,
let's make a change to `mars.txt`.

which is the same as what you would get if you leave out `HEAD` (try it).

---

What about looking further back in time?

```bash
git diff HEAD~1 mars.txt
```

--

```
diff --git a/mars.txt b/mars.txt
index 315bf3a..b36abfd 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1,2 +1,3 @@
 Cold and dry, but everything is my favorite color
 The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
```

???

The real goodness in all this is when you can refer to previous commits.  We do
that by adding `~1` to refer to the commit one before `HEAD`.

If we want to see what we changed at different steps, we can use `git diff`
again, but with the notation `HEAD~1`, `HEAD~2`, and so on, to refer to old
commits.


--

```bash
git diff HEAD~2 mars.txt
```

--

```
diff --git a/mars.txt b/mars.txt
index df0654a..b36abfd 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1 +1,3 @@
 Cold and dry, but everything is my favorite color
+The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
```

???

In this way, we can build up a chain of commits.

The most recent end of the chain is referred to as `HEAD`;
we can refer to previous commits using the `~` notation,
so `HEAD~1` (pronounced "head minus one")
means "the previous commit",
while `HEAD~123` goes back 123 commits from where we are now.

---

We can refer to commits by id:

```bash
git diff f22b25e3233b4645dabd0d81e651fe074bd8e73b mars.txt
```

--

```
diff --git a/mars.txt b/mars.txt
index df0654a..b36abfd 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1 +1,3 @@
 Cold and dry, but everything is my favorite color
+The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
```

--

Or short id:

```bash
git diff f22b25e mars.txt
```

--

```
diff --git a/mars.txt b/mars.txt
index df0654a..b36abfd 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1 +1,3 @@
 Cold and dry, but everything is my favorite color
+The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
```

???

We can also refer to commits using
those long strings of digits and letters
that `git log` displays.
These are unique IDs for the changes,
and "unique" really does mean unique:
every change to any set of files on any computer
has a unique 40-character identifier.
Our first commit was given the ID
f22b25e3233b4645dabd0d81e651fe074bd8e73b,
so let's try this:


That's the right answer,
but typing out random 40-character strings is annoying,
so Git lets us use just the first few characters.

---

Let's suppose we accidentally overwrite our file:

```bash
notepad mars.txt
cat mars.txt
```

```
We will need to manufacture our own oxygen
```

--

`git status` now tells us that the file has been changed,
but those changes haven't been staged:

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

All right! So
we can save changes to files and see what we've changed—now how
can we restore older versions of things?

---

We can put things back the way they were
by using `git checkout`:

```bash
git checkout HEAD mars.txt
cat mars.txt
```

--

```
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
```

--

To go back even further, we can use a commit identifier instead:

```bash
git checkout f22b25e mars.txt
```

???

As you might guess from its name,
`git checkout` checks out (i.e., restores) an old version of a file.
In this case,
we're telling Git that we want to recover the version of the file recorded in `HEAD`,
which is the last saved commit.

---

## Note: Don't Lose Your HEAD

Above we used

```bash
git checkout f22b25e mars.txt
```

to revert mars.txt to its state after the commit f22b25e.

If you forget `mars.txt` in that command, Git will tell you that `You are in
'detached HEAD' state.`

In this state, you shouldn't make any changes.

You can fix this by reattaching your head using `git checkout master`

---

Remember to use the commit number that identifies the state of the repository
*before* the change we're trying to undo.

![Git Checkout](../fig/git-checkout.svg)

???

A common mistake is to use the number of
the commit in which we made the change we're trying to get rid of.
In the example below, we want to retrieve the state from before the most
recent commit (`HEAD~1`), which is commit `f22b25e`:

---

## Simplifying the Common Case

If you read the output of `git status` carefully,
you'll see that it includes this hint:

```
(use "git checkout -- <file>..." to discard changes in working directory)
```

Try deleting a file:

```bash
rm mars.txt
ls
```

--

Then put it back:

```bash
git checkout -- mars.txt
```

???

As it says,
`git checkout` without a version identifier restores files to the state saved in `HEAD`.
The double dash `--` is needed to separate the names of the files being recovered
from the command itself:
without it,
Git would try to use the name of the file as the commit identifier.


The fact that files can be reverted one by one
tends to change the way people organize their work.
If everything is in one large document,
it's hard (but not impossible) to undo changes to the introduction
without also undoing changes made later to the conclusion.
If the introduction and conclusion are stored in separate files,
on the other hand,
moving backward and forward in time becomes much easier.

---

## Explore and Summarize Histories

Recorded that the `git diff` command allow us to explore one specific file,
e.g. `git diff mars.txt`. We can apply the similar idea here.

```bash
git log mars.txt
```

--

Both `git diff` and `git log` are very useful and they summarize different part of the history for you.
Is that possible to combine both? Let's try the following:

```bash
git log --patch mars.txt
```

--

You should get a long list of output, and you should be able to see both commit
messages and the difference between each commit.

Question: What does the following command do?

```bash
git log --patch HEAD~3 HEAD~1 *.txt
```

???

Exploring history is an important part of git, often it is a challenge to find
the right commit ID, especially if the commit is from several months ago.

Imaging the `planets` project has more than 50 files.
You would like to find a commit with specific text in `mars.txt` is modified.
When you type `git log`, a very long list appeared,
How can you narrow down the search?

---

## Exercise: Recovering Older Versions of a File

Jennifer has made changes to the Python script that she has been working on for weeks, and the
modifications she made this morning "broke" the script and it no longer runs. She has spent
~ 1hr trying to fix it, with no luck...

Luckily, she has been keeping track of her project's versions using Git! Which commands below will
let her recover the last committed version of her Python script called
`data_cruncher.py`?

1. `$ git checkout HEAD`
2. `$ git checkout HEAD data_cruncher.py`
3. `$ git checkout HEAD~1 data_cruncher.py`
4. `$ git checkout <unique ID of last commit> data_cruncher.py`
5. Both 2 and 4

---

## Exercise: Reverting a Commit

Jennifer is collaborating on her Python script with her colleagues and
realises her last commit to the group repository is wrong and wants to
undo it.  Jennifer needs to undo correctly so everyone in the group
repository gets the correct change.

`git revert [wrong commit ID]` will make a new commit that undoes Jennifer's
previous commit. Below are the right steps and explanations for
Jennifer to use `git revert`. The first step is to look at the git history of
the project to find the commit ID

What is the missing command?

1. ...
2. Copy the ID (the first few characters of the ID, e.g. 0b1d055).
3. `git revert [commit ID]`
4. Type in the new commit message.
5. Save and close


---

## Exercise: Understanding Workflow and History

What is the output of `cat venus.txt` at the end of this set of commands?

```bash
cd planets
notepad venus.txt # add text: Venus is beautiful and full of love
git add venus.txt
notepad venus.txt # add text: Venus is too hot to be suitable as a base
git commit -m "comments on Venus as an unsuitable base"
git checkout HEAD venus.txt
cat venus.txt # print the contents of venus.txt to the screen
```

1. `Venus is too hot to be suitable as a base`
2. `Venus is beautiful and full of love`
3. Both lines: <br>`Venus is beautiful and full of love`<br>`Venus is too hot to be suitable as a base`
4. Error because you have changed venus.txt without committing the changes

---

## Exercise: Checking Understanding of `git diff`

Consider this command: `git diff HEAD~3 mars.txt`. What do you predict this command
will do if you execute it? What happens when you do execute it? Why?

Try another command, `git diff [ID] mars.txt`, where [ID] is replaced with
the unique identifier for your most recent commit. What do you think will happen,
and what does happen?


---

## Exercise: Getting Rid of Staged Changes

`git checkout` can be used to restore a previous commit when unstaged changes have
been made, but will it also work for changes that have been staged but not committed?

Make a change to `mars.txt`, `git add` that change, and use `git checkout` to see if
you can remove your change.

(Hint: read the output of `git status` after you've staged the change)

---

## Summary

- `git log` shows the history as a list of commits.
- `git diff` displays differences between commits.
- `git checkout` recovers old versions of files.
