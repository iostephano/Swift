# Closures

> Agrupar el código que se ejecuta juntos, sin crear una función con nombre.
> 

Los closures son bloques de código autocontenidos que puedes pasar y usar en tu código. Los closures tienen funcionalidades similares a las funciones, pero son más ligeros y flexibles. A menudo se usan como callbacks o para tareas que necesitan encapsular lógica para ser ejecutada posteriormente.

# ***1. Características de los Closures***

- Capturan y almacenan referencias a cualquier constante o variable del contexto donde fueron definidos.
- Son funciones anónimas, aunque pueden asignarse a una variable para ser reutilizados.
- Inferencia de tipos, lo que significa que Swift puede deducir su tipo basándose en el contexto.
- Sintaxis compacta, que se vuelve especialmente útil en combinaciones como `sorted`, `map`, `filter`, y `reduce`.

**Sintaxis:**

```swift
{ (parámetros) -> TipoDeRetorno in
    // Código
}
```

```swift
let closure = { (value: Int) -> Int in
			print("Value: \(value)")
			return value
}
closure(1)  // Value: 1
```

**Comparación: Función vs. Closure**

| Característica | Función | Closure |
| --- | --- | --- |
| Tiene nombre | Sí | Opcional |
| Captura valores del entorno | No | Sí |
| Independencia | Total | Depende del contexto |
| Uso común | Operaciones generales | Operaciones específicas |

# ***2. Closures como Parámetros***

Pueden usarse como parámetros de funciones para personalizar su comportamiento.

```swift
func realizarOperacion(a: Int, b: Int, operacion: (Int, Int) -> Int) -> Int {
    return operacion(a, b)
}

let resultado = realizarOperacion(a: 10, b: 5) { (x, y) -> Int in
    return x * y
}
print(resultado) // Resultado: 50

```

<aside>
📎

*Este código puede leerse como:*

*1. Declaración de la función `realizarOperacion`*

- `*a` y `b`: son dos enteros que se pasan como parámetros a la función.*
- `*operacion`: es un parámetro que recibe una función (o closure). Esta función debe aceptar dos parámetros de tipo `Int` y devolver un `Int`.*
- `*> Int`: indica que la función `realizarOperacion` también devuelve un entero.*
- `*return operacion(a, b)`: ejecuta la función (o closure) `operacion` pasando `a` y `b` como argumentos, y retorna el resultado.*

*2. Llamada a `realizarOperacion` con una closure*

- `*a: 10` y `b: 5`: valores que se pasan a los parámetros `a` y `b`.*
- *Closure: `{ (x, y) -> Int in return x * y }` es una función anónima que se pasa como argumento. Desglosémosla:*
    - `*(x, y)`: define los parámetros de entrada de la closure, que corresponden a `a` y `b`.*
    - `*> Int`: especifica que la closure devuelve un entero.*
    - `*return x * y`: realiza la multiplicación de `x` e `y`.*

*Cuando se ejecuta, `realizarOperacion` reemplaza `operacion(a, b)` con `x * y`, lo que equivale a `10 * 5`.*

*3. Imprimir el resultado*

*El valor calculado es `10 * 5 = 50`, que se guarda en `resultado` y se imprime.*

</aside>

# *3. Closures que Capturan Valores*

Un closure puede capturar y modificar valores externos.

```swift
func contadorIncremental(inicio: Int) -> () -> Int {
    var total = inicio
    return {
        total += 1
        return total
    }
}

let contador = contadorIncremental(inicio: 10)
print(contador()) // 11
print(contador()) // 12
```

<aside>
📎

*Este código puede leerse como:*

1. *Definición de la función `contadorIncremental`*
- *Esta función toma un parámetro entero llamado `inicio`.*
- *Devuelve una closure (función anónima) que no recibe parámetros (`()`) pero devuelve un entero (`Int`).*

*2. Variable `total`*

- *Se define una variable `total` inicializada con el valor de `inicio`.*
- *Importante: Esta variable se encuentra dentro del alcance de la función, pero también estará accesible para la closure que se devuelve. Esto se llama captura de valores.*
1. *Closure devuelta*
- *Aquí se devuelve una closure.*
- *Esta closure tiene acceso a `total` gracias a la captura de contexto.*
- *Cada vez que se llame a esta closure:*
    
    *Incrementará `total` en 1 (`total += 1`).*
    
    *Retornará el valor actualizado de `total`.*
    
