# Vim

## How to manually set the eslint path for syntastic
Add the following to your project's `.vimrc` file:
```
let g:syntastic_javascript_eslint_exec='/full/path/to/node_modules/.bin/eslint'
```

## Folding
http://vimdoc.sourceforge.net/htmldoc/fold.html#zf
zf - create a fold
zo - open fold under cursor
zc - close fold under cursor

## cTags
[Make Your Vim Smarter Using Ctrlp and Ctags](https://medium.freecodecamp.org/make-your-vim-smarter-using-ctrlp-and-ctags-846fc12178a4)
[Exuberant Ctags Patterns for JavaScript](https://github.com/romainl/ctags-patterns-for-javascript)

To generate ctags for your project:
```
ctags -R .
```

You can use `Ctrlp` to search for tags instead of files. To do this, first you need to map a shortcut in your .vimrc:
`nnoremap <buffer> <localleader>p :CtrlPTag<cr>`

