# Package service
This package provides a simple way to manage services in a Go application. It allows you to register and retrieve services using Go interfaces.

## Installation
To install this package, use the `go get` command:

```bash
go get github.com/lab210-dev/service
```

## Usage
To use this package, you must first register your service using the Register function :

```go
package example

import "github.com/lab210-dev/service"

type MyService interface {
	DoSomething()
}

type myServiceImpl struct{}

func (s *myServiceImpl) DoSomething() {
	// Do something here...
}

func init() {
	service.Register(&myServiceImpl{})
}
```

You can now retrieve your service using the `Get` function :

```go
func main() {
	myService := service.Get().(MyService)
	myService.DoSomething()
}
```

You can also use the GetAfterRegister function to execute a callback once the service has been registered :

```go 
func main() {
	service.GetAfterRegister(func(s MyService) {
		s.DoSomething()
	})
}
```

To reset all registered services, use the Reset function :
```go
service.Reset()
```

### Notes
- Services must be registered using interfaces, not concrete types.
- If you try to retrieve a service that has not been registered, an error will panic. Make sure to check if the service has been registered using GetServiceByIdentifier before using it.

I hope this package is helpful to you! If you have any questions or comments, don't hesitate to contact me.