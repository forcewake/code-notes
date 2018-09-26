---
title: Git
category: Unix
order: 3
---

## How to avoid being asked passphrase each time I push to remote git

A way to solve this is with `ssh-agent` and `ssh-add`:

```bash
$ exec ssh-agent bash
$ ssh-add
Enter passphrase for ~/.ssh/id_rsa:
```

After this the passphrase is saved for the current session. and won't be asked again.

## How to git add only modified changes and ignore untracked files

> Answer from https://stackoverflow.com/a/7124760

You can do `git add -u` so that it will stage the modified and deleted files.

You can also do `git commit -a` to commit only the modified and deleted files.

Note that if you have Git of version before 2.0 and used `git add .`, then you would need to use `git add -u .`

or unix way

```bash
git ls-files --modified | xargs git add
```