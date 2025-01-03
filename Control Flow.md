# Control Flow

> Código de estructura con ramas, bucles y salidas tempranas.
> 

Swift ofrece diversas sentencias de flujo de control. 

- Las condicionales (`if`, `switch`, `guard`) se utilizan para evaluar expresiones y ejecutar bloques de código solo si se cumplen ciertas condiciones.
- `break` y `continue` permiten controlar el flujo dentro de los bucles.
- Los bucles (`for-in`, `while`, `repeat-while`) son útiles para iterar sobre colecciones como `Array`, `Set`, y `Dictionary`, y permiten trabajar con colecciones y tipos iterables.
- Los tipos de datos en Swift como `String`, `Array`, `Set`, `Dictionary`, `Tuple`, `Struct`, `Func`, `Enum`, y `Closures` tienen sus propios métodos y propiedades que interactúan de manera fluida con los controles de flujo, permitiendo un código limpio y eficiente.

Estos controles de flujo te permiten manejar diferentes situaciones en el código de manera estructurada y clara, adaptándose a las necesidades de cualquier tipo de dato en Swift.

# ***1. Condicionales***

Swift proporciona dos formas de añadir ramas condicionales a su código: la sentencia `if` y la sentencia `switch`.

## ***1.1 If***

La sentencia `if` se usa para ejecutar un bloque de código simples, cuenta con condiciones como `else if` y `else` .

```swift
if condición {
    // Código que se ejecuta si la condición es verdadera
}
```

```swift
let edad = 20

if edad >= 18 {
    print("Eres mayor de edad")
}
// En este caso, como edad es mayor o igual a 18, se imprimirá:
// Eres mayor de edad.
```

Propiedades: Evalúa condiciones lógicas sobre cualquier tipo de dato compatible con operaciones booleanas, como `Int`, `String`, `Bool`, etc.

### ***1.1.1 Else***

Añade una alternativa para cuando la condición del `if` no se cumple.

```swift
if condición {
    // Código si la condición es verdadera
} else {
    // Código si la condición es falsa
}
```

```swift
let temperatura = 15

if temperatura > 20 {
    print("Hace calor")
} else {
    print("Hace frío")
}
// Hace frío
```

***Propiedades***

`isEmpty` : verifica si la cadena está vacía.

```swift
let mensaje = "Bienvenido"
if mensaje.isEmpty {
    print("El mensaje está vacío.")
} else {
    print("El mensaje no está vacío.")
}
// El mensaje no está vacío.
```

### ***1.1.2 Else if - Else***

Permite evaluar múltiples condiciones secuencialmente. Una vez que una condición se cumple, las demás no se evalúan.

```swift
if condición1 {
    // Código si condición1 es verdadera
} else if condición2 {
    // Código si condición2 es verdadera
} else {
    // Código si ninguna condición anterior se cumple
}
```

```swift
let nota = 75

if nota >= 90 {
    print("Sobresaliente")
} else if nota >= 70 {
    print("Aprobado")
} else {
    print("Reprobado")
}
// Aprobado
```

### ***1.1.3 Uso de condicionales con múltiples condiciones***

Puedes combinar condiciones usando operadores lógicos como `&&` (AND) y `||` (OR).

```swift
let hora = 10

if hora >= 6 && hora < 12 {
    print("Es de mañana")
} else if hora >= 12 && hora < 18 {
    print("Es de tarde")
} else {
    print("Es de noche")
}
// Es de mañana
```

### ***1.1.4 Operador ternario***

Una forma abreviada de escribir un `if-else`. Tiene la siguiente sintaxis:

```swift
condición ? expresión_si_verdadera : expresión_si_falsa
```

```swift
let esMayor = edad >= 18 ? "Sí" : "No"
print("¿Eres mayor de edad? \(esMayor)")
// ¿Eres mayor de edad? Sí
```

## ***1.2 Switch***

La sentencia `switch` es más adecuada para condiciones más complejas con múltiples permutaciones posibles y es útil en situaciones donde la coincidencia de patrones puede ayudar a seleccionar una rama de código apropiada para ejecutar.

