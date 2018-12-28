# HTTP Server Request Handlers

PSR-15 Like HTTP Server Request Handlers Interface For Hack

## Require

HHVM 3.30.0 and above.  
required [hsl-experimental](https://github.com/hhvm/hsl-experimental)

## Install

```bash
$ hhvm $(which composer) require ytake/hack-http-server-request-handlers-interfaces
```

## Usage

Golang style

```go
func middleware(next http.HandlerFunc) http.HandlerFunc {
  return func(w http.ResponseWriter, r *http.Request) {
		log.Printf("Hello World, %s", r.RequestURI)
		next.ServeHTTP(w, r)
	}
}
```

For Hack

```hack
<?hh // strict

namespace Acme\Middleware;

use type HH\Lib\Experimental\IO\WriteHandle;
use type Facebook\Experimental\Http\Message\ResponseInterface;
use type Facebook\Experimental\Http\Message\ServerRequestInterface;
use type Nazg\Http\Server\MiddlewareInterface;
use type Nazg\Http\Server\RequestHandlerInterface;

final class ExampleMiddleware implements MiddlewareInterface {

  public function process(
    WriteHandle $writeHandle,
    ServerRequestInterface $request,
    RequestHandlerInterface $handler,
  ): ResponseInterface {
    return $handler->handle($write, $request);
  }
}
```
