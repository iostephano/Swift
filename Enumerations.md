# Enumerations

> Modele tipos personalizados que definen una lista de posibles valores.
> 

Los enumerations (o enums) son un tipo de dato que permite definir un grupo de valores relacionados de manera organizada. Los enums en Swift son potentes y flexibles, ya que no solo definen un conjunto de casos, sino que también pueden tener propiedades, métodos y valores asociados.

# ***1. Sintaxis***

```swift
enum DíaSemana {
    case lunes
    case martes
    case miércoles
    case jueves
    case viernes
    case sábado
    case domingo
}

// Tambien puedes declararlo con comas

enum DíaSemana {
    case lunes, martes, miércoles, jueves, viernes, sábado, domingo
}
```

En este ejemplo, `DíaSemana` es un tipo que puede tener uno de los valores definidos (como `lunes`, `martes`, etc.).

```swift
var día: DíaSemana = .lunes
día = .viernes
```

<aside>
📎

*Este código puede leerse como:*

1. `*= .lunes`: Esto asigna el valor `.lunes` a la variable `día`. El prefijo `.` indica que estamos utilizando un valor que pertenece al tipo `DíaSemana`. En este caso, `.lunes` es un caso de la enumeración `DíaSemana`.*
2. `*día = .viernes`: Estamos reasignando un nuevo valor a la variable `día`. En lugar de ser `.lunes`, ahora es `.viernes`. El valor `.viernes` también es uno de los casos posibles dentro de la enumeración `DíaSemana`.*
    
    *En resumen, el código está creando una variable llamada `día` que almacena un valor de tipo `DíaSemana`. Inicialmente, se le asigna el valor `.lunes`, pero luego se cambia a `.viernes`. Este tipo de código es común cuando se trabaja con enumeraciones que definen un conjunto limitado de valores posibles.*
    
</aside>

# ***2. Valores asociados***

Los enums pueden asociar diferentes tipos de datos con cada caso:

```swift
enum Resultado {
    case éxito(mensaje: String)
    case error(código: Int, mensaje: String)
}
```

```swift
let respuesta = Resultado.éxito(mensaje: "Operación completada")
let fallo = Resultado.error(código: 404, mensaje: "No encontrado")

switch respuesta {
case .éxito(let mensaje):
    print("Éxito: \(mensaje)")
case .error(let código, let mensaje):
    print("Error \(código): \(mensaje)")
}
```

<aside>
📎

*Este código puede leerse como:*

1. *Definición de la enum (implícita en el código)*
    
    *Esto define que `Resultado` tiene dos casos:*
    
    - `*éxito`: Que tiene un valor asociado, un `String` llamado `mensaje`.*
    - `*error`: Que tiene dos valores asociados, un `Int` llamado `código` y un `String` llamado `mensaje`.*
2. *Creación de instancias de `Resultado`*
    
    *Aquí, se están creando dos instancias de la `enum` `Resultado`:*
    
    - `*respuesta` es una instancia de `.éxito` con un mensaje "Operación completada".*
    - `*fallo` es una instancia de `.error` con un código de error 404 y un mensaje "No encontrado".*
3. *Uso de `switch` para manejar los casos*
    
    *Se usa una declaración `switch` para evaluar el valor de `respuesta` y manejarlo según su tipo:*
    
    - `*case .éxito(let mensaje)`: Este caso se ejecutará si `respuesta` es de tipo `.éxito`. El valor asociado `mensaje` se extrae y se imprime en consola con el prefijo "Éxito: ".*
    - `*case .error(let código, let mensaje)`: Este caso se ejecutará si `respuesta` es de tipo `.error`. Extrae los valores asociados `código` y `mensaje` y los imprime con el formato "Error (código): (mensaje)".*
    
    *Resumen:*
    
    *Este código utiliza una enumeración para representar dos posibles resultados de una operación (éxito o error), y luego usa un `switch` para manejar ambos casos de manera diferente. Dependiendo de si el resultado es un éxito o un error, el código imprime un mensaje específico con los datos asociados.*
    
</aside>

# *3. Valores por defecto (raw values)*

Los enums también pueden tener valores por defecto, llamados **raw values**, que deben ser del mismo tipo (como `String`, `Int`, etc.)

```swift
enum Moneda: String {
    case dólar = "USD"
    case euro = "EUR"
    case yen = "JPY"
}
```

```swift
let miMoneda = Moneda.euro
print("Código: \(miMoneda.rawValue)") // Código: EUR
```

