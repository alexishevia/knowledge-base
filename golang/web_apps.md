# Web Applications with Go
Go’s standard library contains a variety of packages to build web applications, like `net/http`.

However, there are some packages that make building web apps a bit easier:
- [Gorilla Web Toolkit](http://www.gorillatoolkit.org/)

## Hello World
```go
package main

import (
	"fmt"
	"net/http"
)

func main() {
	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprintf(w, "Hello Gopher")
	})

	err := http.ListenAndServe(":3001", nil)

	if err != nil {
		fmt.Println(err)
	}
}
```

## Route Pattern Matching
Go has a built-in [http.ServeMux](https://golang.org/pkg/net/http/#ServeMux) type. `ServeMux` is a request multiplexer, which handles matching an incoming request’s URL against the registered handlers and calling the handler for the pattern that most closely matches the URL.

The http package creates a default `ServeMux` instance for you, and the `http.HandleFunc` function is actually a shortcut to the `(*ServeMux) HandleFunc` method on that default `ServeMux`.

Read more about ServeMux and Handlers: [here](https://www.alexedwards.net/blog/a-recap-of-request-handling)

```go
package main

import (
	"fmt"
	"net/http"
)

func main() {
	mux := http.NewServeMux()
	mux.HandleFunc("/articles/", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprintf(w, "Hello from /articles/")
	})
	mux.HandleFunc("/users", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprintf(w, "Hello from /users")
	})
	err := http.ListenAndServe(":3001", mux)
	if err != nil {
		fmt.Println(err)
	}
}
```

There are two types of patterns:
- path: defined without a trailing backslash `/`, and refers to an explicit path.
- subtree: include the trailing backslack `/`. Designed to match the start of a path.

```bash
curl http://localhost:3001/users
>> Hello from /users

curl http://localhost:3001/users/123
>> 404 page not found

curl http://localhost:3001/articles/
>> Hello from /articles/

curl http://localhost:3001/articles/123
>> Hello from /articles/
```

## Precedence
The length of a pattern is important. The longer a pattern is, the higher a precedence it has. A pattern of `/articles/latest/` has a higher precedence than `/articles/`, for example. Because of this order precedence, it makes no difference which order you add the routes in.

## Returning Errors
```go
http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
	http.Error(w, "Something has gone wrong", 500)
})
```

## The Handler Interface and Middlewares
Any type that implements the interface [http.Handler](https://golang.org/pkg/net/http/#Handler) can be passed to the [http.Handle](https://golang.org/pkg/net/http/#Handle) function, along with a pattern string.

It’s easy —and very common—to chain `http.Handler`s together to create middleware. For example, we could create a handler that requires a secret token to be sent via the query string in the request. If it finds the token, it will call the next handler; otherwise it will return a `404 Not Found` response:
```go
package main

import (
	"fmt"
	"net/http"
	"time"
)

// UptimeHandler writes the number of seconds since starting the response
type UptimeHandler struct {
	Started time.Time
}

func NewUptimeHandler() UptimeHandler {
	return UptimeHandler{Started: time.Now()}
}

func (h UptimeHandler) ServeHTTP(w http.ResponseWriter, req *http.Request) {
	fmt.Fprintf(w, fmt.Sprintf("Current Uptime: %s", time.Since(h.Started)))
}

// SecretTokenHandler secures a request with a secret token.
type SecretTokenHandler struct {
	next   http.Handler
	secret string
}

func (h SecretTokenHandler) ServeHTTP(w http.ResponseWriter, req *http.Request) {
	// Check the query string for the secret token
	if req.URL.Query().Get("secret_token") == h.secret {
		// The secret token matched, call the next handler
		h.next.ServeHTTP(w, req)
	} else {
		// No match, return a 404 Not Found response
		http.NotFound(w, req)
	}
}

func main() {
	http.Handle("/", SecretTokenHandler{
		next:   NewUptimeHandler(),
		secret: "foobar",
	})

	http.ListenAndServe(":3001", nil)
}
```

```bash
curl http://localhost:3001
>> 404 page not found

curl http://localhost:3001?secret_token=baz
>> 404 page not found

curl http://localhost:3001?secret_token=foobar
>> Current Uptime: 16.013515472s
```

## Working with JSON

```go
package main

import (
	"encoding/json"
	"fmt"
)

type Article struct {
	Name       string `json:"name"`
	AuthorName string `json:"author_name,omitempty"`
	draft      bool
}

func main() {
	article := Article{
		Name:       "JSON in Go",
		AuthorName: "Mal Curtis",
		draft:      true,
	}

	// Marshal / Stringify
	data, err := json.Marshal(article)
	if err != nil {
		fmt.Println("Couldn't marshal article:", err)
	} else {
		fmt.Println(string(data))
	}

	jsonString := `{
	"name": "10 reasons you will love Go",
	"author_name": "Jeff Winger"
}`

	// Unmarshal / Parse
	otherArticle := Article{}
	err = json.Unmarshal([]byte(jsonString), &otherArticle)
	if err != nil {
		panic(err)
	}

	fmt.Printf("%s by %s", otherArticle.Name, otherArticle.AuthorName)
}
```

```
{"name":"JSON in Go","author_name":"Mal Curtis"}
10 reasons you will love Go by Jeff Winger
```
