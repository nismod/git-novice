---
# 3. Creating a Repository

Questions:
- Where does Git store information?

Objectives:
- Create a local Git repository.

Keypoints:
- `git init` initializes a repository.

---

## Starting a project

Imagine we're starting a new project to establish a space base, possibly on
mars.

Let's move to our home directory, create a directory for our work and then move into that directory:

```bash
cd
mkdir planets
cd planets
```

## Note

Your 'home directory' on Windows is something like `C:\Users\Dracula\`

???

Once Git is configured,
we can start using it.

Then we tell Git to make `planets` a [repository]({{ page.root }}/reference/#repository)—a place where
Git can store versions of our files:

---

Make a git repository!

```bash
git init
```

--

Look to see if any files were added:

```bash
ls
```

--

What about hidden files or folders?

```bash
ls -a
```

--

```
.	..	.git
```

--

We could ask for more details from `ls`:

```bash
ls -al
```

???

But if we add the `-a` flag to show everything,
we can see that Git has created a hidden directory within `planets` called `.git`:

Git stores information about the project in this special sub-directory.
If we ever delete it,
we will lose the project's history.

---

Let's ask Git to tell us the status of our project:

```bash
git status
```

--

```bash
On branch master

Initial commit

nothing to commit (create/copy files and use "git add" to track)
```

???

We can check that everything is set up correctly
by asking git for a status update

---

## Exercise: Places to Create Git Repositories

Think about starting a new project, `moons`, related to our `planets` project.

```bash
cd             # return to home directory
mkdir planets  # make a new directory planets
cd planets     # go into planets
git init       # make the planets directory a Git repository
mkdir moons    # make a sub-directory planets/moons
cd moons       # go into planets/moons
git init       # make the moons sub-directory a Git repository
```

Why might it be a bad idea to do this?

How can we undo the last `git init`?

## Note

The commands above make the following directory structure:

```
~/planets/
~/planets/.git
~/planets/moons
~/planets/moons/.git
```

---

## Summary

Use `git init` to initialise a repository
