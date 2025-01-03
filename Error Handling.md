# Error Handling

> Responder y recuperarse de los errores.
> 

El manejo de errores (Error Handling) es un enfoque estructurado que te permite manejar situaciones excepcionales o errores que pueden ocurrir durante la ejecución de tu programa. En lugar de depender de códigos de error o condiciones, Swift utiliza lanzamiento y captura de errores.

# ***1. Conceptos Básicos***

- Definir tipos de error: Conformes al protocolo `Error`.
- Lanzar errores: Usando la palabra clave `throw`.
- Capturar errores: Utilizando una estructura `do-catch`.
- Propagar errores: Usando la palabra clave `throws` en funciones.

# ***2. Definir y Lanzar Errores***

```swift
enum ValidationError: Error {
    case emptyField
    case invalidEmail
}

func validateEmail(_ email: String) throws {
    guard !email.isEmpty else {
        throw ValidationError.emptyField
    }
    guard email.contains("@") else {
        throw ValidationError.invalidEmail
    }
}

do {
    try validateEmail("example.com")
} catch ValidationError.emptyField {
    print("El campo está vacío.")
} catch ValidationError.invalidEmail {
    print("El email no es válido.")
} catch {
    print("Ocurrió un error inesperado: \(error).")
}
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición de un `enum` para los errores de validación*

*Aquí se define un `enum` llamado `ValidationError` que adopta el protocolo `Error`. Este `enum` tiene dos casos posibles:*

`*emptyField`: Para indicar que el campo está vacío.*

`*invalidEmail`: Para indicar que el correo electrónico proporcionado no es válido.*

*Esto servirá para representar los posibles errores que puedan ocurrir durante la validación de un correo electrónico.*

*2. Función de validación `validateEmail`*

*La función `validateEmail` toma un `String` llamado `email` y verifica dos cosas:*

*Comprobación de si el campo está vacío:*

- *Usamos un `guard` para verificar si el correo electrónico está vacío. Si lo está, lanzamos el error `ValidationError.emptyField`.*

*Comprobación de si el correo contiene un "@":*

- *En un segundo `guard`, verificamos si el correo electrónico contiene el carácter "@" (un chequeo básico para saber si el formato es válido, aunque no suficiente para una validación completa). Si no lo contiene, lanzamos el error `ValidationError.invalidEmail`.*

*La palabra clave `throws` en la declaración de la función significa que esta función puede lanzar (o "tirar") un error si alguna de las condiciones no se cumple.*

*3. Bloque `do-catch`*

*Este bloque maneja los errores que puedan ocurrir al llamar a la función `validateEmail`.*

`*do`: Aquí se intenta ejecutar la función `validateEmail("example.com")`. En este caso, el correo "example.com" no contiene un "@" y por lo tanto lanzará el error `ValidationError.invalidEmail`.*

`*catch ValidationError.emptyField`: Si la función lanza el error `emptyField`, este bloque se ejecutará y mostrará el mensaje "El campo está vacío."*

`*catch ValidationError.invalidEmail`: Si la función lanza el error `invalidEmail`, este bloque se ejecutará y mostrará el mensaje "El email no es válido." Este es el bloque que se ejecutará en este caso porque "example.com" no tiene el "@".*

`*catch` general: Si ocurre cualquier otro tipo de error no específico, este bloque manejará el error y lo imprimirá en formato de texto, indicando que hubo un "error inesperado". En este caso no se ejecutará porque todos los errores posibles están cubiertos por los bloques anteriores.*

*Ejecución del código*

*Si ejecutamos el código, el flujo será el siguiente:*

*Se llama a `validateEmail("example.com")`.*

*La función intenta verificar si el correo está vacío (no lo está), luego verifica si contiene un "@", y como no lo contiene, lanza el error `ValidationError.invalidEmail`.*

*El bloque `catch ValidationError.invalidEmail` se ejecuta, imprimiendo:"El email no es válido."*

*Resumen*

*Este código es un ejemplo de validación de correos electrónicos que usa un `enum` para definir errores específicos (`emptyField` y `invalidEmail`), y luego maneja esos errores con un bloque `do-catch`. Este patrón es útil para realizar validaciones o cualquier operación que pueda fallar y manejar esos fallos de manera controlada.*

</aside>

# ***3. Propagar Errores***

```swift
func loadFile(named filename: String) throws -> String {
    guard filename == "data.txt" else {
        throw NSError(domain: "Archivo no encontrado", code: 404, userInfo: nil)
    }
    return "Contenido del archivo"
}

