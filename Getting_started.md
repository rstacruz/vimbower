# Detailed instructions

This guide is broken into these steps:

1. Install node.js and bower
2. Set up `~/.vim` under Git version control
3. Set up bower to manage `~/.vim/bundle`
4. Set up pathogen in `~/.vimrc`

## 1. Install node and bower

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

## 3. Set up bower

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

## 4. Set up pathogen

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

[pathogen]: https://github.com/tpope/vim-pathogen
[bower]: http://bower.io
[Homebrew]: http://brew.sh
[nvm]: https://github.com/creationix/nvm
[node.js]: http://nodejs.org
[pathogen-setup]: https://github.com/tpope/vim-pathogen#runtime-path-manipulation
[git]: http://git-scm.com
[github.com/vim-scripts]: https://github.com/vim-scripts
