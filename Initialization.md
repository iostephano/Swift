# Initialization

> Establezca los valores iniciales para las propiedades almacenadas de un tipo y realice una configuración única.
> 

En Swift, Initialization es el proceso de configurar un objeto, estructura o enumeración para que esté listo para su uso. Esto se hace mediante inicializadores (constructores), que son funciones especiales llamadas al crear una instancia de una clase, estructura o enumeración.

# *1. Características principales*

- Los inicializadores aseguran que todas las propiedades de la instancia tengan un valor inicial válido.
- Swift no requiere que uses un inicializador explícito si todas las propiedades tienen valores predeterminados.

# ***2. Tipos de inicializadores***

1. Inicializador por defecto: Se genera automáticamente si todas las propiedades tienen valores iniciales.
2. Inicializador designado: Define un inicializador personalizado que inicializa todas las propiedades necesarias.
3. Inicializador de conveniencia (solo en clases): Un inicializador secundario que delega la inicialización a otro inicializador designado.
4. Failable initializer (`init?`): Permite devolver `nil` si la inicialización falla.

## *2.1 Inicializador por defecto con estructuras*

```swift
struct Persona {
    var nombre: String
    var edad: Int
}

let persona = Persona(nombre: "Luis", edad: 25) // Se usa el inicializador generado automáticamente.
print(persona.nombre) // Luis
```

## *2.2 Inicializador personalizado*

Puedes definir un inicializador para asignar valores iniciales o aplicar lógica.

```swift
struct Rectangulo {
    var ancho: Double
    var alto: Double

    // Inicializador personalizado
    init(ancho: Double, alto: Double) {
        self.ancho = ancho
        self.alto = alto
    }

    // Método para calcular el área
    func calcularArea() -> Double {
        return ancho * alto
    }
}

let rectangulo = Rectangulo(ancho: 10, alto: 5)
print(rectangulo.calcularArea()) // 50.0
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición de la estructura:*

`*struct`: En Swift, las estructuras (`struct`) son tipos de datos que pueden contener propiedades y métodos. En este caso, la estructura se llama `Rectangulo` y tiene propiedades y métodos relacionados con un rectángulo.*

*2. Propiedades de la estructura:*

`*var`: Define dos propiedades variables, `ancho` y `alto`, de tipo `Double`. Esto significa que estas propiedades pueden cambiar de valor durante la vida del objeto.*

`*ancho` y `alto` son las dimensiones del rectángulo y están representadas como números de punto flotante (`Double`).*

*3. Inicializador personalizado:*

`*init`: Es el inicializador de la estructura. Es un método especial que se ejecuta cuando se crea una nueva instancia de `Rectangulo`. El inicializador toma dos parámetros: `ancho` y `alto`, que son los valores que se usarán para inicializar las propiedades de la estructura.*

`*self`: Se refiere a la instancia actual del objeto (en este caso, el objeto de tipo `Rectangulo`). Usamos `self.ancho` y `self.alto` para referirnos a las propiedades de la estructura, y `ancho` y `alto` son los parámetros que se pasan al inicializador. Esta distinción es necesaria porque los nombres de las propiedades y los parámetros coinciden.*

*4. Método para calcular el área:*

`*func`: Define un método llamado `calcularArea` dentro de la estructura `Rectangulo`.*

`*calcularArea() -> Double`: El método no toma parámetros (solo usa las propiedades de la estructura) y devuelve un valor de tipo `Double` que representa el área del rectángulo.*

`*return ancho * alto`: El método calcula el área multiplicando `ancho` por `alto`, y luego devuelve este valor.*

*5. Creación de una instancia y llamada al método:*

`*let rectangulo`: Aquí creamos una constante llamada `rectangulo`, que es una instancia de la estructura `Rectangulo`.*

`*Rectangulo(ancho: 10, alto: 5)`: Esto llama al inicializador personalizado de la estructura, creando un nuevo `Rectangulo` con un `ancho` de 10 y un `alto` de 5.*

*6. Impresión del resultado:*

`*rectangulo.calcularArea()`: Llamamos al método `calcularArea()` sobre la instancia `rectangulo`. Este método devuelve el área del rectángulo, que es 10 * 5 = 50.*

`*print(...)`: Muestra en consola el resultado del cálculo, es decir, `50.0`.*

*Resumen:*

*Este código define una estructura `Rectangulo` que tiene dos propiedades (`ancho` y `alto`), un inicializador personalizado para configurar esas propiedades, y un método para calcular el área del rectángulo. Luego, crea un rectángulo con dimensiones específicas, calcula su área y la imprime en consola.*

</aside>

## *2.3 Inicializadores de conveniencia*

```swift
class Vehiculo {
    var ruedas: Int
    var color: String

    // Inicializador designado
    init(ruedas: Int, color: String) {
        self.ruedas = ruedas
        self.color = color
    }

    // Inicializador de conveniencia
    convenience init(color: String) {
        self.init(ruedas: 4, color: color)
    }
}

let carro = Vehiculo(color: "Rojo") // Usa el inicializador de conveniencia
print(carro.ruedas) // 4
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición de la clase `Vehiculo`*

`*class Vehiculo`: Aquí se define una clase llamada `Vehiculo`. Una clase es como un plano o plantilla para crear objetos (instancias). En este caso, `Vehiculo` representa un vehículo con ciertas características.*

*Propiedades:*

- `*ruedas: Int`: Una propiedad llamada `ruedas` que es de tipo `Int`, es decir, un número entero que guarda la cantidad de ruedas del vehículo.*
- `*color: String`: Otra propiedad llamada `color`, de tipo `String`, que almacenará el color del vehículo.*

