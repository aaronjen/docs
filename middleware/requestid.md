# RequestID

RequestID middleware for [Fiber](https://github.com/gofiber/fiber) that adds an indentifier to the response.

## Signatures

```go
func New(config ...Config) fiber.Handler
```

## Examples

Import the middleware package that is part of the [Fiber web framework](https://github.com/gofiber/fiber)

```go
import (
  "github.com/gofiber/fiber/v2"
  "github.com/gofiber/fiber/v2/middleware/requestid"
)
```

After you initiate your Fiber app, you can use the following possibilities:

```go
// Default middleware config
app.Use(requestid.New())

// Or extend your config for customization
app.Use(requestid.New(requestid.Config{
    Header:    "X-Custom-Header",
    Generetor: func() string {
        return "static-id"
    }
}))
```

## Config

```go
// Config defines the config for middleware.
type Config struct {
    // Next defines a function to skip this middleware when returned true.
    //
    // Optional. Default: nil
    Next func(c *fiber.Ctx) bool

    // Header is the header key where to get/set the unique request ID
    //
    // Optional. Default: "X-Request-ID"
    Header string

    // Generator defines a function to generate the unique identifier.
    //
    // Optional. Default: func() string {
    //   return utils.UUID()
    // }
    Generator func() string
}
```

## Default Config

```go
var ConfigDefault = Config{
    Next:      nil,
    Header:    fiber.HeaderXRequestID,
    Generator: func() string {
        return utils.UUID()
    },
}
```

