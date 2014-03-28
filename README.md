<<<<<<< HEAD
# bling.vim

A highly tuned vim distribution that will blow your socks off!

## introduction

this is my ***personal*** vim distribution that i have tweaked over time and evolved from a simple vanilla vimrc configuration to a full-blown distribution that it is today.

while it is very easy to install this and get up and running on a brand new machine (a use case i have), i recommend that you do not install this unless you fully understand everything that's going on inside.  scan it for tips and tricks, or fork and customize it for *your* needs.

## installation

1.  clone this repository into your `~/.vim` directory
1.  `git submodule init && git submodule update`
1.  `mv ~/.vimrc ~/.vimrc.backup`
1.  create the following shim and save it as `~/.vimrc`:

```
let g:dotvim_settings = {}
let g:dotvim_settings.version = 1
source ~/.vim/vimrc
```

1.  startup vim and neobundle will detect and ask you install any missing plugins.  you can also manually initiate this with `:NeoBundleInstall`
1.  done!

### versioning

the `g:dotvim_settings.version` is a simple version number which is manually edited.  it is used to detect whether significant breaking changes have been introduced so that users of the distribution can be notified accordingly.

## customization

*  since the distribution is just one file, customization is straightforward.  any customizations can be added to the `g:dotvim_settings` variable, which will be used whilst sourcing the distribution's `vimrc` file.  here is an example:

```
" this is the bare minimum
let g:dotvim_settings = {}
let g:dotvim_settings.version = 1

" here are some basic customizations, please refer to the top of the vimrc file for all possible options
let g:dotvim_settings.default_indent = 3
let g:dotvim_settings.max_column = 80
let g:dotvim_settings.colorscheme = 'my_awesome_colorscheme'

" by default, language specific plugins are not loaded.  this can be changed with the following:
let g:dotvim_settings.plugin_groups_exclude = ['ruby','python']

" if there are groups you want always loaded, you can use this:
let g:dotvim_settings.plugin_groups_include = ['go']

" alternatively, you can set this variable to load exactly what you want
let g:dotvim_settings.plugin_groups = ['core','web']

" if there is a particular plugin you don't like, you can define this variable to disable them entirely
let g:dotvim_settings.disabled_plugins=['vim-foo','vim-bar']

" finally, load the distribution
source ~/.vim/vimrc

" anything defined here are simply overrides
set wildignore+=\*/node_modules/\*
set guifont=Wingdings:h10
```

## autocomplete

this distribution will pick one of three combinations, in the following priority:

1.  [neocomplete][nc] + [neosnippet][ns] if you have `lua` enabled.
2.  [youcompleteme][ycm] + [ultisnips][us] if you have compiled YCM.
3.  [neocomplcache][ncl] + [neosnippet][ns] if you only have vimscript available

this can be overridden with `g:dotvim_settings.autocomplete_method`

## standard modifications

