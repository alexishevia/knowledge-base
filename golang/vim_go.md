# Vim + Go

[vim-go](https://github.com/fatih/vim-go) is the most complete Go development plugin for Vim.

Tutorials:

- [vim-go-tutorial](https://github.com/fatih/vim-go-tutorial) 
- [Go Development with Vim-go](https://www.youtube.com/watch?v=7BqJ8dzygtU)
- [Vim IDE setup for Go](https://tpaschalis.github.io/vim-go-setup/)

## Useful Commands
- `:GoDef` `-f` jump to the definition of the current function.
- `:GoDefPop` `-F` go back to original code 
- `:GoDefStack` show the complete stack of `:GoDef` calls
- `:GoBuild` `-b`
- `:GoRun` `-r`
- `:GoTest` `-t`
- `:GoCoverageToggle` `-c`
- `:GoMetaLinter` `-l`  
    If you get an error saying something like `WARNING: exec: "govet": executable file not found in $PATH`, you might need to run: `gometalinter --install`

## Debugging

If you have [vim-go](https://github.com/fatih/vim-go) installed, you can debug programs using the integrated [delve](https://github.com/derekparker/delve) support.

Full documentation: https://github.com/fatih/vim-go/blob/master/doc/vim-go.txt#L1850

- Start debugging with: `:GoDebugStart` `-dS`
- Add breakpoints with: `:GoDebugBreakPoint` `-db`
- Advance until next breakpoint with: `:GoDebugContinue` `-dc`
- Advance to next line with: `:GoDebugNext` `-dn`
- Step into the function with: `:GoDebugStep` `-ds`
- Step out of the function with: `:GoDebugStepOut` `-do`
- Set a variable value with `:GoDebugSet {var} {value}`. Example: `:GoDebugSet foo 42`
- Print the result of a Go expression with `:GoDebugPrint` `-dp`. Example: `:GoDebugPrint truth == 42`
- Stop debugging with: `:GoDebugStop` `-dX`

Another helpful package for debugging is [go-spew](https://github.com/davecgh/go-spew). Go-spew implements a deep pretty printer for Go data structures to aid in debugging.
