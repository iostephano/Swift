# Generics

> Escriba código que funcione para múltiples tipos y especifique los requisitos para esos tipos.
> 

Son una característica poderosa que permite escribir código flexible, reutilizable y que trabaja con cualquier tipo, mientras sigue siendo seguro en cuanto a tipos. Se utilizan para evitar duplicación de código, crear colecciones genéricas, definir métodos flexibles, y más. Vamos a explorarlos en detalle con todos los aspectos que mencionaste.

***Los Generics son ideales para:***

- Definir estructuras y funciones reutilizables.
- Manejar tipos de datos de manera segura.
- Reducir duplicación en el código.

# ***1. Sintaxis Básica y Declaración***

Un tipo genérico usa un marcador de tipo (como `T`) que actúa como un comodín que será reemplazado por un tipo específico cuando el código se ejecute.

```swift
func intercambiarValores<T>(a: inout T, b: inout T) {
    let temporal = a
    a = b
    b = temporal
}

// Uso
var x = 10
var y = 20
intercambiarValores(a: &x, b: &y)
print(x, y) // Salida: 20, 10

var str1 = "Hola"
var str2 = "Mundo"
intercambiarValores(a: &str1, b: &str2)
print(str1, str2) // Salida: Mundo, Hola
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición de la función genérica*

- `*func intercambiarValores<T>`: Esta es una función genérica. El tipo `T` es un parámetro de tipo genérico que puede ser cualquier tipo de dato (int, string, custom types, etc.). Esto hace que la función sea reutilizable con cualquier tipo de dato.*
- `*a: inout T, b: inout T`: Los parámetros `a` y `b` son pasados por referencia usando el modificador `inout`. Esto significa que cualquier cambio que hagas dentro de la función en `a` o `b` se reflejará en las variables originales fuera de la función. Es decir, las variables son pasadas por referencia y no por valor.*
- *Cuerpo de la función:*
    - `*let temporal = a`: Se almacena el valor de `a` en la variable `temporal`, para poder usarlo después sin perder el valor original de `a` cuando asignemos a `a` el valor de `b`.*
    - `*a = b`: El valor de `a` es reemplazado por el valor de `b`. Ahora `a` tiene el valor de `b`.*
    - `*b = temporal`: Finalmente, `b` toma el valor original de `a`, que guardamos en la variable `temporal`.*
- *La función, por lo tanto, intercambia los valores de `a` y `b`.*

*2. Uso de la función*

- *Aquí estás usando la función `intercambiarValores` para intercambiar los valores de las variables `x` y `y`.*
- `*&x` y `&y`: En Swift, el prefijo `&` se utiliza para pasar las variables por referencia (en lugar de por valor). Esto permite que la función `intercambiarValores` modifique directamente los valores de `x` y `y`.*
- *Después de llamar a la función, los valores de `x` y `y` se han intercambiado. Por lo tanto, cuando imprimes `x` y `y`, la salida es: 20 10*

*3. Otro ejemplo con cadenas de texto*

- *Aquí haces lo mismo que en el ejemplo anterior, pero con cadenas de texto.*
- `*str1` y `str2` son variables de tipo `String`. Cuando llamas a la función `intercambiarValores`, se intercambian sus valores, y la salida es: Mundo Hola*

*Resumen*

- *La función `intercambiarValores` permite intercambiar los valores de dos variables de cualquier tipo (genérico) que se pase como argumento.*
- *Utiliza el modificador `inout` para permitir que los valores de las variables originales sean modificados dentro de la función.*
- *Los parámetros son pasados por referencia con el operador `&`.*
</aside>

# ***2. Tipos Genéricos***

Puedes declarar clases, estructuras y enumeraciones genéricas.

```swift
struct Caja<T> {
    var valor: T
    
    func mostrarValor() {
        print("El valor es: \(valor)")
    }
}

// Uso
let cajaInt = Caja(valor: 42)
cajaInt.mostrarValor() // Salida: El valor es: 42

let cajaString = Caja(valor: "Swift")
cajaString.mostrarValor() // Salida: El valor es: Swift

