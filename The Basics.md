# The Basics

> Trabaja con tipos comunes de datos y escribe sintaxis básica.
> 

# ***1. Comando Print***

El comando `print` se usa para enviar información a la consola, lo cual es muy útil para depurar tu código, es decir, para verificar valores de variables, el flujo del programa o cualquier mensaje de interés.

```swift
print("Texto a mostrar")
```

Esto imprimirá el texto "Texto a mostrar" en la consola. Además, se pueden imprimir variables y expresiones dentro de `print`:

```swift
let nombre = "Juan"
print("Hola, \(nombre)") // Imprime: Hola, Juan
```

En este caso, el uso de `\(nombre)` es una forma de interpolación de cadenas, lo que significa que puedes insertar el valor de una variable o expresión dentro de una cadena de texto.

**Propiedades y Uso**

- Debugging: Usamos `print` para ver el valor de variables en diferentes puntos del código.
- Seguimiento del flujo del programa: Puedes agregar `print` en varias secciones del código para ver cómo se ejecuta.
- Imprimir datos complejos: Puedes imprimir cualquier tipo de datos (como arrays, diccionarios, objetos) y Swift automáticamente mostrará su descripción.
    
    ```swift
    let numeros = [1, 2, 3, 4]
    print(numeros)  // Imprime: [1, 2, 3, 4]
    ```
    

## ***1.1 Opciones adicionales***

El comando `print` tiene dos parámetros adicionales que se pueden usar:

- `separator`: Define un string que separa los elementos cuando hay más de uno. Por defecto es un espacio.
    
    ```swift
    print(1, 2, 3, separator: "-")  // Imprime: 1-2-3
    ```
    
- `terminator`: Especifica el carácter al final de la impresión. Por defecto es una nueva línea (`\n`).
    
    ```swift
    print("Hola", terminator: "") // No imprime un salto de línea al final.
    print("Mundo") // Continúa en la misma línea: "HolaMundo"
    ```
    

# *2. Comentarios*

Los comentarios se usan para agregar anotaciones al código que no afectan su ejecución, pero sirven para explicar o documentar lo que hace el código, lo que facilita su comprensión.

**Comentarios de una sola línea:**

Se usan con dos barras `//`. Todo lo que esté a la derecha de `//` en esa línea será ignorado por el compilador.

```swift
// Este es un comentario de una sola línea

let numero = 42  // También puedes escribir un comentario al final de una línea de código
```

**Comentarios multilínea:**

Se utilizan cuando el comentario ocupa varias líneas. Se abre con `/*` y se cierra con `*/`.

```swift
/*
Este es un comentario que puede
ocupar varias líneas.
Es útil para explicaciones más largas.
*/
```

También puedes usar `/*` para comentar parte de una línea de código:

```swift
let a = 10 /* esto es un comentario dentro de una línea */
```

**Propiedades y Usos de los Comentarios:**

- Documentación: Los comentarios son útiles para documentar funciones o algoritmos complejos, explicando lo que hace cada parte del código.
- Desactivar código temporalmente: Puedes comentar una sección del código para desactivarlo sin eliminarlo. Esto es útil, por ejemplo, al probar diferentes implementaciones o para desactivar funcionalidades temporalmente durante la depuración.
- Mejorar la legibilidad: Ayudan a que otras personas (o incluso tú mismo en el futuro) comprendan el propósito y la lógica detrás de ciertas secciones del código.

# ***3. Constantes y Variables***

En Swift, las constantes y variables son dos estructuras fundamentales para almacenar y manipular datos en tu código. La elección de una u otra depende de si el valor almacenado cambiará o permanecerá constante a lo largo de la ejecución del programa.

## ***3.1** Constantes Let*

- Definición: Una constante en Swift es una entidad cuyo valor no puede cambiar una vez que se le ha asignado. Se define con la palabra clave `let` .
    
    ```swift
    let nombreDeLaConstante = valor
    
    let nombre = "Juan"
    let pi = 3.14159
    ```
    
