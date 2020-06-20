# Vim + Go

There are two plugins which help a lot with Go development in Vim:
- [vim-go](https://github.com/fatih/vim-go)
- [gotests-vim ](https://github.com/buoto/gotests-vim)

Tutorials:

- [vim-go-tutorial](https://github.com/fatih/vim-go-tutorial)
- [Go Development with Vim-go](https://www.youtube.com/watch?v=7BqJ8dzygtU)

## Useful Commands
- `:GoDef` jump to the declaration/definition for the identifier under the cursor.
- `:GoDefPop` or `Ctrl+O` jump back to original code.
- `:GoDefStack` show the complete stack of `:GoDef` calls.
- `:GoTests` generate a test for the function at the current line.
- `:GoTestFunc` run the tests currently under the cursor.
- `:GoCoverageToggle` toggle between showing test coverage or not.
- `:GoMetaLinter` displays all warnings and errors in a quickfix window.  
    If you get an error saying something like `WARNING: exec: "govet": executable file not found in $PATH`, you might need to run: `gometalinter --install`

## Running a project
vim-go includes a `:GoRun` command you can use to run the current main package.

However, I usually just spin up a new terminal and run: `go run .` to run my projects.

## Debugging with vim-go

If you have [vim-go](https://github.com/fatih/vim-go) installed, you can debug programs using the integrated [delve](https://github.com/derekparker/delve) support.

Full documentation: https://github.com/fatih/vim-go/blob/master/doc/vim-go.txt#L1850

- Start debugging with: `:GoDebugStart`
- Add breakpoints with: `:GoDebugBreakPoint`
- Advance until next breakpoint with: `:GoDebugContinue`
- Advance to next line with: `:GoDebugNext`
- Step into the function with: `:GoDebugStep`
- Step out of the function with: `:GoDebugStepOut`
- Set a variable value with `:GoDebugSet {var} {value}`. Example: `:GoDebugSet foo 42`
- Print the result of a Go expression with `:GoDebugPrint`. Example: `:GoDebugPrint truth == 42`
- Stop debugging with: `:GoDebugStop`

## Debugging with delve
1. Instead of starting the server with `go run .`, run: `dlv debug .`
2. Set up a breakpoint in the method you're inspecting.
    eg: `break handler.V1Stations` or `break handler/handler.go:56`
3. Start program execution: `continue`

For more info, see: https://github.com/go-delve/delve/blob/master/Documentation/cli/getting_started.md

## Running tests
To run all tests in the project: `go test ./...` or `go test -v ./...`

To run a single test, you can use vim-go's `:GoTestFunc`. It will run whichever test the cursor is currently on.

You can also run `go test` with the `-run` flag to specify the test you want to run.

The `-run` flag takes a regular expression as its argument, but the easiest way to get the test name is to first run `go test -v ./...` and then copy the test name from the output. Then you can run `go test ./... -run <YourTestName>`. eg: `go test ./... -run TestLiveRestartPlayer_Get`

## Debugging tests with delve
You can replace `go test` with `dlv test` to get into a debug session, but you need to keep a couple things in mind:
1. dlv test does not support multiple packages (ie: no `./...`).  
    Instead, either `cd` into the package directory, or specify the package you want to test:

    `dlv test github.com/foxbroadcasting/cpe-psu`
2. If you want to debug a specific test, use `-test.run` instead of `-run`.  

    `dlv test github.com/foxbroadcasting/cpe-psu -test.run TestLiveRestartPlayer_Get`

## Debugging tests with vim-go
You can use the `:GoDebugTest .` command to start a new debug session in vim-go.

If you want to run a specific test, you will need to use the `-test.run` parameter. eg:

`:GoDebugTest . -test.run TestLiveRestartPlayer_Get`
