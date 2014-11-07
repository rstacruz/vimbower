# Maintaining packages

Use bower's commands to add, remove, or update packages.

<br>

## Adding packages

Use bower to install packages. Adding `--save` will automatically save it to `bower.json`.

```sh
$ bower install --save tpope/vim-sensible
```

By default, bower will only fetch the latest semver tag (eg, `0.3.0`). This is usually a good thing. However, some plugins don't maintain their tags (example: [nerdtree] doesn't update with new versions). You can add `#master` to ensure that bower fetches from master.

```sh
$ bower install --save scrooloose/nerdtree#master
```

<br>

## Installing from vim.org/scripts

Scripts in the vim repository are available in GitHub under [github.com/vim-scripts].

```sh
$ bower install --save vim-scripts/indenthtml.vim
```

<br>

## Removing packages

```sh
$ bower uninstall --save vim-haml
```

<br>

## Updating packages

This will check for new versions.

```sh
$ bower update
```

<br>