<aside>
📎

*Este código puede leerse como:*

*Este código define una constante `miMoneda` que almacena un valor del tipo `Moneda`. El valor de `miMoneda` se asigna a `Moneda.euro`, y luego, se imprime su valor crudo (`rawValue`), que en este caso sería "EUR".*

</aside>

# *4. Métodos en enums*

Un enum puede incluir métodos para encapsular lógica específica:

```swift
enum LuzSemáforo {
    case verde, amarillo, rojo

    func descripción() -> String {
        switch self {
        case .verde:
            return "Avanzar"
        case .amarillo:
            return "Precaución"
        case .rojo:
            return "Detenerse"
        }
    }
}
```

```swift
let estado = LuzSemáforo.rojo
print(estado.descripción()) // Detenerse
```

<aside>
📎

*Este código puede leerse como:*

1. *Se define el enumerado llamado `LuzSemáforo`. Un enumerado es un tipo de dato que tiene un conjunto de valores posibles, que en este caso son:*
- `*.verde*`
- `*.amarillo*`
- `*.rojo*`
1. *El método se llama `descripción()` y devuelve un String que indica lo que debería hacer el conductor según el color del semáforo.*
- `*switch self` es una declaración de control que examina el valor actual del enumerado. El valor de `self` es uno de los casos de `LuzSemáforo` (es decir, `.verde`, `.amarillo`, o `.rojo`).*
- *Dependiendo del caso, se devuelve una cadena de texto diferente:*
    - *Si el valor es `.verde`, devuelve `"Avanzar"`.*
    - *Si el valor es `.amarillo`, devuelve `"Precaución"`.*
    - *Si el valor es `.rojo`, devuelve `"Detenerse"`.*
1. *Se crea una constante llamada `estado`, que almacena el valor del enum `LuzSemáforo.rojo`, lo que indica que el semáforo está en color rojo.*
2. *Finalmente, se llama al método `descripción()` sobre el valor de `estado` (que es `LuzSemáforo.rojo`), lo que ejecuta el `switch` dentro de `descripción()` y devuelve la cadena `"Detenerse"`. Luego, se imprime esa cadena en la consola.*

*Resumen:*

*Este código define un enumerado para los colores de un semáforo y un método que devuelve un mensaje apropiado según el color del semáforo. Luego, se crea una variable para representar el color rojo del semáforo y se imprime su descripción, que es `"Detenerse"`.*

</aside>

# ***5. Propiedades calculadas***

Los enums también pueden tener **propiedades calculadas** para proporcionar información adicional.

```swift
enum Figura {
    case círculo(radio: Double)
    case cuadrado(lado: Double)

    var área: Double {
        switch self {
        case .círculo(let radio):
            return .pi * radio * radio
        case .cuadrado(let lado):
            return lado * lado
        }
    }
}
```

```swift
let círculo = Figura.círculo(radio: 5)
print("Área del círculo: \(círculo.área)")
// Área del círculo: 78.53981633974483
```

<aside>
📎

*Este código puede leerse como:*

1. *Definición de la enumeración `Figura`*
- `*enum Figura`: Esto define una enumeración llamada `Figura`. En una enumeración, puedes definir varios casos, que son las diferentes posibilidades de una variable de ese tipo.*
- `*case círculo(radio: Double)`: Este es un caso de la enumeración que representa un círculo. Tiene un valor asociado, que es el `radio` del círculo y es de tipo `Double`.*
- `*case cuadrado(lado: Double)`: Este es otro caso de la enumeración, que representa un cuadrado. Tiene un valor asociado, que es el `lado` del cuadrado y también es de tipo `Double`.*
1. *Propiedad computada `área`*
- `*var área: Double`: Esta es una propiedad computada de la enumeración `Figura`. Es decir, no almacena un valor directamente, sino que lo calcula cuando se accede a ella.*
- `*switch self`: La propiedad `área` depende del tipo de figura en el que esté la instancia de `Figura` (ya sea un círculo o un cuadrado). El `switch` examina el valor actual de `self` (el objeto de la enumeración).*
    - `*case .círculo(let radio)`: Si el caso actual es un círculo, extrae el valor de `radio` y luego calcula el área del círculo usando la fórmula:*
        
        $$
        Área = π × radio²
        $$
        
    - `*case .cuadrado(let lado)`: Si el caso actual es un cuadrado, extrae el valor de `lado` y calcula el área del cuadrado usando la fórmula:*
        
        $$
        Área = lado²
        $$
        
