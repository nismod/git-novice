---
# 8. Collaborating

Questions:
- How can I use version control to collaborate with other people?

Objectives:
- Clone a remote repository.
- Collaborate pushing to a common repository.

Keypoints:
- `git clone` copies a remote repository to create a local repository with a remote called `origin` automatically set up.

---

## Setup in Pairs

* The Owner needs to give the Collaborator access.
* On GitHub
    * click the _Settings_ button on the right of the screen,
    * then select _Collaborators_  and enter your partner's username.

![Adding Collaborators on GitHub](../fig/github-add-collaborators.png)

To accept access to the Owner's repo, the Collaborator
needs to go to [https://github.com/notifications](https://github.com/notifications).
Once there she can accept access to the Owner's repo.

???

* For the next step, get into pairs.
* One person will be the "Owner" and the other
will be the "Collaborator".
* The goal is that the Collaborator add changes into
the Owner's repository.
* We will switch roles at the end, so both persons will
play Owner and Collaborator.

---

## Cloning a repository

Next, the Collaborator needs to download a copy of the Owner's repository to her
 machine. This is called "cloning a repo". To clone the Owner's repo into
her `Desktop` folder, the Collaborator enters:

```bash
git clone https://github.com/vlad/planets.git ~/Desktop/vlad-planets
```

Replace `vlad` with the Owner's username.

---

<img alt="After Creating Clone of Repository" src="../fig/github-collaboration.svg" style="width: 80%;" />

---

The Collaborator can now make a change in her clone of the Owner's repository,
exactly the same way as we've been doing before:

```bash
cd ~/Desktop/vlad-planets
notepad pluto.txt
cat pluto.txt
```

```
It is so a planet!
```

--

```bash
git add pluto.txt
git commit -m "Some notes about Pluto"
```

```
 1 file changed, 1 insertion(+)
 create mode 100644 pluto.txt
```

---

Then push the change to the Owner's repository on GitHub:

```bash
git push origin master
```

```
Counting objects: 4, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 306 bytes, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/vlad/planets.git
   9272da5..29aba7c  master -master
```

Note that we didn't have to create a remote called `origin`: Git uses this
name by default when we clone a repository.  (This is why `origin` was a
sensible choice earlier when we were setting up remotes by hand.)

---

Take a look to the Owner's repository on its GitHub website now (maybe you need
to refresh your browser.) You should be able to see the new commit made by the
Collaborator.

To download the Collaborator's changes from GitHub, the Owner now enters:

```bash
git pull origin master
```

```
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0)
Unpacking objects: 100% (3/3), done.
From https://github.com/vlad/planets
 * branch            master     -FETCH_HEAD
Updating 9272da5..29aba7c
Fast-forward
 pluto.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 pluto.txt
```

Now the three repositories (Owner's local, Collaborator's local, and Owner's on
GitHub) are back in sync.

---

## A Basic Collaborative Workflow

In practice, it is good to be sure that you have an updated version of the
repository you are collaborating on, so you should `git pull` before making
our changes. The basic collaborative workflow would be:

* update your local repo with `git pull origin master`,
* make your changes and stage them with `git add`,
* commit your changes with `git commit -m`
* upload the changes to GitHub with `git push origin master`

It is better to make many commits with smaller changes rather than
of one commit with massive changes: small commits are easier to
read and review.


## Switch Roles and Repeat

Switch roles and repeat the whole process.

---

## Discuss: Review Changes

The Owner pushes commits to the repository without giving any information
to the Collaborator.

How can the Collaborator find out what has changed with
command line?

How can they find out what changed on GitHub?

---

## Exercise: Comment Changes in GitHub

The Collaborator has some questions about one line change made by the Owner and
has some suggestions to propose.

With GitHub, it is possible to comment the diff of a commit. Over the line of
code to comment, a blue comment icon appears to open a comment window.

The Collaborator posts their comments and suggestions using the GitHub interface.

---

## Discuss: Version History, Backup, and Version Control

Some backup software can keep a history of the versions of your files. They also
allows you to recover specific versions.

How is this functionality different from version control?

What are some of the benifits of using version control, Git and Github?

---

## Summary

- `git clone` copies a remote repository to create a local repository with a remote called `origin` automatically set up.