```

<aside>
📎

*Este código puede leerse como:*

*1. Definición de la estructura `Caja`*

- `*struct Caja<T>`: Aquí estamos creando una estructura genérica llamada `Caja`. El `T` entre los signos `<` y `>` es un tipo genérico. Esto significa que cuando crees una instancia de la estructura, puedes decidir qué tipo de dato (como `Int`, `String`, `Double`, etc.) usarás para `T`. `T` actúa como un marcador de posición para cualquier tipo de datos que elijas.*
- `*var valor: T`: Dentro de la estructura, tenemos una propiedad llamada `valor`. El tipo de esta propiedad es `T`, lo que significa que `valor` puede ser de cualquier tipo que se pase cuando se cree una instancia de `Caja`. Esto le da flexibilidad, ya que podemos usar diferentes tipos de datos con la misma estructura.*

*2. Definición del método `mostrarValor()`*

- `*func mostrarValor()`: Este es un método que imprime el valor de la propiedad `valor` en la consola. No toma parámetros y simplemente imprime el valor almacenado en la estructura.*
- `*print("El valor es: \(valor)")`: Aquí se utiliza la interpolación de cadenas (`\(valor)`) para insertar el valor de la propiedad `valor` dentro del mensaje impreso en consola. Esto permite mostrar el valor de cualquier tipo de dato que esté almacenado en `valor`.*

*3. Uso de la estructura `Caja`*

- `*let cajaInt = Caja(valor: 42)`: Aquí estamos creando una instancia de `Caja` llamada `cajaInt`. Especificamos que el tipo de la caja es `Int`, ya que pasamos un valor de tipo `Int` (42) como argumento al inicializador.*
- `*cajaInt.mostrarValor()`: Luego llamamos al método `mostrarValor()` en la instancia `cajaInt`, lo cual imprimirá en consola: `El valor es: 42`.*
- `*let cajaString = Caja(valor: "Swift")`: Aquí estamos creando otra instancia de `Caja`, pero esta vez con un valor de tipo `String` (la cadena `"Swift"`).*
- `*cajaString.mostrarValor()`: Al llamar a `mostrarValor()` en esta instancia, se imprimirá en consola: `El valor es: Swift`.*

*Resumen*

- *Este código utiliza una estructura genérica para crear un contenedor flexible que puede almacenar valores de cualquier tipo y luego muestra esos valores. La principal ventaja de usar generics es que puedes reutilizar la misma estructura para diferentes tipos de datos sin tener que duplicar el código.*
</aside>

# ***3. Funciones Genéricas***

Las funciones genéricas son ideales para operaciones repetitivas que trabajan con diferentes tipos.

```swift
func encontrarElemento<T: Equatable>(en array: [T], elemento: T) -> Bool {
    return array.contains(elemento)
}

// Uso
let numeros = [1, 2, 3, 4, 5]
print(encontrarElemento(en: numeros, elemento: 3)) // Salida: true

let palabras = ["manzana", "pera", "naranja"]
print(encontrarElemento(en: palabras, elemento: "limón")) // Salida: false
```

<aside>
📎

*Este código puede leerse como:*

1. *Definición de la función `encontrarElemento`:*
- `*<T: Equatable>`: Aquí `T` es un parámetro genérico. Esto significa que la función puede trabajar con cualquier tipo de datos, pero con una restricción: el tipo `T` debe ser Equatable. Esto significa que los elementos de tipo `T` deben ser comparables usando el operador `==` (igualdad). Esto es necesario para verificar si un elemento está presente en el arreglo.*
- `*en array: [T]`: La función toma como parámetro un arreglo de tipo `T` (es decir, un arreglo de elementos de cualquier tipo que sea Equatable).*
- `*elemento: T`: Este es el segundo parámetro, que representa el elemento que se va a buscar en el arreglo. También es de tipo `T`.*
- `*> Bool`: La función devuelve un valor booleano (`Bool`), que será `true` si el elemento está presente en el arreglo y `false` si no lo está.*
1. *Cuerpo de la función:*
- *La función utiliza el método `contains` del arreglo, que devuelve `true` si el arreglo contiene el `elemento` y `false` en caso contrario. El método `contains` internamente usa el operador `==` para comparar cada elemento del arreglo con el `elemento`proporcionado, por lo que la restricción de que `T` debe ser `Equatable` asegura que la comparación sea válida.*

*Ejemplo de uso:*

- *Aquí, el arreglo `numeros` es de tipo `[Int]`, y se está buscando si el número `3` está presente en el arreglo. Como `3`está en la lista, el resultado es `true`, y eso es lo que se imprime.*
- *En este caso, el arreglo `palabras` es de tipo `[String]`, y se está buscando si la palabra `"limón"` está en el arreglo. Dado que `"limón"` no está presente, el resultado es `false`.*

*Resumen:*

- *La función `encontrarElemento` es genérica y puede trabajar con cualquier tipo de dato que sea Equatable (es decir, que permita comparaciones de igualdad).*
- *Utiliza el método `contains` de los arreglos para verificar si el `elemento` está en el `array`, y devuelve `true` o `false`según corresponda.*
</aside>

# ***4. Restricciones (Requisitos de Tipo)***

Puedes restringir un genérico a un protocolo o clase específica usando `where` o `:`

```swift
func sumarElementos<T: Numeric>(_ a: T, _ b: T) -> T {
    return a + b
}

