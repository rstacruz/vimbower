# vimbower

You can use [bower], [pathogen] and [git] to manage your vim dependencies. This is a guide on setting this up and maintaining it.

*(Just to clear a misconception: this is NOT a vim plugin to use Bower from vim.)*

<br>

## Get started

Here are instructions to set up a new configuration from scratch. If you're migrating your existing setup, feel free to gloss over anything you've already done before.

 * Install node.js and bower
 * Set up `~/.vim` under Git version control
 * Set up bower to manage `~/.vim`
 * Set up pathogen in `~/.vimrc`

<br>
 
### 1. Install node and bower

Install [node.js]. In OS X, the preferred way to to use [Homebrew].

```sh
$ brew install nodejs          # osx
$ sudo apt-get install nodejs  # ubuntu
```

Install bower.

```sh
$ npm install -g bower
```

<br>

### 2. Set up git in *~/.vim*

You can manage your setup with Git. This allows you to share your vimfiles via GitHub, as well as be able to deploy your vim setup anywhere. Let's start by putting everything in `~/.vim` under version control.

```sh
$ mkdir ~/.vim
$ cd ~/.vim
```

##### Ignoring /bundle
Since `bundle/` (where your vim plugins lie) will be managed by bower, it's best you add this to your `.gitignore`.

```sh
$ echo "/bundle" >> .gitignore
```

##### Symlink ~/.vimrc
You might want to put your `~/.vimrc` in this directory as well and just symlink to it.

```sh
$ touch vimrc.vim
$ ln -s ~/.vim/vimrc.vim ~/.vimrc
```

##### Init and commit
Get Git started.

```sh
$ git init
$ git add -u .
$ git commit -m "Initial"
```

<br>

### 3. Set up bower

##### Create *.bowerrc*
Configure bower to use `bundle/` as its directory.

```sh
$ cd ~/.vim
$ echo '{"directory":"bundle"}' > .bowerrc
```

##### Create *bower.json*
Create a bower manifest (`bower.json`) in your `~/.vim`. Easiest way to do
this is to do *bower init* with defaults.

```sh
$ bower init
```

<br>

### 4. Set up pathogen

##### Install vim-pathogen
Install pathogen via bower.

```sh
$ bower install --save tpope/vim-pathogen
```

##### Setup pathogen
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

Assuming your setup is managed via Git, you can just check out into `~/.vim`. You can then run `bower install`.

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

* No easy way to lock versions yet.
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