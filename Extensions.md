# Extensions

> Añadir funcionalidad a un tipo existente.
> 

Son una forma de agregar nuevas propiedades, métodos, inicializadores, subscripts o conformidades a protocolos en un tipo existente. Sin embargo, las extensiones no pueden sobrescribir funcionalidad ya existente.

# ***1. Sintaxis***

```swift
extension NombreDelTipo {
    // Nuevos métodos, propiedades calculadas, inicializadores, etc.
}
```

Agregamos un método a `Int` para saber si es par:

```swift
extension Int {
    func esPar() -> Bool {
        return self % 2 == 0
    }
}

print(4.esPar()) // true
print(7.esPar()) // false
```

<aside>
📎

*Este código puede leerse como:*

*1. Extensión de `Int`*

- *En Swift, las extensiones permiten añadir nuevas funcionalidades a clases, estructuras, enumeraciones y protocolos ya existentes, sin tener que modificar el código original. En este caso, estamos extendiendo el tipo `Int` (que representa números enteros) para añadirle un nuevo método.*

*2. Método `esPar`*

- *Aquí estamos definiendo un método dentro de la extensión, llamado `esPar`. Este método no toma ningún argumento, y devuelve un valor de tipo `Bool`, que puede ser `true` o `false`.*
- `*self`: Hace referencia al valor del objeto sobre el que se está llamando el método. Si tienes un número entero (por ejemplo, `4`), `self` se refiere a ese número.*
- `*self % 2`: Esto calcula el residuo de dividir el número entre 2. En otras palabras, verifica si el número es divisible por 2.*
    - *Si el residuo es 0, significa que el número es par, porque cualquier número divisible por 2 es par.*
    - *Si el residuo es distinto de 0, el número es impar.*
- *Por lo tanto, el método devuelve `true` si el número es par (es decir, el residuo de la división es 0), y `false` si es impar.*

*3. Uso de la extensión*

- `*4.esPar()`: Llama al método `esPar()` en el número `4`. Como 4 es un número par (porque `4 % 2 == 0`), la función retorna `true`.*
- `*7.esPar()`: Llama al mismo método en el número `7`. Como 7 es un número impar (porque `7 % 2 != 0`), la función retorna `false`.*

*Resumen*

- *Este código amplía el tipo `Int` para añadir un método `esPar()`, que permite comprobar si un número es par o impar. La extensión permite escribir de forma más sencilla y expresiva código como `4.esPar()`, en lugar de tener que escribir la lógica de la comprobación de paridad manualmente cada vez.*
- *Este es un ejemplo de cómo Swift permite personalizar y extender tipos básicos para hacer el código más legible y reutilizable.*
</aside>

# ***2. Usos principales de las extensiones***

## ***2.1 Métodos y Propiedades***

Solo se pueden agregar propiedades calculadas, no almacenadas.

```swift
extension String {
    var primeraLetra: Character? {
        return self.isEmpty ? nil : self.first
    }
}

print("Hola".primeraLetra!) // H
```

<aside>
📎

*Este código puede leerse como:*

*1. Extensión de `String`*

- *En Swift, las extensiones permiten agregar nuevas funcionalidades a tipos existentes, como clases, estructuras, enumeraciones, o protocolos, sin necesidad de modificar el código original del tipo. En este caso, estamos extendiendo el tipo `String` para agregar una propiedad nueva.*

*2. Propiedad calculada `primeraLetra`*

- `*primeraLetra` es una propiedad calculada. Las propiedades calculadas no almacenan valores, sino que calculan un valor cada vez que se accede a ellas.*
- *El tipo de la propiedad es `Character?`, lo que significa que devuelve un valor de tipo `Character` (un único carácter) o `nil` si no hay un carácter disponible.*
- *Dentro del bloque de la propiedad, se hace una comprobación con `self.isEmpty`. `self` se refiere al string sobre el cual se está llamando la propiedad, y `isEmpty` es una propiedad que indica si la cadena de texto está vacía (`true` si no contiene ningún carácter y `false` si tiene uno o más).*
    - *Si el string está vacío (`self.isEmpty` es `true`), la propiedad retorna `nil` (no hay primera letra).*
    - *Si el string no está vacío, la propiedad retorna el primer carácter del string, lo cual se consigue con `self.first`. `self.first` es una propiedad de `String` que devuelve el primer carácter de la cadena, o `nil` si el string está vacío.*

*3. Ejemplo de uso*

- *Aquí estamos llamando a la propiedad `primeraLetra` sobre el string `"Hola"`.*
- *Como `"Hola"` no está vacío, la propiedad devuelve el primer carácter de la cadena, que es `'H'`.*
- *El `!` al final de `primeraLetra!` significa que estamos forzando el desempaquetado de un valor opcional (`Character?`). Sabemos que el valor no es `nil` porque `"Hola"` no está vacío, por lo que podemos usar el operador `!`con seguridad.*
- *El valor de `'H'` se imprime en la consola.*