// Uso
print(sumarElementos(5, 10)) // Salida: 15
print(sumarElementos(3.5, 2.5)) // Salida: 6.0

```

<aside>
📎

*Este código puede leerse como:*

1. *Declaración de la función genérica:*
- `*func sumarElementos`: La palabra clave `func` indica que estamos declarando una función llamada `sumarElementos`.*
- `*<T: Numeric>`: Esta parte indica que la función es genérica, es decir, puede aceptar diferentes tipos de datos, pero el tipo `T` debe cumplir con el protocolo `Numeric`. Esto asegura que `a` y `b` sean números, lo que nos permite realizar operaciones matemáticas como la suma (`+`).*
    - `*T` es un tipo genérico que se ajustará en tiempo de compilación a un tipo específico (por ejemplo, `Int`, `Double`, etc.), pero siempre que ese tipo sea compatible con operaciones numéricas.*
    - `*Numeric` es un protocolo que abarca varios tipos numéricos en Swift, como `Int`, `Double`, `Float`, etc.*
- `*(_ a: T, _ b: T)`: Los parámetros `a` y `b` son de tipo `T`, lo que significa que la función puede aceptar cualquier tipo de datos que sea numérico. Los guiones bajos (`_`) antes de los parámetros indican que no se utilizarán nombres explícitos para los argumentos en la llamada a la función.*
- `*> T`: La función devuelve un valor de tipo `T`, es decir, el mismo tipo que los parámetros de entrada. El tipo de retorno será el resultado de sumar los dos valores.*
1. *Implementación de la función:*
- *En el cuerpo de la función, se realiza la operación de suma entre `a` y `b`, y el resultado se devuelve. La suma `a + b` es válida porque `T` está restringido al protocolo `Numeric`, que garantiza que los valores `a` y `b` puedan ser sumados.*

*Ejemplos de uso:*

- *En el primer ejemplo, se pasa `5` y `10` a la función. Como ambos son de tipo `Int`, el tipo `T` se inferirá como `Int`. La función suma estos valores y devuelve `15`.*
- *En el segundo ejemplo, se pasan `3.5` y `2.5`. Estos valores son de tipo `Double`, por lo que `T` se infiere como `Double` y la función devuelve `6.0` como resultado de la suma.*

*Resumen:*

- *La función `sumarElementos` está diseñada para ser flexible y trabajar con cualquier tipo numérico que se ajuste al protocolo `Numeric`.*
- *El uso de un tipo genérico permite que la función sea reutilizable con distintos tipos, como `Int`, `Double`, etc.*
- *La restricción `T: Numeric` asegura que solo tipos que soporten operaciones matemáticas como la suma puedan ser utilizados.*
</aside>

# ***5. Propiedades y Métodos Genéricos***

Puedes definir propiedades y métodos dentro de clases o estructuras genéricas.

```swift
class Pila<T> {
    private var elementos: [T] = []
    
    func apilar(_ item: T) {
        elementos.append(item)
    }
    
    func desapilar() -> T? {
        return elementos.popLast()
    }
    
    var cima: T? {
        return elementos.last
    }
}

// Uso
var pilaDeEnteros = Pila<Int>()
pilaDeEnteros.apilar(10)
pilaDeEnteros.apilar(20)
print(pilaDeEnteros.cima!) // Salida: 20
print(pilaDeEnteros.desapilar()!) // Salida: 20

