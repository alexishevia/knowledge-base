# Documentation
Golang has a built-in `godoc` command that lets you view the full Golang documentation even when offline.

However, the biggest benefit is that you can also view documentation for your own packages, and any testable examples you add will be automatically appended to the documentation.

## Running godoc
Execute `godoc -http=:3000`, and open http://localhost:3000 (you can choose any port you want).

You can then navigate to the "Packages" section and view documentation for your own packages.

## Testable Examples
Testables examples are a type of test that demonstrate how a package/type/function can be used.

They serve as "living documentation" for your code, because they will cause tests to fail if they ever go out of date.

## References
- [Test With Go: Viewing Examples in the docs](https://courses.calhoun.io/lessons/les_twg_les_14)
- [Testable Examples in Go](https://blog.golang.org/examples)
