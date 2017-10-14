# echo-logrus
## Overview
Middleware echo-logrus is a [logrus](https://github.com/sirupsen/logrus) logger support for [Echo](https://github.com/labstack/echo).  
This middleware is working on echo v3.

## Getting Started
### For [dep](https://github.com/golang/dep) users
When your project top dir run this.  
```bash
$ dep ensure -add github.com/neko-neko/echo-logrus
```

### Other users
Run this.  
```bash
$ go get github.com/neko-neko/echo-logrus
```

## Example
```go
package main

import (
	"os"
	"time"

	"github.com/Sirupsen/logrus"
	"github.com/labstack/echo"
	echoLog "github.com/labstack/gommon/log"
	"github.com/neko-neko/echo-logrus/log"
	"github.com/neko-neko/echo-logrus/middleware"
)

func main() {
	e := echo.New()

	// Logger
	log.Logger().SetOutput(os.Stdout)
	log.Logger().SetLevel(echoLog.INFO)
	log.Logger().SetFormatter(&logrus.JSONFormatter{
		TimestampFormat: time.RFC3339,
	})
	e.Logger = log.Logger()
	e.Use(middleware.Logger())
	log.Info("Logger enabled!!")

	e.Logger.Fatal(e.Start(":1323"))
}
```