```

<aside>
📎

*Este código puede leerse como:*

*1. Declaración de la clase*

- *Aquí se está declarando una clase llamada `Pila` que es genérica, es decir, el tipo de los elementos que almacenará no está predefinido, sino que se define al crear una instancia de la clase. El tipo `T` representa el tipo de los elementos que se almacenarán en la pila. Por ejemplo, si quieres una pila de enteros, usarás `Pila<Int>`, o si quieres una pila de cadenas, usarás `Pila<String>`.*

*2. Propiedad `elementos`*

- *Se define una propiedad privada llamada `elementos`, que es un arreglo (`[T]`), donde `T` es el tipo de los elementos de la pila. Este arreglo almacenará los elementos de la pila.*
- *La palabra clave `private` significa que esta propiedad solo puede ser accedida dentro de la clase, lo que asegura la encapsulación de la implementación interna.*

*3. Método `apilar`*

- *Este es un método público que permite agregar un elemento a la pila.*
- *Recibe un parámetro de tipo `T` (el tipo de los elementos que almacena la pila) y lo agrega al final del arreglo `elementos`utilizando el método `append`.*

*4. Método `desapilar`*

- *Este es otro método público que permite eliminar y devolver el último elemento de la pila (el elemento más recientemente agregado).*
- *Utiliza el método `popLast()` del arreglo `elementos`, que elimina y devuelve el último elemento del arreglo. Si el arreglo está vacío, `popLast()` devuelve `nil`, por eso el tipo de retorno es un `T?` (opcional).*

*5. Propiedad `cima`*

- *La propiedad `cima` devuelve el último elemento de la pila (el que está en la parte superior).*
- *Se utiliza la propiedad `last` del arreglo `elementos`, que devuelve el último elemento del arreglo o `nil` si el arreglo está vacío. Por lo tanto, `cima` es de tipo `T?` (opcional).*

*Uso del código*

- *Se crea una instancia de `Pila` que almacena enteros (`Pila<Int>`), y se le asigna a la variable `pilaDeEnteros`.*
- *Se utiliza el método `apilar` para agregar dos elementos a la pila: el `10` y luego el `20`.*
- *Se imprime el valor de `cima`, que es el último elemento agregado (20).*
- *Luego, se utiliza el método `desapilar` para eliminar y obtener el último elemento (20). Después de esto, el elemento 20 se elimina de la pila.*

*Explicación de la salida*

- `*print(pilaDeEnteros.cima!)`: El operador `!` se utiliza para forzar el desempaquetado del valor opcional. Como la pila tiene un valor en la cima, este código imprime `20`, que es el último elemento apilado.*
- `*print(pilaDeEnteros.desapilar()!)`: Llamar a `desapilar()` elimina el último elemento de la pila (el `20`), y luego lo imprime. Como la pila no está vacía en este punto, el valor de retorno de `desapilar()` es el número `20`, y el operador `!` desempaqueta este valor para imprimirlo.*

*Resumen*

- *Este código muestra una implementación de una pila genérica utilizando un arreglo subyacente para almacenar los elementos. Se proporciona funcionalidad para apilar elementos, desapilar elementos y consultar el elemento en la cima de la pila. Además, se aprovechan las capacidades de Swift para trabajar con tipos genéricos y opcionales, lo que hace que la pila pueda almacenar cualquier tipo de dato y manejar casos donde la pila esté vacía.*
</aside>

# ***6. Extensiones de Genéricos***

Puedes extender tipos genéricos como cualquier otro tipo.

```swift
extension Pila {
    func estaVacia() -> Bool {
        return elementos.isEmpty
    }
}

// Uso
print(pilaDeEnteros.estaVacia()) // Salida: false

```

<aside>
📎

*Este código puede leerse como:*

*1. Definición de la extensión:*

- *Esta línea indica que estás añadiendo nuevas funcionalidades a la estructura o clase `Pila`, sin tener que modificar directamente su código original. Las extensiones en Swift te permiten agregar métodos, propiedades computadas, inicializadores, y más a tipos existentes, como en este caso, `Pila`.*

*2. Método `estaVacia()`:*

- `*func estaVacia() -> Bool`: Aquí defines un nuevo método llamado `estaVacia` que no recibe parámetros y devuelve un valor de tipo `Bool` (un valor de verdadero o falso).*
- `*return elementos.isEmpty`: El método verifica si la propiedad `elementos` de la `Pila` está vacía, usando la propiedad `isEmpty` de las colecciones en Swift. Si `elementos` es una colección (como un arreglo o lista), `isEmpty`devuelve `true` si la colección no tiene elementos, o `false` si tiene al menos un elemento.*
- *Nota: `elementos` es una propiedad interna de la `Pila` que supongo es un arreglo o alguna otra estructura similar que almacena los elementos de la pila.*

*3. Uso del método:*

- *Aquí, se utiliza el método `estaVacia()` en un objeto llamado `pilaDeEnteros` de tipo `Pila`. La salida será `false` si la pila tiene al menos un elemento, y `true` si la pila está vacía.*

*Ejemplo:*

- *Si `pilaDeEnteros` tiene elementos, por ejemplo, `[5, 10, 15]`, el método `estaVacia()` devolverá `false`.*
- *Si la pila estuviera vacía, como `[]`, el método devolvería `true`.*

*Resumen:*

- *El código añade un método `estaVacia()` a la estructura `Pila`, que permite verificar si la pila no tiene elementos. Esto es útil para evitar errores o verificar el estado de la pila antes de realizar operaciones como desapilar un elemento.*
</aside>

# ***7. Delegación con Genéricos***

Puedes usar genéricos al definir protocolos para delegación.

```swift
protocol Proveedor {
    associatedtype Item
    func proveer() -> Item
}

