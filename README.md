# masnes-bling.vim

What I use with vim

## introduction

This is what I currently use as my vim configuration. It's built off of [bling's configuration](https://github.com/bling/dotvim), but with numerous changes. 

Here's a general overview of what's different:
* Added check for osx to vimrc. al
* Added support for osx terminal ^[[A - ^[[D. arrow character associations
  * Added support for osx terminal tmux's slightly different ^[OA - ^[OD associations
* Defaults
  * Set relative numbering in normal mode by default 
    * toggle this with leader-nt
    * absolute numbering will be present in insert mode
    * in gui this will toggle on/off based on window focus
  * Turned off list by default
    * toggle this with leader-l
  * set wrap by default
  * Changed scrolling behavior
    * scrolloff = 7 now by default
    * scrolljump = 1 now by default
  * Disabled initial folding 
* Plugin changes
  * Removed auto-pairs plugin
  * Removed undotree
  * Added gundo
    * use gundu with leader-u
  * Added LaTeX-Box plugin
    * Added TeX spell files
  * Added vim-exchange plugin
  * Added eclim plugin 
* Mappings
  * leader-w saves file 
    * same as blings setup, but awesome enough to reiterate here
  * leader-ss turns on/off spell checking
  * Tab no longer expands neosnippets (it now only affects autocompletion)
    * Use ctrl-j in terminal, and/or ctrl-tab in gui to expand snippets
  * use gundu with leader-u
  * backspace now toggles :nohighlight
  * leader-cr now toggles :hlsearch
  * q: now opens command window in normal mode instead of insert mode
  * gj and gk added - function like j and k in unmodified vim 
    * ignore screenwrapping when changing lines
  * swapped function of 0 and ^. Use 0 to go to the soft BOL, ^ or g0 to go to the hard BOL
* Functions
  * Added function to toggle relative numbering