```swift
switch valor {
case patrón1:
    // Código para patrón1
case patrón2:
    // Código para patrón2
default:
    // Código para el caso por defecto
}
```

**Características Clave**

1. Sin necesidad de `break`: Cada caso debe manejarse de forma explícita, evitando errores por flujo inesperado.
2. Cobertura exhaustiva: Si el conjunto de patrones no cubre todos los posibles valores, se debe incluir un caso `default`.
3. Coincidencia de patrones: Puede comparar rangos, tuples, strings, y más.
4. Case múltiple: Puedes agrupar varios valores en un solo caso usando comas.

```swift
let numero = 3

switch numero {
case 1:
    print("Es uno")
case 2:
    print("Es dos")
case 3:
    print("Es tres")
default:
    print("Otro número")
}
// Es tres
```

### *1.2.1 Uso de Rangos*

```swift
let edad = 25

switch edad {
case 0...12:
    print("Es un niño")
case 13...19:
    print("Es un adolescente")
case 20...35:
    print("Es un adulto joven")
default:
    print("Es un adulto mayor")
}
// Es un adulto joven
```

### *1.2.2 **Coincidencia con Tuples***

```swift
let coordenada = (x: 5, y: 0)

switch coordenada {
case (0, 0):
    print("Está en el origen")
case (let x, 0):
    print("Está en el eje X en \(x)")
case (0, let y):
    print("Está en el eje Y en \(y)")
case (let x, let y) where x == y:
    print("Está en la diagonal")
default:
    print("Está en algún lugar en (\(coordenada.x), \(coordenada.y))")
}
// Está en el eje X en 5
```

### *1.2.3 **Múltiples valores en un Case***

```swift
let día = "sábado"

switch día {
case "lunes", "martes", "miércoles", "jueves", "viernes":
    print("Es un día laboral")
case "sábado", "domingo":
    print("Es un fin de semana")
default:
    print("No es un día válido")
}
// Es un fin de semana
```

### *1.2.4 Where*

La cláusula `where` en un `switch` permite agregar una condición adicional que debe cumplirse para que un caso coincida. Esto se conoce como cláusula de guardia condicional.

```swift
case patrón where condición:
    // Código a ejecutar si se cumple el patrón y la condición
```

```swift
let temperatura = 35

switch temperatura {
case let t where t < 0:
    print("Temperatura bajo cero")
case 0...30:
    print("Temperatura agradable")
case let t where t > 30:
    print("Hace mucho calor, \(t) grados")
default:
    print("Valor desconocido")
}
// Hace mucho calor, 35 grados
```

¿Cuándo usar `where`?

- Para filtrar valores adicionales dentro de un patrón.
- Para evitar crear muchos casos anidados.
- Para hacer el código más legible y expresivo.

### *1.2.5 As*

El operador `as` en un `switch` se utiliza principalmente para realizar casting (conversión de tipo) cuando se trabaja con tipos de datos heterogéneos o protocolos.

Tipos de `as`:

1. `as?` (Opcional): Devuelve un valor opcional si el casting tiene éxito.
2. `as!` (Forzado): Obliga al casting y genera un error si falla (menos seguro).

Ejemplo: Casting Opcional con Protocolos

```swift
let elementos: [Any] = [42, "Swift", 3.14, true]

for elemento in elementos {
    switch elemento {
    case let entero as Int:
        print("Es un entero: \(entero)")
    case let cadena as String:
        print("Es una cadena: \(cadena)")
    case let decimal as Double:
        print("Es un número decimal: \(decimal)")
    case let booleano as Bool:
        print("Es un booleano: \(booleano)")
    default:
        print("Tipo desconocido")
    }
}
// Es un entero: 42  
// Es una cadena: Swift  
// Es un número decimal: 3.14  
// Es un booleano: true
```

Ejemplo: Casting Forzado (`as!`)

Nota: Esto es menos seguro, pero puede ser útil cuando tienes certeza del tipo.

