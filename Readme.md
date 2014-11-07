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

Just configure Bower to manage `~/.vim/bundle`, and set up Pathogen. For those already familiar with these tools:

```sh
cd ~/.vim
npm install -g bower                     # install bower via npm
echo '{"directory":"bundle"}' > .bowerrc # make bower put plugins in bundle/
echo "bundle/" >> .gitignore             # don't commit bundles
bower init                               # create bower.json
bower install --save tpope/vim-pathogen  # install pathogen
```

And add Pathogen to vimrc:

```vim
" ~/.vimrc
execute pathogen#infect()
syntax on
filetype plugin indent on
```

Set up git, and that's pretty much it. Skip to the next section.

### Step-by-step guide

**[Detailed instructions are available](Details.md)** for those new to Pathogen and Bower.

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
