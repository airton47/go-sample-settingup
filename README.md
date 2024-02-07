# Guide to Set Up a Go App

Primero de se debe inicializar la aplicacion de la siguiente forma:

```sh
go mod init sample-app
```

Con el comando anterior se creara un archivo `go.mod` en la raiz del proyecto, dicho archivo servira para tener el control de versiones y el manejo de paquetes y dependencias que se usaran en la aplicacion. Dicho archivo tendra un contenido similar a este:

```go
module sample-app

go 1.22.0

require{
    github.com/some/dependency v1.2.3
    github.com/another/dependency v1.1.2
}
```

A continuacion se debe crear el archivo principal en donde se ejecutara la función de entrada del la aplicacion:

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

> [!NOTE]
> Notas: El compilador de Go es estricto y no permitira que haya variables no usadas en el codigo que se ha escrito.

> [!TIP]
> Blanck Identifier: `_` es una guion bajo utilizado para obviar el uso de variables indefinidas dentro del codigo de `Go`.

Ademas de la funcion prindicipal es posible definir mas de una funcion de inicializacion en nuestra aplicacion, las funciones `init` se ejecutaran en roden y la funcion `main` de arriba hacia abajo segun se hayan definido, dichas funciones `init` son el lugar ideal para inicializar conexiones a bases de datos o cargar archivos de propiedades.

> [!WARNING]
> Nota: las funciones `init` no pueden ser llamdas o referenciadas directamente en la funcion `main` de nuestra aplicacion.

```go
package main

import "fmt"

func init() {
  fmt.Println(a.... "This runs first")
}

func main() {
    fmt.Println(a..., "This runs after init()")
  init() // Esto provocara un Error
}

func init() {
  fmt.Println(a..., "This runs second")
}
```

> [!IMPORTANT]
> Convenciones: El nombre del paquete debera ser igual al nombre de la carpeta en donde esta contenido
> Ademas los elementos del paquete con identificadores con inicial `Mayuscula` seran visibles fuera del paquete, mientras que aquellos con inicial `Minuscula` deberan mantenerse como privados y no accesibles fuera del paquete.

```go
package handler

import (
  "awesome/view/home"
  "awesome/view/write"
  "github.com/labstack/echo/v4"
)

type BasicHandler struct{}

func (h BasicHandler) ShowHome (ctx echo.Context) error {
  return render(ctx, home.ShowHome())
}

func (h BasicHandler) ShowWrite(ctx echo. Context) error {
  return render(ctx, write.ShowWrite())
}
```

Para ejecutar la aplicacion y el codigo de esta, se usa el siguiente comando en la terminal:

```sh
# ejecutar
go run .
# o bien
go run ./sample-app.go
```

Para construir y compilar el codigo de nuestra aplicacion se debe escribir en la terminal el siguiente comando:

```sh
go build sample-app.go
```

El comando anterior genera un archivo ejecutable como resultado de la operación.