class GeneradorNumerico: Proveedor {
    func proveer() -> Int {
        return Int.random(in: 1...100)
    }
}

let generador = GeneradorNumerico()
print(generador.proveer()) // Salida: Un número aleatorio
```

<aside>
📎

*Este código puede leerse como:*

 *1. Definición del protocolo `Proveedor`:*

- `*protocol`: Los protocolos en Swift son una forma de definir un conjunto de métodos, propiedades o requisitos que una clase, estructura o enumeración debe cumplir. Es similar a una interfaz en otros lenguajes.*
- `*associatedtype Item`: Esta línea define un tipo asociado llamado `Item`. Un tipo asociado permite que el protocolo trabaje con tipos genéricos. Es decir, no se define un tipo específico para el ítem que se proveerá, sino que el tipo será determinado por la clase o estructura que adopte el protocolo.*
- `*func proveer() -> Item`: Este método está declarado en el protocolo. El propósito de este método es proveer un valor de tipo `Item`, que será determinado por la implementación concreta de la clase que adopte el protocolo.*

*2. Clase `GeneradorNumerico`:*

- `*class GeneradorNumerico`: Aquí se define una clase que adopta el protocolo `Proveedor`.*
- `*func proveer() -> Int`: La clase `GeneradorNumerico` implementa el método `proveer` del protocolo. El tipo de retorno es `Int`, lo que significa que esta clase está proveyendo un valor de tipo `Int`. En este caso, el valor es un número aleatorio entre 1 y 100, generado por `Int.random(in: 1...100)`.*

*3. Creación de una instancia y llamada al método `proveer`:*

- `*let generador = GeneradorNumerico()`: Aquí se crea una instancia de la clase `GeneradorNumerico`.*
- `*generador.proveer()`: Se llama al método `proveer` de la instancia `generador`. Dado que `proveer` devuelve un `Int`, se imprimirá un número aleatorio entre 1 y 100.*

*Resumen:*

- *Este código define un protocolo `Proveedor` que tiene un método `proveer` que devuelve un valor de un tipo asociado `Item`. La clase `GeneradorNumerico` adopta este protocolo, implementando el método `proveer` y devolviendo un número aleatorio (`Int`). Al crear una instancia de `GeneradorNumerico` y llamar a `proveer()`, obtenemos un número aleatorio en el rango de 1 a 100.*
- *Este enfoque hace que el código sea flexible y reutilizable para diferentes tipos de generadores que puedan adoptar el protocolo `Proveedor`, y cada uno de esos generadores podría proveer diferentes tipos de valores (por ejemplo, `String`, `Double`, etc.).*
</aside>

# ***8. Colecciones y Genéricos***

Las colecciones como `Array`, `Dictionary` y `Set` son genéricas en Swift. 

- Array<T>: Una colección ordenada de elementos de tipo `T`.
- Dictionary<K, V>: Una colección de pares clave-valor donde `K` es el tipo de clave y `V` el tipo de valor.

```swift
var diccionario: Dictionary<String, Int> = ["Uno": 1, "Dos": 2]
diccionario["Tres"] = 3
print(diccionario) // Salida: ["Uno": 1, "Dos": 2, "Tres": 3]
```

<aside>
📎

*Este código puede leerse como:*

1. *Declaración e inicialización del diccionario:*
- `*var diccionario:` declara una variable llamada `diccionario`. Usamos `var` porque esta es una variable que puede cambiar.*
- `*Dictionary<String, Int>` define que `diccionario` es un diccionario en el que las claves (`key`) son de tipo `String` y los valores (`value`) son de tipo `Int`.*
- `*= ["Uno": 1, "Dos": 2]` inicializa el diccionario con dos pares clave-valor: `"Uno": 1` y `"Dos": 2`.*
1. *Añadir un nuevo par clave-valor:*
- *Aquí, se está agregando un nuevo par clave-valor al diccionario:*
    - *La clave es `"Tres"`.*
    - *El valor correspondiente es `3`.*
- *Este código modifica el diccionario, añadiendo la entrada `["Tres": 3]`. El diccionario ahora tiene tres elementos:*
1. *Imprimir el diccionario:*
- *La función `print(diccionario)` imprime el contenido del diccionario en la consola.*

*Resumen:*

- *Se crea un diccionario con claves de tipo `String` y valores de tipo `Int`.*
- *Se añaden elementos al diccionario usando la sintaxis de corchetes (`diccionario["clave"] = valor`).*
- *Finalmente, se imprime el diccionario para ver el resultado.*
</aside>

# ***9. Valores Predeterminados en Genéricos***

Puedes usar inicializadores o valores predeterminados en tus genéricos.

```swift
struct Contenedor<T> {
    var valor: T?
    