*Resumen:*

- *Este código extiende el tipo `String` para agregar una propiedad calculada llamada `primeraLetra`, que devuelve el primer carácter del string o `nil` si el string está vacío. En el ejemplo, `"Hola".primeraLetra!` imprime `'H'` porque es la primera letra de la cadena `"Hola"`.*
</aside>

## ***2.2 Inicializadores***

Puedes agregar inicializadores adicionales a estructuras y clases.

```swift
struct Punto {
    var x: Double
    var y: Double
}

extension Punto {
    init(coordenada: Double) {
        self.x = coordenada
        self.y = coordenada
    }
}

let punto = Punto(coordenada: 3.0)
print(punto) // Punto(x: 3.0, y: 3.0)
```

<aside>
📎

*Este código puede leerse como:*

1. *Definición de la estructura `Punto`*
- *Aquí defines una estructura llamada `Punto` con dos propiedades:*
    - `*x`: un valor de tipo `Double` que representa la coordenada en el eje X.*
    - `*y`: otro valor de tipo `Double` que representa la coordenada en el eje Y.*
- *Una estructura en Swift es un tipo de datos que te permite agrupar diferentes valores. En este caso, `Punto` agrupa dos valores numéricos (`x` y `y`) que corresponden a una coordenada en un plano cartesiano.*
1. *Extensión de `Punto`*
- *Usas una extensión para añadir una nueva función constructora (init) a la estructura `Punto`.*
- *En esta extensión, defines un nuevo inicializador (`init(coordenada:)`) que toma un solo parámetro de tipo `Double`llamado `coordenada`. Este inicializador crea un nuevo `Punto` con el mismo valor tanto para la coordenada `x` como para la coordenada `y`. Es decir, al usar este inicializador, `x` y `y` se inicializan con el mismo valor.*
1. *Creación de una instancia de `Punto`*
- *Aquí estás creando una instancia de `Punto` usando el inicializador que definiste en la extensión. Le pasas el valor `3.0`como argumento para la coordenada. Debido al inicializador que definiste, tanto `x` como `y` se asignan a `3.0`.*
    - *El resultado es un `Punto` con `x = 3.0` y `y = 3.0`.*
- *Luego, imprimes el valor de `punto`, y la salida será: Punto(x: 3.0, y: 3.0)*
- *Esto es porque la estructura `Punto` implementa un método estándar de Swift para representar sus valores cuando se imprime, mostrando las propiedades de la estructura.*

*Resumen*

- *Tienes una estructura `Punto` con dos propiedades: `x` y `y`.*
- *Definiste una extensión de `Punto` donde agregas un inicializador que toma un único valor para establecer tanto `x`como `y`.*
- *Creas un objeto `Punto` con ese inicializador y lo imprimes.*
- *El código te permite crear puntos en un plano cartesiano donde las coordenadas `x` e `y` son iguales cuando usas este inicializador.*
</aside>

## ***2.3 Conformidad a Protocolos***

Las extensiones pueden usarse para hacer que un tipo conforme a un protocolo.

```swift
protocol Saludable {
    func mensajeDeSalud() -> String
}

extension String: Saludable {
    func mensajeDeSalud() -> String {
        return "Hola, \(self), estás aprendiendo extensiones."
    }
}

print("Estudiante".mensajeDeSalud()) // Hola, Estudiante, estás aprendiendo extensiones.
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición del `protocol` Saludable:*

- *Aquí se define un protocol llamado `Saludable`. Los protocolos en Swift son como plantillas que definen métodos o propiedades que deben ser implementadas por las clases, estructuras o tipos que los adopten.*
- *El protocolo `Saludable` tiene un único método:*
    - `*mensajeDeSalud() -> String`: un método que debe devolver un `String`.*

*2. Extensión de `String` para adoptar el protocolo:*

- *Aquí se está utilizando una extensión en Swift para hacer que el tipo `String` adopte el protocolo `Saludable`.*
- `*extension String` significa que estamos extendiendo la funcionalidad de `String` (es decir, los objetos de tipo `String`).*
- *Al hacerlo, estamos implementando el método `mensajeDeSalud()` que se requiere por el protocolo `Saludable`.*
- *Dentro de este método, `self` hace referencia a la instancia de `String` sobre la que se llama este método. En este caso, el mensaje que se devuelve es una cadena de texto que dice: `"Hola, \(self), estás aprendiendo extensiones."`, donde `self` es el valor de la cadena sobre la que se invoca el método.*

*3. Llamada al método:*

- *Finalmente, se crea una instancia de tipo `String`, en este caso `"Estudiante"`, y se llama al método `mensajeDeSalud()`sobre esa instancia.*
- `*"Estudiante".mensajeDeSalud()` invoca el método que implementamos en la extensión de `String`. El valor de `self` es `"Estudiante"`, así que el resultado será:*
    - `*"Hola, Estudiante, estás aprendiendo extensiones."*`
- *El resultado se imprime en la consola con `print`.*

*Resumen:*

- *Este código muestra cómo puedes usar un protocolo en Swift para definir un comportamiento que debe ser implementado por ciertos tipos, y luego usar una extensión para agregar ese comportamiento a un tipo ya existente, como `String`. Esto te permite agregar funcionalidades de manera flexible sin modificar la definición original del tipo `String`.*
</aside>

## ***2.4 Subscripts***

Agregar subscripts adicionales a un tipo.

```swift
extension Array {
    subscript(circular index: Int) -> Element {
        return self[(index % self.count + self.count) % self.count]
    }
}

