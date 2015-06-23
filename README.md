Brew-file
=========

[![Build Status](https://travis-ci.org/rcmdnk/homebrew-file.svg?branch=master)](https://travis-ci.org/rcmdnk/homebrew-file)
[![Coverage Status](https://coveralls.io/repos/rcmdnk/homebrew-file/badge.png?branch=master)](https://coveralls.io/r/rcmdnk/homebrew-file?branch=master)

Manager for packages of Homebrew, inspired by [Brewdler](https://github.com/andrew/brewdler)
(Renamed from brewall).

Brewfile dumped by [homebrew-brewdler](https://github.com/Homebrew/homebrew-brewdler)
can be used as input, too.


## Installation

By install script:

    $ curl -fsSL https://raw.github.com/rcmdnk/homebrew-file/install/install.sh |sh

This installs Homebrew if it has not been installed, too.

By Homebrew:

    $ brew install rcmdnk/file/brew-file

Or download `bin/brew-file` and put it in anywhere under `PATH` (e.g. `~/usr/bin/`)


Then, add following lines in you **.bashrc** or **.zshrc** to wrap `brew` command:

```sh
if [ -f $(brew --prefix)/etc/brew-wrap ];then
  source $(brew --prefix)/etc/brew-wrap
fi
```

**brew-wrap** wraps original `brew` command
for an automatic update of **Brewfile** when you execute
such `brew install` or `brew uninstall`.

## Use local Brewfile

By default, **Brewfile** is **/usr/local/Library/Brewfile**.

If you don't have **Brewfile**, first, do:

    $ brew file init

You can check your package list by:

    $ brew file edit

If you already have **Brewfile**, then copy it to 
**/usr/local/Library/Brewfile**
and install packages listed in **Brewfile** by:

    $ brew file install

After that, you need to do only normal `brew` commands, like `brew install` or `brew uninstall`.
After each commands, **Brewfile** is updated automatically
if you set `brew-wrap` as above.

When you get new Mac, copy 
**/usr/local/Library/Brewfile** to new Mac
and just do:

    $ brew file install

## use Dropbox (or any online storages) for Brewfile management

### Set Brewfile place

You can set the place of Brewfile by using environment variable like:

    export HOMEBREW_BREWFILE=~/Dropbox/Brewfile

Then, you can use Brewfile as same as original Brewfile place.

In this case, when you have new Mac,
set `HOMEBREW_BREWFILE` and synchronize the file with a online storage service,
then do:

    $ brew file install

If you are using multiple Mac in the same time,
it is good to have a cron job like

    30 12 * * * brew file update

This command installs new package which was installed in another Mac
at a lunch time (12:30) every day.

This command also does `brew update && brew upgrade`,
and removes packages not listed in `Brewfile`.

If you want to do only installing new package, then set as:

    30 12 * * * brew file install

## Use GitHub (or any git repository) for Brewfile management

### Setup a repository

First, create a repository with a file named **Brwefile**.

If you use GitHub, you can make it with brew-file:

    $ brew file set_repo

    Set repository, "non" for local Brewfile.
    <user>/<repo> for GitHub repository,
    or full path for the repository: 

Give a name like `rcmdnk/Brewfile` (will be recognized as a GitHub repository),
or such `git@github.com:rcmdnk/Brewfile`.

Then, initialize **Brewfile**:

    $ brew file init

### Setup new Mac with your Brewfile in the repository

Do:

    $ brew file set_repo

and give your repository name.

And install packages listed in **Brewfile** like:

    $ brew file install

### Brewfile management

To update the repository, do:

    $ brew file update

If you have set the repository,
this command does `git pull` and `git push`
in addition to such brew's `install`, `update`, `updgrade` and removing packages
described in online storages section.

It is good if you have such cron job like:

    30 12 * * * brew file update

The repository is updated at lunch time every day.

## More details

[README.DETAILS.md](README.DETAILS.md)