func readFile() {
    do {
        let content = try loadFile(named: "missing.txt")
        print(content)
    } catch {
        print("Error al leer el archivo: \(error.localizedDescription)")
    }
}
```

<aside>
📎

*Este código puede leerse como:*

*1. Función `loadFile(named:)`*

*Explicación:*

*Parámetro: La función recibe un parámetro `filename` de tipo `String`, que es el nombre del archivo que se intenta cargar.*

*Uso de `guard`: El bloque `guard` verifica si el nombre del archivo es igual a `"data.txt"`. Si no lo es, se ejecuta el bloque de código dentro de `else`, lo que hace que la función lance un error usando `throw`.*

- *En este caso, se lanza un error de tipo `NSError` con un dominio de "Archivo no encontrado" y un código de error `404`.*

*Lanzamiento de error: Si el archivo no se llama `"data.txt"`, la función lanza el error y se detiene en ese punto, devolviendo el control al bloque `catch` que lo maneja (más adelante en el código).*

*Valor de retorno: Si el nombre del archivo es `"data.txt"`, la función devuelve el texto `"Contenido del archivo"`.*

`*throws`:*

*La palabra clave `throws` indica que esta función puede lanzar un error, por lo tanto, debe ser llamada dentro de un bloque `do-catch`, como veremos en la función `readFile()`.*

*2. Función `readFile()`*

*Explicación:*

*Bloque `do`: Dentro del bloque `do`, se llama a la función `loadFile(named:)` utilizando `try`, lo que indica que estamos intentando ejecutar una función que puede lanzar un error. En este caso, el archivo solicitado es `"missing.txt"`, que no coincide con `"data.txt"`.*

*Manejo de error con `catch`: Si la función `loadFile(named:)` lanza un error (como es el caso aquí porque el archivo no se llama `"data.txt"`), el flujo de ejecución se mueve al bloque `catch`.*

`*catch`: Dentro del bloque `catch`, el error se captura y se imprime un mensaje de error usando `error.localizedDescription`, que proporciona una descripción legible del error (en este caso, el mensaje será "Archivo no encontrado" porque así está configurado en el `NSError`).*

*Comportamiento esperado:*

*La función `readFile()` llama a `loadFile(named: "missing.txt")`.*

*El archivo `"missing.txt"` no existe según la implementación de `loadFile(named:)`, por lo que se lanza un error con el código `404`.*

*El flujo de ejecución entra en el bloque `catch`, donde se imprime:`"Error al leer el archivo: El dominio del error es 'Archivo no encontrado' y el código es 404."`*

*Resumen:*

*La función `loadFile(named:)` verifica si el nombre del archivo es `"data.txt"`. Si no lo es, lanza un error.*

*La función `readFile()` llama a `loadFile(named:)` y maneja cualquier error que ocurra usando un bloque `do-catch`. Si se produce un error, se imprime un mensaje explicativo del error.*

</aside>

# ***4.** Usar TRY? para Manejo Seguro*

Puedes convertir el resultado en un valor opcional. Si ocurre un error, el resultado será `nil`.

```swift
let email = try? validateEmail("example.com")
print(email) // nil
```

<aside>
📎

*Este código puede leerse como:*

*1. `validateEmail("example.com")`*

*En esta parte, se está llamando a una función llamada `validateEmail`, que probablemente esté diseñada para verificar si un correo electrónico (en este caso `"example.com"`) es válido según ciertas reglas (por ejemplo, si tiene el formato adecuado, como `usuario@dominio.com`).*

*La función `validateEmail` parece estar lanzando errores (lo cual indica que puede ser una función que usa el mecanismo de errores en Swift), ya que está siendo llamada con `try?`.*

*2. `try?`*

*El operador `try?` se usa en Swift para manejar errores de manera opcional. Esto significa que si la función `validateEmail` lanza un error, no causará una interrupción del flujo del programa, sino que el resultado de la función será `nil`. En otras palabras:*

*Si la función `validateEmail` tiene éxito (es decir, no lanza un error), el valor devuelto se asigna a la variable `email`.*

*Si la función lanza un error, `email` se asignará a `nil`.*

*Este operador convierte el error en un valor opcional (`nil` en caso de error), lo que facilita el manejo de errores sin necesidad de usar un bloque `do-catch`.*

*3. `let email = try? validateEmail("example.com")`*

*Esta línea intenta ejecutar la función `validateEmail` con el argumento `"example.com"`. Dado que no se está manejando el error explícitamente (con un `do-catch`), el resultado se asigna a `email`, que será de tipo opcional (`String?`):*

*Si `validateEmail` devuelve un valor, `email` tendrá ese valor (probablemente una cadena de texto).*

*Si ocurre un error en `validateEmail` (por ejemplo, si el correo no es válido), `email` será `nil`.*

*4. `print(email)`*

*Finalmente, esta línea imprime el valor de `email`. Como `email` es opcional, la impresión mostrará:*

*El valor de `email` si la validación fue exitosa.*

`*nil` si ocurrió un error en la validación.*

*Posible Implementación de `validateEmail`*

*Aunque no se proporciona el código de la función `validateEmail`, se puede suponer que esta función podría verse algo así:*

```swift
func validateEmail(_ email: String) throws -> String {
    // Supón que validamos el correo electrónico aquí
    // Si el correo es válido, lo devolvemos
    // Si no es válido, lanzamos un error
    if email.contains("@") {
        return email
    } else {
        throw ValidationError.invalidEmail
    }
}
```

*En este ejemplo, si el correo electrónico no contiene el símbolo `@`, lanzaría un error del tipo `ValidationError.invalidEmail`.*

*Resumen*

*El código `let email = try? validateEmail("example.com")` intenta validar un correo electrónico y manejar el error de forma segura:*

*Si el correo electrónico es válido, se asigna a `email`.*

*Si el correo electrónico no es válido, `email` será `nil`.*

*Luego, se imprime el valor de `email` (que podría ser el correo validado o `nil` si ocurrió un error).*

</aside>

# ***5.** TRY! para Errores No Controlados*

Usa `try!` si estás completamente seguro de que la operación no fallará. Esto provocará un error en tiempo de ejecución si falla.

```swift
let validEmail = try! validateEmail("user@example.com")
print(validEmail)
```

<aside>
📎

*Este código puede leerse como:*

*1. `let validEmail = ...`*

*Aquí estamos declarando una constante llamada `validEmail` que va a almacenar el resultado de la función `validateEmail("user@example.com")`.*

`*let` se usa para declarar una constante (es decir, un valor que no puede cambiar después de su asignación).*

*El tipo de `validEmail` se determinará automáticamente dependiendo del tipo de valor que devuelva la función `validateEmail`.*

*2. `validateEmail("user@example.com")`*

*Este es un llamado a la función `validateEmail`, pasando como argumento el string `"user@example.com"`, que parece representar una dirección de correo electrónico.*

*Aunque no vemos la implementación de `validateEmail` en el código que proporcionas, podemos suponer que su propósito es verificar si la cadena pasada como argumento (`"user@example.com"`) es un correo electrónico válido.*

*Es probable que `validateEmail` sea una función que devuelve algún tipo de valor, como un `Bool` (para indicar si el correo electrónico es válido o no) o un `String` (que podría ser el correo electrónico validado o un error en caso de que no sea válido).*

*Es importante notar que `validateEmail` podría lanzar un error si la validación falla, lo cual explicaría el uso de `try!`.*

*3. `try!`*

*Este operador en Swift se utiliza cuando estás trabajando con funciones que pueden lanzar errores (funciones que tienen la palabra clave `throws` en su definición).*

`*try` se usa para llamar a una función que puede lanzar un error.*

`*try!` se usa para forzar la ejecución de la función y presumir que no ocurrirá ningún error. Si la función lanza un error, el programa se detendrá inmediatamente (se producirá un crash).*

*En este caso, se está usando `try!` para llamar a `validateEmail`. Esto significa que el código está asumiendo que la función `validateEmail` no fallará y que el correo electrónico proporcionado es válido. Si `validateEmail` encuentra un error o falla, el programa se detendría en ese punto.*

*4. `print(validEmail)`*

*Finalmente, el valor de `validEmail` (que es el resultado de la validación del correo electrónico) se imprime en la consola.*

*¿Qué puede hacer `validateEmail`?*

*La función `validateEmail` probablemente realiza alguna validación para verificar si el correo electrónico tiene el formato correcto (por ejemplo, que contiene "@" y un dominio válido). Si el correo es válido, podría devolver `true` o el mismo correo como resultado; si no lo es, podría lanzar un error o devolver algún mensaje de error.*

*Resumen*

*Este código valida si la dirección de correo electrónico `"user@example.com"` es válida mediante la función `validateEmail`. Si la validación es exitosa, el resultado se almacena en la constante `validEmail` y se imprime. Si ocurre un error, el programa se detendrá debido al uso de `try!`.*

*Es un ejemplo de cómo usar manejo de errores de manera explícita en Swift, aunque al usar `try!`, el manejo de errores es omiso, ya que asume que no fallará.*

</aside>

# ***6. Personalizar Errores***

Puedes incluir datos adicionales en tus errores.

```swift
enum NetworkError: Error {
    case badURL(String)
    case timeout(Int)
}

