---
title: Github
category: Unix
order: 1
---

## How to avoid being asked passphrase each time I push to remote git

A way to solve this is with `ssh-agent` and `ssh-add`:

```bash
$ exec ssh-agent bash
$ ssh-add
Enter passphrase for ~/.ssh/id_rsa: 
```

After this the passphrase is saved for the current session. and won't be asked again.