```swift
let valor: Any = "Hola, mundo"

switch valor {
case let texto as! String:
    print("Es una cadena forzada: \(texto)")
default:
    print("Tipo desconocido")
}
```

¿Cuándo usar `as`?

- Cuando trabajas con tipos genéricos o heterogéneos (`Any`).
- Para manejar objetos de diferentes tipos bajo un mismo `switch`.

### *1.2.6 Where y As*

Puedes usar `where` junto con `as` para agregar condiciones adicionales al casting.

Ejemplo: Filtrar por Tipo y Condición

```swift
let elementos: [Any] = ["Swift", 2024, 3.14, "Aprender", 100]

for elemento in elementos {
    switch elemento {
    case let texto as String where texto.count > 5:
        print("Cadena larga: \(texto)")
    case let numero as Int where numero > 100:
        print("Número grande: \(numero)")
    default:
        print("Elemento no clasificado: \(elemento)")
    }
}
// Cadena larga: Aprender  
// Elemento no clasificado: 2024  
// Elemento no clasificado: 3.14  
// Elemento no clasificado: Swift  
// Elemento no clasificado: 100
```

### *1.2.7 Casos específicos en un Enum*

```swift
enum mensajeEstado {
    case enviado
    case entregado
    case leido
}

let estado: mensajeEstado = .leido

switch estado {
case .enviado:
    print("Mensaje enviado")
case .entregado:
    print("Mensaje entregado")
case .leido:
    print("Mensaje leído")
}
// Mensaje leído
```

```swift
enum Estado {
    case cargando
    case completado(String)
    case error(String)
}

let estado = Estado.completado("Todo bien")

switch estado {
case .cargando:
    print("Está cargando...")
case .completado(let mensaje):
    print("Completado: \(mensaje)")
case .error(let mensaje):
    print("Error: \(mensaje)")
}
// Completado: Todo bien
```

## ***1.3 Guard***

`guard` se usa para verificar condiciones antes de ejecutar un bloque de código. Si la condición no se cumple, ejecuta un `else` y normalmente se sale de la función con `return`, `break`, `continue` o incluso `throws` para manejar errores.

Propiedades: El `guard` asegura que las condiciones se cumplan antes de proceder con el código restante.

```swift
guard condición else {
    // Código que se ejecuta si la condición es falsa
    salida // return, break, continue o throw
}
// Código que se ejecuta si la condición es verdadera
```

### *1.3.1 Return, Break o Continue*

Ejemplo con `return` : retorna un valor desde la función si una condición no se cumple.

```swift
func squareRoot(of number: Double) -> Double? {
    guard number >= 0 else {
        return nil
    }
    return number.squareRoot()
}
print(squareRoot(of: 16) ?? "Número inválido") // 4.0
print(squareRoot(of: -4) ?? "Número inválido") // Número inválido
```

Ejemplo con `break` : para salir de un ciclo al cumplir una condición.

```swift
func findFirstEven(in numbers: [Int]) {
    for number in numbers {
        if number % 2 == 0 {
            print("Primer número par: \(number)")
            break
        }
    }
}
findFirstEven(in: [1, 3, 5, 8, 10]) // Primer número par: 8
```

Ejemplo con `continue`: para saltar una iteración y continuar con el resto del ciclo.

```swift
func printNonNegativeNumbers(numbers: [Int]) {
    for number in numbers {
        if number < 0 {
            continue
        }
        print("Número: \(number)")
    }
}
printNonNegativeNumbers(numbers: [-1, 3, -5, 8, 0]) 
// Número: 3
// Número: 8
// Número: 0
```

Ejemplo con `throw`: para manejo de errores.

