# macOS basic Setup

## Introduction

This document contains a full installation guide to setup all tools with a config file in this repository to a clean macOS install.

## Cloning to new Device

Before starting to clone this repository we have to make sure, that the existing config files do not collide. The easiest way to archive this is by moving the existing configs.

```shell
mv .config .config_back
mv .tmux.conf .tmux.conf_back
mv .zshrc .zshrc_back
```

This way at the end, the not needed files can be easily removed by executing the following

```shell
rm -rf **/**/*_back
```

Bfore starting, make sure that the ssh key is added to the github account.

To make things easier, make sure to load this alias in the running evironment and add the bare repo to the .gitignore file

```shell
alias config='/usr/bin/git --git-dir=$HOME/Dev/dotfiles --work-tree=$HOME'
echo "~/Dev/dotfiles" >> .gitignore
```

Once everything is ready, we can create the directory to store the bare repository and clone our bare repository into there

```shell
mkdir -p ~/Dev/dotfiles
git clone --bare <git-repo-url> $HOME/Dev/dotfiles
```

Once the bare rpository is on the machine, we can use the alias described above, to pull the files down

```shell
config checkout
```

If you get any error message while cloning because of existing files, make sure to move them as described above

To finish the migration, set the option to show untracked files to disabled, as this would otherwise list all files in the home directory

```shell
config config --local status.showUntrackedFiles no
```

For full documentation, visit this [Bitbucket Blog](https://www.atlassian.com/git/tutorials/dotfiles)