let numeros = [1, 2, 3, 4, 5]
print(numeros[circular: -1]) // 5
```

<aside>
📎

*Este código puede leerse como:*

*1. Extensión de la clase `Array`*

- `*extension Array {}`: Esto extiende la funcionalidad de los arreglos en Swift (`Array`) sin tener que modificar directamente su implementación original.*
- `*subscript(circular index: Int) -> Element`: Este es un subíndice (o índice) que toma un argumento llamado `index` de tipo `Int` y devuelve un valor del tipo `Element` (el tipo de los elementos dentro del arreglo). La palabra clave `circular` es solo un nombre dado al subíndice, para diferenciarlo de otros subíndices estándar.*

*2. Cálculo del índice "circular"*

- `*self.count`: Obtiene el número de elementos del arreglo (es decir, su longitud).*
- `*index % self.count`: La operación de módulo asegura que cualquier índice esté dentro del rango válido. Si `index`es mayor que el tamaño del arreglo o negativo, el módulo ajusta el índice dentro de los límites del arreglo.*
    - *Si `index` es positivo, el resultado de `index % self.count` será simplemente `index` (siempre que no sea mayor que el tamaño del arreglo).*
    - *Si `index` es negativo, la operación de módulo lo ajustará de tal forma que apunte a un índice correspondiente desde el final del arreglo.*
- `*+ self.count`: Esta suma asegura que si `index` es negativo, la operación de módulo lo "traiga" al rango positivo. Por ejemplo, si `index = -1`, el resultado de `1 % 5` sería `1`, pero al agregar `self.count` (que es 5), se convierte en `4`, lo cual es un índice válido.*
- `*% self.count` (de nuevo): Esta operación asegura que el índice resultante se mantenga dentro del rango de los índices válidos del arreglo. Si el índice es mayor que el número de elementos, lo ajusta para que se envuelva dentro del arreglo (circularmente).*

*3. Ejemplo con un arreglo*

- *El arreglo `numeros` contiene los elementos `[1, 2, 3, 4, 5]`.*
- *Se está intentando acceder al índice `1`. Usando la lógica del subíndice "circular", el índice `1` se convierte en el último índice del arreglo, es decir, `4` (ya que el arreglo tiene 5 elementos, y el índice de su último elemento es `4`).*
- *Resultado: El elemento en el índice `4` del arreglo es `5`. Por lo tanto, el código imprimirá `5`.*

*Resumen*

- *Este código proporciona un mecanismo para acceder a los elementos de un arreglo de forma "circular". Los índices negativos se ajustan automáticamente para que apunten a los elementos correspondientes desde el final del arreglo, permitiendo un acceso flexible sin preocuparse por los límites de los índices.*
</aside>

## ***2.5 Restricciones con Genéricos***

Se puede limitar una extensión a un tipo que cumpla ciertas condiciones.

```swift
extension Collection where Element: Numeric {
    func suma() -> Element {
        return reduce(0, +)
    }
}