```swift
// Definir un enum para los posibles errores
enum ValidationError: Error {
    case emptyName
    case nameTooShort
    case nameTooLong
}

// Función que valida el nombre usando guard y lanza errores si no cumple los criterios
func validateUsername(_ name: String) throws {
    guard !name.isEmpty else {
        throw ValidationError.emptyName
    }
    
    guard name.count >= 3 else {
        throw ValidationError.nameTooShort
    }
    
    guard name.count <= 15 else {
        throw ValidationError.nameTooLong
    }
    
    print("Nombre de usuario válido: \(name)")
}

// Uso de la función con manejo de errores
do {
    try validateUsername("John") // Nombre de usuario válido: John
    try validateUsername("")     // Error: emptyName
    try validateUsername("Al")   // Error: nameTooShort
    try validateUsername("NombreDeUsuarioMuyLargo") // Error: nameTooLong
} catch ValidationError.emptyName {
    print("El nombre de usuario está vacío.")
} catch ValidationError.nameTooShort {
    print("El nombre de usuario es demasiado corto.")
} catch ValidationError.nameTooLong {
    print("El nombre de usuario es demasiado largo.")
} catch {
    print("Error desconocido: \(error)")
}
```

**Explicación del código:**

`enum ValidationError`: Enumera los errores que pueden ocurrir.

`guard` con `throw`: Cada bloque `guard` verifica una condición. Si falla, lanza un error específico.

`do-catch`: Captura y maneja los errores lanzados por la función `validateUsername`.

### *1.3.2 En una Func*

Validación de parámetros:

```swift
func validateUser(age: Int?) {
    guard let age = age, age >= 18 else {
        print("Edad inválida o menor de 18.")
        return
    }
    print("Usuario válido con edad \(age).")
}
validateUser(age: 20) // Usuario válido con edad 20.
validateUser(age: nil) // Edad inválida o menor de 18.
```

Asegurar la existencia de un archivo:

```swift
func readFile(fileName: String?) {
    guard let fileName = fileName else {
        print("Nombre de archivo no proporcionado.")
        return
    }
    print("Leyendo el archivo \(fileName).")
}
readFile(fileName: "documento.txt") // Leyendo el archivo documento.txt.
readFile(fileName: nil) // Nombre de archivo no proporcionado.

```

Control de entrada en un rango:

```swift
func checkNumber(number: Int) {
    guard (1...100).contains(number) else {
        print("Número fuera de rango.")
        return
    }
    print("El número \(number) está en el rango permitido.")
}
checkNumber(number: 50) // El número 50 está en el rango permitido.
checkNumber(number: 150) // Número fuera de rango.

```

Búsqueda de valor negativo:

```swift
func procesarNumeros(numeros: [Int]) {
    for numero in numeros {
        guard numero > 0 else {
            print("Se encontró un número no positivo: \(numero)")
            continue  // Continúa con el siguiente número en lugar de terminar el ciclo
        }
        print("Procesando el número: \(numero)")
    }
}

procesarNumeros(numeros: [1, -2, 3, 4]) 
// Procesando el número: 1
// Se encontró un número no positivo: -2
// Procesando el número: 3
// Procesando el número: 4
```

### *1.3.3 Utilizando un Closure*

```swift
func realizarTarea(completion: (Bool) -> Void) {
    let tareaExitosa = true
    
    guard tareaExitosa else {
        completion(false)
        return
    }
    
    completion(true)
}

realizarTarea { resultado in
    if resultado {
        print("Tarea completada con éxito.")
    } else {
        print("Hubo un error en la tarea.")
    }
}
// Tarea completada con éxito.
```

### *1.3.4 En un Struct*

```swift
struct Producto {
    let nombre: String
    let precio: Double
}

func mostrarPrecioDelProducto(producto: Producto?) {
    guard let productoDesempaquetado = producto else {
        print("El producto no está disponible.")
        return
    }
    
    guard productoDesempaquetado.precio > 0 else {
        print("El precio del producto es inválido.")
        return
    }
    
    print("El precio del producto \(productoDesempaquetado.nombre) es \(productoDesempaquetado.precio)€")
}

let producto = Producto(nombre: "Camiseta", precio: 25.5)
mostrarPrecioDelProducto(producto: producto) // El precio del producto Camiseta es 25.5€
mostrarPrecioDelProducto(producto: nil)      // El producto no está disponible.
mostrarPrecioDelProducto(producto: Producto(nombre: "Camiseta", precio: -5)) // El precio del producto es inválido.
```

