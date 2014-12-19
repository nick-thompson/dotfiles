# Dotfiles

My OS X dotfiles.

## How to install

The installation step requires the [XCode Command Line
Tools](https://developer.apple.com/downloads) and may overwrite existing
dotfiles in your HOME and `.vim` directories.

```bash
git clone git@github.com:nick-thompson/dotfiles.git ~/.dotfiles
~/.dotfiles/bin/dotfiles
```

## How to update

You should run the update when:

* You make a change to `~/.dotfiles/git/gitconfig` (the only file that is
  copied rather than symlinked).
* You want to pull changes from the remote repository.
* You want to update Homebrew formulae.

Run the dotfiles command:

```bash
$ dotfiles
```

Options:

<table>
    <tr>
        <td><code>-h</code>, <code>--help</code></td>
        <td>Help</td>
    </tr>
    <tr>
        <td><code>--no-brew</code></td>
        <td>Suppress attempts to install/update Homebrew</td>
    </tr>
    <tr>
        <td><code>--no-update</code></td>
        <td>Suppress pulling from the remote repository</td>
    </tr>
</table>


## Features

### Automatic software installation

Homebrew formulae:

* GNU core utilities
* [git](http://git-scm.com/)
* [bash-completion](http://bash-completion.alioth.debian.org/)
* jpeg
* [optipng](http://optipng.sourceforge.net/)
* [phantomjs](http://phantomjs.org/)
* [tree](http://mama.indstate.edu/users/ice/tree/)
* [wget](http://www.gnu.org/software/wget/)
* [mosh](http://mosh.mit.edu/)

N.B. If your pre-existing Homebrew installation is not in `usr/local` then you
must add your custom location's `bin` to the PATH in `.bash_profile.local`:

```bash
# Add `brew` command's custom location to PATH
PATH="/opt/acme/bin:$PATH"
```

### Local and private configurations

Any special-case Vim directives local to a machine should be stored in a
`.vimrc.local` file on that machine. The directives will then be automatically
imported into your master `.vimrc`.

Any private and custom commands should be stored in a `~/.bash_profile.local`
file. Any commands included in this file will not be under version control or
committed to a public repository. If `~/.bash_profile.local` exists, it will be
sourced for inclusion in `bash_profile`.

Here is an example `~/.bash_profile.local`:

```bash
# PATH exports
PATH=$PATH:~/.gem/ruby/1.8/bin
export PATH

# Git credentials
# Not under version control to prevent people from
# accidentally committing with your details
GIT_AUTHOR_NAME="Nicolas Gallagher"
GIT_AUTHOR_EMAIL="nicolas@example.com"
GIT_COMMITTER_NAME="$GIT_AUTHOR_NAME"
GIT_COMMITTER_EMAIL="$GIT_AUTHOR_EMAIL"
# Set the credentials (modifies ~/.gitconfig)
git config --global user.name "$GIT_AUTHOR_NAME"
git config --global user.email "$GIT_AUTHOR_EMAIL"
```

The `git/gitconfig` file is copied to `~/.gitconfig`, so any private git
configuration specified in `~/.bash_profile.local` will not be committed to
your dotfiles repository.

## Vim

Vim plugins are managed with [Vundle](https://github.com/gmarik/vundle). With
any updates or additional plugins, run :BundleInstall from inside Vim.