1. *Creación de un contador*
- *Se llama a `contadorIncremental` con `inicio: 10`.*
- *La función devuelve una closure, que es asignada a la constante `contador`.*
- *Esta closure recuerda el valor de `total`, que inicialmente es 10.*
1. *Uso del contador*

*Llamas a `(contador())`* 

- *Dentro de la closure, `total` se incrementa en 1, pasando de 10 a 11.*
- *Luego, la closure devuelve 11, que se imprime.*

*Llamas a `(contador())` nuevamente*

- `*total` se incrementa otra vez, pasando de 11 a 12.*
- *La closure devuelve 12, que se imprime.*

*Conceptos clave*

- *Captura de valores:*
    - *La closure devuelta recuerda y mantiene el estado de la variable `total`, incluso después de que la función `contadorIncremental` haya terminado su ejecución.*
- *Closures como estado:*
    - *En este caso, la closure actúa como un contador que "recuerda" el valor previo y lo actualiza cada vez que se llama.*
- *Ejemplo de uso:*
    - *Este patrón es útil para implementar funciones que mantienen estados internos sin necesidad de usar clases u objetos.*
</aside>

# *4. Método sorted(by:)*

El método `sorted(by:)` ordena un array basado en un closure que define cómo comparar los elementos, esto ayuda a definir el criterio de ordenamiento.

1. Usando una función normal

```swift
let letras = ["C", "A", "E", "B", "D"]

func ordenDescendente(_ s1: String, _ s2: String) -> Bool {
    return s1 > s2
}

let letrasOrdenadas = letras.sorted(by: ordenDescendente)
print(letrasOrdenadas) // ["E", "D", "C", "B", "A"]
```

2. Usando un closure como expresión

En lugar de una función aparte, puedes escribir el closure directamente.

```swift
let letras = ["C", "A", "E", "B", "D"]

let letrasOrdenadas = letras.sorted(by: { (s1: String, s2: String) -> Bool in
    return s1 > s2
})
print(letrasOrdenadas) // ["E", "D", "C", "B", "A"]
```

3. Simplificando el closure

**Inferencia de tipos**: Swift deduce que los parámetros son `String` y el resultado es `Bool`. No necesitas escribirlo.

```swift
let letrasOrdenadas = letras.sorted(by: { s1, s2 in
    return s1 > s2
})
```

**Retorno implícito**: Si el closure tiene una sola línea, puedes omitir `return`.

```swift
let letrasOrdenadas = letras.sorted(by: { s1, s2 in s1 > s2 })
```

**Nombres abreviados**: Puedes usar `$0`, `$1`, etc., para los parámetros.

```swift
let letrasOrdenadas = letras.sorted(by: { $0 > $1 })
```

**Uso de operadores**: Si el closure es simple y usa un operador como `>`, puedes usarlo directamente.

```swift
let letrasOrdenadas = letras.sorted(by: >)
```

# *5. Método .map {  }*

El método `.map` es una función poderosa disponible para colecciones como arreglos (`Array`) y diccionarios (`Dictionary`) en Swift. Permite transformar cada elemento de una colección aplicando un closure, devolviendo una nueva colección con los elementos transformados.

**Características principales de `.map`:**

- Transformación: Aplica un closure a cada elemento de la colección.
- Inmutabilidad: No modifica la colección original; devuelve una nueva.
- Uso en Arrays, Sets y Diccionarios.
1. Sintaxis básica

```swift
let numeros = [1, 2, 3, 4, 5]
let numerosDobles = numeros.map { $0 * 2 }
print(numerosDobles) // [2, 4, 6, 8, 10]
```

<aside>
📎

*Este código puede leerse como:*

- `numeros` es el arreglo original.
- `map` aplica el closure `{ $0 * $0 }` a cada elemento.
- `$0` representa el elemento actual del arreglo.
</aside>

1. Ejemplo con un closure explícito

```swift
let nombres = ["Ana", "Luis", "María", "Carlos"]
let saludos = nombres.map { (nombre) -> String in
    return "Hola, \(nombre)!"
}

print(saludos)
// ["Hola, Ana!", "Hola, Luis!", "Hola, María!", "Hola, Carlos!"]
```