---

# ***2. Bucles***

## *2.1 For-in*

El bucle `for-in` se utiliza para iterar sobre una secuencia, como rangos, colecciones, o incluso otros tipos iterables. Es una forma muy flexible de iterar sobre tipos como `Array`, `Set`, `Dictionary`, `String`, y más.

Sintaxis básica:

```swift
for item in collection {
    // Código que se ejecuta con cada item de la colección
}
```

Rango Abierto

```swift
for i in 0..<5 {
    print(i)
}
// Imprime del 0 al 4
```

Rango Cerrado

```swift
for i in 0...5 {
    print("Número \(i)")
}
// Imprime del 0 al 5
```

Ignorar el Valor

```swift
for _ in 0..<5 {
    print("Hola!")
}
// Imprime "Hola!" 5 veces
```

Propiedades

`reversed()` : Invierte el orden de un rango o una colección.

```swift
for i in (0...5).reversed() {
    print(i)
}
// Imprime 5, 4, 3, 2, 1, 0
```

`stride(from:to:by:)` y `stride(from:through:by:)`: Permite especificar un paso personalizado en el rango. Con `to` excluye el valor final, y con `through` lo incluye.

```swift
for i in stride(from: 0, to: 10, by: 2) {
    print(i) // Imprime 0, 2, 4, 6, 8
}

for i in stride(from: 0, through: 10, by: 2) {
    print(i) // Imprime 0, 2, 4, 6, 8, 10
}
```

## ***2.2 While***

El bucle `while` ejecuta un bloque de código mientras se cumpla una condición booleana.

```swift
var i = 0
while i < 5 {
    print(i)
    i += 1
}
// 0
// 1
// 2
// 3
// 4
```

**Condición**: En este caso, el bucle sigue ejecutándose mientras `i < 5`.

**Propiedades y métodos:**

- Funciona con cualquier tipo de dato que permita realizar comparaciones (`Int`, `Bool`, etc.).
- Es comúnmente usado con `Int` y otras colecciones para realizar iteraciones basadas en contadores.

## ***2.3 Repeat-While***

A diferencia de `while`, el bucle `repeat-while` siempre ejecutará al menos una vez el bloque de código, porque la condición es evaluada después de la ejecución.

```swift
var i = 0
repeat {
    print(i)
    i += 1
} while i < 5
// 0
// 1
// 2
// 3
// 4
```

**Condición**: La condición es evaluada después de cada ejecución, por lo que el código se ejecuta al menos una vez.

## *2.4 Con condicionales*

```swift
let numeros = [1, 2, 3, 4, 5]

for numero in numeros {
    if numero % 2 == 0 {
        print("\(numero) es par")
    } else {
        print("\(numero) es impar")
    }
}
// 1 es impar
// 2 es par
// 3 es impar
// 4 es par
// 5 es impar
```

## ***2.5 Con tipos y sus propiedades***

### *2.5.1 String*

Cuando usas un bucle `for-in` sobre un tipo `String` iteras sobre cada caracter del `String`.

```swift
for caracter in "Hola" {
    print(caracter)
}
// H
// o
// l
// a
```

```swift
let texto = "Hello, Swift!"

for caracter in texto {
    print(caracter, terminator: " ")
}
// H e l l o ,   S w i f t ! 
```

Propiedades

`count` : contar los elementos

```swift
let saludo = "Hola"
for i in 0..<saludo.count {
    print("Letra \(i): \(saludo[saludo.index(saludo.startIndex, offsetBy: i)])")
}
// Letra 0: H
// Letra 1: o
// Letra 2: l
// Letra 3: a
```

`split()` : dividir una cadena

```swift
let texto = "Swift es un lenguaje"
let palabras = texto.split(separator: " ")
for palabra in palabras {
    print("Palabra: \(palabra)")
}
// Palabra: Swift
// Palabra: es
// Palabra: un
// Palabra: lenguaje
```

`hasPrefix()` y `hasSuffix()` : comprueba el prefijo y sufijo

