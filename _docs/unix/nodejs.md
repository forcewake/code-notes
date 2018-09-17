---
title: Nodejs
category: Unix
order: 2
---

## Node.js on Debian and Ubuntu based Linux distributions

Node.js is available from the NodeSource Debian and Ubuntu binary distributions repository (formerly Chris Lea's Launchpad PPA). Support for this repository, along with its scripts, can be found on GitHub at nodesource/distributions.

``` bash
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt-get install -y nodejs
```

Alternatively, for Node.js 10:

``` bash
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt-get install -y nodejs
```

Optional: install build tools

To compile and install native addons from npm you may also need to install build tools:

``` bash
sudo apt-get install -y build-essential
```