<aside>
📎

*Este código puede leerse como:*

- Aquí, el closure se define explícitamente con un parámetro llamado `nombre` y un tipo de retorno `String`.
- El closure transforma cada elemento añadiendo un saludo.
</aside>

1. Uso de `.map` con operaciones complejas

```swift
let numeros = [10, 20, 30]
let resultados = numeros.map { numero in
    if numero % 20 == 0 {
        return "\(numero) es divisible por 20"
    } else {
        return "\(numero) no es divisible por 20"
    }
}
print(resultados)
// ["10 no es divisible por 20",
//   "20 es divisible por 20",
//   "30 no es divisible por 20"]
```

<aside>
📎

*Este código puede leerse como:*

- El closure incluye lógica condicional para decidir cómo transformar cada número.
- Esto muestra que los closures en `.map` pueden ser tan simples o complejos como sea necesario.
</aside>

1. Uso de `.map` con Diccionarios

```swift
let edades = ["Luis": 25, "Ana": 30, "Carlos": 20]
let descripciones = edades.map { (nombre, edad) in
    return "\(nombre) tiene \(edad) años"
}

print(descripciones)
// ["Luis tiene 25 años", "Ana tiene 30 años", "Carlos tiene 20 años"]
```

<aside>
📎

*Este código puede leerse como:*

- Para diccionarios, el closure en `.map` recibe dos parámetros: la clave (`nombre`) y el valor (`edad`).
- El resultado es un arreglo con los valores transformados.
</aside>

1. Uso combinado con otros métodos funcionales

```swift
let numeros = [1, 2, 3, 4, 5, 6]
let paresCuadrados = numeros
    .filter { $0 % 2 == 0 } // Filtrar solo los números pares
    .map { $0 * $0 }        // Calcular el cuadrado de cada número par

print(paresCuadrados) // [4, 16, 36]
```

<aside>
📎

*Este código puede leerse como:*

`.map` puede combinarse con métodos como `.filter` y `.reduce` para realizar operaciones más avanzadas.

- `filter` elimina los números impares.
- `map` aplica el cuadrado a los números restantes.
</aside>

1. Mapeo con valores opcionales

```swift
let nombre: String? = "Luis"
let saludo = nombre.map { "Hola, \($0)!" }
print(saludo ?? "No hay nombre disponible")
// Hola, Luis!
```

<aside>
📎

*Este código puede leerse como:*

Cuando trabajas con valores opcionales, `.map` también es útil para manipularlos sin desenrollarlos manualmente.

- Si `nombre` es `nil`, el resultado del `.map` será `nil`.
- Esto permite trabajar con opcionales de manera segura.
</aside>

1. Uso avanzado con tipos personalizados

Aquí, cada objeto de tipo `Persona` se transforma en su propiedad `nombre`.

```swift
struct Persona {
    let nombre: String
    let edad: Int
}

let personas = [
    Persona(nombre: "Luis", edad: 25),
    Persona(nombre: "Ana", edad: 30),
    Persona(nombre: "Carlos", edad: 20)
]

let nombres = personas.map { $0.nombre }
print(nombres) // ["Luis", "Ana", "Carlos"]
```

# ***6. Método .filter {  }***

El método `.filter` permite filtrar elementos de una colección (como un arreglo o diccionario) que cumplen con una condición específica definida en un closure. Devuelve una nueva colección con los elementos que satisfacen el criterio del filtro.

**Características principales de `.filter`:**

- Filtrado condicional: El closure debe devolver un valor booleano (`true` para incluir el elemento, `false` para excluirlo).
- Inmutabilidad: No modifica la colección original; devuelve una nueva.
- Uso en Arrays, Sets y Diccionarios.
1. Ejemplo básico

```swift
let numeros = [1, 2, 3, 4, 5, 6]
let numerosPares = numeros.filter { $0 % 2 == 0 }
print(numerosPares) // [2, 4, 6]
```

<aside>
📎

*Este código puede leerse como:*

- El closure `{ $0 % 2 == 0 }` evalúa si cada número es divisible por 2.
- Solo los números que cumplen esta condición (`true`) se incluyen en el arreglo `numerosPares`.
</aside>

1. Filtrando con closures explícitos

