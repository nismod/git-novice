---
# 2. Setting Up Git

Questions:
- How do I get set up to use Git?

Objectives:
- Configure `git` the first time it is used on a computer.
- Understand the meaning of the `--global` configuration flag.

Keypoints:
- Use `git config` to configure a user name, email address, editor, and other preferences once per machine.

---

## Git config

So here is how Dracula sets up his new laptop:

```bash
git config --global user.name "Vlad Dracula"
git config --global user.email "vlad@tran.sylvan.ia"
git config --global color.ui "auto"
```

* Please use your own name and email address instead of Dracula's
* This should be the same e-mail you used to sign up to Github

???

On a command line, Git commands are written as `git verb`,
where `verb` is what we actually want to do.

When we use Git on a new computer for the first time,
we need to configure a few things. Below are a few examples
of configurations we will set as we get started with Git:

*   our name and email address,
*   to colorize our output,
*   what our preferred text editor is,
*   and that we want to use these settings globally (i.e. for every project)

--

![Bela Lugosi as Dracula](../fig/dracula.jpg)

???

This user name and email will be associated with your subsequent Git activity,
which means that any changes pushed to
[GitHub](http://github.com/),
[BitBucket](http://bitbucket.org/),
[GitLab](http://gitlab.com/) or
another Git host server
in a later lesson will include this information.
If you are concerned about privacy, please review [GitHub's instructions for keeping your email address private][git-privacy].

---

## Text editor for git commit messages

Pick a text editor to use (we'll use `notepad` for the rest of this presentation):

| Command-line editors | Configuration command                          |
|:-------------------|:-------------------------------------------------|
| Notepad            | `git config --global core.editor notepad`
| nano               | `git config --global core.editor "nano -w"`    |
| vim                | `git config --global core.editor "vim"`        |

| Graphical editors  | Configuration command                            |
|:-------------------|:-------------------------------------------------|
| Atom               | `git config --global core.editor "atom --wait"`|
| Sublime Text (Mac) | `git config --global core.editor "subl -n -w"` |
| Sublime Text (Win, 64-bit) | `git config --global core.editor "'C:\Program files\sublime text 3\sublime_text.exe' -w"` |
| Visual Studio Code (Win)   | `git config --global core.editor "'C:\Program Files (x86)\Microsoft VS Code\bin\code' --wait"` |
| Notepad++ (Win, 64-bit)    | `git config --global core.editor "'C:\Program files\Notepad++\notepad++.exe' -multiInst -notabbar -nosession -noPlugin"`|


???

It is possible to reconfigure the text editor for Git whenever you want to change it.

## Exiting Vim

Note that `vim` is the default editor for for many programs, if you haven't used `vim` before and wish to exit a session, type `Esc` then `:q!` and `Enter`.

The four commands we just ran above only need to be run once: the flag `--global` tells Git
to use the settings for every project, in your user account, on this computer.

You can change your configuration as many times as you want: just use the
same commands to choose another editor or update your email address.

---

## Line endings

Windows and Mac/Linux handle line endings differently, and we want to be able to
share files between operating systems.

Git has a setting that _should_ let us set a sensible default.

On Windows, set it to `true`:

```bash
git config --global core.autocrlf true
```

On Mac or Linux, set it to `input`:

```bash
git config --global core.autocrlf input
```

---

## Checking config

You can check your settings at any time:

```bash
git config --list
```

## Git Help and Manual

```bash
git config -h
git config --help
```

[Git Docs](https://git-scm.com/doc)
- [online book](https://git-scm.com/book)
- [cheatsheet](https://services.github.com/kit/downloads/github-git-cheat-sheet.pdf)
- [full reference](https://git-scm.com/docs)

???

Always remember that if you forget a git command, you can access the list of command by using -h and access the git manual by using --help :

[git-privacy]: https://help.github.com/articles/keeping-your-email-address-private/

---

## Summary

* Use `git config` to setup configuration before using git on a new computer
* You only need to do this once
