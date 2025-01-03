# Opaque and Boxed Protocol Types

> Ocultar los detalles de la implementación sobre el tipo de un valor.
> 

En Swift, los tipos opacos (opaque types) y los protocolos empaquetados (protocols with associated types o existential types) son conceptos clave para manejar abstracción y polimorfismo de forma eficiente y segura. Veamos en qué se diferencian y cuándo utilizarlos.

# ***1. Tipos Opacos (Opaque Types)***

Un tipo opaco permite ocultar el tipo específico que estás retornando, pero garantiza que el tipo subyacente es consistente. Esto se logra utilizando la palabra clave `some`.

***Características***

- El compilador sabe cuál es el tipo real, pero no lo expone fuera de la función o contexto.
- Los tipos opacos son útiles para mantener detalles internos mientras proporcionan una interfaz común.
- Permiten aprovechar la optimización estática, ya que el tipo subyacente es conocido en tiempo de compilación.

```swift
protocol Shape {
    func area() -> Double
}

struct Circle: Shape {
    var radius: Double
    func area() -> Double {
        return .pi * radius * radius
    }
}

struct Square: Shape {
    var side: Double
    func area() -> Double {
        return side * side
    }
}

// Usamos un tipo opaco para retornar algo que implementa Shape
func createShape(isCircle: Bool) -> some Shape {
    if isCircle {
        return Circle(radius: 5)
    } else {
        return Square(side: 4)
    }
}

let shape = createShape(isCircle: true)
print(shape.area()) // Salida: 78.53981633974483
```

<aside>
📎

*Este código puede leerse como:*

*1. Protocolo `Shape`* 

- *El protocolo `Shape` define una interfaz que debe ser adoptada por cualquier tipo que desee ser considerado una "forma" en el contexto de este código.*
- *El protocolo tiene un método `area()` que devuelve un valor `Double`, que representa el área de la forma. Cualquier tipo que implemente este protocolo debe proporcionar una implementación de este método.*

*2. Estructura `Circle` (Círculo)*

- `*Circle` es una estructura que representa un círculo.*
- *Tiene una propiedad `radius` (radio) que es de tipo `Double`.*
- *La estructura `Circle` adopta el protocolo `Shape` y proporciona su propia implementación del método `area()`, que calcula el área de un círculo usando la fórmula estándar: π×r2, donde `r` es el radio del círculo.*

*3. Estructura `Square` (Cuadrado)*

- `*Square` es una estructura que representa un cuadrado.*
- *Tiene una propiedad `side` (lado) de tipo `Double`.*
- *La estructura `Square` también adopta el protocolo `Shape` y proporciona su propia implementación del método `area()`, que calcula el área de un cuadrado usando la fórmula estándar: lado×lado.*

*4. Función `createShape(isCircle:)`* 

- `*createShape(isCircle:)` es una función que toma un parámetro `isCircle` de tipo `Bool` para determinar qué tipo de forma crear.*
- *Tipo opaco (`some Shape`): La palabra clave `some` indica que la función devolverá un tipo que implementa el protocolo `Shape`, pero sin especificar exactamente cuál es ese tipo. Es decir, el tipo que se devuelve puede ser `Circle` o `Square`, pero la firma de la función solo indica que será algo que cumple con el protocolo `Shape`. El tipo exacto se resuelve en tiempo de ejecución.*
- *Este tipo opaco es útil cuando quieres devolver un valor que se ajusta a un protocolo pero no necesitas (o no quieres) exponer el tipo exacto. La ventaja es que el consumidor de la función no necesita saber si la forma es un círculo o un cuadrado, solo que puede llamar al método `area()` en el objeto devuelto.*

*5. Uso de la función y salida*

- *Aquí, se llama a la función `createShape(isCircle:)` con el argumento `true`, lo que provoca que se cree un objeto `Circle` con un radio de 5.*
- *El método `area()` se llama en el objeto `shape` (que es de tipo opaco `some Shape`). Como `shape` es en realidad un `Circle`, el cálculo del área será el correspondiente al círculo: π×52=78.53981633974483.*

*Resumen*

- *Este código demuestra cómo utilizar protocolos y tipos opacos en Swift para crear una función flexible que devuelve diferentes tipos de objetos (`Circle` o `Square`) que comparten la misma interfaz (`Shape`). La clave aquí es el uso de `some Shape`, que permite que la función `createShape(isCircle:)` devuelva un tipo que se ajusta al protocolo sin exponer el tipo concreto al consumidor de la función.*
- *Protocolo `Shape`: Define la interfaz para las formas.*
- *Tipos opacos: Usados en la función `createShape(isCircle:)` para retornar un tipo que implementa el protocolo sin especificar su tipo exacto.*
- *Áreas: Cada tipo (Círculo y Cuadrado) implementa el cálculo de área de manera diferente, pero ambos cumplen con el protocolo `Shape`.*
- *Este enfoque es útil cuando quieres que tu código sea flexible y puedas cambiar el tipo de la forma sin afectar a otras partes del programa.*
</aside>

