# Collection Types

> Cada una de estas estructuras tiene su uso particular según las necesidades de la aplicación.
> 

En Swift, las **tuples**, **array**, **set** y **dictionary** son estructuras de datos fundamentales que se utilizan para almacenar y organizar información de diferentes maneras. A continuación te explico qué son y cómo se usan cada uno de estos tipos:

# ***1. Tuples***

En Swift, las tuples son estructuras que permiten agrupar varios valores en una única unidad. Esto es útil cuando deseas manejar y pasar múltiples valores relacionados sin necesidad de crear una clase o estructura separada. Cada valor en una tuples puede tener un tipo distinto, y puedes acceder a los elementos de la tuples tanto por su posición como por nombres si los asignas.

```swift
let persona = ("Juan", 30, "España")
```

Aquí, `persona` es una tuples que agrupa el nombre de una persona, su edad y su país de origen. Puedes acceder a los elementos de la siguiente forma:

```swift
print(persona.0) // "Juan"
print(persona.1) // 30
print(persona.2) // "España"
```

## ***1.1 Tuples con nombres para los elementos***

Una de las grandes ventajas de las tuplas en Swift es que puedes darle nombres a cada uno de los valores que contiene. Esto hace que el código sea más claro y legible:

```swift
let persona = (nombre: "Juan", edad: 30, pais: "España")
print(persona.nombre) // "Juan"
print(persona.edad)   // 30
print(persona.pais)   // "España"
```

## ***1.2 Usos y utilidades de las Tuples***

- Devolver múltiples valores de una función: una de las aplicaciones más comunes de las tuples es devolver varios valores de una función sin tener que crear una estructura personalizada.
    
    ```swift
    func obtenerDimensiones() -> (ancho: Int, alto: Int) {
        return (1024, 768)
    }
    
    let dimensiones = obtenerDimensiones()
    print(dimensiones.ancho) // 1024
    print(dimensiones.alto)  // 768
    ```
    
- Agrupar datos temporalmente: las tuples son ideales cuando necesitas agrupar datos de manera temporal. Por ejemplo, en una función que sólo necesita devolver un par de valores relacionados.
- Trabajar con patrones de correspondencia (pattern matching): Swift permite descomponer las tuples mediante *pattern matching*, lo cual es útil en bucles `for`, `switch` y otras estructuras de control.
    
    ```swift
    let coordenada = (x: 10, y: 20)
    
    switch coordenada {
    case (0, 0):
        print("Origen")
    case (let x, 0):
        print("En el eje X en \(x)")
    case (0, let y):
        print("En el eje Y en \(y)")
    case (let x, let y):
        print("En algún lugar en (\(x), \(y))")
    }
    ```
    
- Comparar valores fácilmente: Puedes comparar tuples que tengan el mismo tipo de elementos. Swift permite comparaciones directas entre ellas:
    
    ```swift
    let punto1 = (x: 10, y: 20)
    let punto2 = (x: 10, y: 20)
    
    if punto1 == punto2 {
        print("Los puntos son iguales")
    }
    ```
    

## ***1.3 Ventajas y limitaciones de las Tuples***

Ventajas:

- Son fáciles de usar y permiten agrupar valores sin crear nuevas clases o estructuras.
- Son útiles para funciones que necesitan devolver múltiples valores rápidamente.
- Pueden mejorar la legibilidad cuando se usan para datos de corto plazo.

Limitaciones:

- No están pensadas para datos complejos o que necesiten persistir durante un tiempo prolongado.
- Las tuples no tienen métodos o funcionalidades avanzadas como las estructuras o clases.
- No se puede modificar el tipo o cantidad de elementos una vez que una tuples ha sido creada.

## ***1.4 Cuándo usar las Tuples***

Las tuples son perfectas para casos simples y de corto plazo. Si necesitas representar una estructura de datos más compleja o que tenga lógica adicional, es mejor usar `struct` o `class`.

# ***2. Array***

Las array (o arreglos) en Swift son estructuras de datos que permiten almacenar una colección de elementos del mismo tipo en un orden específico. Vamos a desglosar su funcionamiento, propiedades y usos:

## *2.1 **Creación de Array***

En Swift, puedes crear un array especificando su tipo entre corchetes `[]`, o dejando que Swift infiera el tipo a partir de los elementos:

```swift
// Creación de un array vacío de enteros
var numeros: [Int] = []

// Usando inferencia de tipo
var frutas = ["Manzana", "Banana", "Cereza"]

// Modificando su valor
frutas[1] = "Platano"
```

## *2.2 **Propiedades de los Array***

Los array en Swift tienen varias propiedades útiles:

- `count`: Devuelve la cantidad de elementos en el array.
    
    ```swift
    print(frutas.count) // Resultado: 3
    ```
    
