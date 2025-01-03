# Functions

> Defina y llame a las funciones, etiquete sus argumentos y use sus valores de retorno
> 

Las funciones son bloques de código que realizan tareas específicas y se identifican por un nombre. Swift ofrece una sintaxis flexible para definir funciones, incluyendo parámetros con valores predeterminados y funciones anidadas. Cada función tiene un tipo que incluye sus parámetros y tipo de retorno, facilitando su uso como parámetros en otras funciones.

# ***1. Definición de funciones***

Una función se define utilizando la palabra clave `func` , seguida del nombre de la función, los parámetros (si los hay), el tipo de valor que devuelve (si lo tiene) y el cuerpo de la función (el código que ejecuta)

```swift
func nombreDeLaFuncion(parametros) -> TipoDeValorDeRetorno {
    // Cuerpo de la función
    return valor
}
```

- `nombreDeLaFuncion`: El nombre que le das a la función
- `parametros`: Los valores que la función recibe (opcional)
- `TipoDeValorDeRetorno`: El tipo de dato que la función devuelve (opcional si no devuelve nada)
- `cuerpo de la función`: El bloque de código que realiza una acción

```swift
func saludar(nombre: String) {
    print("¡Hola, \(nombre)!")
}

saludar(nombre: "Juan")
// ¡Hola, Juan!
```

<aside>
📎

*Este código puede leerse como:*

- *La función `saludar` toma un parámetro llamado `nombre` de tipo String*
- *No devuelve ningún valor, por lo que no se especifica el tipo de retorno (se asume que es `Void`, es decir, no devuelve nada)*
</aside>

# ***2. Funciones con valor de retorno***

Las funciones pueden devolver un valor. Para ello, se especifica el tipo de retorno después de la lista de parámetros

```swift
func sumar(a: Int, b: Int) -> Int {
    return a + b
}

let resultado = sumar(a: 3, b: 4)
// resultado es 7
```

<aside>
📎

*Este código puede leerse como:*

- *La función `sumar` toma dos parámetros `a` y `b` de tipo Int*
- *Devuelve un valor de tipo Int, que es la suma de `a` y `b`*
</aside>

# ***3. Funciones sin parámetros opcionales***

También puedes definir funciones que no reciben parámetros ni devuelven ningún valor

```swift
func saludarMundo() {
    print("¡Hola, mundo!")
}

saludarMundo()
// ¡Hola, mundo!
```

# ***4. Funciones con parámetros Opcionales***

Puedes utilizar parámetros opcionales, lo que significa que la función puede recibir o no un valor para esos parámetros. Esto se logra con el uso del tipo opcional 

```swift
func saludar(nombre: String?) {
    if let nombreDesempaquetado = nombre {
        print("¡Hola, \(nombreDesempaquetado)!")
    } else {
        print("¡Hola, invitado!")
    }
}

saludar(nombre: "Juan")  // Imprime: ¡Hola, Juan!
saludar(nombre: nil)     // Imprime: ¡Hola, invitado!

```

<aside>
📎

*Este código puede leerse como:*

- *El parámetro `nombre` es opcional de tipo String*
- *Usamos `if let` para desempaquetar el valor de `nombre` si está presente, y si no, se imprime un saludo genérico*
</aside>

# ***5. Funciones con valores de defecto***

Puedes asignar valores por defecto a los parámetros, lo que permite llamarlos sin tener que especificar todos los argumentos

```swift
func saludar(nombre: String = "invitado") {
    print("¡Hola, \(nombre)!")
}

saludar()        // Imprime: ¡Hola, invitado!
saludar(nombre: "Juan")  // Imprime: ¡Hola, Juan!
```

En este caso, el valor por defecto para `nombre` es `"invitado"`, pero si se proporciona un valor explícito, ese valor se usará

# ***6. Funciones con Variadic Parameters***

Swift permite funciones con parámetros **variádicos**, lo que significa que la función puede aceptar una cantidad variable de argumentos del mismo tipo. Estos parámetros se manejan como un arreglo dentro de la función.

```swift
func imprimirNumeros(_ numeros: Int...) {
    for numero in numeros {
        print(numero)
    }
}

imprimirNumeros(1, 2, 3, 4, 5)
// 1
// 2
// 3
// 4
// 5
```

<aside>
📎

*Este código puede leerse como:*

- *El parámetro `numeros` es variádico (`Int...`), lo que significa que puede aceptar cualquier cantidad de enteros*
- *Internamente, Swift maneja estos parámetros como un* array
</aside>

# ***7. Funciones Anidadas***

Puedes definir funciones dentro de otras funciones. Estas funciones internas pueden ser útiles cuando necesitas realizar operaciones locales que no requieren ser accesibles desde fuera de la función externa

```swift
func operar() {
    func sumar(a: Int, b: Int) -> Int {
        return a + b
    }
    
    let resultado = sumar(a: 5, b: 3)
    print("Resultado de la suma: \(resultado)")
}

operar()
// Resultado de la suma: 8
```

# ***8. Funciones de Orden Superior***

Las funciones de orden superior son aquellas que pueden recibir otras funciones como parámetros o devolver una función. Swift tiene un soporte excelente para funciones de este tipo, lo que facilita la creación de código más flexible y abstracto.

```swift
func aplicarOperacion(_ a: Int, _ b: Int, operacion: (Int, Int) -> Int) -> Int {
    return operacion(a, b)
}

let resultado = aplicarOperacion(3, 4, operacion: sumar)
// Devuelve 7
```

<aside>
📎

*Este código puede leerse como:*

- `*aplicarOperacion` es una función de orden superior que toma dos enteros y una función `operacion` que define cómo operar esos enteros*
</aside>

# ***9. Closures como funciones***

En Swift, los **closures** son bloques de código que pueden usarse de manera similar a las funciones. A menudo se usan cuando se necesita una función como parámetro, o para operaciones cortas y específicas.

```swift
let multiplicar = { (a: Int, b: Int) -> Int in
    return a * b
}

let resultado = multiplicar(3, 4)
// Resultado es 12

```

El closure `multiplicar` funciona como una función, pero puede ser definido de manera más concisa

# ***10. Funciones Asíncronas***

Swift también admite funciones asíncronas que pueden ser ejecutadas de manera concurrente. Estas funciones se definen usando la palabra clave `async` y pueden devolver un valor de forma asincrónica usando `await`.

```swift
func obtenerDatos() async -> String {
    // Simula una tarea asíncrona
    return "Datos obtenidos"
}

```

Para llamar una función asíncrona, necesitas usar `await`:

```swift
async {
    let datos = await obtenerDatos()
    print(datos)
}
```

# ***11. Funciones inout***

Puedes pasar parámetros a las funciones por referencia, usando la palabra clave `inout`. Esto permite que las funciones modifiquen los valores de los parámetros directamente.

```swift
func incrementar(valor: inout Int) {
    valor += 1
}

var numero = 5
incrementar(valor: &numero)
// El valor de numero se incrementa a 6

```

En este caso, el parámetro `valor` se pasa por referencia y su valor se modifica dentro de la función

---