# ***2. Protocolos Empaquetados (Boxed Protocol Types o Existential Types)***

Un protocolo empaquetado permite manejar tipos que cumplen con un protocolo, pero el tipo específico subyacente puede variar en tiempo de ejecución.

***Características***

- Puedes usarlo con protocolos que no tienen tipos asociados o requisitos de tipo genéricos.
- No garantiza que el tipo sea consistente.
- Es más flexible pero menos eficiente que los tipos opacos debido al dinamismo.

```swift
protocol Drawable {
    func draw()
}

struct Circle: Drawable {
    var radius: Double
    func draw() {
        print("Dibujando un círculo con radio \(radius)")
    }
}

struct Square: Drawable {
    var side: Double
    func draw() {
        print("Dibujando un cuadrado con lado \(side)")
    }
}

// Usamos un protocolo empaquetado para admitir diferentes tipos que cumplen con Drawable
func display(drawable: Drawable) {
    drawable.draw()
}

let circle = Circle(radius: 5)
let square = Square(side: 4)

display(drawable: circle) // Salida: Dibujando un círculo con radio 5
display(drawable: square) // Salida: Dibujando un cuadrado con lado 4
```

<aside>
📎

*Este código puede leerse como:*

*1. Protocolo `Drawable`*

- *El protocolo `Drawable` define un contrato que cualquier tipo que lo adopte debe cumplir. En este caso, el protocolo requiere que haya un método `draw()` que no reciba parámetros y no devuelva nada (`void`).*
- *Los tipos que implementen este protocolo deberán definir este método `draw()` con su propia lógica de dibujo.*

*2. Estructura `Circle`*

- *La estructura `Circle` tiene una propiedad `radius` que indica el radio del círculo.*
- *Implementa el método `draw()`, que imprime un mensaje con el valor del radio del círculo. Aquí, el valor de `radius`se incluye en la cadena de texto usando interpolación de cadenas: `\(radius)`.*

*3. Estructura `Square`*

- *La estructura `Square` tiene una propiedad `side` que representa la longitud del lado del cuadrado.*
- *Al igual que `Circle`, implementa el método `draw()`, que imprime un mensaje con el valor de `side` usando interpolación de cadenas.*

*4. Función `display(drawable:)`*

- *Esta función acepta un parámetro de tipo `Drawable`, lo que significa que puede recibir cualquier objeto que adopte el protocolo `Drawable` (en este caso, puede ser un `Circle` o un `Square`).*
- *Dentro de la función, llama al método `draw()` del objeto pasado como parámetro. Gracias a que tanto `Circle` como `Square` implementan este método, se invoca la versión correspondiente de `draw()`, según el tipo del objeto.*

*5. Creación de instancias y ejecución*

- *Se crean dos instancias: un `Circle` con radio 5 y un `Square` con lado 4.*
- *Luego, se pasa cada una de estas instancias a la función `display(drawable:)`.*
    - *Cuando se pasa `circle`, se llama a `draw()` de `Circle`, lo que imprime `"Dibujando un círculo con radio 5"`.*
    - *Cuando se pasa `square`, se llama a `draw()` de `Square`, lo que imprime `"Dibujando un cuadrado con lado 4"`.*

*Resumen:*

- *Este código demuestra cómo se pueden usar protocolos en Swift para permitir que diferentes tipos de objetos (como `Circle` y `Square`) implementen una funcionalidad común (el método `draw()`). La función `display` puede manejar objetos de diferentes tipos, pero siempre llama al mismo método `draw()`, sin preocuparse de qué tipo específico de objeto está recibiendo. Esto es un ejemplo básico de polimorfismo, que es uno de los principios fundamentales de la programación orientada a objetos.*
</aside>

# ***3. Diferencias Principales***

| **Característica** | **Tipos Opacos** (`some`) | **Protocolos Empaquetados** |
| --- | --- | --- |
| **Conocimiento del tipo** | Conocido por el compilador, oculto al usuario. | Desconocido por el compilador en tiempo de ejecución. |
| **Consistencia del tipo** | Garantiza el mismo tipo en todas las llamadas. | Puede variar entre diferentes instancias. |
| **Rendimiento** | Más eficiente debido a la optimización estática. | Menos eficiente por la abstracción dinámica. |
| **Flexibilidad** | Menos flexible. | Más flexible. |

***Recomendaciones***

- Usa tipos opacos cuando:
    - Quieres ocultar detalles internos pero mantener consistencia en el tipo retornado.
    - Necesitas alto rendimiento y optimización.
- Usa protocolos empaquetados cuando:
    - Necesitas soportar múltiples tipos que comparten una interfaz común.
    - No puedes usar tipos opacos debido a restricciones en los tipos asociados.

---