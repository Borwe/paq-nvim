# Paq

Paq is a Neovim package manager written in Lua.


## Features

- __Simple__: Easy to use and configure
- __Fast__:   Installs and updates packages concurrently using Neovim's event-loop
- __Small__:  Around 250 LOC


## Requirements

- git
- [Neovim](https://github.com/neovim/neovim) 0.4.4 (stable)


## Installation

Clone this repository.

For Unix-like systems:

```sh
git clone --depth=1 https://github.com/savq/paq-nvim.git \
    "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/pack/paqs/start/paq-nvim
```

For Windows:
```
git clone https://github.com/savq/paq-nvim.git "$env:LOCALAPPDATA\nvim-data\site\pack\paqs\start\paq-nvim"
```


## Usage

In your init.lua, you can write something like:

```lua
require 'paq-nvim' {
    -- Add your packages
    'savq/paq-nvim';                  -- Let Paq manage itself

    'neovim/nvim-lspconfig';          -- Mind the semi-colons
    'nvim-lua/completion-nvim';
    'nvim-lua/lsp_extensions.nvim';

    {'lervag/vimtex', opt=true};      -- Use braces when passing options

    {'dracula/vim', as='dracula'};    -- Use `as` to alias a package name (here `vim`)
}
```

Then, source your configuration (using `luafile %`) and run `:PaqInstall`.

In general, to add packages to Paq's list, call `paq '<gh-username>/<repo>'`
inside a Lua chunk (or in a separate Lua module).

**NOTICE:**
Calling the `paq` function per package is deprecated. Users should now pass a
list to the `'paq-nvim'` module instead.


## Commands

- `PaqInstall`: Install all packages listed in your configuration.
- `PaqUpdate`: Update all packages already on your system (it won't implicitly install them).
- `PaqClean`: Remove all packages (in Paq's directory) that aren't listed on your configuration.


## Options

| Option | Type     |                                                           |
|--------|----------|-----------------------------------------------------------|
| as     | string   | Name to use for the package locally                       |
| branch | string   | Branch of the repository                                  |
| opt    | boolean  | Is the package optional?                                  |
| run    | string   | Shell command to run after install/update                 |
| run    | function | Lua function to run after install/update                  |
| url    | string   | URL of the remote repository, useful for non-GitHub repos |

For more details on each option, refer to the
[documentation](https://github.com/savq/paq-nvim/tree/master/doc/paq-nvim.txt).

**NOTICE:**
The `hook` option is deprecated, and will be removed in Paq 1.0. Use `run` instead.


## Related projects

You can find a [comparison](https://github.com/savq/paq-nvim/wiki/Comparisons)
with other package managers in the [wiki](https://github.com/savq/paq-nvim/wiki).