    init(valorInicial: T? = nil) {
        self.valor = valorInicial
    }
}

let contenedorVacio = Contenedor<Int>()
let contenedorLleno = Contenedor(valorInicial: 42)
print(contenedorVacio.valor) // Salida: nil
print(contenedorLleno.valor!) // Salida: 42
```

<aside>
📎

*Este código puede leerse como:*

1. Definición de la estructura `Contenedor`
- `struct Contenedor<T>`:
    - Aquí estamos declarando una estructura genérica llamada `Contenedor`. El tipo de datos que almacenará dentro de esta estructura es `T`, un tipo genérico que será especificado cuando creemos una instancia de `Contenedor`. Este tipo `T` puede ser cualquier tipo, como `Int`, `String`, `Double`, etc.
    - El tipo `T` es genérico, lo que significa que la estructura `Contenedor` puede adaptarse a diferentes tipos de datos.
- `var valor: T?`:
    - Dentro de la estructura, tenemos una propiedad llamada `valor` de tipo `T?`, que es un valor opcional. Esto significa que el `valor` puede ser de tipo `T` o puede ser `nil` (es decir, que no contenga ningún valor).
    - El signo de interrogación (`?`) indica que esta propiedad es opcional.
- `init(valorInicial: T? = nil)`:
    - La estructura `Contenedor` tiene un inicializador llamado `init`, que permite establecer el valor de la propiedad `valor` cuando creamos una instancia de la estructura.
    - El parámetro `valorInicial` es opcional (ya que tiene un valor predeterminado de `nil`), lo que significa que si no se proporciona ningún valor al crear la instancia de `Contenedor`, la propiedad `valor` será `nil` por defecto.
    - Si se proporciona un valor para `valorInicial`, entonces `valor` se inicializa con ese valor.
1. Creación de instancias
2. **`let contenedorVacio = Contenedor<Int>()`**:
    - Aquí creamos una instancia de `Contenedor`, donde el tipo genérico `T` es `Int`. Dado que no proporcionamos ningún valor para `valorInicial`, la propiedad `valor` de esta instancia será `nil` por defecto (porque `valorInicial` tiene un valor predeterminado de `nil` en el inicializador).
    - Entonces, `contenedorVacio.valor` es `nil`.
3. **`let contenedorLleno = Contenedor(valorInicial: 42)`**:
    - En esta línea, también estamos creando una instancia de `Contenedor` con el tipo `Int`. Pero esta vez, le pasamos el valor `42` como `valorInicial`, por lo que la propiedad `valor` se inicializa con `42` en lugar de `nil`.

**3**. Imprimir los valores

1. `print(contenedorVacio.valor)`:
    - En este caso, el valor de `contenedorVacio.valor` es `nil`, porque no se proporcionó un valor inicial cuando se creó la instancia `contenedorVacio`.
    - Por lo tanto, la salida será `nil`.
2. `print(contenedorLleno.valor!)`:
    - Aquí, `contenedorLleno.valor` es `42`, ya que se pasó ese valor en el inicializador.
    - El operador `!` se utiliza para deshacer el opcional y obtener el valor no opcional. Esto es seguro en este caso, ya que sabemos que `valor` no es `nil` en `contenedorLleno` (está inicializado con `42`).
    - La salida será `42`.

Resumen:

- La estructura `Contenedor` es genérica y puede almacenar un valor de cualquier tipo (`T`), que puede ser opcional (`T?`).
- Puedes inicializar la estructura con un valor opcional o dejarla vacía (sin valor, `nil`).
- Dependiendo de cómo se inicialice, el valor dentro del contenedor puede ser `nil` o algún valor del tipo `T`.
</aside>

# ***10. Uso Avanzado: Protocolo con Genéricos***

Puedes usar protocolos para definir estructuras más flexibles.

```swift
protocol Proceso {
    associatedtype Elemento
    func ejecutar(con elemento: Elemento)
}