- `isEmpty`: Retorna `true` si el array está vacío, `false` en caso contrario.
    
    ```swift
    print(numeros.isEmpty) // Resultado: true
    ```
    
- `first` y `last`: Retornan el primer y último elemento respectivamente (opcionales, ya que pueden ser `nil` en un array vacío).
    
    ```swift
    print(frutas.first) // Resultado: Optional("Manzana")
    print(frutas.last) // Resultado: Optional("Cereza")
    ```
    

## *2.3 **Acceso y modificación de elementos***

Los array permiten acceder y modificar sus elementos mediante índices:

```swift
// Acceso por índice
let primeraFruta = frutas[0] // "Manzana"

// Modificar un elemento
frutas[1] = "Fresa"
print(frutas) // Resultado: ["Manzana", "Fresa", "Cereza"]
```

## *2.4 **Métodos de manipulación de Array***

Swift proporciona métodos muy útiles para manipular array:

- `append(_:)`: Agrega un elemento al final del array.
    
    ```swift
    frutas.append("Naranja")
    ```
    
- `insert(_:at:)`: Inserta un elemento en una posición específica.
    
    ```swift
    frutas.insert("Uva", at: 1)
    ```
    
- `remove(at:)`: Elimina un elemento en un índice específico.
    
    ```swift
    frutas.remove(at: 2)
    ```
    
- `removeLast()` y `removeAll()`: Elimina el último elemento o todos los elementos respectivamente.
    
    ```swift
    frutas.removeLast()
    frutas.removeAll()
    ```
    

## *2.5 **Iteración sobre Array***

Puedes recorrer los array con distintos bucles:

```swift
for fruta in frutas {
    print(fruta)
}

// Acceder al índice y al elemento al mismo tiempo
for (indice, fruta) in frutas.enumerated() {
    print("La fruta en el índice \(indice) es \(fruta)")
}
```

## *2.6 **Arrays Inmutables***

Si declaras un array como `let`, se vuelve inmutable; es decir, no puedes cambiar sus elementos ni agregar o eliminar:

```swift
let numerosConstantes = [1, 2, 3]
// numerosConstantes.append(4) // Esto generará un error
```

## *2.7 **Otras Operaciones y Funcionalidades Avanzadas***

- `map(_:)`: Transforma cada elemento del array aplicándole una función.
    
    ```swift
    let longitudes = frutas.map { $0.count }
    ```
    
- `filter(_:)`: Retorna un nuevo array con los elementos que cumplen una condición.
    
    ```swift
    let frutasConA = frutas.filter { $0.contains("a") }
    ```
    
- `reduce(_:_:)`: Acumula los elementos en un solo valor usando una operación.
    
    ```swift
    let suma = numeros.reduce(0, +)
    ```
    

Aquí tienes un ejemplo completo que usa varios de los conceptos mencionados:

```swift
var numeros = [1, 2, 3, 4, 5]

// Agregar elementos
numeros.append(6)
numeros.insert(0, at: 0)

// Filtrar y mapear
let numerosPares = numeros.filter { $0 % 2 == 0 }
let numerosCuadrados = numeros.map { $0 * $0 }

// Sumar elementos
let sumaTotal = numeros.reduce(0, +)

print("Array original: \(numeros)")
print("Números pares: \(numerosPares)")
print("Cuadrados: \(numerosCuadrados)")
print("Suma total: \(sumaTotal)")
```

***Cuándo usar una Array***

Los array en Swift son estructuras potentes y versátiles. Tienen propiedades y métodos que permiten tanto operaciones básicas (como agregar o eliminar elementos) como manipulaciones avanzadas (como transformaciones y filtrados).

# ***3. Set***

En Swift, un `Set` es una colección de elementos únicos y no ordenados, lo que significa que no contiene duplicados y no mantiene el orden de inserción. Es ideal para trabajar con colecciones donde no importa el orden, pero sí la unicidad de los elementos. Aquí tienes una explicación detallada de sus propiedades, métodos y usos.

## *3.1 Creación de un Set*

Para crear un `Set`, puedes usar la sintaxis de literales (`[]`) o el inicializador estándar:

```swift
var conjuntoDeNúmeros: Set<Int> = [1, 2, 3, 4, 5]
var conjuntoVacio = Set<String>()  // Crea un Set vacío de cadenas
```

## *3.2 Propiedades de un Set*

- `count`: Devuelve el número de elementos en el `Set`.

```swift
print(conjuntoDeNúmeros.count)    // Imprime 5
```

- `isEmpty`: Retorna `true` si el `Set` está vacío.

```swift
print(conjuntoDeNúmeros.isEmpty)  // Imprime false
```

- `contains(_:)`: Verifica si un elemento específico está en el `Set`.

```swift
print(conjuntoDeNúmeros.contains(3))  // Imprime true
```

## *3.3 Métodos Comunes*

### *3.3.1 Agregar y Eliminar Elementos*