1. *Creación de una instancia de `Figura` y uso de la propiedad `área`*
- `*let círculo = Figura.círculo(radio: 5)`: Aquí se crea una instancia de la enumeración `Figura`, específicamente un `círculo` con un radio de 5 unidades.*
- `*print("Área del círculo: \(círculo.área)")`: Se imprime el área del círculo. Cuando se accede a `círculo.área`, el `switch` en la propiedad computada se activa, calcula el área del círculo (que es π×52=78.54) y lo imprime en la consola.*

$$
Área =  78.53981633974483
$$

***Resumen:***

*Este código define una enumeración `Figura` que puede ser un círculo o un cuadrado, y tiene una propiedad computada `área` que calcula el área dependiendo del tipo de figura. Luego, crea un círculo con radio 5 y muestra su área en la consola.*

</aside>

# ***6. Configuraciones avanzadas***

## ***6.1 Enum con protocolo***

Si deseas recorrer todos los casos de un enum, puedes conformar el protocolo `CaseIterable`:

```swift
enum Fruta: CaseIterable {
    case manzana, naranja, plátano, fresa
}
for fruta in Fruta.allCases {
    print(fruta)
}
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición del Enum `Fruta`*

- `*enum` es una palabra clave en Swift que define un tipo de datos enumerado. Un enum es una forma de agrupar un conjunto de valores relacionados.*
- `*Fruta` es el nombre del enum. En este caso, representa un conjunto de tipos de frutas.*
- *Dentro de las llaves `{}` están los casos posibles del enum: `manzana`, `naranja`, `plátano`, y `fresa`. Estos son los valores posibles que puede tomar una variable de tipo `Fruta`.*
- `*CaseIterable` es un protocolo que permite acceder a todos los casos de un enum de manera automática a través de la propiedad estática `allCases`. Esto es útil para iterar sobre todos los casos del enum, lo que sería difícil de hacer sin esta característica.*
1. *Uso de `allCases` y el Bucle `for`*
- `*Fruta.allCases` es una propiedad estática proporcionada por el protocolo `CaseIterable`. Devuelve un array que contiene todos los casos del enum. En este caso, será un array con los valores `[Fruta.manzana, Fruta.naranja, Fruta.plátano, Fruta.fresa]`.*
- `*for fruta in Fruta.allCases` es un bucle `for-in` que itera sobre cada uno de los casos del enum `Fruta`.*
- *En cada iteración, la variable `fruta` tomará el valor de uno de los casos del enum (por ejemplo, `Fruta.manzana`, luego `Fruta.naranja`, etc.).*
- `*print(fruta)` imprime el valor de `fruta` en cada iteración, mostrando los casos del enum.*

*Resumen:*

- *Se define un enum `Fruta` con 4 casos.*
- *Se utiliza el protocolo `CaseIterable` para permitir acceder a todos los casos del enum.*
- *Luego, se recorre cada caso de `Fruta` con un bucle `for-in` y se imprime cada uno.*

*Este patrón es útil cuando necesitas trabajar con todos los casos de un enum sin tener que escribirlos manualmente.*

</aside>

## ***6.2 Enum con rawValue implícito***

Para `Int` o `String`, los valores por defecto se asignan automáticamente:

```swift
enum Día: Int {
    case lunes = 1, martes, miércoles, jueves, viernes
}

