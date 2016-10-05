---
# 10. Communication

Questions:
- How do I communicate with other groups?
- How do I keep track of bugs and ideas?

Objectives:
- Explain the principle of issue tracking
- Introduce git flow, Slack and resources

Keypoints:
- Issues trackers help keep track of bugs and ideas
- Git flow is one way to organise multiple modellers who collaborate on a code base
---

## Communications

Discuss problems in our Slack team `nismod.slack.com`:

- Slack has channels
    - `#helpme` for help on programming, version control etc.
    - `#general` for general discussion
    - `#modelling` for technical discussion of sector models and integration
    - `#development` is mainly filled with notifications from Github
    - `#random` is for anything else
- Integrations with Skype, Github etc.
- Upload files, add snippets of text
- A record of our discussion and decisions

---

## Issues are found in the github repository

![Github repo](../fig/github-issue.png)

---

## The issues tab lists all of the issues

![Issues Page](../fig/github-issue-clicked.png)

---

## Create an issue to record a bug, feature idea or to ask a question

![Create an Issue](../fig/github-issue-enter.png)

## Tag colleagues, add labels, assign someone to work on the bug

???

- Useful descriptive title
- BUG: Steps required to recreate the problem
- FEATURE:

---

## Each issue is referenced with an id number

![Create an Issue](../fig/github-issue-numbered.png)

Reference issues in commit messages

```bash
git commit -m "Fixes bug #25. Added float to variable"
```

---

## Practical: Use issues as part of a work flow

With your neighbour:

1. Create an issue
1. Give it a descriptive title
1. Write the idea in the description
1. Add an appropriate tag
1. Assign it to a milestone or project
1. Assign the issue to your colleague

Swap:

1. Implement the idea
1. Add a reference to the issue in a commit message
1. Submit a pull request

---

# Feedback

- Alternative positive and negative feedback
- What should we cover next?
