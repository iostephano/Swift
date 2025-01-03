# Subscripts

> Determine el tipo de tiempo de ejecución de un valor y déle información de tipo más específica.
> 

Los subscripts permiten acceder a elementos de una colección, lista o secuencia mediante una sintaxis similar a la de los índices de los arreglos. Sin embargo, no están limitados a colecciones: se pueden personalizar para trabajar con cualquier clase, estructura o enumeración.

# ***1. ¿Qué son los Subscripts?***

Un subscript es una forma abreviada de acceder o establecer valores dentro de un tipo. Usan una sintaxis similar a `[ ]` y pueden aceptar uno o más parámetros.

## *1.1 Definición Básica de un Subscript*

Un subscript se declara dentro de una clase, estructura o enumeración usando la palabra clave `subscript`. La sintaxis básica es:

```swift
subscript(index: Tipo) -> TipoDeRetorno {
    get {
        // Código para devolver un valor
    }
    set(nuevoValor) {
        // Código para asignar un valor
    }
}
```

Si solo necesitas leer valores, puedes omitir el `set` y hacer que el subscript sea de solo lectura.

## *1.2 Subscript en una Clase*

Ejemplo: Supongamos que queremos crear una clase que gestione una tabla de multiplicar.

```swift
class TablaDeMultiplicar {
    let factor: Int
    
    init(factor: Int) {
        self.factor = factor
    }
    
    subscript(index: Int) -> Int {
        return factor * index
    }
}

// Uso
let tablaDelTres = TablaDeMultiplicar(factor: 3)
print(tablaDelTres[5])

// Salida: 15 (3 * 5)
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición de la clase*

`*class TablaDeMultiplicar`: Define una nueva clase llamada `TablaDeMultiplicar`.*

`*let factor: Int`: Declara una propiedad `factor` de tipo `Int` (entero). Esta propiedad almacena el número que se utilizará para multiplicar.*

*2. Inicializador (Constructor)*

`*init(factor: Int)`: Este es el inicializador de la clase. Los inicializadores son métodos especiales que se llaman cuando creas una nueva instancia de la clase.*

`*self.factor = factor`: Dentro del inicializador, el parámetro `factor` se asigna a la propiedad `factor` de la clase. La palabra clave `self` se refiere a la instancia actual de la clase.*

*3. Subíndice*

`*subscript(index: Int) -> Int`: Aquí se está definiendo un subíndice. En Swift, un subíndice permite acceder a los elementos de una clase de forma similar a cómo se accede a los elementos de un array o diccionario.*

*El subíndice toma un índice (en este caso un `Int`) como parámetro y devuelve un valor de tipo `Int`.*

`*return factor * index`: El subíndice devuelve el resultado de multiplicar el valor de la propiedad `factor` por el valor de `index`. Esto simula el comportamiento de una tabla de multiplicar, donde puedes pedir el producto del número almacenado (el factor) por cualquier otro número (el índice).*

*4. Uso del código*

`*let tablaDelTres = TablaDeMultiplicar(factor: 3)`: Aquí se crea una nueva instancia de `TablaDeMultiplicar` llamada `tablaDelTres`, con el `factor` establecido en 3. Esto significa que `tablaDelTres`representará la tabla de multiplicar del número 3.*

`*print(tablaDelTres[5])`: Luego, se usa el subíndice para obtener el producto de 3 (el factor) por 5 (el índice), lo que dará como resultado `15` (ya que `3 * 5 = 15`).*

*Salida*

*La salida del programa será `15`, que es el resultado de multiplicar 3 por 5.*

*Resumen:*

*Este código define una clase que simula una tabla de multiplicar, permitiendo calcular el producto de un número (el `factor`) por cualquier otro número que se pase como índice. El subíndice es una característica especial de Swift que permite acceder a los valores de la clase de manera más intuitiva, como si fuera un array.*

</aside>

## *1.3 Subscript en una Estructura*

Los subscripts también pueden ser útiles para acceder a valores personalizados en una estructura:

```swift
struct Matriz {
    let filas: Int, columnas: Int
    private var elementos: [Int]
    
    init(filas: Int, columnas: Int) {
        self.filas = filas
        self.columnas = columnas
        self.elementos = Array(repeating: 0, count: filas * columnas)
    }
    
    subscript(fila: Int, columna: Int) -> Int {
        get {
            return elementos[fila * columnas + columna]
        }
        set {
            elementos[fila * columnas + columna] = newValue
        }
    }
}

// Uso
var matriz = Matriz(filas: 2, columnas: 2)
matriz[0, 1] = 5
print(matriz[0, 1])

// Salida: 5
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición de la estructura `Matriz`:*

`*struct Matriz`: Aquí estamos declarando una estructura llamada `Matriz`.*

`*let filas: Int, columnas: Int`: Estas son dos constantes (`filas` y `columnas`) que definen el tamaño de la matriz. Es decir, cuántas filas y cuántas columnas tiene la matriz.*

`*private var elementos: [Int]`: Esta variable privada es un arreglo unidimensional (`[Int]`) que almacena todos los elementos de la matriz de manera secuencial. Esta propiedad no es accesible directamente desde fuera de la estructura.*

*2. Inicializador (`init`)*

`*init(filas: Int, columnas: Int)`: El inicializador permite crear una instancia de la estructura `Matriz`, tomando el número de filas y columnas como parámetros.*

`*self.filas = filas` y `self.columnas = columnas`: Aquí estamos asignando los valores de `filas` y `columnas` a las propiedades de la estructura.*

`*self.elementos = Array(repeating: 0, count: filas * columnas)`: Inicializa el arreglo `elementos` con ceros. Este arreglo tiene una longitud igual al número total de elementos en la matriz (es decir, el número de filas multiplicado por el número de columnas).*