- Uso: Las constantes son útiles para almacenar datos que se sabe no cambiarán durante la ejecución del programa, como valores matemáticos (`pi`), datos de configuración, o datos de un usuario que no se modificarán.
- Ventajas:
    - Seguridad: Al ser inmutables, garantizan que los valores no se modifiquen accidentalmente.
    - Optimización: Swift puede optimizar el uso de memoria para constantes, ya que el valor no se actualiza.

## ***3.2 Variables Var***

- Definición: Una variable es una entidad cuyo valor puede cambiar a lo largo de la ejecución del programa. Se define con la palabra clave `var`.
    
    ```swift
    var nombreDeLaVariable = valor
    
    var edad = 25
    edad = 26 // Se permite cambiar el valor
    ```
    
- Uso: Las variables son útiles para valores que se espera que cambien, como el puntaje en un juego, el saldo de una cuenta, o datos temporales que puedan requerir modificaciones.
- Ventajas:
    - Flexibilidad: Permite almacenar datos dinámicos o temporales.
    - Interactividad: Ideal para valores que responden a acciones del usuario o datos en tiempo real.

## ***3.3 Diferencias clave entre Constantes y Variables***

| Característica | Constante (`let`) | Variable (`var`) |
| --- | --- | --- |
| **Mutabilidad** | Inmutable (no cambia) | Mutable (puede cambiar) |
| **Uso de memoria** | Optimizado | Puede ocupar más memoria por cambios |
| **Sintaxis** | `let nombre = valor` | `var nombre = valor` |

## ***3.4 Mutación de datos***

Se refiere a cambiar o modificar el valor de una variable, propiedad o estructura de datos después de que ha sido creada. La mutación solo es posible en **variables** (declaradas con `var`), ya que las **constantes** (declaradas con `let`) no permiten cambios en su valor después de la inicialización.

```swift
var nombre = "Ana"       // variable mutable
nombre = "Luis"          // mutación: se cambia el valor de "Ana" a "Luis"

let apellido = "Gómez"   // constante inmutable
apellido = "Martínez"    // error: las constantes no pueden mutarse
```

## ***3.5 Declaración multiple***

Para declarar varias variables o constantes en una sola línea, puedes separar los valores con comas (`,`)y asígnales sus valores directamente.

```swift
var x = 5, y = 10, z = 15
```

O puedes utilizar el punto y coma (`;`) para separar múltiples declaraciones en una misma línea de código. 

```swift
let a = 10; let b = 20; let c = a + b
```

<aside>
📎

*Aunque es posible usar el punto y coma para escribir múltiples declaraciones en una sola línea, en Swift es más común y recomendado escribir una declaración por línea, ya que esto mejora la legibilidad del código.*

</aside>

## ***3.6 Nombrar Constantes y Variables***

En Swift, los nombres de constantes y variables pueden incluir casi cualquier carácter, incluyendo caracteres Unicode. Esto permite utilizar nombres expresivos y personalizados.

```swift
let π = 3.14159
let 你好 = "你好世界"
let 🐶🐮 = "dogcow"
```

Reglas para Nombres de Constantes y Variables

- No deben incluir espacios en blanco, símbolos matemáticos, flechas, caracteres Unicode privados ni caracteres de dibujo de líneas y recuadros.
- No pueden comenzar con un número, aunque los números se pueden usar en otras posiciones del nombre.

Una vez que declares una constante o variable de un tipo específico, no puedes:

- Volver a declararla con el mismo nombre.
- Cambiarla para almacenar valores de un tipo diferente.
- Convertir una constante en una variable o viceversa.

<aside>
📎

