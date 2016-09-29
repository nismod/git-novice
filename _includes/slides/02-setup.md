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

When we use Git on a new computer for the first time,
we need to configure a few things. Below are a few examples
of configurations we will set as we get started with Git:

*   our name and email address,
*   to colorize our output,
*   what our preferred text editor is,
*   and that we want to use these settings globally (i.e. for every project)

---

On a command line, Git commands are written as `git verb`,
where `verb` is what we actually want to do. So here is how
Dracula sets up his new laptop:

```bash
$ git config --global user.name "Vlad Dracula"
$ git config --global user.email "vlad@tran.sylvan.ia"
$ git config --global color.ui "auto"
```

---

Please use your own name and email address instead of Dracula's.
This user name and email will be associated with your subsequent Git activity,
which means that any changes pushed to
[GitHub](http://github.com/),
[BitBucket](http://bitbucket.org/),
[GitLab](http://gitlab.com/) or
another Git host server
in a later lesson will include this information.
If you are concerned about privacy, please review [GitHub's instructions for keeping your email address private][git-privacy].

---

He also has to set his favorite text editor, following this table:

| Editor             | Configuration command                            |
|:-------------------|:-------------------------------------------------|
|Atom | `$ git config --global core.editor "atom --wait"`|
| nano               | `$ git config --global core.editor "nano -w"`    |
| Text Wrangler      | `$ git config --global core.editor "edit -w"`    |
| Sublime Text (Mac) | `$ git config --global core.editor "subl -n -w"` |
| Sublime Text (Win, 32-bit install) | `$ git config --global core.editor "'c:/program files (x86)/sublime text 3/sublime_text.exe' -w"` |
| Sublime Text (Win, 64-bit install) | `$ git config --global core.editor "'c:/program files/sublime text 3/sublime_text.exe' -w"` |
| Notepad++ (Win, 32-bit install)    | `$ git config --global core.editor "'c:/program files (x86)/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"`|
| Notepad++ (Win, 64-bit install)    | `$ git config --global core.editor "'c:/program files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"`|
| Kate (Linux)       | `$ git config --global core.editor "kate"`       |
| Gedit (Linux)      | `$ git config --global core.editor "gedit -s -w"`   |
| Scratch (Linux)       | `$ git config --global core.editor "scratch-text-editor"`  |
| emacs              | `$ git config --global core.editor "emacs"`   |
| vim                | `$ git config --global core.editor "vim"`   |

It is possible to reconfigure the text editor for Git whenever you want to change it.

---

> ## Exiting Vim
>
> Note that `vim` is the default editor for for many programs, if you haven't used `vim` before and wish to exit a session, type `Esc` then `:q!` and `Enter`.
{: .callout}

---

The four commands we just ran above only need to be run once: the flag `--global` tells Git
to use the settings for every project, in your user account, on this computer.

You can check your settings at any time:

```bash
$ git config --list
```

You can change your configuration as many times as you want: just use the
same commands to choose another editor or update your email address.

---

## Git Help and Manual

Always remember that if you forget a git command, you can access the list of command by using -h and access the git manual by using --help :

```bash
$ git config -h
$ git config --help
```

[git-privacy]: https://help.github.com/articles/keeping-your-email-address-private/
