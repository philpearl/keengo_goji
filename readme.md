#keengo goji

Middleware for [Goji](https://github.com/zenazn/goji) to track HTTP requests and responses on keen.io.

See the documentation at https://godoc.org/github.com/philpearl/keengo_goji

## Example
Here's how I use this middleware to track calls to my API.

```golang

package main

import (
        "fmt"
        "net/http"

        "github.com/philpearl/keengo_goji"

        "github.com/zenazn/goji"
        "github.com/zenazn/goji/web"
)

func hello(c web.C, w http.ResponseWriter, r *http.Request) {
        fmt.Fprintf(w, "Hello, %s!", c.URLParams["name"])
}

func main() {
        goji.Use(keengo_goji.BuildMiddleWare("mykeenprojectID", "mykeenwritekey","requests", nil)
        goji.Get("/hello/:name", hello)
        goji.Serve()
}

```