*Si necesitas usar una palabra clave reservada de Swift como nombre de una constante o variable, puedes encerrarla en comillas invertidas (`) al declararla. Sin embargo, esto es algo que se recomienda evitar, a menos que sea absolutamente necesario, ya que podría causar confusión.*

```swift
let `class` = "Este es un ejemplo"
```

</aside>

# *4. Tipos de datos*

Tanto las constantes como las variables en Swift pueden almacenar cualquier tipo de datos, ya sea de tipo primitivo (como `Int`, `Float`, `Double`, `String`, `Bool`) o tipos de datos complejos (como `Array`, `Dictionary`, `Set`, `Struct`, `Class`).

## *4.1 Enteros Int*

Los enteros (`Int`) representan números sin decimales, positivos o negativos. Swift ajusta automáticamente el tamaño de `Int` según la arquitectura del dispositivo (por ejemplo, 32 o 64 bits).

```swift
let edad: Int = 30
var diasEnUnAno = 365
```

- Características: Los enteros pueden ser positivos o negativos, y también pueden manejar números grandes en dispositivos modernos.
- Límites: Swift proporciona métodos como `Int.min` y `Int.max` para obtener el límite mínimo y máximo que puede contener un `Int`.

### *4.1.1 Subtipos de Enteros*

Swift también tiene subtipos para enteros con tamaños específicos, que incluyen:

- **`Int8` y `UInt8`**: Enteros de 8 bits con signo y sin signo, respectivamente.
- **`Int16` y `UInt16`**: Enteros de 16 bits.
- **`Int32` y `UInt32`**: Enteros de 32 bits.
- **`Int64` y `UInt64`**: Enteros de 64 bits.

El prefijo `U` en estos tipos indica que son "unsigned" o sin signo (es decir, solo pueden ser positivos o cero).

```swift
let numeroPequeño: Int8 = -120
let numeroGrande: UInt64 = 18446744073709551615
```

## *4.2 Decimales Double y Float*

Swift usa los tipos `Double` y `Float` para manejar números decimales. La diferencia principal entre ellos es la precisión:

- **`Double`**: Usa 64 bits para almacenar valores y ofrece una mayor precisión (hasta 15-16 decimales). Es ideal para cálculos que requieren alta precisión.
- **`Float`**: Usa 32 bits y es menos preciso (hasta 6-7 decimales). Se utiliza en casos donde la precisión no es tan crucial y el espacio es más importante.

```swift
let pi: Double = 3.14159265358979 // Mayor precisión
let temperatura: Float = 21.5      // Menor precisión
```

Swift infiere automáticamente `Double` para valores decimales si no se especifica el tipo.

### ***4.2.1 Conversion de numeros enteros a decimales***

Puedes usar el inicializador `Double` pasando el valor `Int` como argumento. Esto creará una nueva variable de tipo `Double`a partir del valor original de tipo `Int`.

```swift
let numeroEntero: Int = 42
let numeroDouble: Double = Double(numeroEntero)
```

En este caso, `numeroDouble` tendrá el valor `42.0` como `Double`. Esto se debe a que el inicializador `Double()` toma el valor entero y lo convierte al tipo `Double` sin perder precisión en la conversión.

## *4.3 Cadenas de texto String*

`String` es el tipo de datos para manejar texto en Swift. Puede contener cualquier secuencia de caracteres, desde palabras y frases hasta números y símbolos. Swift permite varias operaciones de manipulación de texto con este tipo de datos, como concatenación y mutabilidad.

```swift
let saludo: String = "Hola, mundo!"
var nombre: String = "Carlos"
```

**Características adicionales**

- Interpolación de cadenas: Swift permite insertar valores dentro de una cadena usando `\(valor)`.
    
    ```swift
    let edad = 25
    let mensaje = "Tengo \(edad) años"
    ```
    
- Cadenas multilínea: Puedes usar tres comillas dobles `"""` para definir cadenas que ocupen múltiples líneas.
    
    ```swift
    let poema = """
    Este es un poema
    que tiene varias líneas.
    """
    ```
    

## *4.4 Booleanos Bool*

`Bool` es el tipo de datos que representa valores de verdad: `true` o `false`. Es útil para manejar condiciones y control de flujo en Swift.

```swift
let esMayorDeEdad: Bool = true
var estaLloviendo = false
```

Los valores booleanos suelen utilizarse en declaraciones `if`, `while` y `for` para controlar la lógica del programa.

## ***4.5 Asignación multiple***

Puedes declarar una variable o constante que comparten el mismo tipo de datos, asignándoles al final de la linea el tipo.

```swift
var x, y, z: Int  // Declaras el tipo Int para todas
x = 5
y = 10
z = 15
```

# *5. Opcionales*

En Swift, los opcionales son un tipo de datos que permiten que una variable o constante tenga un valor o no. Es decir, pueden almacenar un valor válido o representar la ausencia de valor. Los opcionales son muy importantes en Swift porque manejan de manera segura la posibilidad de que algo no exista, evitando errores comunes de referencia nula.

**¿Qué es un opcional?**

Un opcional en Swift es un tipo de variable que puede contener un valor de un tipo específico o puede no tener ningún valor en absoluto. El tipo de un opcional se declara agregando un signo de interrogación (`?`) al tipo de datos.

```swift
var nombre: String?  // Aquí, `nombre` puede ser un String o `nil`
nombre = "Juan"  // Asignamos un valor
nombre = nil  // O podemos asignar nil, que indica que no tiene valor
```

**Propiedades y características de los opcionales**

1. Valor o nil: Un opcional puede tener un valor o estar vacío (representado por `nil`).
    - Valor: Contiene un valor válido del tipo de datos específico.
    - nil: Indica la ausencia de valor, es decir, no contiene ningún valor.
2. Tipo de datos opcionales: Un tipo opcional se define con `?` (signo de interrogación).
    - Ejemplo: `String?` indica un tipo que puede ser un `String` o `nil`.
3. Desempaquetado (unwrapping): Para acceder al valor de un opcional, primero debes "desempaquetarlo". Hay varias formas de hacerlo:
    - Desempaquetado forzado (`!`): Si estás seguro de que el opcional tiene un valor, puedes desempaquetarlo usando el operador `!`.
        
        ```swift
        var nombre: String? = "Juan"
        print(nombre!)  // Desempaquetado forzado, esto imprimirá "Juan"
        ```
        
        Precaución: Si el opcional tiene valor `nil` y se intenta desempaquetar de esta manera, tu programa generará un error en tiempo de ejecución.
        
    - Desempaquetado opcional seguro (`if let` y `guard let`): Una forma más segura de desempaquetar es mediante el uso de `if let` o `guard let`. Esto solo se ejecuta si el opcional tiene un valor.
        
        ```swift
        var nombre: String? = "Juan"
        
        // Usando `if let`
        if let nombreDesempaquetado = nombre {
            print("El nombre es \(nombreDesempaquetado)")  // Imprime "El nombre es Juan"
        } else {
            print("No hay valor para el nombre")
        }
        ```
        
        ```swift
        var nombre: String? = "Juan"
        
        // Usando `guard let`
        func saludar() {
            guard let nombreDesempaquetado = nombre else {
                print("No hay valor para el nombre")
                return
            }
            print("Hola, \(nombreDesempaquetado)")  // Imprime "Hola, Juan"
        }
        saludar()
        ```
        
4. **Desempaquetado implícito** (`Implicitly Unwrapped Optionals`): Cuando estás seguro de que un opcional tendrá un valor después de ser inicializado, puedes usar un opcional desempaquetado implícitamente. Esto es similar a un opcional normal, pero puedes acceder directamente al valor sin necesidad de desempaquetarlo.
    
    ```swift
    var nombre: String! = "Juan"
    print(nombre)  / No es necesario desempaquetar, se puede acceder directamente
    ```
    
    Precaución: Si intentas acceder a un opcional desempaquetado implícitamente que es `nil`, tu programa generará un error.
    
5. Nil-Coalescing Operator (`??`): Este operador te permite proporcionar un valor predeterminado en caso de que el opcional sea `nil`.
    
    ```swift
    var nombre: String? = nil
    let nombreFinal = nombre ?? "Desconocido"  // Si `nombre` es nil, asigna "Desconocido"
    print(nombreFinal)  // Imprime "Desconocido"
    ```
    

## *5.1 Tipos de opcionales en Swift*

1. Opcionales de referencia (`Optional<SomeType>`): Puedes hacer uso de un tipo opcional de referencia.
    1. Opcionales simples (`?`): Como hemos visto, un tipo opcional puede ser de cualquier tipo, como `String?`, `Int?`, etc.
    
    ```swift
    var objeto: MyClass?  // `MyClass?` es un opcional de un tipo de clase.
    ```
    
2. Tipos con valores predeterminados: Al usar el operador nil-coalescing, puedes proporcionar un valor predeterminado cuando un opcional es `nil`, como se mostró antes.

**Uso común de los opcionales**

- Manejo de errores: En muchas situaciones, como cuando trabajas con datos que pueden ser opcionales (por ejemplo, al hacer una consulta a una base de datos, o cuando recibes datos de una API), los opcionales te permiten manejar casos donde no se encuentra el valor sin que el programa falle.
- Interacción con interfaces gráficas o datos no garantizados: En situaciones donde los datos pueden no estar disponibles o donde el valor podría ser `nil` (como campos de texto en un formulario que podrían estar vacíos), los opcionales proporcionan una forma clara de manejar esos casos.
- Almacenamiento de valores opcionales en colecciones: Cuando trabajas con arrays o diccionarios, puedes tener valores opcionales en las colecciones.
    
    ```swift
    var edades: [String: Int?] = ["Juan": 30, "Ana": nil]
    ```
    

**Resumen**

- Los opcionales en Swift representan la posibilidad de que una variable no tenga valor (`nil`).
- Se declaran con el signo `?` (por ejemplo, `String?`).
- El valor de un opcional puede ser desempaquetado de forma forzada (`!`), segura (`if let`, `guard let`), o implícita (`String!`).
- El operador `??` permite proporcionar un valor predeterminado si el opcional es `nil`.

El uso adecuado de los opcionales ayuda a escribir código más seguro y predecible, ya que fuerza al programador a manejar explícitamente los casos en los que una variable puede no tener valor.

## *5.2 Custom Optional*

El tipo CustomOptional te permite declarar una variable como opcional.

```swift
let myOptionalInt = CustomOptional<Int>.none
let myInt = CustomOptional<Int>some(10)

print(myOpcionalInt)   //  none
print(myInt)           //  some(10)  
```

Podemos usar los enumeradores para opcional personalizado

```swift
enum CustomOptional<Wrapped> {
			case none
			case some(Wrapped)
}

let myOptionalInt = CustomOptional<Int>.none
let myInt = CustomOptional<Int>.some(10)

print(myOptionalInt)   //  none  - estado de Nil
print(myInt)           //  some(10) - un posible valor de 10
```

# *6. Typealias*

En Swift, los typealiases (alias de tipo) son una forma de asignar un nombre más legible o más conveniente a un tipo existente. Un typealias no crea un tipo nuevo, sino que es simplemente un sinónimo del tipo original. Su uso principal es mejorar la legibilidad y la claridad del código, o proporcionar una forma más concisa para referirse a tipos complejos.

**Sintaxis de un Typealias**

La sintaxis básica de un typealias es la siguiente:

```swift
typealias Nombre = String
let username: Nombre = "Nombre reemplaza al Tipo String"
```

**Propiedades de los Typealiases**

1. No crea un tipo nuevo: Un typealias no crea un tipo nuevo, solo es un alias. El tipo original sigue existiendo, pero puedes referirte a él con un nombre diferente.
2. Alias de tipos complejos: Son especialmente útiles para simplificar tipos complejos o largos, como los tipos de funciones, genéricos, o tipos de colecciones anidadas.
3. Uso en funciones, estructuras, y clases: Los typealiases se pueden utilizar en cualquier parte del código: dentro de funciones, estructuras, clases, o incluso de manera global.
4. El tipo original se mantiene: Los alias no afectan el comportamiento del tipo original, ni lo hacen más flexible. 

**¿Cuándo usarlos?**

- Cuando el nombre del tipo original es largo o complicado.
- Cuando quieras mejorar la legibilidad del código.
- Para simplificar la declaración de tipos complejos que se usan varias veces en el código.

**Limitaciones**

- No puedes usar typealiases para modificar el comportamiento de un tipo. Un alias es solo un nombre alternativo, el tipo original sigue siendo el mismo.
- No puedes crear typealiases para tipos que no sean tipos de datos (como funciones, protocolos, etc.).

## *6.1 Typealias en una Tuples *****

Tipo de tuplas como alias: Supón que tienes una tupla que contiene un `Int` y un `String`, y la usas en varias partes del código. Un typealias puede ayudar a que tu código sea más expresivo.

```swift
typealias Person = (id: Int, name: String)

let person1: Person = (id: 1, name: "John")
let person2: Person = (id: 2, name: "Alice")
```

## ***6.2 Typealias en colecciones***

Si trabajas con un conjunto de tipos complejos, los **typealiases** pueden ser útiles para hacer que las colecciones sean más legibles.

```swift
typealias ProductList = [Int: String]
```

Los typealiases también se pueden usar con tipos genéricos para simplificar la definición de tipos complejos. Por ejemplo, si estás trabajando con un diccionario de clave-valor donde la clave es un `String` y el valor es una lista de enteros:

```swift
typealias DictionaryOfLists = [String: [Int]]

let myData: DictionaryOfLists = [
    "key1": [1, 2, 3],
    "key2": [4, 5, 6]
]
```

<aside>
📎

*Este código puede leerse como:*

1. `*typealias DictionaryOfLists = [String: [Int]]`:*
    
    *Esta línea define un alias de tipo llamado `DictionaryOfLists`. Lo que hace es asignar un nombre más legible o conveniente a un tipo de datos más complejo.*
    
    - `*[String: [Int]]` es un diccionario (también conocido como `Dictionary` en Swift) donde:*
        - *La clave (key) es de tipo `String`.*
        - *El valor (value) es una lista (o array) de números enteros (`[Int]`).*
    
    *Es decir, `DictionaryOfLists` es un tipo que representa un diccionario cuyas claves son cadenas de texto (de tipo `String`) y los valores asociados son arreglos de enteros (de tipo `[Int]`).*
    
2. `*let myData: DictionaryOfLists = [...]`:*

*En esta línea, se declara una constante llamada `myData` y se le asigna un valor que corresponde a un diccionario con claves de tipo `String` y valores que son arrays de enteros.*

1. `*myData` es de tipo `DictionaryOfLists`, es decir, debe ser un diccionario donde las claves son `String` y los valores son arrays de enteros.*
</aside>

## ***6.2 Typealias de tipo de cierre (Closures)***

Imagina que tienes una función que acepta un tipo de cierre muy largo y complicado:

```swift
let completion: (Bool, String) -> Void = { success, message in
    print("Success: \(success), Message: \(message)")
}
```

Puedes crear un typealias para hacer que el código sea más legible:

```swift
typealias CompletionHandler = (Bool, String) -> Void

let completion: CompletionHandler = { success, message in
    print("Success: \(success), Message: \(message)")
}
```

<aside>
📎

Este código puede leerse como:

1. `typealias CompletionHandler = (Bool, String) -> Void`
2. Esta línea crea un alias para un tipo de función. En lugar de escribir la firma de la función completa cada vez, se usa el alias `CompletionHandler`. La firma de la función es:
    - Toma dos parámetros:
        - `Bool`: un valor booleano (verdadero o falso).
        - `String`: un valor de texto.
    - Devuelve `Void`, es decir, no devuelve ningún valor.
    
    Entonces, `CompletionHandler` es un alias para cualquier función que reciba un `Bool` y un `String` como parámetros y no devuelva ningún valor (es decir, solo realice una acción como imprimir o modificar algo).
    
3. `let completion: CompletionHandler = { success, message in ... }` 
    
    En esta línea, defines una constante llamada `completion` que es una función de tipo `CompletionHandler` (es decir, una función que recibe un `Bool` y un `String` y no devuelve nada). La función se define de manera inline (usando una closure).
    
    - `success` y `message` son los parámetros de la closure.
        - `success`: un valor de tipo `Bool`, indica si una operación fue exitosa o no.
        - `message`: un valor de tipo `String`, generalmente es un mensaje relacionado con el resultado de la operación.
    - Dentro del cuerpo de la closure, se imprime un mensaje que incluye los valores de `success` y `message` utilizando `print`.
    
    Entonces, el código completo es una forma compacta de definir un "manejador de finalización" (completion handler), una función que se llama cuando una operación asíncrona o algún proceso finaliza, para informar si la operación fue exitosa y dar más detalles a través de un mensaje.
    
</aside>

## ***6.3 Typealias para tipos con Protocolos***

Si estás trabajando con protocolos o combinaciones de tipos que pueden ser largos, puedes usar typealiases para hacer que el código sea más limpio:

```swift
protocol Drawable {
    func draw()
}

typealias DrawableObject = Drawable & CustomStringConvertible

struct Circle: DrawableObject {
    var description: String {
        return "Circle"
    }

    func draw() {
        print("Drawing a circle")
    }
}
```

<aside>
📎

*Este código puede leerse como:*

*1. Protocolo `Drawable`*

*Aquí defines un protocolo llamado `Drawable`. Los protocolos en Swift son similares a las interfaces en otros lenguajes. Este protocolo establece una regla: cualquier tipo que adopte este protocolo debe implementar un método llamado `draw()`, el cual no recibe parámetros y no retorna nada (es un `void` en términos de otros lenguajes).*

*2. `typealias` para combinar protocolos*

*En esta línea, se está creando un alias de tipo llamado `DrawableObject`. Este alias representa la combinación de dos protocolos:*

- `*Drawable`: el protocolo que tiene el método `draw()`.*
- `*CustomStringConvertible`: este protocolo exige que el tipo tenga una propiedad llamada `description` de tipo `String`. Es utilizado para permitir que un objeto tenga una representación en forma de texto personalizada.*

*El operador `&` en este contexto se usa para componer protocolos. En otras palabras, `DrawableObject` es un tipo que debe adoptar ambos protocolos: `Drawable` y `CustomStringConvertible`.*

1. *Estructura `Circle`* 

*Aquí defines una estructura llamada `Circle`, que adopta el tipo `DrawableObject`. Esto significa que `Circle` debe cumplir con los requisitos de ambos protocolos:*

- *Protocolo `Drawable`: Implementa el método `draw()`, que en este caso imprime "Drawing a circle".*
- *Protocolo `CustomStringConvertible`: Implementa la propiedad `description`, la cual devuelve la cadena `"Circle"`, lo que permite que la estructura `Circle` pueda ser representada como una cadena de texto de forma personalizada.*

*Resumen*

- `*Drawable`: Protocolo que exige un método `draw()`.*
- `*CustomStringConvertible`: Protocolo que exige una propiedad `description` de tipo `String`.*
- `*DrawableObject`: Es un alias de tipo que representa la combinación de ambos protocolos.*
- `*Circle`: Estructura que adopta el alias `DrawableObject`, implementando tanto el método `draw()` como la propiedad `description`.*

*En resumen, el código define una estructura `Circle` que es tanto dibujable (porque implementa `draw()`) como describible (porque implementa `description`).*

</aside>

---