```swift
let nombres = ["Ana", "Luis", "María", "Carlos", "Juan"]
let nombresConA = nombres.filter { (nombre) -> Bool in
    return nombre.contains("a") || nombre.contains("A")
}
print(nombresConA) // ["Ana", "María", "Carlos"]
```

<aside>
📎

*Este código puede leerse como:*

- Aquí se usa un closure explícito con un parámetro llamado `nombre`.
- La condición `nombre.contains("a") || nombre.contains("A")` filtra solo los nombres que contienen la letra "a" (mayúscula o minúscula).
</aside>

1. Filtrando números mayores a un valor

```swift
let edades = [15, 18, 21, 24, 30, 12]
let mayoresDeEdad = edades.filter { $0 >= 18 }
print(mayoresDeEdad) // [18, 21, 24, 30]
```

<aside>
📎

*Este código puede leerse como:*

- El closure `{ $0 >= 18 }` evalúa si la edad es mayor o igual a 18.
- Solo las edades que cumplen la condición se incluyen en el resultado.
</aside>

1. Uso de `.filter` con Diccionario

```swift
let inventario = ["Manzanas": 50, "Peras": 20, "Plátanos": 0, "Naranjas": 30]
let productosDisponibles = inventario.filter { $0.value > 0 }

print(productosDisponibles)
// ["Manzanas": 50, "Peras": 20, "Naranjas": 30]
```

<aside>
📎

*Este código puede leerse como:*

- En un diccionario, el closure recibe cada clave y valor como un par `(key, value)`.
- La condición `$0.value > 0` filtra los productos con existencias mayores a 0.
</aside>

1. Uso combinado con otros métodos funcionales

```swift
let numeros = [1, 2, 3, 4, 5, 6]
let cuadradosDePares = numeros
    .filter { $0 % 2 == 0 } // Filtrar números pares
    .map { $0 * $0 }        // Calcular el cuadrado de cada par

print(cuadradosDePares) // [4, 16, 36]
```

<aside>
📎

*Este código puede leerse como:*

Puedes combinar `.filter` con otros métodos como `.map` para realizar transformaciones adicionales después del filtrado.

- Primero, `.filter` selecciona solo los números pares.
- Luego, `.map` transforma estos números al calcular sus cuadrados.
</aside>

1. Ejemplo avanzado: Filtrando objetos personalizados

```swift
struct Persona {
    let nombre: String
    let edad: Int
}

let personas = [
    Persona(nombre: "Luis", edad: 25),
    Persona(nombre: "Ana", edad: 17),
    Persona(nombre: "Carlos", edad: 30)
]

let mayoresDeEdad = personas.filter { $0.edad >= 18 }
print(mayoresDeEdad.map { $0.nombre })
// ["Luis", "Carlos"]
```

<aside>
📎

*Este código puede leerse como:*

- Se filtran los objetos de tipo `Persona` cuyo atributo `edad` sea mayor o igual a 18.
- Con `.map`, extraemos los nombres de las personas filtradas.
</aside>

1. Uso de `.filter` con valores opcionales

```swift
let numeros: [Int?] = [1, 2, nil, 4, nil, 6]
let numerosValidos = numeros.compactMap { $0 }.filter { $0 % 2 == 0 }
print(numerosValidos) // [2, 4, 6]
```

<aside>
📎

*Este código puede leerse como:*

Si trabajas con opcionales, `.filter` puede ayudarte a ignorar valores no deseados.

- `compactMap` elimina los valores `nil`.
- Luego, `.filter` selecciona solo los números pares.
</aside>

1. Uso avanzado con cadenas

```swift
let frases = ["Swift es genial", "Me gusta programar", "Swift es fácil de aprender", "Python es popular"]
let frasesConSwift = frases.filter { $0.contains("Swift") }
print(frasesConSwift)
// ["Swift es genial", "Swift es fácil de aprender"]
```

<aside>
📎

*Este código puede leerse como:*

La condición `contains("Swift")` filtra las frases que contienen la palabra "Swift".

</aside>

# ***7. Método .reduce( )***

El método `.reduce` se utiliza para combinar los elementos de una colección en un único valor, aplicando un closure que especifica cómo combinar los elementos. Es especialmente útil para operaciones como la suma, la concatenación o la creación de valores complejos a partir de colecciones.

Sintaxis de `.reduce`