let numeros = [1, 2, 3, 4]
print(numeros.suma()) // 10
```

<aside>
📎

*Este código puede leerse como:*

*1. Extensión de `Collection`:*

- *La palabra clave `extension` permite agregar funcionalidades adicionales a un tipo ya existente. En este caso, se está extendiendo el tipo `Collection`, que es un protocolo en Swift que incluye colecciones como arrays, sets y diccionarios.*
- `*where Element: Numeric` es una restricción de tipo que asegura que esta extensión solo se aplicará a colecciones cuyo tipo de elemento (`Element`) sea algo que cumpla con el protocolo `Numeric`. El protocolo `Numeric` incluye tipos como `Int`, `Double`, `Float`, entre otros que permiten realizar operaciones matemáticas.*

*2. Método `suma()`:*

- *Este método `suma()` devuelve un valor del tipo `Element`, que es el tipo de los elementos de la colección.*
- `*reduce(0, +)` es una función que toma dos parámetros:*
    - `*0` es el valor inicial con el que empezamos la operación de reducción (en este caso, el valor neutro para la suma, es decir, cero).*
    - `*+` es la operación que se aplica entre los elementos de la colección. En cada paso de la reducción, el operador `+` suma los elementos de la colección al valor acumulado (que empieza en `0`).*

*3. Uso del código:*

- *Aquí, se crea una colección de tipo `Array` llamada `numeros` con los valores `[1, 2, 3, 4]`.*
- *Luego se llama al método `suma()` sobre esta colección. El método va a sumar todos los elementos del array: `1 + 2 + 3 + 4`, lo que da como resultado `10`, y se imprime este valor.*

*Resumen:*

- *Este código agrega un método `suma()` a todas las colecciones cuyos elementos sean numéricos (`Numeric`), permitiendo calcular la suma de todos los elementos de la colección de manera sencilla utilizando la función `reduce()`. En el ejemplo, el array `[1, 2, 3, 4]` es sumado y el resultado `10` es impreso.*
</aside>

# ***3. Limitaciones de las Extensiones***

- No puedes agregar propiedades almacenadas.
- No puedes sobrescribir métodos o propiedades existentes.

Ejemplo avanzado con delegación y colecciones, Imaginemos que queremos extender `Array` para filtrar elementos únicos:

```swift
extension Array where Element: Hashable {
    func elementosUnicos() -> [Element] {
        var set: Set<Element> = []
        return self.filter { set.insert($0).inserted }
    }
}

let duplicados = [1, 2, 2, 3, 3, 4, 5]
print(duplicados.elementosUnicos()) // [1, 2, 3, 4, 5]
```

<aside>
📎

*Este código puede leerse como:*

*1. Extensión de `Array`:*

- *Esta línea declara una extensión de la clase `Array`. Las extensiones en Swift permiten agregar nuevas funcionalidades a tipos existentes sin modificar su código original. Aquí se especifica que esta extensión solo se aplicará a los arrays cuyo tipo de elementos sea `Hashable`, lo cual garantiza que los elementos del array puedan ser usados dentro de un `Set` (un conjunto, que en Swift no permite duplicados).*

*2. Método `elementosUnicos()`:*

- *Aquí se define la función `elementosUnicos()`, que devuelve un array de los elementos únicos del array original. El tipo de retorno es un array de tipo `Element`, donde `Element` es el tipo de los elementos del array original.*

*3. Uso de un `Set` para eliminar duplicados:*

- *Dentro de la función, se declara un conjunto vacío (`Set<Element>`), llamado `set`. En Swift, un `Set` es una colección no ordenada de elementos únicos. Es decir, no permite duplicados. Este conjunto se usará para llevar un registro de los elementos que ya hemos visto en el array original.*

*4. Filtrado con `filter`:*

- *Este código utiliza el método `filter` de los arrays en Swift. `filter` recorre todos los elementos del array original (`self`hace referencia al array sobre el cual se invoca el método). Para cada elemento, ejecuta el bloque de código dentro de las llaves `{ ... }`.*
    - `*$0` es una forma corta de referirse al elemento actual del array en cada iteración.*
    - `*set.insert($0)` intenta insertar el elemento actual en el conjunto `set`.*
    - `*inserted` es una propiedad de `Set` que indica si el elemento fue insertado con éxito. Si el elemento ya estaba en el conjunto, no se insertará de nuevo, y `inserted` será `false`. Si el elemento no estaba presente, se insertará y `inserted` será `true`.*
- *El `filter` devuelve solo aquellos elementos para los cuales `inserted` es `true`, es decir, aquellos que aún no estaban en el conjunto `set` (es decir, los elementos únicos).*

*5. Uso del código:*

- *Aquí creamos un array llamado `duplicados`, que contiene algunos elementos repetidos. Luego, llamamos a `duplicados.elementosUnicos()`, que aplica la función definida en la extensión y devuelve un nuevo array con solo los elementos únicos: `[1, 2, 3, 4, 5]`. Como se puede ver, los números repetidos (`2` y `3`) son eliminados.*

*Resumen:*

- *El código extiende el tipo `Array` para agregar un método que elimina los elementos duplicados, aprovechando el comportamiento de los `Set`, que no permiten elementos duplicados. Utilizando el método `insert` del conjunto, se asegura de que solo se conserven los elementos únicos del array original.*
- *Este código es una forma eficiente de eliminar duplicados en un array en Swift.*
</aside>

***Conclusión***

Las extensiones son una herramienta clave en Swift que permiten escribir código modular y reutilizable, facilitando la extensión de funcionalidad de tipos existentes sin modificar el código original. Puedes utilizarlas para conformar protocolos, agregar propiedades calculadas, métodos, inicializadores adicionales, y mucho más. ¡Es una característica fundamental para aprovechar Swift al máximo!

---