func fetchData(from url: String) throws {
    guard url.starts(with: "https://") else {
        throw NetworkError.badURL(url)
    }
    throw NetworkError.timeout(30)
}

do {
    try fetchData(from: "http://example.com")
} catch NetworkError.badURL(let url) {
    print("URL inválida: \(url)")
} catch NetworkError.timeout(let duration) {
    print("Tiempo de espera agotado después de \(duration) segundos.")
} catch {
    print("Error inesperado: \(error)")
}
```

<aside>
📎

*Este código puede leerse como:*

1. *Definición del Enum `NetworkError`:*

*Aquí se define un enum llamado `NetworkError` que conforma el protocolo `Error` (lo cual es necesario para usarlo en un bloque `do-catch`). Este enum tiene dos casos posibles:*

`*badURL(String)`: Este caso representa un error relacionado con una URL inválida. El caso almacena un valor de tipo `String`, que es la URL que causó el error.*

`*timeout(Int)`: Este caso representa un error de tiempo de espera agotado (timeout). El caso almacena un valor de tipo `Int`, que indica la duración del tiempo de espera en segundos.*

1. *Función `fetchData(from:)`:*

*La función `fetchData(from:)` intenta simular una operación que podría fallar. Está marcada con `throws`, lo que significa que puede lanzar errores que deben ser manejados por el código que llame a la función.*

`*guard`: Verifica que la URL empiece con `"https://"`. Si no es así, se lanza un error de tipo `NetworkError.badURL`con la URL problemática.*

`*throw NetworkError.timeout(30)`: Si la URL pasa la verificación, inmediatamente se lanza un error de tipo `NetworkError.timeout` con el valor 30, que podría representar un tiempo de espera agotado después de 30 segundos.*

1. *Bloque `do-catch`:*

*El bloque `do-catch` se utiliza para manejar los posibles errores que podrían surgir al llamar a la función `fetchData(from:)`.*

`*try fetchData(from: "http://example.com")`: Aquí se llama a la función `fetchData(from:)`, pasando una URL inválida (`"http://example.com"`). Debido a que esta URL no comienza con `"https://"`, el código lanzará un error de tipo `badURL`.*

*Primer `catch`: Captura el error `NetworkError.badURL` y extrae el valor de la URL que causó el error, imprimiendo el mensaje: `"URL inválida: http://example.com"`.*

*Segundo `catch`: Captura el error `NetworkError.timeout` y extrae la duración del timeout. Si se hubiera lanzado un error de timeout, habría impreso algo como: `"Tiempo de espera agotado después de 30 segundos."`.*

`*catch` final: Si algún otro tipo de error (no relacionado con `NetworkError`) es lanzado, este bloque de captura final se encargaría de manejarlo, imprimiendo `"Error inesperado: ..."`. Aunque en este caso no es necesario, porque los errores lanzados son del tipo `NetworkError`.*

1. *Explicación del flujo de ejecución:*

*Se llama a `fetchData(from:)` con la URL `"http://example.com"`.*

*El `guard` falla porque la URL no comienza con `"https://"`, por lo que lanza un error de tipo `NetworkError.badURL`.*

*El bloque `catch` captura ese error y se imprime: `URL inválida: http://example.com`.*

*Nota: En el código que has proporcionado, se lanza un `timeout` después de lanzar el error de URL inválida, pero el código nunca llega a ese punto porque el primer error (URL inválida) se lanza primero y se captura en el bloque `catch`.*

*Resumen:*

*El código define un enum `NetworkError` con dos tipos de errores: URL inválida y timeout.*

*La función `fetchData(from:)` lanza errores dependiendo de la URL proporcionada.*

*El bloque `do-catch` maneja estos errores y proporciona mensajes adecuados según el tipo de error que se lance.*

*Este patrón es común para manejar errores en Swift, especialmente cuando se trabaja con operaciones que pueden fallar, como peticiones de red.*

</aside>

***Resumen***

Swift ofrece un sistema de manejo de errores flexible y seguro, con opciones para:

- Detectar errores específicos (`do-catch`).
- Manejar errores opcionalmente (`try?`).
- Lanzar errores fatales cuando es seguro (`try!`).

---