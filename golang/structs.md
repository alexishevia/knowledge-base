# Structs
```go
package main

import "fmt"

type Movie struct {
	Actors      []string
	Rating      float32
	ReleaseYear int
	Title       string
}

func main() {
	episodeIV := Movie{
		Title:       "Star Wars: A New Hope",
		Rating:      5.0,
		ReleaseYear: 1977,
	}

	episodeIV.Actors = []string{
		"Mark Hamill",
		"Harrison Ford",
		"Carrie Fisher",
	}

	fmt.Println(episodeIV.Title, "has a rating of", episodeIV.Rating)
	fmt.Println("Actors:")
	for i, actor := range episodeIV.Actors {
		fmt.Println(i, ":", actor)
	}
}
```

```
Star Wars: A New Hope has a rating of 5
Actors:
0 : Mark Hamill
1 : Harrison Ford
2 : Carrie Fisher
```

## Type Methods
You can add your own methods to any types you define. This is as easy as defining a function with a receiver type. 

A receiver type is similar to a single parameter definition in a function, but is declared just after the func keyword but before the function name.

```go
package main

import "fmt"

type Movie struct {
	Actors      []string
	Rating      float32
	ReleaseYear int
	Title       string
}

func (movie Movie) DisplayTitle() string {
	return fmt.Sprintf("%s (%d)", movie.Title, movie.ReleaseYear)
}

func main() {
	episodeIV := Movie{
		Title:       "Star Wars: A New Hope",
		Rating:      5.0,
		ReleaseYear: 1977,
	}
	fmt.Println(episodeIV.DisplayTitle())
}
```

```
Star Wars: A New Hope (1977)
```

Receiver types can also refer to a pointer of a type. Without a pointer, any changes that you make to the instance will fail to make it any further than the end of the method.

```go
package main

import "fmt"

type Counter struct {
	Count int
}

func (c Counter) Increment() {
	c.Count++
}

func (c *Counter) IncrementWithPointer() {
	c.Count++
}

func main() {
	counter := &Counter{}
	fmt.Println(counter.Count)

	counter.Increment()
	fmt.Println(counter.Count)

	counter.IncrementWithPointer()
	fmt.Println(counter.Count)
}
```

```
0
0
1
```
