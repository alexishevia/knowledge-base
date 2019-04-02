# Interfaces
An interface is a type defined with a specific set of method signatures, and any type that matches the method signatures implicitly implements the interface; there’s no need to explicitly declare that you’re implementing “interface X”.

```go
package main

import "fmt"

type Fruit interface {
	String() string
}

type Apple struct {
	Variety string
}

func (a Apple) String() string {
	return fmt.Sprintf("A %s apple", a.Variety)
}

type Orange struct {
	Size string
}

func (o Orange) String() string {
	return fmt.Sprintf("A %s orange", o.Size)
}

func PrintFruit(fruit Fruit) {
	fmt.Println("I have this fruit:", fruit.String())
}

func main() {
	apple := Apple{"Golden Delicious"}
	orange := Orange{"large"}
	PrintFruit(apple)
	PrintFruit(orange)
}
```

```
I have this fruit: A Golden Delicious apple
I have this fruit: A large orange
```