*2. Inicializador designado*

`*init(ruedas: Int, color: String)`: Este es el inicializador designado de la clase `Vehiculo`. Los inicializadores son métodos especiales que se usan para configurar el objeto cuando se crea. Este inicializador permite crear un objeto `Vehiculo` con un número de ruedas y un color específicos.*

- `*self.ruedas = ruedas`: Asigna el valor de la propiedad `ruedas` del objeto a la variable que se pasa como argumento al inicializador.*
- `*self.color = color`: Asigna el valor de la propiedad `color` del objeto al argumento `color`.*

*Este inicializador es designado porque es el inicializador principal y es el responsable de asignar todos los valores iniciales de las propiedades del objeto.*

*3. Inicializador de conveniencia*

`*convenience init(color: String)`: Este es un inicializador de conveniencia. Los inicializadores de conveniencia son inicializadores adicionales que no son necesarios para crear un objeto, pero pueden simplificar la creación de instancias en situaciones comunes.*

- `*self.init(ruedas: 4, color: color)`: Este inicializador de conveniencia llama al inicializador designado (`init(ruedas: Int, color: String)`) y le pasa un valor predeterminado de `4` para las ruedas y el valor recibido para color.*

*En este caso, si no se especifica el número de ruedas al crear un objeto de tipo `Vehiculo`, este inicializador de conveniencia asume que el vehículo tiene 4 ruedas.*

*4. Crear una instancia de `Vehiculo`*

*Este código crea una nueva instancia de la clase `Vehiculo` usando el inicializador de conveniencia.*

*El valor `"Rojo"` se pasa como argumento para el color del vehículo.*

*Como se está usando el inicializador de conveniencia, el número de ruedas se establece automáticamente en 4(como se definió en el inicializador de conveniencia).*

*5. Imprimir las propiedades del objeto*

*Aquí, se imprime el valor de la propiedad `ruedas` del objeto `carro`. Como se usó el inicializador de conveniencia, el número de ruedas es 4, y eso es lo que se imprime.*

*Resumen de lo que hace el código:*

*Define una clase `Vehiculo` con dos propiedades: `ruedas` y `color`.*

*La clase tiene dos inicializadores:*

- *El inicializador designado acepta ambos parámetros (`ruedas` y `color`) para crear un vehículo con los valores que se pasen.*
- *El inicializador de conveniencia solo acepta un parámetro (`color`), y establece automáticamente `4` para las ruedas.*

*Crea una instancia de `Vehiculo` llamada `carro`, usando el inicializador de conveniencia con el color `"Rojo"`, y luego imprime el número de ruedas, que es 4.*

*Este patrón es útil cuando quieres ofrecer formas más convenientes o simplificadas de crear instancias de una clase, sin requerir que el usuario siempre pase todos los parámetros posibles.*

</aside>

## *2.4 Failable Initializer*

```swift
struct Producto {
    var nombre: String
    var precio: Double

    init?(nombre: String, precio: Double) {
        if precio < 0 {
            return nil // Falla la inicialización si el precio es negativo.
        }
        self.nombre = nombre
        self.precio = precio
    }
}

if let producto = Producto(nombre: "Laptop", precio: -1000) {
    print("Producto creado: \(producto.nombre)")
} else {
    print("Error al crear el producto.") // Este será el resultado.
}
```

<aside>
📎

*Este código puede leerse como:*

1. *Definición de la estructura `Producto`*

*Aquí definimos la estructura `Producto`, que tiene dos propiedades:*

- `*nombre`: una cadena de texto (`String`).*
- `*precio`: un número de punto flotante de doble precisión (`Double`), que representará el costo del producto.*

*2. Inicializador con failable initialization*

*El inicializador `init?` es un inicializador failable. Esto significa que puede fallar y devolver `nil` si no puede inicializar correctamente un objeto.*

*En este caso, si el `precio` es negativo (lo cual no tiene sentido en este contexto), el inicializador devuelve `nil` y la inicialización falla. Esto previene la creación de un `Producto` con un precio no válido.*

*Si el precio es positivo o cero, el inicializador asigna el valor de `nombre` y `precio` a las propiedades correspondientes de la estructura.*

*3. Usando el inicializador para crear un producto*

*Aquí estamos intentando crear un `Producto` con el nombre "Laptop" y un precio de `1000`.*

*Debido a que el precio es negativo, el inicializador failable devolverá `nil`, y el bloque dentro del `if let` no se ejecutará.*

*En lugar de eso, el `else` se ejecutará, imprimiendo `"Error al crear el producto."`.*

*Resultado*

*Como el precio es negativo, el inicializador fallará y el programa imprimirá: Error al crear el producto.*

*Resumen*

*Se define una estructura `Producto` con propiedades `nombre` y `precio`.*

*Se crea un inicializador failable que devuelve `nil` si el precio es negativo.*

*Se intenta crear un `Producto` con un precio negativo, lo que causa que la inicialización falle y el mensaje de error se imprima.*

*Este código muestra cómo manejar inicializaciones que podrían fallar debido a condiciones lógicas, como en este caso, un precio inválido.*

</aside>

***Resumen:***

- Los inicializadores permiten controlar cómo se crean las instancias.
- Puedes personalizar la lógica inicial para validar datos o establecer configuraciones específicas.
- Las clases pueden tener inicializadores adicionales como los de conveniencia, mientras que estructuras y enumeraciones se limitan a inicializadores básicos.

---