- `insert(_:)`: Inserta un elemento en el `Set`. Si ya existe, no hace nada.

```swift
conjuntoDeNúmeros.insert(6)  // Añade el 6 al conjunto
```

- `remove(_:)`: Elimina un elemento específico del `Set` si está presente.

```swift
conjuntoDeNúmeros.remove(2)  // Elimina el 2 del conjunto
```

- `removeAll()`: Elimina todos los elementos del `Set`.

```swift
conjuntoDeNúmeros.removeAll()  // Limpia el conjunto
```

### *3.3.2 Operaciones de Conjunto*

Swift proporciona varias operaciones de teoría de conjuntos estándar como la unión, intersección, diferencia y diferencia simétrica:

```swift
let setA: Set = [1, 2, 3, 4]
let setB: Set = [3, 4, 5, 6]
```

- `union(_:)`: Devuelve un nuevo `Set` con todos los elementos de ambos conjuntos.

```swift
let unionSet = setA.union(setB)  // [1, 2, 3, 4, 5, 6]
```

- `intersection(_:)`: Devuelve un `Set` con solo los elementos comunes entre ambos conjuntos.

```swift
let intersectionSet = setA.intersection(setB)  // [3, 4]

```

- `subtracting(_:)`: Devuelve un `Set` con los elementos de un conjunto excluyendo los del otro.

```swift
let subtractingSet = setA.subtracting(setB)  // [1, 2]
```

- `symmetricDifference(_:)`: Devuelve un `Set` con los elementos que están en uno u otro conjunto, pero no en ambos.

```swift
let symmetricDifferenceSet = setA.symmetricDifference(setB)  // [1, 2, 5, 6]
```

### *3.3.3 Comparación de Conjuntos*

```swift
let setC: Set = [1, 2]
```

- `isSubset(of:)`: Retorna `true` si todos los elementos de un `Set` están contenidos en otro.

```swift
print(setC.isSubset(of: setA))  // true
```

- `isSuperset(of:)`: Retorna `true` si el conjunto contiene todos los elementos del otro.

```swift
print(setA.isSuperset(of: setC))  // true
```

- `isDisjoint(with:)`: Retorna `true` si los conjuntos no tienen elementos en común.

```swift
print(setA.isDisjoint(with: setB))  // false, tienen 3 y 4 en común
```

### *3.3.4 **Iteración***

Para recorrer un `Set`, puedes usar un bucle `for`. Dado que el `Set` es una colección no ordenada, el orden de los elementos no está garantizado:

```swift
for número in setA {
    print(número)
}
```

Aquí tienes un ejemplo práctico que cubre varios usos:

```swift
var frutas: Set = ["Manzana", "Plátano", "Cereza"]

// Agregar elementos
frutas.insert("Naranja")
print(frutas)  // ["Manzana", "Plátano", "Cereza", "Naranja"]

// Verificar existencia
if frutas.contains("Plátano") {
    print("Plátano está en el conjunto")
}

// Operaciones de conjunto
let otrasFrutas: Set = ["Cereza", "Mango"]
let frutasComunes = frutas.intersection(otrasFrutas)  // ["Cereza"]
let todasLasFrutas = frutas.union(otrasFrutas)  // ["Manzana", "Plátano", "Cereza", "Naranja", "Mango"]

print(frutasComunes)
print(todasLasFrutas)
```

**Cuándo Usar un Set**

Usa `Set` cuando:

- Necesites almacenar elementos únicos sin preocuparte por el orden.
- Realices operaciones frecuentes de búsqueda y verificación de existencia (es más eficiente que `Array` en estos casos).
- Tengas que trabajar con operaciones de conjunto como unión, intersección y diferencia.

Los `Set` en Swift son muy útiles para manejar colecciones con condiciones de unicidad y se optimizan en cuanto a eficiencia cuando necesitas verificar rápidamente la existencia de elementos.

# ***4. Dictionary***

Los dictionaries en Swift son colecciones de pares clave-valor. Cada valor está asociado a una clave única, lo que permite almacenar datos de manera estructurada y acceder a ellos de manera rápida usando sus claves. A continuación, te explico en detalle cómo funcionan, sus propiedades, métodos y ejemplos de uso.

## *4.1 **Creación de un Dictionary***

Un diccionario en Swift se declara con el tipo `Dictionary<KeyType, ValueType>`, donde `KeyType` es el tipo de las claves y `ValueType` el tipo de los valores.

```swift
var capitales: [String: String] = ["Italia": "Roma", "Perú": "Lima", "Holanda": "Ámsterdam"]
```

Swift infiere los tipos automáticamente, así que también podrías escribirlo como:

```swift
var capitales = ["Italia": "Roma", "Perú": "Lima", "Holanda": "Ámsterdam"]
```

## *4.2 **Propiedades de los Dictionary***

