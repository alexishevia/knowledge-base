# Concurrency in Go
Concurrenty Patterns: https://www.youtube.com/watch?v=f6kdp27TYZs

To run code asynchronously inside a goroutine, we simply use the `go` command in front of the function call.

```go
package main

import (
	"fmt"
	"time"
)

func count() {
	for i := 1; i <= 10; i++ {
		fmt.Printf("%d,", i)
	}
}

func main() {
	go count()
	fmt.Println("Start")
	time.Sleep(time.Second)
	fmt.Println("Done")
}
```

```
Start
1,2,3,4,5,6,7,8,9,10,Done
```

Go maintains a philosophy of *Don’t communicate by sharing memory, share memory by communicating.* Instead of having variables that are accessed by multiple goroutines, Go provides a method to communicate between goroutines so that you only have to access variables in a single coordinating scope.

To enable this communication, Go has a special primitive called the channel. **Channels** are a way to send and receive data between goroutines, and provide a way to block your code until you receive information on it.

Channels are typed and created with the make command. Here’s an example creating a channel of type int: 
```
myChan := make(chan int)
```

Sending and receiving on a channel happens with the `<-` command. 

By placing the arrow in front of the channel, you’re saying that you want to receive from the channel (for example, `myInt := <-myChan` ), whereas placing the arrow after the channel is how to send on a channel (for example, `myChan <- 1` ). 

It’s important to note that this is a blocking action. If you’re sending on a channel and no code is ready to receive it, the execution will block, and vice versa when receiving on the channel, it will block if nothing is ready

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	intChan := make(chan int)

	for i := 1; i <= 10; i++ {
		go func(j int) {
			time.Sleep(time.Duration(j) * time.Second)
			intChan <- j
			if j == 10 {
				close(intChan)
			}
		}(i)
	}

	for j := range intChan {
		fmt.Printf("%d,", j)
	}

	fmt.Println("Done")
}
```

```
1,2,3,4,5,6,7,8,9,10,Done
```