```swift
let rutaArchivo = "/Users/john/Documents/archivo.txt"
if rutaArchivo.hasPrefix("/Users") {
    print("El archivo está en la carpeta de usuarios.")
}
if rutaArchivo.hasSuffix(".txt") {
    print("El archivo es de tipo texto.")
}
// El archivo está en la carpeta de usuarios.
// El archivo es de tipo texto.
```

- `hasPrefix()`: Verifica si una cadena tiene un prefijo específico.
- `hasSuffix()`: Verifica si una cadena tiene un sufijo específico.

Puedes acceder a cada carácter de la cadena, y puedes trabajar con propiedades del tipo `Character` como:

- `isLetter`: Verifica si el carácter es una letra.
- `isNumber`: Verifica si el carácter es un número.
- `isPunctuation`: Verifica si el carácter es un signo de puntuación.
- `isWhitespace`: Verifica si el carácter es un espacio o salto de línea.

```swift
let mensaje = "H8la!"
for caracter in mensaje {
    if caracter.isLetter {
        print("\(caracter) es una letra.")
    }
}
// H es una letra.
// l es una letra.
// a es una letra.
```

### ***2.5.2 Array***

```swift
let numeros = [1, 2, 3, 4]
for numero in numeros {
    print(numero)
}
```

```swift
let matriz = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

for fila in matriz {
    for elemento in fila {
        print(elemento, terminator: " ")
    }
    print() // Salto de línea después de cada fila
}
// 1 2 3 
// 4 5 6 
// 7 8 9 
```

```swift
let arreglo = [10, 20, 30, 40, 50]
let subArreglo = arreglo[1...3] // ArraySlice

for elemento in subArreglo {
    print(elemento)
}
// 20
// 30
// 40

// ArraySlice - trabajas con una parte del array 
```

**Propiedades**

`count` : para iterar sobre un array y contar elementos.

```swift
var numeros = [1, 2, 3, 4, 5]
for i in 0..<numeros.count {
    print("Elemento \(i): \(numeros[i])")
}
// Elemento 0: 1
// Elemento 1: 2
// Elemento 2: 3
// Elemento 3: 4
// Elemento 4: 5
```

`enumerated()` para agregar un indice.

```swift
let frutas = ["manzana", "naranja", "plátano"]

for (indice, fruta) in frutas.enumerated() {
    print("Fruta \(indice): \(fruta)")
}
// Fruta 0: manzana
// Fruta 1: naranja
// Fruta 2: plátano
```

`append()` para agregar elementos dentro del bucle.

```swift
var colores = ["Rojo", "Azul", "Verde"]
for color in colores {
    print("El color es \(color)")
    colores.append("Amarillo")  // Añadir un nuevo color en cada iteración
}
print(colores)
```

`uppercased()` para convertir a mayusculas.

```swift
let palabras = ["hola", "mundo"]

for palabra in palabras {
    print(palabra.uppercased())
}
// HOLA
// MUNDO
```

`remove()` para eliminar elementos durante la iteración.

```swift
var frutas = ["Manzana", "Plátano", "Cereza", "Fresa"]
for i in 0..<frutas.count {
    if frutas[i] == "Plátano" {
        frutas.remove(at: i)  // Eliminar el "Plátano"
        break  // Salir del bucle para evitar problemas con el cambio de índices
    }
}
print(frutas)
```

### *2.5.3 Set*

```swift
let numerosUnicos: Set = [1, 2, 3]
for numero in numerosUnicos {
    print(numero)
}
```

`count` para iterar sobre los elementos del set.

```swift
var numerosUnicos: Set = [1, 2, 3, 4, 5]
for numero in numerosUnicos {
    print("Número: \(numero)")
}
print("Cantidad de elementos: \(numerosUnicos.count)")
```

`insert()` para agregar elementos al set.

```swift
var frutas: Set = ["Manzana", "Plátano", "Cereza"]
for fruta in frutas {
    print("Fruta disponible: \(fruta)")
    frutas.insert("Uva")  // Intentamos agregar "Uva" en cada iteración
}
print(frutas)
```