- `count`: Devuelve el número de pares clave-valor en el diccionario.
    
    ```swift
    print(capitales.count) // Ejemplo de salida: 3
    ```
    
- `isEmpty`: Verifica si el diccionario está vacío.
    
    ```swift
    if capitales.isEmpty {
        print("El diccionario está vacío")
    } else {
        print("El diccionario no está vacío")
    }
    ```
    
- `keys`: Devuelve una colección con todas las claves del diccionario.
    
    ```swift
    let claves = capitales.keys
    ```
    
- `values`: Devuelve una colección con todos los valores del diccionario.
    
    ```swift
    let valores = capitales.values
    ```
    

## *4.3 **Acceso y Modificación de Valores***

- Acceso a un valor: Puedes acceder a un valor mediante su clave.
    
    ```swift
    let capitalDeItalia = capitales["Italia"] // "Roma"
    ```
    
- Agregar o actualizar un valor: Usando la clave, puedes agregar o actualizar un valor.
    
    ```swift
    capitales["Francia"] = "París" // Añade un nuevo par clave-valor
    capitales["Italia"] = "Milán"  // Actualiza el valor para la clave "Italia"
    ```
    
- Eliminar un valor: Usa el método `removeValue(forKey:)` para eliminar un valor.
    
    ```swift
    capitales.removeValue(forKey: "Italia") // Elimina "Italia": "Roma"
    ```
    
- Remover todos los elementos: Usa `removeAll()` para vaciar el diccionario.
    
    ```swift
    capitales.removeAll() // El diccionario estará vacío después de esto
    ```
    

## *4.4 **Métodos Comunes***

- `updateValue(forKey:)`: Agrega o actualiza un valor y devuelve el valor anterior si existe.
    
    ```swift
    if let valorAnterior = capitales.updateValue("Ámsterdam", forKey: "Holanda") {
        print("Valor anterior: \(valorAnterior)")
    }
    ```
    
- `contains(where)`: Verifica si el diccionario contiene un par clave-valor que cumpla una condición.
    
    ```swift
    let existe = capitales.contains { $0.key == "Italia" && $0.value == "Roma" }
    print(existe) // true si existe la clave "Italia" con el valor "Roma"
    ```
    
- `merge(_:uniquingKeysWith:)` ****: Combina otro diccionario con el diccionario actual. Si hay claves duplicadas, puedes decidir qué hacer con el conflicto.
    
    ```swift
    let otrosCapitales = ["Alemania": "Berlín", "Italia": "Roma"]
    capitales.merge(otrosCapitales) { (actual, nuevo) in nuevo }
    ```
    
- `mapValues(_:)`: Aplica una función a cada valor del diccionario, devolviendo un nuevo diccionario.
    
    ```swift
    let capitalesEnMayusculas = capitales.mapValues { $0.uppercased() }
    ```
    

## *4.5 **Iteración***

Swift permite recorrer los diccionarios usando bucles `for-in`:

```swift
for (pais, capital) in capitales {
    print("La capital de \(pais) es \(capital).")
}
```

Aquí tienes un ejemplo que usa varias de las propiedades y métodos descritos:

```swift
var capitales: [String: String] = ["Italia": "Roma", "Perú": "Lima", "Holanda": "Ámsterdam"]

// Acceder a un valor
if let capital = capitales["Italia"] {
    print("La capital de Italia es \(capital)")
}

// Añadir un nuevo valor
capitales["España"] = "Madrid"

// Actualizar un valor existente
capitales["Italia"] = "Milán"

// Eliminar un valor
capitales.removeValue(forKey: "Holanda")

// Iterar sobre el diccionario
for (pais, capital) in capitales {
    print("La capital de \(pais) es \(capital)")
}

// Verificar si está vacío
print("¿Está vacío? \(capitales.isEmpty)")

// Contar elementos
print("Número de elementos: \(capitales.count)")

// Obtener todas las claves y valores
print("Claves: \(capitales.keys)")
print("Valores: \(capitales.values)")

// Usar mapValues para crear un nuevo diccionario con las capitales en minúsculas
let capitalesMinusculas = capitales.mapValues { $0.lowercased() }
print(capitalesMinusculas)
```

***Cuándo usar los Dictionary***

Los diccionarios en Swift son estructuras poderosas para organizar datos en pares clave-valor, con propiedades y métodos útiles que permiten manipular y acceder de manera eficiente a sus contenidos.

Usa un diccionario en Swift cuando trabajes con datos que:

1. Deben ser accedidos y gestionados rápidamente por una clave única.
2. Representan una estructura de relación clave-valor única.
3. Requieran modificaciones frecuentes.
4. Necesiten organizarse en categorías o agruparse bajo un mismo identificador.

En estos casos, los diccionarios proporcionan una solución eficiente para gestionar y manipular la información.

---