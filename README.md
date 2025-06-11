# Cosmic for Vim/Neovim

Vim-cosmic is a dark & light color scheme designed to use on vim, gvim and neovim. It consists of 16 colors selected procedurally (algorithms) and it's part of a bigger project: [Cosmic](https://github.com/gerardbm/cosmic), which also includes color schemes for the terminals URxvt and XTerm.

![Cosmic Lunar Screenshot](https://github.com/gerardbm/vim-cosmic/blob/master/img/Cosmic-Lunar-Mode.png)

![Cosmic Solar Screenshot](https://github.com/gerardbm/vim-cosmic/blob/master/img/Cosmic-Solar-Mode.png)

Cosmic has support for 8, 16 and 256 colors, and *True Color* (24 bits) on the last versions of vim, gvim, neovim and nvim-qt. It uses the setting `termguicolors` properly (some color schemes don't).

It comes with two modes: the dark mode, called **Lunar** (hue 222°), and the light one, called **Solar** (hue 55°).

Each mode has 3 contrasts:

- Very high contrast (HC), +4%
- high contrast (HC), +2%
- Medium contrast (MC), 0
- Low contrast (LC), -2%
- Very low contrast (LC), -4%

## Installation

#### Manual installation

1. Copy the file `cosmic.vim` to your `~/.vim/colors/` directory (for vim) or `~/.config/nvim/colors/` directory (for neovim).

```bash
$ cd vim-cosmic
$ cp cosmic.vim ~/.vim/colors/
```

#### Using a plugin manager (i.e., [vim-plug](https://github.com/junegunn/vim-plug))

1. Paste this in your `.vimrc` file:
```viml
Plug 'gerardbm/vim-cosmic'
```
2. Reload your settings and install it:
```viml
:source $MYVIMRC
:PlugInstall
```

#### Modify your .vimrc

1. Set the colorscheme in your `.vimrc` configuration file:
```viml
syntax enable
colorscheme cosmic
```

## Configuration

#### Color support

If your terminal does not support *True color*, you can take a look at the main [Cosmic](https://github.com/gerardbm/cosmic) repository to see if Cosmic colors are available for your terminal and how to install them.

If your terminal supports *True color* (1), you can enable it configuring your `~/.vimrc` file with the setting `set termguicolors` (2) **before** the color scheme definition (`colorscheme cosmic`).

---

1. See [https://gist.github.com/XVilka/8346728](https://gist.github.com/XVilka/8346728) for a list of terminals that support *True color*.

2. Sometimes setting `termguicolors` is not enough and one has to set the `t_8f` and `t_8b` options explicitly, also **before** the color scheme definition:

```viml
if has("termguicolors")
	let &t_8f = "\<Esc>[38;2;%lu;%lu;%lum"
	let &t_8b = "\<Esc>[48;2;%lu;%lu;%lum"
	set termguicolors
endif
```

Use it when `$TERM` is not `xterm`, for example, running vim into tmux or using a terminal with different `$TERM`, like st case.

More info, see `:h xterm-true-color`.

#### Color palettes

If your terminal have *True color* support or if you are using a GUI (like gvim or nvim-qt), you have the following commands to switch between the different color modes and contrast:

- (1) `CosmicLunarC1`: sets the lunar mode (dark background) in very high contrast (+4%).
- (2) `CosmicLunarC2`: sets the lunar mode (dark background) in high contrast (+2%).
- (3) `CosmicLunarC3`: sets the lunar mode (dark background) in medium contrast (default).
- (4) `CosmicLunarC4`: sets the lunar mode (dark background) in low contrast (-2%).
- (5) `CosmicLunarC5`: sets the lunar mode (dark background) in very contrast (-4%).
- (6) `CosmicSolarC6`: sets the solar mode (light background) in very high contrast (+4%).
- (7) `CosmicSolarC7`: sets the solar mode (light background) in high contrast (+2%).
- (8) `CosmicSolarC8`: sets the solar mode (light background) in medium contrast (default).
- (9) `CosmicSolarC9`: sets the solar mode (light background) in low contrast (-2%).
- (0) `CosmicSolarC0`: sets the solar mode (light background) in very low contrast (-4%).

Use one of them **after** the color scheme definition in your `~/.vimrc` or `~/.gvimrc`.

Switch them automatically depending on the current time. For example, if you would like to use the CosmicSolarC8 between 8 am and 8 pm and switch to CosmicLunarC3 at night, simply paste this in your `~/.vimrc` or `~/.gvimrc`:

```viml
function! CosmicSwitcher()
	if (strftime('%H') > 8) && (strftime('%H') < 20)
		CosmicSolarC8
	else
		CosmicLunarC3
	endif
endfunction
```

Alternatively, you can cycle them (from 0 to 9) with a shortcut (for example: <kbd>Shift</kbd>+<kbd>F9</kbd>). Paste this in your `~/.vimrc` or `~/.gvimrc`:

```viml
nnoremap <S-F9> :call CycleModes()<CR>:colorscheme cosmic<CR>
```

#### Emphasis

Some terminals don't handle italics correctly, so in case you need to disable italics set `let g:cosmic_italic=0` in your `~/.vimrc`, **before** the color scheme definition.

Full list of options to disable italic text, bold, underline and undercurl:

```viml
let g:cosmic_italic = 0
let g:cosmic_bold = 0
let g:cosmic_underline = 0
let g:cosmic_undercurl = 0
```

If this options are not defined, default value is 1 for all of them.

#### MatchParen highlight

By default, Cosmic will use an orange color to highlight the background for `MatchParen`. To use the orange color for the foreground instead, use the following option:

```viml
let g:cosmic_matchparen = 0
```

As with emphasis cases, add this to your `~/.vimrc`, **before** the color scheme definition.

#### Example configuration

```viml
if has("termguicolors")
	let &t_8f = "\<Esc>[38;2;%lu;%lu;%lum"
	let &t_8b = "\<Esc>[48;2;%lu;%lu;%lum"
	set termguicolors
endif

syntax enable

let g:cosmic_italic = 0
colorscheme cosmic
CosmicLunarC5
```
