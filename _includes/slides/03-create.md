---
# 3. Creating a Repository

Questions:
- Where does Git store information?

Objectives:
- Create a local Git repository.

Keypoints:
- `git init` initializes a repository.

---

Let's move to our home directory, create a directory for our work and then move into that directory:

```bash
$ cd
$ mkdir planets
$ cd planets
```

???

Once Git is configured,
we can start using it.

Then we tell Git to make `planets` a [repository]({{ page.root }}/reference/#repository)—a place where
Git can store versions of our files:

---

Make a git repository!

```bash
$ git init
```

Look to see if any files were added:

```bash
$ ls
```
What about hidden files?

```bash
$ ls -a
```

```
.	..	.git
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
$ git status
```

```bash
# On branch master
#
# Initial commit
#
nothing to commit (create/copy files and use "git add" to track)
```

???

We can check that everything is set up correctly
by asking git for a status update

---

## Places to Create Git Repositories

Dracula starts a new project, `moons`, related to his `planets` project.
Despite Wolfman's concerns, he enters the following sequence of commands to
create one Git repository inside another:

```bash
cd             # return to home directory
mkdir planets  # make a new directory planets
cd planets     # go into planets
git init       # make the planets directory a Git repository
mkdir moons    # make a sub-directory planets/moons
cd moons       # go into planets/moons
git init       # make the moons sub-directory a Git repository
```

Why is it a bad idea to do this?

How can Dracula undo his last `git init`?