class ImprimirProceso: Proceso {
    func ejecutar(con elemento: String) {
        print("Procesando: \(elemento)")
    }
}

let proceso = ImprimirProceso()
proceso.ejecutar(con: "Swift Generics") // Salida: Procesando: Swift Generics

```

<aside>
📎

*Este código puede leerse como:*

1. *Definición del protocolo `Proceso`*
- `*protocol Proceso`: Esto define un protocolo llamado `Proceso`. Un protocolo en Swift define un conjunto de métodos y propiedades que una clase, estructura o enumeración debe implementar para cumplir con ese protocolo.*
- `*associatedtype Elemento`: Aquí se usa un tipo asociado. El `associatedtype` es un marcador de posición para un tipo que será determinado más adelante, cuando una clase o estructura que adopte este protocolo lo implemente. Es una forma de hacer que el protocolo sea genérico.*
    
    *En este caso, `Elemento` es un tipo asociado, lo que significa que el tipo concreto de `Elemento` será especificado más tarde cuando un tipo real (como una clase o estructura) adopte este protocolo.*
    
- `*func ejecutar(con elemento: Elemento)`: Este es el método que debe implementar cualquier tipo que adopte el protocolo `Proceso`. La función `ejecutar` toma un parámetro llamado `elemento` de tipo `Elemento`, que es el tipo asociado en este caso. Al ser un protocolo, no define lo que hace `ejecutar`, solo su firma, y serán las clases o estructuras que adopten el protocolo las que proporcionen la implementación concreta.*

*2. Definición de la clase `ImprimirProceso`*

- `*class ImprimirProceso: Proceso`: Aquí, se define una clase llamada `ImprimirProceso` que adopta el protocolo `Proceso`.*
    
    *En otras palabras, esta clase se compromete a implementar el protocolo `Proceso`. Al ser una clase, puede ser instanciada y utilizada más adelante.*
    
- `*func ejecutar(con elemento: String)`: En la clase `ImprimirProceso`, el tipo asociado `Elemento` del protocolo `Proceso` se ha definido como `String`, lo que significa que la función `ejecutar` espera un parámetro de tipo `String`. La implementación de la función `ejecutar` simplemente imprime el texto `"Procesando: "` seguido del valor de `elemento`.*

*3. Uso del `ImprimirProceso`*

- `*let proceso = ImprimirProceso()`: Se crea una instancia de la clase `ImprimirProceso`, llamada `proceso`. Dado que `ImprimirProceso` cumple con el protocolo `Proceso` y proporciona una implementación para el método `ejecutar`, ahora se puede usar esta instancia para invocar `ejecutar`.*
- `*proceso.ejecutar(con: "Swift Generics")`: Finalmente, se llama al método `ejecutar` de la instancia `proceso`, pasando el valor `"Swift Generics"` como argumento. Esto produce la salida: Procesando: Swift Generics*

*Resumen*

- *Este código muestra cómo crear un protocolo con un tipo asociado (en este caso, `Elemento`), cómo una clase puede adoptar ese protocolo y proporcionar una implementación concreta para el método definido en el protocolo, y cómo finalmente usar una instancia de esa clase. El uso de generics y protocolos permite crear código más flexible y reutilizable.*
- *En este ejemplo, el protocolo `Proceso` puede ser adoptado por otras clases con diferentes tipos de `Elemento`, lo que hace que el código sea aún más general y reutilizable. Por ejemplo, podrías crear otra clase que implemente el protocolo `Proceso` pero con un tipo distinto para `Elemento`, como `Int`, y así poder procesar enteros de manera similar.*
</aside>

---