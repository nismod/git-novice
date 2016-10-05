---
# 1. Concepts

Questions:
- What is version control and why should I use it?

Objectives:
- Understand the benefits of an automated version control system.
- Understand the basics of how Git works.

Keypoints:
- Version control is like an unlimited 'undo'.
- Version control also allows many people to work in parallel.

---

<div class="fit-image" style="background-image: url(../fig/phd101212s.png);"></div>

["Piled Higher and Deeper" by Jorge Cham, http://www.phdcomics.com](http://www.phdcomics.com/comics.php?f=1531)

---

## Sequential changes (_commits_)

*   Version control systems start with a base version of a document
*   They record a sequence of changes to this document

![Changes Are Saved Sequentially](../fig/play-changes.svg)

*   Each change is recorded as a `commit`
*   At any point, you can rewind - **undo** - or pick and choose which changes
    to keep

???

Version control systems start with a base version of the document and
then save just the changes you made at each step of the way. You can
think of it as a tape: if you rewind the tape and start at the base
document, then you can play back each change and end up with your
latest version.

---

## Concurrent changes (_branches_)

*  You can make independent sets of changes based on the
    same document

![Different Versions Can be Saved](../fig/versions.svg)

*   These result in the creation of a `branch`
*   Branches let you take risks

???

Once you think of changes as separate from the document itself, you
can then think about "playing back" different sets of changes onto the
base document and getting different versions of the document. For
example, two users can make independent sets of changes based on the
same document.

---

## Compiling a version (_merging_)

* Version control keeps track of different `branches`
* It also helps us `merge` different branches to make one master version

![Multiple Versions Can be Merged](../fig/merge.svg)

???

A version control system is a tool that keeps track of these changes for us and
helps us version and merge our files. It allows you to
decide which changes make up the next version, called a
[commit]({{ page.root }}/reference/#commit), and keeps useful metadata about them. The
complete history of commits for a particular project and their metadata make up
a [repository]({{ page.root }}/reference/#repository). Repositories can be kept in sync
across different computers facilitating collaboration among different people.

---

## A project keeps all changes in a _repository_

* The complete history of commits for a particular project and their metadata make up
a `repository`
* Git requires a two step process
    * `git add` to add files to a staging area
    * `git commit` to write this commit to the repository

![Stage changes to a repository](../fig/git-staging-area.svg)

## Note

* At no point are we copying files around
* We just record which changes have been since the last commit

???

## The Long History of Version Control Systems

Automated version control systems are nothing new.
Tools like RCS, CVS, or Subversion have been around since the early 1980s and are used by many large companies.
However, many of these are now becoming considered as legacy systems due to various limitations in their capabilities.
In particular, the more modern systems, such as Git and [Mercurial](http://swcarpentry.github.io/hg-novice/)
are *distributed*, meaning that they do not need a centralized server to host the repository.
These modern systems also include powerful merging tools that make it possible for multiple authors to work within
the same files concurrently.

---

## Exercise: Paper Writing

*   Imagine you drafted an excellent paragraph for a paper you are writing, but later ruin it. How would you retrieve
    the *excellent* version of your conclusion? Is it even possible?
*   Imagine you have 5 co-authors. How would you manage the changes and comments they make to your paper?
    If you use LibreOffice Writer or Microsoft Word, what happens if you accept changes made using the
    `Track Changes` option? Do you have a history of those changes?

---

## Exercise: System of Systems National Infrastructure Model

*   Imagine you're part of a consortium of several universities, as part of a
    research project to model national infrastructure systems over the next
    50-100 years. How would you approach developing a suite of models in
    parallel?
*   How might a history of the development process be useful?
*   How could you manage the development and integration of various models?

---

## Summary

Two main concepts:

*   A `commit` is a package of changes made to some files
*   A `repository` is a store of all the commits for a project
