# Functions

## Simple function declaration

```go
package main

import "fmt"

func noParamsNoReturn() {
	fmt.Println("I'm not really doing much!")
}

func main() {
	noParamsNoReturn()
}
```

```
I'm not really doing much!
```

## Two parameters and a single return value

```go
package main

import "fmt"

func twoParamsOneReturn(myInt int, myString string) string {
	return fmt.Sprintf("myInt: %d, myString: %s", myInt, myString)
}

func main() {
	result := twoParamsOneReturn(1, "hello")
	fmt.Println(result)
}
```

```
myInt: 1, myString: hello
```

## Multiple return values

```go
package main

import "fmt"

func oneParamTwoReturns(myInt int) (string, int) {
	return fmt.Sprintf("Int: %d", myInt), myInt + 1
}

func main() {
	foo, bar := oneParamTwoReturns(2)
	fmt.Println("foo:", foo, "| bar:", bar)
}
```

```
foo: Int: 2 | bar: 3
```

## Same typed params

```go
package main

import "fmt"

func twoSameTypedParams(myString1, myString2 string) {
	fmt.Println("String 1", myString1)
	fmt.Println("String 2", myString2)
}

func main() {
	twoSameTypedParams("hello", "world")
}
```

```
String 1 hello
String 2 world
```

## Pointer Arguments
When you pass a variable to a function, it receives a copy of the variable, rather than the variable itself. Pointers allow you to pass a reference to an object.

```go
package main

import "fmt"

// regular function argument (copy)
func giveMePearCopy(fruit string) {
	fruit = "pear"
}

// pointer argument (reference)
func giveMePearReference(fruit *string) {
	*fruit = "pear"
}

func main() {
	fruit := "banana"
	giveMePearCopy(fruit)
	fmt.Println(fruit)
	giveMePearReference(&fruit)
	fmt.Println(fruit)
}
```

```
banana
pear
```