*  if you have either [ack](http://betterthangrep.com/) or [ag](https://github.com/ggreer/the_silver_searcher) installed, they will be used for `grepprg`
*  all temporary files are stored in `~/.vim/.cache`, such as backup files and persistent undo

## mappings

### insert mode
*  `<C-h>` move the cursor left
*  `<C-l>` move the cursor right
*  `jk`, `kj` remapped for "smash escape"

### normal mode
*  `<leader>fef` format entire file
*  `<leader>f$` strip current line of trailing white space
*  window shortcuts
  *  `<leader>v` vertical split
  *  `<leader>s` horizontal split
  *  `<leader>vsa` vertically split all buffers
  *  `<C-h>` `<C-j>` `<C-k>` `<C-l>` move to window in the direction of hkjl
*  window killer
  *  `Q` remapped to close windows and delete the buffer (if it is the last buffer window)
* searching
  *  `<leader>fw` find the word under cursor into the quickfix list
  *  `<leader>ff` find the last search into the quickfix list
  *  `/` replaced with `/\v` for sane regex searching
  *  `<cr>` toggles hlsearch
*  `<Down>` `<Up>` maps to `:bprev` and `:bnext` respectively
*  `<Left>` `<Right>` maps to `:tabprev` and `:tabnext` respectively
*  `gp` remapped to visually reselect the last paste
*  `gb` for quick going to buffer
*  `<leader>l` toggles `list` and `nolist`
*  profiling shortcuts
   * `<leader>DD` starts profiling all functions and files into a file `profile.log`
   * `<leader>DP` pauses profiling
   * `<leader>DC` continues profiling
   * `<leader>DQ` finishes profiling and exits vim

### visual mode
*  `<leader>s` sort selection
*  `>` and `<` automatically reselects the visual selection

## plugins

### [unite.vim](https://github.com/Shougo/unite.vim)
*  this is an extremely powerful plugin that lets you build up lists from arbitrary sources
*  mappings
  *  `<space><space>` go to anything (files, buffers, MRU, bookmarks)
  *  `<space>y` select from previous yanks
  *  `<space>l` select line from current buffer
  *  `<space>b` select from current buffers
  *  `<space>o` select from outline of current file
  *  `<space>s` quick switch buffer
  *  `<space>/` recursively search all files for matching text (uses `ag` or `ack` if found)

### [bufkill.vim](http://www.vim.org/scripts/script.php?script_id=1147)
*  `<leader>bd` or `:BD` will kill a buffer without changing the window layout

### [sneak.vim](https://github.com/justinmk/vim-sneak)
*  motion on steriods

### [easygrep](http://www.vim.org/scripts/script.php?script_id=2438)
*  makes search/replacing in your project a lot easier without relying on `find` and `sed`
*  the loading time of this plugin is relatively heavy, so it is not loaded at startup.  to load it on-demand, use `<leader>vo`, which opens the options window.
*  `<leader>vv` find word under the cursor
*  `<leader>vV` find whole word under the cursor
*  `<leader>vr` perform global search replace of word under cursor, with confirmation
*  `<leader>vR` same as vr, but matches whole word

### [fugitive](https://github.com/tpope/vim-fugitive)
*  git wrapper
*  `<leader>gs` status
*  `<leader>gd` diff
*  `<leader>gc` commit
*  `<leader>gb` blame
*  `<leader>gl` log
*  `<leader>gp` push
*  `<leader>gw` stage
*  `<leader>gr` rm
*  in addition to all the standard bindings when in the git status window, you can also use `U` to perform a `git checkout --` on the current file

### [gitv](https://github.com/gregsexton/gitv)
*  nice log history viewer for git
*  `<leader>gv`

### [unimpaired](https://github.com/tpope/vim-unimpaired)
*  many additional bracket `[]` maps
*  `<C-up>` to move lines up
*  `<C-down>` to move lines down

### [nerdtree](https://github.com/scrooloose/nerdtree)
*  file browser
*  `<F2>` toggle browser
*  `<F3>` open tree to path of the current file

### [tcomment](https://github.com/tomtom/tcomment_vim)
*  very versatile commenting plugin that can do motions
*  `gcc` to toggle or `gc{motion}`

### [ctrlp](https://github.com/kien/ctrlp.vim)
*  fuzzy file searching
*  `<C-p>` to bring up the search
*  `\t` search the current buffer tags
*  `\T` search global tags
*  `\l` search all lines of all buffers
*  `\b` search open buffers
*  `\o` parses the current file for functions with [funky](https://github.com/tacahiroy/ctrlp-funky)

### [nrrwrgn](http://github.com/chrisbra/NrrwRgn)
*  `<leader>nr` puts the current visual selection into a new scratch buffer, allowing you to perform global commands and merge changes to the original file automatically

### [tabular](https://github.com/godlygeek/tabular)
*  easily aligns code
*  `<leader>a&`, `<leader>a=`, `<leader>a:`, `<leader>a,`, `<leader>a|`

### [gist](https://github.com/mattn/gist-vim)
*  automatically get or push changes for gists with `:Gist`

### [emmet](https://github.com/mattn/emmet-vim)
*  makes for writing html/css extremely fast
*  for supported most filetypes, `<tab>` will be mapped to automatically expand the line (you can use `<C-v><Tab>` to insert a tab character if needed)
*  for other features, default plugin mappings are available, which means `<C-y>` is the prefix, followed by a variety of options (see `:help zencoding`)

### [undotree](https://github.com/mbbill/undotree)
*  visualize the undo tree
*  `<F5>` to toggle

### [youcompleteme][ycm]/[ultisnips][us]
*  amazingly fast fuzzy autocomplete engine combined with an excellent snippets library
*  use `<C-n>` and `<C-p>` to go back/forward between selections, and `<tab>` to expand snippets

### [neocomplcache][ncl]/[neosnippet][ns]
*  autocomplete/snippet support as a fallback choice when YCM and/or python is unavailable
*  `<Tab>` to select the next match, or expand if the keyword is a snippet
*  if you have lua installed, it will use [neocomplete][nc] instead

### [vimshell](https://github.com/Shougo/vimshell)
*  `<leader>c` splits a new window with an embedded shell

### [vim-multiple-cursors](https://github.com/terryma/vim-multiple-cursors)
*  mapped to `<C-N>`, this will select all matching words and lets you concurrently change all matches at the same time

# and some more plugins
*  [surround](https://github.com/tpope/vim-surround) makes for quick work of surrounds
*  [repeat](https://github.com/tpope/vim-repeat) repeat plugin commands
*  [speeddating](https://github.com/tpope/vim-speeddating) `Ctrl+A` and `Ctrl+X` for dates
*  [gist](https://github.com/mattn/gist-vim) awesome plugin for your gist needs
*  [signature](https://github.com/kshenoy/vim-signature) shows marks beside line numbers
*  [matchit](https://github.com/vim-scripts/matchit.zip) makes your `%` more awesome
*  [syntastic](https://github.com/scrooloose/syntastic) awesome syntax checking for a variety of languages
*  [bufferline](https://github.com/bling/vim-bufferline) simple plugin which prints all your open buffers in the command bar
*  [indent-guides](https://github.com/nathanaelkane/vim-indent-guides) vertical lines
*  [signify](https://github.com/mhinz/vim-signify) adds + and - to the signs column when changes are detected to source control files (supports git/hg/svn)
*  [delimitmate](https://github.com/Raimondi/delimitMate) automagically adds closing quotes and braces
*  [startify](https://github.com/mhinz/vim-startify) gives you a better start screen

# and even more plugins...
*  i think i've listed about half of the plugins contained in this distribution, so please have a look at the vimrc directly to see all plugins in use

## credits

i wanted to give special thanks to all of the people who worked on the following projects, or people simply posted their vim distributions, because i learned a lot and took many ideas and incorporated them into my configuration.

*  [janus](https://github.com/carlhuda/janus)
*  [spf13](https://github.com/spf13/spf13-vim)
*  [yadr](http://skwp.github.com/dotfiles/)
*  [astrails](https://github.com/astrails/dotvim)
*  [tpope](https://github.com/tpope)
*  [scrooloose](https://github.com/scrooloose)
*  [shougo](https://github.com/Shougo)
*  [lokaltog](https://github.com/Lokaltog)
*  [sjl](https://github.com/sjl)
*  [terryma](https://github.com/terryma)

## license
[WTFPL](http://sam.zoy.org/wtfpl/)

## changelog

*  v1
  * requires `g:dotvim_settings.version` to be defined
  * disable all langauge-specific plugins by default
  * add support for `g:dotvim_settings.plugin_groups_include`


[ycm]: https://github.com/Valloric/YouCompleteMe
[us]: https://github.com/SirVer/ultisnips
[nc]: https://github.com/Shougo/neocomplete.vim
[ncl]: https://github.com/Shougo/neocomplcache.vim
[ns]: https://github.com/Shougo/neosnippet.vim
=======
**neocomplcache**
=================

Description
-----------

neocomplcache is the abbreviation of "neo-completion with cache". It
provides keyword completion system by maintaining a cache of keywords in the
current buffer. neocomplcache could be customized easily and has a lot more
features than the Vim's standard completion feature.

If you use Vim 7.3.885 or above with if\_lua feature, you should use
neocomplete.  It is faster than neocomplcache.

https://github.com/Shougo/neocomplete.vim

Installation
============

* Extract the file and put files in your Vim directory
   (usually ~/.vim/ or Program Files/Vim/vimfiles on Windows).
* Execute `|:NeoComplCacheEnable|` command or
`let g:neocomplcache_enable_at_startup = 1`
in your `.vimrc`. Not in `.gvimrc`(`_gvimrc`)!

Caution
-------

Because all variable names were changed in neocomplcache Ver.5, it is not
backwards compatible. If you want to upgrade, you should use the following
script from Mr.thinca.

http://gist.github.com/422503

Snippets feature(snippets\_complete source) was split from Ver.7.
If you used it, please install neosnippet source manually.

https://github.com/Shougo/neosnippet

Screen shots
============

Original filename completion.
-----------
![Original filename completion.](http://1.bp.blogspot.com/_ci2yBnqzJgM/TD1O5_bOQ2I/AAAAAAAAADE/vHf9Xg_mrTI/s1600/filename_complete.png)

Omni completion.
----------------
![Omni completion.](http://2.bp.blogspot.com/_ci2yBnqzJgM/TD1PTolkTBI/AAAAAAAAADU/knJ3eniuHWI/s1600/omni_complete.png)

Completion with vimshell(http://github.com/Shougo/vimshell).
------------------------------------------------------------
![Completion with vimshell(http://github.com/Shougo/vimshell).](http://1.bp.blogspot.com/_ci2yBnqzJgM/TD1PLfdQrwI/AAAAAAAAADM/2pSFRTHwYOY/s1600/neocomplcache_with_vimshell.png)

Vim completion
------------------------------------------------------------
![Vim completion.](http://1.bp.blogspot.com/_ci2yBnqzJgM/TD1PfKTlwnI/AAAAAAAAADs/nOGWTRLuae8/s1600/vim_complete.png)

Setting examples

```vim
"Note: This option must set it in .vimrc(_vimrc).  NOT IN .gvimrc(_gvimrc)!
" Disable AutoComplPop.
let g:acp_enableAtStartup = 0
" Use neocomplcache.
let g:neocomplcache_enable_at_startup = 1
" Use smartcase.
let g:neocomplcache_enable_smart_case = 1
" Set minimum syntax keyword length.
let g:neocomplcache_min_syntax_length = 3
let g:neocomplcache_lock_buffer_name_pattern = '\*ku\*'

" Enable heavy features.
" Use camel case completion.
"let g:neocomplcache_enable_camel_case_completion = 1
" Use underbar completion.
"let g:neocomplcache_enable_underbar_completion = 1

" Define dictionary.
let g:neocomplcache_dictionary_filetype_lists = {
    \ 'default' : '',
    \ 'vimshell' : $HOME.'/.vimshell_hist',
    \ 'scheme' : $HOME.'/.gosh_completions'
        \ }

" Define keyword.
if !exists('g:neocomplcache_keyword_patterns')
    let g:neocomplcache_keyword_patterns = {}
endif
let g:neocomplcache_keyword_patterns['default'] = '\h\w*'

" Plugin key-mappings.
inoremap <expr><C-g>     neocomplcache#undo_completion()
inoremap <expr><C-l>     neocomplcache#complete_common_string()

" Recommended key-mappings.
" <CR>: close popup and save indent.
inoremap <silent> <CR> <C-r>=<SID>my_cr_function()<CR>
function! s:my_cr_function()
  return neocomplcache#smart_close_popup() . "\<CR>"
  " For no inserting <CR> key.
  "return pumvisible() ? neocomplcache#close_popup() : "\<CR>"
endfunction
" <TAB>: completion.
inoremap <expr><TAB>  pumvisible() ? "\<C-n>" : "\<TAB>"
" <C-h>, <BS>: close popup and delete backword char.
inoremap <expr><C-h> neocomplcache#smart_close_popup()."\<C-h>"
inoremap <expr><BS> neocomplcache#smart_close_popup()."\<C-h>"
inoremap <expr><C-y>  neocomplcache#close_popup()
inoremap <expr><C-e>  neocomplcache#cancel_popup()
" Close popup by <Space>.
"inoremap <expr><Space> pumvisible() ? neocomplcache#close_popup() : "\<Space>"

" For cursor moving in insert mode(Not recommended)
"inoremap <expr><Left>  neocomplcache#close_popup() . "\<Left>"
"inoremap <expr><Right> neocomplcache#close_popup() . "\<Right>"
"inoremap <expr><Up>    neocomplcache#close_popup() . "\<Up>"
"inoremap <expr><Down>  neocomplcache#close_popup() . "\<Down>"
" Or set this.
"let g:neocomplcache_enable_cursor_hold_i = 1
" Or set this.
"let g:neocomplcache_enable_insert_char_pre = 1

" AutoComplPop like behavior.
"let g:neocomplcache_enable_auto_select = 1

" Shell like behavior(not recommended).
"set completeopt+=longest
"let g:neocomplcache_enable_auto_select = 1
"let g:neocomplcache_disable_auto_complete = 1
"inoremap <expr><TAB>  pumvisible() ? "\<Down>" : "\<C-x>\<C-u>"

" Enable omni completion.
autocmd FileType css setlocal omnifunc=csscomplete#CompleteCSS
autocmd FileType html,markdown setlocal omnifunc=htmlcomplete#CompleteTags
autocmd FileType javascript setlocal omnifunc=javascriptcomplete#CompleteJS
autocmd FileType python setlocal omnifunc=pythoncomplete#Complete
autocmd FileType xml setlocal omnifunc=xmlcomplete#CompleteTags

" Enable heavy omni completion.
if !exists('g:neocomplcache_omni_patterns')
  let g:neocomplcache_omni_patterns = {}
endif
let g:neocomplcache_omni_patterns.php = '[^. \t]->\h\w*\|\h\w*::'
let g:neocomplcache_omni_patterns.c = '[^.[:digit:] *\t]\%(\.\|->\)'
let g:neocomplcache_omni_patterns.cpp = '[^.[:digit:] *\t]\%(\.\|->\)\|\h\w*::'

" For perlomni.vim setting.
" https://github.com/c9s/perlomni.vim
let g:neocomplcache_omni_patterns.perl = '\h\w*->\h\w*\|\h\w*::'
```
>>>>>>> da44ba4a92eef3860bdee2d96d755a7171889a70