`remove()` para eliminar elementos del set.

```swift
var colores: Set = ["Rojo", "Verde", "Azul"]
for color in colores {
    if color == "Verde" {
        colores.remove(color)  // Eliminar "Verde"
        break  // Salir del bucle después de eliminar el elemento
    }
}
print(colores)
```

`contains()` para comprobar la existencia de un elemento.

```swift
var animales: Set = ["Perro", "Gato", "Conejo"]
if animales.contains("Gato") {
    print("El set contiene un Gato.")
}
```

### ***2.5.4 Dictionary***

```swift
let edades = ["Juan": 30, "Ana": 25]
for (nombre, edad) in edades {
    print("\(nombre) tiene \(edad) años")
}
// Juan tiene 30 años
// Ana tiene 25 años
```

`count` para iterar sobre un diccionario y contar elementos.

```swift
var edades: [String: Int] = ["Juan": 30, "Ana": 25, "Pedro": 40]
for (nombre, edad) in edades {
    print("\(nombre) tiene \(edad) años")
}
print("Cantidad de entradas: \(edades.count)")
```

`keys` para iterar solo sobre las claves del diccionario.

```swift
let personas: [String: String] = ["Juan": "Ingeniero", "Ana": "Médico", "Pedro": "Abogado"]
for nombre in personas.keys {
    print("Nombre: \(nombre)")
}
```

`values` para iterar solo sobre los valores del diccionario.

```swift
let idiomas: [String: String] = ["ES": "Español", "EN": "Inglés", "FR": "Francés"]
for idioma in idiomas.values {
    print("Idioma: \(idioma)")
}
```

`updateValue()` para actualizar el valor de una clave en el diccionario.

```swift
var inventario: [String: Int] = ["Manzanas": 10, "Naranjas": 20]
for (producto, cantidad) in inventario {
    print("Producto: \(producto), Cantidad: \(cantidad)")
    if let nuevoCantidad = inventario.updateValue(30, forKey: "Manzanas") {
        print("Se actualizó \(producto) de \(nuevoCantidad) a \(inventario[producto]!)")
    }
}
```

### *2.5.5 Tuples*

```swift
let puntos = [(x: 1, y: 2), (x: 3, y: 4), (x: 5, y: 6)]

for punto in puntos {
    print("Punto en x: \(punto.x), y: \(punto.y)")
}
// Punto en x: 1, y: 2
// Punto en x: 3, y: 4
// Punto en x: 5, y: 6
```

## *2.6 Sobre un Struct*

```swift
struct Persona {
    let nombre: String
    let edad: Int
}

let personas = [Persona(nombre: "Juan", edad: 25),
                Persona(nombre: "Ana", edad: 30),
                Persona(nombre: "Pedro", edad: 28)]

for persona in personas {
    print("\(persona.nombre) tiene \(persona.edad) años.")
}
// Juan tiene 25 años.
// Ana tiene 30 años.
// Pedro tiene 28 años.
```

## *2.7 Sobre un Enum*

```swift
enum Direccion {
    case norte, sur, este, oeste
}

let direcciones: [Direccion] = [.norte, .sur, .este, .oeste]

for direccion in direcciones {
    switch direccion {
    case .norte:
        print("Vas al norte.")
    case .sur:
        print("Vas al sur.")
    case .este:
        print("Vas al este.")
    case .oeste:
        print("Vas al oeste.")
    }
}
// Vas al norte.
// Vas al sur.
// Vas al este.
// Vas al oeste.
```

```swift
enum Dia {
    case lunes, martes, miércoles, jueves, viernes, sábado, domingo
}

let diasDeLaSemana: [Dia] = [.lunes, .martes, .miércoles, .jueves, .viernes]

for dia in diasDeLaSemana {
    print("Hoy es \(dia).")
}
// Hoy es lunes.
// Hoy es martes.
// Hoy es miércoles.
// Hoy es jueves.
// Hoy es viernes.  
```

---