```swift
let resultado = coleccion.reduce(valorInicial) { acumulador, elemento in
    // Operación para combinar acumulador y elemento
}
```

- **`valorInicial`**: Punto de partida para la operación.
- **`acumulador`**: Valor acumulado hasta el momento.
- **`elemento`**: Cada elemento de la colección que se está procesando.
1. Sumar los elementos de un arreglo

```swift
let numeros = [1, 2, 3, 4, 5]
let suma = numeros.reduce(0) { acumulador, numero in
    acumulador + numero
}

print(suma) // 15
```

Versión simplificada:

```swift
let suma = numeros.reduce(0, +)
print(suma) // 15
```

<aside>
📎

*Este código puede leerse como:*

- `0` es el valor inicial del acumulador.
- El closure suma cada número al acumulador.
</aside>

1. Concatenar cadenas

```swift
let palabras = ["Swift", "es", "genial"]
let frase = palabras.reduce("") { acumulador, palabra in
    acumulador + " " + palabra
}.trimmingCharacters(in: .whitespaces)
print(frase) // Salida: "Swift es genial"
```

<aside>
📎

*Este código puede leerse como:*

- El valor inicial es una cadena vacía `""`.
- El closure combina el acumulador con cada palabra separándolas por un espacio.
- Se usa `trimmingCharacters` para eliminar espacios iniciales o finales.
</aside>

1. Encontrar el producto de los números

```swift
let numeros = [1, 2, 3, 4]
let producto = numeros.reduce(1) { acumulador, numero in
    acumulador * numero
}
print(producto) // 24
```

<aside>
📎

*Este código puede leerse como:*

- El valor inicial es `1` porque es el elemento neutro para la multiplicación.
- El closure multiplica cada número con el acumulador.
</aside>

1. Contar ocurrencias de elementos

```swift
let letras = ["a", "b", "a", "c", "a", "b"]
let conteo = letras.reduce(into: [:]) { acumulador, letra in
    acumulador[letra, default: 0] += 1
}
print(conteo) // ["a": 3, "b": 2, "c": 1]
```

<aside>
📎

*Este código puede leerse como:*

- Se usa `reduce(into:)` para modificar un diccionario mutable como acumulador.
- Cada letra se cuenta usando el índice `[letra, default: 0]`.
</aside>

1. Crear un diccionario desde un arreglo

```swift
let numeros = [1, 2, 3, 4]
let cuadradoPorNumero = numeros.reduce(into: [:]) { acumulador, numero in
    acumulador[numero] = numero * numero
}
print(cuadradoPorNumero) // [1: 1, 2: 4, 3: 9, 4: 16]
```

<aside>
📎

*Este código puede leerse como:*

- Se inicializa un diccionario vacío como acumulador.
- Para cada número, se calcula su cuadrado y se almacena como un par clave-valor.
</aside>

1. Calcular el valor máximo o mínimo

```swift
let numeros = [3, 7, 1, 9, 5]

let maximo = numeros.reduce(numeros[0]) { max($0, $1) }
print(maximo) // 9

let minimo = numeros.reduce(numeros[0]) { min($0, $1) }
print(minimo) // 1
```

<aside>
📎

*Este código puede leerse como:*

- El acumulador se inicializa con el primer elemento de la colección.
- Se compara cada elemento con el acumulador usando `max` o `min`.
</aside>

1. Uso avanzado con estructuras personalizadas

```swift
struct Producto {
    let nombre: String
    let precio: Double
}

let productos = [
    Producto(nombre: "Laptop", precio: 1200.0),
    Producto(nombre: "Mouse", precio: 50.0),
    Producto(nombre: "Teclado", precio: 80.0)
]

let precioTotal = productos.reduce(0.0) { acumulador, producto in
    acumulador + producto.precio
}

print(precioTotal) // 1330.0
```

<aside>
📎

*Este código puede leerse como:*

- El acumulador comienza en `0.0`.
- Se suma el precio de cada producto al acumulador.
</aside>

1. Agrupando elementos

```swift
let nombres = ["Ana", "Luis", "María", "Juan", "Ana", "Luis"]
let agrupados = nombres.reduce(into: [:]) { acumulador, nombre in
    acumulador[nombre, default: []].append(nombre)
}
print(agrupados)
// ["Ana": ["Ana", "Ana"], "Luis": ["Luis", "Luis"], "María": ["María"], "Juan": ["Juan"]]
```

