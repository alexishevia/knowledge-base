# Types
## Strings

```go
package main

import "fmt"

func main() {
	myString := "I'm a string."

	// concatenation
	myOtherString := myString + " I really am."

	// print
	fmt.Println(myOtherString)
}
```

```
I'm a string. I really am.
```

## Numbers

```go
package main

import "fmt"

func main() {
	myInt := 2
	myFloat := 1.5
	myOtherFloat := float64(myInt) * myFloat

	fmt.Println("myInt:", myInt)
	fmt.Println("myFloat:", myFloat)
	fmt.Println("myOtherFloat:", myOtherFloat)
}
```

```
myInt: 2
myFloat: 1.5
myOtherFloat: 3
```

## Slices

```go
package main

import "fmt"

func main() {
	mySlice := []int{1, 2, 3, 4, 5}
	mySlice2 := mySlice[0:3]
	mySlice3 := mySlice[1:4]

	fmt.Println("mySlice:", mySlice)
	fmt.Println("mySlice2:", mySlice2)
	fmt.Println("mySlice3:", mySlice3)
	fmt.Println("mySlice[2]:", mySlice[2])
	fmt.Println("len(mySlice):", len(mySlice))
}
```

```
mySlice: [1 2 3 4 5]
mySlice2: [1 2 3]
mySlice3: [2 3 4]
mySlice[2]: 3
len(mySlice): 5
```

Iterating a slice:
```go
package main

import "fmt"

func main() {
	animals := []string{"Cat", "Dog", "Emu", "Warthog"}
	for i, animal := range animals {
		fmt.Println(animal, "is at index", i)
	}
}
```

```
Cat is at index 0
Dog is at index 1
Emu is at index 2
Warthog is at index 3
```

## Maps

```go
package main

import "fmt"

func main() {
	starWarsYears := map[string]int{
		"A New Hope":              1977,
		"The Empire Strikes Back": 1980,
		"Return of the Jedi":      1983,
		"Attack of the Clones":    2002,
		"Revenge of the Sith":     2005,
	}

	// adding a value
	starWarsYears["The Force Awakens"] = 2015

	// checking if a value exists
	val, exists := starWarsYears["Attack of the Clones"]
	if exists {
		fmt.Println("Attack of the Clones was released in", val)
	} else {
		fmt.Println("I don't know Attack of the Clones")
	}

	// removing a value
	delete(starWarsYears, "Attack of the Clones")

	// iterating a map
	for title, year := range starWarsYears {
		fmt.Println(title, "was released in", year)
	}
}
```

```
Attack of the Clones was released in 2002
The Empire Strikes Back was released in 1980
Return of the Jedi was released in 1983
Revenge of the Sith was released in 2005
The Force Awakens was released in 2015
A New Hope was released in 1977
```

## Custom Types
While you can’t add your own methods to built-in types, you can create your own types from other types. A common example of this is a ByteSize type, which extends float64 and provides a custom formatted string to represent a size in bytes such as 2 kilobytes or 3.14 megabytes:
```go
package main

import "fmt"

const (
	KB = 1024
	MB = KB * 1024
	GB = MB * 1024
	TB = GB * 1024
	PB = TB * 1024
)

type ByteSize float64

func (b ByteSize) String() string {
	switch {
	case b >= PB:
		return "Very Big"
	case b >= TB:
		return fmt.Sprintf("%.2fTB", b/TB)
	case b >= GB:
		return fmt.Sprintf("%.2fGB", b/GB)
	case b >= MB:
		return fmt.Sprintf("%.2fGB", b/MB)
	case b >= KB:
		return fmt.Sprintf("%.2fGB", b/KB)
	}
	return fmt.Sprintf("%dB", b)
}

func main() {
	fmt.Println(ByteSize(2048))
	fmt.Println(ByteSize(3292528.64))
}
```

```
2.00GB
3.14GB
```

## Embedded Types
Struct types are allowed to have other types embedded in them. This allows for a level of object “inheritance”, although it’s not quite the same as classic object-oriented inheritance. You embed a type by adding the type to a struct without a field name. The struct then gains access to the embedded value and its methods:
```go
package main

import "fmt"

type User struct {
	Name string
}

func (u User) IsAdmin() bool       { return false }
func (u User) DisplayName() string { return u.Name }

type Admin struct {
	User
}

func (a Admin) IsAdmin() bool { return true }
func (a Admin) DisplayName() string {
	// Add [Admin] in front of the embedded user's display name
	return "[Admin] " + a.User.DisplayName()
}

func main() {
	u := User{"Normal User"}
	fmt.Println(u.Name)
	fmt.Println(u.DisplayName())
	fmt.Println(u.IsAdmin())

	a := Admin{User{"Admin User"}}
	fmt.Println(a.Name)
	fmt.Println(a.User.Name)
	fmt.Println(a.DisplayName())
	fmt.Println(a.IsAdmin())
}
```

```
Normal User
Normal User
false
Admin User
Admin User
[Admin] Admin User
true
```

Embedding types is very useful when implementing interfaces. If your type has an embedded type that implements an interface, then your type automatically implements that interface too. This is because all the methods of the embedded type are available on the type that embeds it, and the methods are what defines whether or not a type implements an interface.

## Type Assertions
https://tour.golang.org/methods/15

To test whether an interface value holds a specific type, a type assertion can return two values: the underlying value and a boolean value that reports whether the assertion succeeded.
```
t, ok := i.(T)
```

```go
package main

import "fmt"

// ValidationError is for form validations
type ValidationError struct {
	msg string
}

func (err ValidationError) Error() string {
	return err.msg
}

// IOError is for io operations
type IOError struct {
	msg string
}

func (err IOError) Error() string {
	return err.msg
}

// IsValidationError returns true if error has type ValidationError
func IsValidationError(err error) bool {
	_, ok := err.(ValidationError)
	return ok
}

func main() {
	exampleValidationError := ValidationError{"this is a validation error"}
	exampleIOError := IOError{"this is an io error"}

	fmt.Println("exampleIOError is a ValidationError?", IsValidationError(exampleIOError))
	fmt.Println("exampleValidationError is a ValidationError?", IsValidationError(exampleValidationError))
}
```

```
exampleIOError is a ValidationError? false
exampleValidationError is a ValidationError? true
```
