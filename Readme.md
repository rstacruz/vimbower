# vimbower

You can use [bower], [pathogen] and [git] to manage your vim dependencies. This is a guide on maintaining a vim setup with these tools.

*(Just to clear a misconception: this is NOT a vim plugin to use Bower from vim.)*

<br>

## What?

[Bower] is a package manager for frontend projects. It doesn't really care what's in a package, it just happens to be used for JS and CSS most of the time. In reality, it's a package manager for *anything*.

[Pathogen] is a small vim plugin to allow you to put vim plugins into `~/.vim/bundle/`.

Vim plugins are typically published in GitHub. Bower fetches from GitHub. Perfect.

Here's how you can use Bower to manage your `~/.vim/bundle`.

<br>

## Get started

Here are instructions to set up a new configuration from scratch. If you're migrating your existing setup, feel free to gloss over anything you've already done before.

 * Install node.js and bower
 * Set up `~/.vim` under Git version control
 * Set up bower to manage `~/.vim`
 * Set up pathogen in `~/.vimrc`

<br>
 
### 1. Install node and bower

Install [node.js]. In OS X, the preferred way is to use [Homebrew].

```sh
$ brew install nodejs          # osx
$ sudo apt-get install nodejs  # ubuntu
```

Install bower.

```sh
$ npm install -g bower
```

<br>

## 2. Set up git in *~/.vim*

__Make ~/.vim__:<br>
You can manage your setup with Git. This allows you to share your vimfiles via GitHub, as well as be able to deploy your vim setup anywhere. Let's start by putting everything in `~/.vim` under version control.

```sh
$ mkdir ~/.vim
$ cd ~/.vim
```

__Ignoring /bundle:__<br>
Since `bundle/` (where your vim plugins lie) will be managed by bower, it's best you add this to your `.gitignore`.

```sh
$ echo "/bundle" >> .gitignore
```

__Symlink ~/.vimrc:__<br>
You might want to put your `~/.vimrc` in this directory as well and just symlink to it.

```sh
$ touch vimrc.vim
$ ln -s ~/.vim/vimrc.vim ~/.vimrc
```

__Init and commit:__<br>
Get Git started.

```sh
$ git init
$ git add -u .
$ git commit -m "Initial"
```

<br>

### 3. Set up bower

__Create *.bowerrc*:__<br>
Configure bower to put vim plugins into `bundle/`.

```sh
$ cd ~/.vim
$ echo '{"directory":"bundle"}' > .bowerrc
```

__Create *bower.json*__:<br>
Create a bower manifest (`bower.json`) in your `~/.vim`. The easiest way to do this is to run *bower init* with defaults.

```sh
$ bower init
```

<br>

### 4. Set up pathogen

__Install vim-pathogen:__<br>
Install pathogen via bower.

```sh
$ bower install --save tpope/vim-pathogen
```

__Setup pathogen:__<br>
Set up pathogen in your `~/.vimrc`. Here's an example vimrc from [Pathogen's documentation][pathogen-setup].

```vim
execute pathogen#infect()
syntax on
filetype plugin indent on
```

<br>

----

<br>

## Working on your setup

You can add and update packages using Bower.

<br>

### Adding packages

Use bower to install packages. Adding `--save` will automatically save it to `bower.json`.

```sh
$ bower install --save tpope/vim-sensible
```

By default, bower will only fetch the latest semver tag (eg, `0.3.0`). This is usually a good thing. However, some plugins don't maintain their tags (example: [nerdtree] doesn't update with new versions). You can add `#master` to ensure that bower fetches from master.

```sh
$ bower install --save scrooloose/nerdtree#master
```

<br>

### Installing from vim.org/scripts

Scripts in the vim repository are available in GitHub under [github.com/vim-scripts].

```sh
$ bower install --save vim-scripts/indenthtml.vim
```

<br>

### Removing packages

```sh
$ bower uninstall --save vim-haml
```

<br>

### Updating packages

This will check for new versions.

```sh
$ bower update
```

<br>

### Deploying to a different system

Assuming your setup is managed via Git, you can just clone your repo into `~/.vim`. You can then run `bower install`.

```sh
$ rm -rf ~/.vim   # ...careful!

$ git clone https://github.com/rstacruz/vimfiles.git ~/.vim
$ ln -s ~/.vim/vimrc.vim ~/.vimrc

$ cd ~/.vim
$ bower install
```

<br>

----

<br>

## Caveats

* No easy way to lock versions until Bower implements [shrinkwrapping][bower#505].
* You'll need bower on the system you want to deploy to.

Until [bower#505] is resolved in Bower 2.0, these caveats are mitigated by a simple script: **[here](https://github.com/rstacruz/vimfiles/blob/master/bin/lock)**

<br>

----

<br>

## Examples

* [rstacruz/vimfiles](http://github.com/rstacruz/vimfiles)

[pathogen]: https://github.com/tpope/vim-pathogen
[bower]: http://bower.io
[Homebrew]: http://brew.sh
[nvm]: https://github.com/creationix/nvm
[node.js]: http://nodejs.org
[pathogen-setup]: https://github.com/tpope/vim-pathogen#runtime-path-manipulation
[git]: http://git-scm.com
[nerdtree]: https://github.com/scrooloose/nerdtree/releases
[bower#505]: https://github.com/bower/bower/issues/505
[github.com/vim-scripts]: https://github.com/vim-scripts