<aside>
📎

*Este código puede leerse como:*

Cada nombre se agrega a un arreglo dentro del diccionario agrupado.

</aside>

# ***8. Método .forEach { }***

El método `.forEach` se utiliza para iterar sobre cada elemento de una colección, ejecutando un closure para cada uno de ellos. Es una alternativa más compacta al bucle `for-in`, aunque con algunas diferencias clave.

Sintaxis de `.forEach`

```swift
coleccion.forEach { elemento in
    // Código para procesar cada elemento
}
```

- **`coleccion`**: Puede ser un arreglo, un conjunto, un diccionario o cualquier colección.
- **`elemento`**: Cada elemento de la colección que se pasa al closure.d
1. Iterar sobre un arreglo

```swift
let numeros = [1, 2, 3, 4, 5]
numeros.forEach { numero in
    print("Número: \(numero)")
}
// Número: 1
// Número: 2
// Número: 3
// Número: 4
// Número: 5
```

<aside>
📎

*Este código puede leerse como:*

El closure imprime cada número del arreglo.

</aside>

1. Operaciones con índices usando `forEach`

```swift
let frutas = ["Manzana", "Plátano", "Cereza"]
frutas.enumerated().forEach { (indice, fruta) in
    print("Fruta \(indice): \(fruta)")
}
// Fruta 0: Manzana
// Fruta 1: Plátano
// Fruta 2: Cereza
```

<aside>
📎

*Este código puede leerse como:*

Aunque `.forEach` no proporciona índices directamente, puedes usar el método `enumerated` para obtener tanto el índice como el valor.

`enumerated()` devuelve tuplas `(índice, elemento)` que se pasan al closure.

</aside>

1. Iterar sobre un diccionario

```swift
let edades = ["Ana": 25, "Luis": 30, "María": 22]
edades.forEach { (nombre, edad) in
    print("\(nombre) tiene \(edad) años.")
}
// Ana tiene 25 años.
// Luis tiene 30 años.
// María tiene 22 años.
```

<aside>
📎

*Este código puede leerse como:*

Con los diccionarios, `.forEach` permite acceder a las claves y valores.

Cada clave-valor del diccionario se pasa como un par `(clave, valor)` al closure.

</aside>

1. Realizar acciones condicionales

```swift
let numeros = [1, 2, 3, 4, 5, 6]
numeros.forEach { numero in
    if numero % 2 == 0 {
        print("\(numero) es par.")
    }
}
// 2 es par.
// 4 es par.
// 6 es par.
```

<aside>
📎

*Este código puede leerse como:*

Puedes usar estructuras condicionales dentro del closure para filtrar elementos.

Se evalúa cada número y solo los pares se procesan dentro del closure.

</aside>

1. Usar `forEach` para cálculos

```swift
var suma = 0
let numeros = [1, 2, 3, 4, 5]
numeros.forEach { numero in
    suma += numero
}
print("La suma es: \(suma)") // La suma es: 15
```

<aside>
📎

*Este código puede leerse como:*

Aunque `.forEach` no devuelve resultados, puedes usarlo para realizar cálculos o modificaciones en elementos mutables.

Se acumula la suma de los elementos del arreglo en la variable `suma`.

</aside>

```swift
var numeros = [1, 2, 3, 4]
numeros.indices.forEach { indice in
    numeros[indice] *= 2
}
print(numeros) // [2, 4, 6, 8]
```

<aside>
📎

*Este código puede leerse como:*

Aunque `.forEach` no modifica directamente los elementos de una colección inmutable, puedes combinarlo con un índice para actualizar un arreglo mutable.

</aside>

1. Diferencia con `for-in`

El método `.forEach` no permite usar `continue` o `break` dentro del closure.

```swift
let numeros = [1, 2, 3, 4, 5]

// Esto funciona con `for-in`:
for numero in numeros {
    if numero == 3 { continue }
    print(numero)
}

// Esto da error con `.forEach`:
numeros.forEach { numero in
    if numero == 3 { 
        // Error: 'continue' cannot be used inside a closure
        // No se permite "continue" ni "break"
    }
}
```

# ***9. Método .compactMap { }***

