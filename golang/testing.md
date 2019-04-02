# Testing in Go

## Resources
- [Learn Go with tests](https://quii.gitbook.io/learn-go-with-tests)
- [GoDoc: Testing](https://godoc.org/testing)

## Tests
You write a test by creating a file with a name ending in `_test.go` that
contains functions named `TestXXX` with signature `func (t *testing.T)`.

Run your tests with:
`go test github.com/alexishevia/foobar` from anywhere on your computer, or
`go test` from the package directory

```go
func TestSumAll(t *testing.T)  {
    got := SumAll([]int{1,2}, []int{0,9})
    want := []int{3, 9}

    if !reflect.DeepEqual(got, want) {
        t.Errorf("got %v want %v", got, want)
    }
}
```

## Benchmarks
You can write benchmarks for your code, which you run with `go test -bench=.`

```go
func BenchmarkSomeFunc(b *testing.B) {
    for i := 0; i < b.N; i++ {
        SomeFunc("a")
    }
}
```

## Coverage
To see code coverage, run: `go test -cover`

## Race Condition Detector
You can run the race condition detector with: `go test -race`

## Other
- [httptest](https://golang.org/pkg/net/http/httptest/)  
    utilities for HTTP testing
- [errcheck](https://github.com/kisielk/errcheck)  
    program for checking for unchecked errors in go programs
- [godog](https://github.com/DATA-DOG/godog)  
    Cucumber for golang