*3. Subscript:*

*El subscript es una forma especial de permitir el acceso a los elementos de la matriz utilizando una sintaxis similar a la de un arreglo bidimensional. En lugar de escribir `matriz[fila][columna]`, puedes usar `matriz[fila, columna]`.*

`*subscript(fila: Int, columna: Int) -> Int`: Esto define un subíndice que toma dos parámetros (fila y columna) y devuelve un valor entero (`Int`).*

`*get`: Cuando accedes a un elemento de la matriz, el método `get` se ejecuta. Calcula la posición correcta en el arreglo `elementos` usando la fórmula `fila * columnas + columna`, lo que permite obtener el valor de la matriz almacenado en la posición correspondiente.*

`*set`: Cuando asignas un valor a un elemento de la matriz (por ejemplo, `matriz[0, 1] = 5`), el método `set` se ejecuta. Esta fórmula `fila * columnas + columna` determina la posición en el arreglo `elementos` y le asigna el nuevo valor.*

*4. Uso de la estructura `Matriz`:*

`*var matriz = Matriz(filas: 2, columnas: 2)`: Se crea una matriz de 2x2 (2 filas y 2 columnas). Al principio, todos los elementos de la matriz están inicializados en 0.*

`*matriz[0, 1] = 5`: Aquí estamos accediendo a la posición de la matriz en la fila 0 y columna 1 y asignándole el valor 5. Internamente, esto invoca el método `set` del subscript.*

`*print(matriz[0, 1])`: Finalmente, mostramos el valor almacenado en la posición (0, 1) de la matriz, que es 5. Esto invoca el método `get` del subscript.*

*Resumen:*

*Este código crea una estructura que simula una matriz bidimensional utilizando un arreglo unidimensional. Utiliza el subscript para acceder a los elementos de manera más intuitiva, y maneja el acceso y la modificación de los valores de la matriz utilizando una fórmula para convertir las coordenadas bidimensionales a una posición en un arreglo unidimensional.*

</aside>

## *1.4 Subscript de Solo Lectura*

Si no necesitas modificar valores, puedes implementar un subscript de solo lectura.

```swift
struct DiccionarioPersonalizado {
    private var datos: [String: String] = ["Hola": "Hello", "Adiós": "Goodbye"]
    
    subscript(palabra: String) -> String? {
        return datos[palabra]
    }
}

// Uso
let diccionario = DiccionarioPersonalizado()
print(diccionario["Hola"] ?? "No encontrado") // Salida: Hello
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición de la estructura `DiccionarioPersonalizado`:*

*Esto define una estructura llamada `DiccionarioPersonalizado`. Las estructuras en Swift son tipos de datos que pueden contener propiedades y métodos.*

*2. Propiedad privada `datos`:*

*Aquí se declara una propiedad privada llamada `datos`, que es un diccionario (`[String: String]`). En Swift, un diccionario es una colección no ordenada de pares clave-valor. En este caso, las claves y los valores son cadenas (`String`).*

*El diccionario contiene dos pares iniciales:*

- `*"Hola"` es la clave y `"Hello"` es el valor.*
- `*"Adiós"` es la clave y `"Goodbye"` es el valor.*

*La palabra clave `private` significa que esta propiedad solo puede ser accedida dentro de la propia estructura `DiccionarioPersonalizado`. Esto hace que el diccionario interno esté oculto fuera de la estructura.*

*3. Subscript:*

*Aquí se define un subscript, que es una característica de Swift que permite acceder a los elementos de una estructura (o clase) de manera similar a como se accede a los elementos de un array o diccionario en Swift usando corchetes (`[]`).*

`*palabra` es el parámetro de entrada del subscript. Es una cadena (`String`) que representa la clave que estamos buscando en el diccionario.*

*El subscript devuelve un valor de tipo `String?`, lo cual indica que puede devolver un valor de tipo `String` o `nil`. Es decir, si la palabra no se encuentra en el diccionario, el subscript retornará `nil`.*

*Dentro del subscript, `datos[palabra]` busca la palabra en el diccionario `datos` y devuelve el valor asociado a esa clave (si existe). Si la clave no se encuentra, devuelve `nil`.*

*4. Uso de la estructura `DiccionarioPersonalizado`:*

*Aquí se crea una instancia de `DiccionarioPersonalizado` llamada `diccionario`.*

*Luego, se intenta acceder al valor asociado a la clave `"Hola"` usando el subscript: `diccionario["Hola"]`.*

*Si la clave existe en el diccionario, se obtiene el valor asociado (en este caso, `"Hello"`). Si no, el operador de fusión con nil (`??`) proporciona un valor predeterminado (`"No encontrado"`), que se imprimirá si el subscript retorna `nil`.*

*En este caso, dado que `"Hola"` está presente en el diccionario, el resultado será `"Hello"`.*

*Resumen:*

*Este código define una estructura personalizada que simula un diccionario con claves y valores tipo `String`. Se proporciona un subscript que permite acceder a las claves del diccionario de una manera más natural y concisa, como si fuera un diccionario regular. Además, el acceso a los datos está encapsulado, ya que la propiedad `datos` es privada y no accesible directamente desde fuera de la estructura.*

</aside>

# ***2. Usos Comunes***

- Colecciones Personalizadas: Crear clases o estructuras que actúen como arreglos, matrices o diccionarios.
- Acceso Simplificado: Proveer una forma más intuitiva de acceder a datos internos.
- Validación de Datos: Usar lógica para validar y transformar los datos antes de devolverlos o almacenarlos.

---