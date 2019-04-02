## Installation
I installed Go 1.10 in Ubuntu using a PPA:
```bash
sudo add-apt-repository --yes ppa:gophers/archive
sudo apt install golang-1.10
```

And I set `~/go` to be my workspace directory
```bash
export GOPATH=/home/alexishevia/go
PATH=$PATH:/usr/lib/go-1.10/bin:/home/alexishevia/go/bin
```

## Code Organization
Go programmers typically keep all their Go code in a single workspace.
A workspace is a directory hierarchy with three directories at its root:
- `src` contains Go source files,
- `pkg` contains package objects, and
- `bin` contains executable commands.

**Note**  
There's a very complete post about best practices for package organization:  
https://medium.com/@benbjohnson/standard-package-layout-7cdbc8391fc1

### Creating a Package
When creating a package, the best practice is to use your github source
repository as your base path. For example, your 'foobar' package would live in:
`$HOME/go/src/github.com/alexishevia/foobar/`

### Installing a Package
To install your package, run:
`go install github.com/alexishevia/foobar` from anywhere on your computer, or
`go install` from the package directory

Installing a package will create an executable in the `$GOPATH/bin` directory,
ie:
`$HOME/go/bin/foobar`

### Building a Package
To build your package, run:
`go build github.com/alexishevia/foobar` from anywhere on your computer, or
`go build` from the package directory

Building a package will not create an executable. Instead, it will add the
package to the `$GOPATH/pkg` directory, and make it available so other
packages can require it, eg:
```go
package main

import (
  "github.com/alexishevia/foobar"
)
```

### Remote packages
You can fetch remote packages by running `go get <pkg_url>`, eg:
`go get github.com/golang/example/hello`

The `go get` command will:
- add the package source code to `$GOPATH/src`
- add the package to `$GOPATH/pkg` (build)
- install the package binaries into `$GOPATH/bin` (install)