El método `.compactMap` aplica un closure a cada elemento de una colección, transforma los elementos y descarta los que resulten en `nil`. El resultado es una colección no opcional.

Sintaxis

```swift
coleccion.compactMap { elemento -> Tipo? in
    // Código que transforma `elemento`
}
```

1. Filtrar valores opcionales

```swift
let numeros: [String?] = ["1", nil, "3", "4", nil]
let enteros = numeros.compactMap { numero -> Int? in
    if let numero = numero {
        return Int(numero)
    }
    return nil
}
print(enteros) // [1, 3, 4]
```

<aside>
📎

*Este código puede leerse como:*

- El closure convierte cada cadena a un número entero si no es `nil`.
- Los valores `nil` se descartan automáticamente.
</aside>

1. Simplificación con transformación directa

```swift
let valores = ["10", "abc", "30", "40"]
let enteros = valores.compactMap { Int($0) }
print(enteros) // [10, 30, 40]
```

<aside>
📎

*Este código puede leerse como:*

Si `Int($0)` devuelve `nil` (porque no se puede convertir una cadena), el valor se omite del resultado.

</aside>

1. Transformación y filtrado en un solo paso

```swift
let edades = [18, 21, nil, 30, nil, 25]
let mayoresDe21 = edades.compactMap { $0 }.filter { $0 > 21 }
print(mayoresDe21) // [30, 25]
```

<aside>
📎

*Este código puede leerse como:*

- `.compactMap` elimina los valores `nil`.
- Luego `.filter` selecciona los mayores de 21.
</aside>

# ***10. Método .flatMap { }***

El método `.flatMap` transforma los elementos de una colección en otros, al igual que `.map`, pero a la vez "aplana" colecciones anidadas. Si el resultado del closure es una colección, `.flatMap` combina los resultados en una sola colección plana.

Sintaxis

```swift
coleccion.flatMap { elemento -> TipoDeColeccion in
    // Código que transforma `elemento`
}
```

1. Aplanar colecciones anidadas

Cada arreglo interno se "aplana" en un solo arreglo.

```swift
let listas = [[1, 2, 3], [4, 5], [6, 7, 8]]
let aplanada = listas.flatMap { $0 }
print(aplanada) // [1, 2, 3, 4, 5, 6, 7, 8]
```

1. Transformar y aplanar

```swift
let cadenas = ["Hola mundo", "Swift 6"]
let palabras = cadenas.flatMap { $0.split(separator: " ") }
print(palabras) // ["Hola", "mundo", "Swift", "6"]
```

<aside>
📎

*Este código puede leerse como:*

- Cada cadena se separa en palabras.
- `.flatMap` combina todas las palabras en una sola colección.
</aside>

1. Trabajar con opcionales

```swift
let numeros: [Int?] = [1, 2, nil, 4, nil]
let filtrados = numeros.flatMap { $0 }
print(filtrados) // [1, 2, 4]
```

<aside>
📎

*Este código puede leerse como:*

- Cuando se usa `.flatMap` en una colección con valores opcionales, se comporta como `.compactMap`.
- `.flatMap` elimina los valores `nil` automáticamente.
</aside>

**Comparación entre `.compactMap` y `.flatMap`**

Diferencia principal

- `.compactMap`: Elimina valores `nil` después de aplicar una transformación.
- `.flatMap`: Aplana colecciones anidadas y, en algunos casos, elimina valores `nil`.

# *11. Optimización de Sintaxis (Trailing Closure)*

**¿Qué son los Trailing Closures?**

Cuando pasamos un closure como **último argumento** de una función, podemos sacarlo fuera de los paréntesis de la llamada a la función. Esto mejora la legibilidad, especialmente si el closure es largo.

```swift
func realizarOperacion(operacion: () -> Void) {
    print("Iniciando operación...")
    operacion()
    print("Operación completada.")
}
```

Podemos llamar a esta función pasando un closure de dos maneras:

**1. Sin Trailing Closure:**

```swift
realizarOperacion(operacion: {
    print("Realizando una tarea importante.")
})
```

2. Con Trailing Closure:

```swift
realizarOperacion {
    print("Realizando una tarea importante.")
}
```

```swift
// Iniciando operación...
// Realizando una tarea importante.
// Operación completada.
```

