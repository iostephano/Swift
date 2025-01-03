# Inheritance

> Subclase para añadir o anular la funcionalidad.
> 

La herencia (inheritance) en Swift es un principio fundamental de la programación orientada a objetos. Permite que una clase (subclase) herede las propiedades, métodos y otras características de otra clase (superclase). Esto ayuda a reutilizar código y crear estructuras jerárquicas en la programación.

# ***1. Declaración de una superclase y una subclase***

## ***1.1 Superclase***

Es la clase base que define propiedades y métodos que otras clases pueden heredar.

```swift
class Animal {
    var nombre: String
    var edad: Int

    init(nombre: String, edad: Int) {
        self.nombre = nombre
        self.edad = edad
    }

    func hacerSonido() {
        print("El animal hace un sonido.")
    }
}
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición de la clase*

*Se define la clase `Animal` con la palabra clave `class`. Las clases en Swift se usan para crear objetos que pueden tener propiedades y métodos.*

*2. Propiedades de la clase*

*Aquí se declaran dos propiedades (también llamadas atributos) para los objetos de la clase:*

- `*nombre` es una propiedad de tipo `String`, que se usará para almacenar el nombre del animal.*
- `*edad` es una propiedad de tipo `Int`, que almacenará la edad del animal.*

*Ambas propiedades se definen sin un valor inicial en este momento. El valor de cada una se asignará cuando se cree una instancia de la clase.*

*3. El inicializador (`init`)*

- *El inicializador es un método especial que se utiliza para configurar los valores iniciales de las propiedades de la clase cuando se crea un objeto de la clase. En este caso, se define un inicializador que acepta dos parámetros: `nombre` y `edad`, que son del tipo `String` y `Int`, respectivamente.*
- *Dentro del inicializador, usamos la palabra clave `self` para referirnos a las propiedades de la clase y asignarles los valores de los parámetros pasados al inicializador. Esto permite que el objeto tenga un nombre y una edad cuando se cree.*

*4. Método `hacerSonido()`*

- *Este es un método de la clase `Animal` llamado `hacerSonido`. Los métodos son funciones que definen el comportamiento de la clase.*
- *Este método no recibe parámetros y simplemente imprime un mensaje en la consola: `"El animal hace un sonido."`. Este es un comportamiento genérico que podría ser sobrescrito o modificado en clases que hereden de `Animal` (si creas subclases).*

*Resumen:*

*Esta clase define un animal genérico que tiene:*

- *Un nombre y una edad.*
- *Un método `hacerSonido()` que, cuando se invoca, imprime un mensaje indicando que el animal hace un sonido.*
</aside>

## ***1.2 Subclase***

Una subclase hereda de la superclase utilizando el símbolo `:`.

```swift
class Perro: Animal {
    var raza: String

    init(nombre: String, edad: Int, raza: String) {
        self.raza = raza
        super.init(nombre: nombre, edad: edad)
    }

    override func hacerSonido() {
        print("\(nombre) dice: ¡Guau!")
    }

    func correr() {
        print("\(nombre) está corriendo.")
    }
}
```

<aside>
📎

*Este código puede leerse como:*

*Una subclase llamada `Perro`, que hereda de una clase base llamada `Animal`.*

*1. Definición de la clase Perro*

- `*class Perro`: Esto indica que estás creando una nueva clase llamada `Perro`.*
- `*: Animal`: Esto significa que la clase `Perro` hereda de la clase `Animal`, es decir, `Perro` es una subclase de `Animal` y hereda sus propiedades y métodos.*

*2. Propiedad `raza`*

- `*var raza: String`: Aquí defines una propiedad llamada `raza` de tipo `String`. Esto almacenará la raza del perro.*

*3. Inicializador (constructor)*

- `*init(nombre: String, edad: Int, raza: String)`: Este es el inicializador de la clase `Perro`, es decir, un constructor que permite crear instancias de la clase `Perro`. Recibe tres parámetros: `nombre`, `edad` y `raza`, que son los valores que se van a asignar a las propiedades del objeto.*
- `*self.raza = raza`: Asigna el valor del parámetro `raza` a la propiedad `raza` del objeto actual.*
- `*super.init(nombre: nombre, edad: edad)`: Llama al inicializador de la clase base (`Animal`). Esto es necesario para asegurarse de que las propiedades heredadas (como `nombre` y `edad`) sean correctamente inicializadas en la clase base.*

*4. Método `hacerSonido`*

- `*override`: Indica que este método está sobrescribiendo un método que probablemente está definido en la clase base `Animal`. En este caso, el método sobrescrito es `hacerSonido`.*
- `*func hacerSonido()`: Define el método `hacerSonido`, que en este caso imprime un mensaje en la consola indicando que el perro está haciendo su sonido característico.*
- `*print("\(nombre) dice: ¡Guau!")`: Aquí, se utiliza `nombre` (que es una propiedad heredada de `Animal`) para imprimir el nombre del perro y el sonido "¡Guau!".*

*5. Método `correr`*

- `*func correr()`: Este es un método de la clase `Perro` que no está presente en la clase base `Animal`.*
- `*print("\(nombre) está corriendo.")`: Imprime un mensaje en la consola indicando que el perro está corriendo, utilizando la propiedad heredada `nombre` para personalizar el mensaje.*

*Resumen*

*La clase `Perro` hereda de la clase `Animal` y tiene:*

- *Una propiedad adicional `raza` que especifica la raza del perro.*
- *Un inicializador que recibe tres parámetros (`nombre`, `edad`, `raza`) y llama al inicializador de la clase base `Animal`para configurar las propiedades heredadas (`nombre` y `edad`).*
- *Un método sobrescrito `hacerSonido()` que personaliza el sonido que hace el perro (en este caso, "¡Guau!").*
- *Un nuevo método `correr()`, que imprime un mensaje diciendo que el perro está corriendo.*

</aside>

# ***2. Aspectos clave***

- Propiedades heredadas
    
    La subclase hereda todas las propiedades de la superclase y puede usarlas directamente.
    
- Métodos heredados
    
    Los métodos definidos en la superclase están disponibles en la subclase.
    
- Anulación (Override)
    
    Puedes modificar el comportamiento de un método, propiedad o subíndice en la subclase utilizando `override`.
    

```swift
override func hacerSonido() {
    print("Nuevo sonido personalizado.")
}
```

- Uso de `super`
    
    Se utiliza para acceder a propiedades o métodos de la superclase.
    

```swift
super.hacerSonido()
```

- Clases finales
    
    Puedes evitar que una clase sea heredada utilizando `final` antes de `class` .
    

```swift
final class Gato: Animal {
    // Esta clase no puede ser heredada
}
```

***Ventajas y usos de la herencia***

1. Reutilización de código: Evita escribir código duplicado.
2. Organización jerárquica: Permite modelar relaciones de "es un" (`is-a`) de manera natural.
3. Extensibilidad: Permite modificar y extender funcionalidad sin alterar la superclase.

***Consideraciones importantes***

- Swift no permite la herencia múltiple (una subclase solo puede heredar de una superclase).
- Usa herencia solo cuando haya una relación lógica; de lo contrario, considera otros patrones como protocolos o composición.

---