print(Día.martes.rawValue) // 2
```

<aside>
📎

*Este código puede leerse como:*

*1. Declaración de la enumeración `Día`:*

- `*enum Día: Int`: Esto define una enumeración llamada `Día`, y está asociada con el tipo de datos `Int` (es decir, los valores de los casos de la enumeración serán enteros).*
- `*case lunes = 1`: Aquí se está asignando explícitamente el valor `1` al caso `lunes`. Es importante destacar que los casos de la enumeración no necesitan necesariamente tener valores consecutivos o comenzando desde 0.*
- `*martes`, `miércoles`, `jueves`, `viernes`: Los casos siguientes no tienen valores explícitos asignados. En Swift, si no se asigna un valor a un caso dentro de una enumeración basada en `Int`, el valor será automáticamente el siguiente valor entero después del anterior. Por ejemplo:*
    - `*martes` tomará el valor `2` (el siguiente entero después de `1`).*
    - `*miércoles` tomará el valor `3`.*
    - `*jueves` tomará el valor `4`.*
    - `*viernes` tomará el valor `5`.*

*2. Uso de `rawValue`:*

- `*Día.martes`: Aquí estamos accediendo al caso `martes` de la enumeración `Día`.*
- `*rawValue`: `rawValue` es una propiedad de las enumeraciones en Swift cuando están asociadas con tipos de datos primitivos como `Int`. Devuelve el valor entero asociado al caso de la enumeración. En este caso, el valor de `Día.martes`es `2`, ya que en la declaración de la enumeración se asignó automáticamente a `martes` el valor siguiente después de `lunes`, que tiene el valor `1`.*

*Resultado:*

*Cuando se ejecuta el código, el `print` muestra `2`, ya que ese es el valor entero asociado al caso `martes`.*

*Resumen:*

*El código define una enumeración para los días de la semana con valores enteros empezando en 1 para `lunes`. Luego, imprime el valor asociado a `martes`, que es `2`, usando la propiedad `rawValue`.*

</aside>

# **7. Enumeraciones recursivas**

Swift soporta enumeraciones recursivas marcándolas con `indirect`:

```swift
indirect enum Expresión {
    case número(Int)
    case suma(Expresión, Expresión)
    case multiplicación(Expresión, Expresión)
}

let expresión = Expresión.suma(.número(2), .multiplicación(.número(3), .número(4)))
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición de la `enum` `Expresión`*

- `*indirect`: La palabra clave `indirect` es usada en Swift para indicar que los casos recursivos de una enumeración deben almacenarse de manera especial, ya que de lo contrario podrían causar un desbordamiento de pila debido a la recursión. En este caso, se usa porque los casos `suma` y `multiplicación` contienen otros valores de tipo `Expresión`, lo que puede generar una estructura de árbol de expresiones.*
- `*enum Expresión`: La `enum` se utiliza para definir un tipo de datos que puede tomar diferentes formas. En este caso, `Expresión` tiene tres casos posibles:*
    - `*número(Int)`: Un número entero. Este caso guarda un valor de tipo `Int`.*
    - `*suma(Expresión, Expresión)`: Una suma de dos expresiones. Es un caso que toma dos valores de tipo `Expresión`, permitiendo representar una suma de dos operaciones o números.*
    - `*multiplicación(Expresión, Expresión)`: Una multiplicación de dos expresiones, que también toma dos valores de tipo `Expresión`.*

*2. Creación de una expresión*

- `*Expresión.suma`: Está creando una operación de tipo suma. Este caso toma dos operandos, que en este caso son:*
    - *El primer operando es `.número(2)`, que es simplemente el número 2.*
    - *El segundo operando es `Expresión.multiplicación(.número(3), .número(4))`, es decir, una multiplicación de 3 por 4.*

*Entonces, la expresión completa que se está creando es una suma de un número 2 y el resultado de multiplicar 3 por 4.* 

$$
2 + (3 * 4)
$$

*3. ¿Cómo se representaría esta estructura?*

*La estructura interna de esta expresión sería un árbol, donde las operaciones están anidadas. La jerarquía se vería algo así:*

```markdown
    suma
   /    \
número   multiplicación
  |        /    \
  2    número  número
              |      |
              3      4
```

*Esto muestra cómo la enumeración de `Expresión` está diseñada para representar de manera recursiva operaciones matemáticas complejas, como expresiones aritméticas.*

*Resumen*

*Este código crea una expresión aritmética que representa la operación matemática `2 + (3 * 4)`. La enumeración `Expresión` permite representar números y operaciones matemáticas (suma y multiplicación) de manera recursiva.*

</aside>

***Conclusión***

Los enums en Swift son mucho más que listas de valores. Su capacidad para almacenar valores asociados, tener propiedades y métodos, e interactuar con protocolos los convierte en una herramienta poderosa y versátil.

Un uso común de enums es manejar estados en una aplicación:

```swift
enum EstadoCarga {
    case cargando
    case éxito(datos: [String])
    case error(mensaje: String)
}

func manejarEstado(_ estado: EstadoCarga) {
    switch estado {
    case .cargando:
        print("Cargando datos...")
    case .éxito(let datos):
        print("Datos recibidos: \(datos)")
    case .error(let mensaje):
        print("Error: \(mensaje)")
    }
}

let estadoActual = EstadoCarga.éxito(datos: ["Elemento 1", "Elemento 2"])
manejarEstado(estadoActual)
```

---