# *12. Closure Escaping*

Los closures escapantes son aquellos que pueden ejecutarse después de que la función que los recibe haya terminado.

Se marcan con `@escaping`.

```swift
var listaDeTareas: [() -> Void] = []

func agregarTarea(tarea: @escaping () -> Void) {
listaDeTareas.append(tarea)
}

agregarTarea {
print("Tarea 1 completada")
}

agregarTarea {
print("Tarea 2 completada")
}

for tarea in listaDeTareas {
tarea()
}
// Tarea 1 completada
// Tarea 2 completada
```

<aside>
📎

*Este código puede leerse como:*

1. *Declaración de la variable `listaDeTareas`:*
- *Tipo: Es una lista (array) de funciones sin parámetros que no retornan nada (`() -> Void`).*
- *Propósito: Almacenar funciones que representan las tareas que se desean ejecutar más tarde.*
1. *Función `agregarTarea`:*
- *Parámetro `tarea`: Es una función (o closure) que se pasa como argumento.*
- *Palabra clave `@escaping`: Indica que el closure se guardará para ser ejecutado después, fuera del alcance de la función. Esto es necesario porque el closure se añade a `listaDeTareas`, que vive más allá del ciclo de vida de la función `agregarTarea`.*
1. *Uso de `agregarTarea`:*

*Aquí se crea un closure que imprime `"Tarea 1 completada"`, y este closure se pasa como argumento a `agregarTarea`. La función lo agrega a `listaDeTareas` , Lo mismo ocurre con la segunda llamada.*

1. *Ejecución de las tareas:*
- *Se recorre la lista de tareas con un bucle `for`.*
- *Cada elemento en `listaDeTareas` es un closure, y al invocar `tarea()` se ejecuta el código que contiene.*

*Resultado en consola:*

- *El primer closure imprime `"Tarea 1 completada"`.*
- *El segundo closure imprime `"Tarea 2 completada"`.*

*Este patrón es útil para almacenar y ejecutar acciones de forma diferida. Por ejemplo, en aplicaciones como gestores de tareas o eventos asíncronos, puedes acumular acciones a realizar y ejecutarlas en el momento adecuado.*

</aside>

# *13. Autoclosure*

Son closures implícitos que no requieren una sintaxis explícita al llamarlos. Su uso es común para operaciones diferidas o con condiciones.

```swift
func ejecutarSoloSi(_ condicion: Bool, tarea: @autoclosure () -> Void) {
    if condicion {
        tarea()
    }
}

ejecutarSoloSi(true, tarea: print("Condición cumplida"))
// Condición cumplida
```

<aside>
📎

*Este código puede leerse como:*

1. *Declaración de la función*

*Argumentos:*

- `*condicion`: Es un parámetro de tipo `Bool` que determina si se ejecutará la tarea.*
- `*tarea`: Es un argumento que utiliza el atributo `@autoclosure`, lo que significa que la expresión que se pasa como argumento será automáticamente transformada en una clausura sin que el usuario tenga que escribir explícitamente `{}`.*

*¿Qué hace la función?*

- *Verifica si `condicion` es `true`.*
- *Si la condición es verdadera, se ejecuta la expresión proporcionada en `tarea`.*
1. *Uso del atributo `@autoclosure`* 

*El atributo `@autoclosure` convierte automáticamente una expresión en una clausura. Esto hace que el código sea más limpio y más fácil de leer. Sin este atributo, tendrías que escribir explícitamente la clausura al llamar a la función.*

*3. Ventajas de `@autoclosure`*

- *Hace que el código sea más limpio y legible.*
- *Permite posponer la evaluación de expresiones hasta que realmente se necesiten, lo cual puede mejorar el rendimiento en algunos casos.*

*4. Casos de uso comunes*

- *Validaciones condicionales.*
- *Implementaciones de operadores como `??` (Nil coalescing).*
- *Código donde quieres retrasar la ejecución de una expresión hasta que sea estrictamente necesaria.*
</aside>

***Usos Comunes***

1. Callbacks en programación asíncrona (por ejemplo, en `URLSession` o `completion handlers`).
2. Procesamiento de colecciones (`map`, `filter`, `reduce`, etc.).
3. Configuración diferida.
4. Encapsular lógica temporal (como en temporizadores o tareas diferidas).

---