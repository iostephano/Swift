# Structures and Classes

> Modele tipos personalizados que encapsulan los datos.
> 

# ***1. Similitudes entre Class y Struct***

- Ambos pueden definir **propiedades** (almacenadas o computadas).
- Pueden contener **métodos** para realizar tareas.
- Pueden usar **inicializadores** para configurar sus valores iniciales.
- Pueden adoptar **protocolos** para definir comportamientos comunes.
- Pueden definir **subíndices** para acceder a valores de forma simplificada.

# ***2. Diferencias clave***

| Característica | `class` | `struct` |
| --- | --- | --- |
| Referencia vs. Valor | Referencia (pointer). Cambios afectan a todas las referencias. | Valor. Se copia cuando se asigna o pasa. |
| Herencia | Permiten herencia. | No soportan herencia. |
| Deinitializers | Tienen `deinit` para liberar recursos. | No tienen `deinit`. |
| Mutabilidad | Mutable solo si se declara como `var` (no depende de si la clase es constante). | Requieren que se declare como `var` y el método debe ser marcado con `mutating`. |

# ***3. Sintaxis de una Class***

```swift
class NombreDeLaClase {
    // Propiedades
    var propiedad1: Tipo
    var propiedad2: Tipo
    
    // Métodos
    func metodo() {
        // Código
    }
    
    // Inicializador (obligatorio si no hay valores predeterminados)
    init(propiedad1: Tipo, propiedad2: Tipo) {
        self.propiedad1 = propiedad1
        self.propiedad2 = propiedad2
    }
    
    // Deinitializador (opcional, solo en clases)
    deinit {
        // Código para liberar recursos
    }
}
```

Las clases son ideales para representar **objetos compartidos o complejos**, como un usuario en una app.

```swift
class Usuario {
    var nombre: String
    var edad: Int
    
    // Inicializador
    init(nombre: String, edad: Int) {
        self.nombre = nombre
        self.edad = edad
    }
    
    // Método
    func saludar() {
        print("Hola, soy \(nombre) y tengo \(edad) años.")
    }
}

// Uso
let usuario1 = Usuario(nombre: "Carlos", edad: 30)
usuario1.saludar()

let usuario2 = usuario1 // Referencia al mismo objeto
usuario2.nombre = "Luis"

print(usuario1.nombre) // Imprime "Luis" (cambio reflejado en ambas referencias)
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición de la clase `Usuario`*

- `*Usuario` es una clase que tiene dos propiedades:*
- `*nombre` (de tipo `String`) para almacenar el nombre de un usuario.*
- `*edad` (de tipo `Int`) para almacenar su edad.*

*2. Inicializador*

- *Este es el inicializador de la clase. Se llama automáticamente cuando se crea un nuevo objeto de la clase `Usuario`.*
- *El uso de `self` es para distinguir las propiedades de la clase (`nombre` y `edad`) de los parámetros del inicializador que tienen el mismo nombre.*
1. *Método*
- *Es un método de la clase `Usuario`.*
- *Imprime un mensaje que incluye las propiedades `nombre` y `edad`.*
1. *Creación de un objeto y uso del método*
- *Se crea un objeto llamado `usuario1` de la clase `Usuario` con los valores `"Carlos"` para el nombre y `30` para la edad.*
- *Al llamar a `usuario1.saludar()`, se imprime: Hola, soy Carlos y tengo 30 años.*
1. *Referencia compartida*
- *Aquí, `usuario2` no es una copia de `usuario1`, sino que ambas variables apuntan al mismo objeto en memoria.*
- *Al cambiar la propiedad `nombre` en `usuario2`, el cambio también se refleja en `usuario1`.*
1. *Impresión final*
- *Como `usuario2` cambió el nombre del objeto, `usuario1` también refleja ese cambio. Por lo tanto, imprime: Luis*
</aside>

# ***4. Sintaxis de una Struct***

```swift
struct NombreDeLaEstructura {
    // Propiedades
    var propiedad1: Tipo
    var propiedad2: Tipo
    
    // Métodos
    func metodoNoMutante() {
        // Código
    }
    
    mutating func metodoMutante() {
        // Código que modifica propiedades
    }
    
    // Inicializador (opcional si usas el inicializador predeterminado)
    init(propiedad1: Tipo, propiedad2: Tipo) {
        self.propiedad1 = propiedad1
        self.propiedad2 = propiedad2
    }
}
```

Las estructuras son ideales para representar **datos inmutables o ligeros**, como un punto en un plano.

```swift
struct Punto {
    var x: Double
    var y: Double
    
    // Método mutante
    mutating func mover(dx: Double, dy: Double) {
        x += dx
        y += dy
    }
}

// Uso
var punto1 = Punto(x: 1.0, y: 2.0)
punto1.mover(dx: 2.0, dy: 3.0)
print("Punto movido: (\(punto1.x), \(punto1.y))") // Imprime "(3.0, 5.0)"

let punto2 = punto1 // Copia el valor, no una referencia
print(punto2.x) // No afecta a punto1
```

<aside>
📎

*Este código puede leerse como:*

1. *Definición de la estructura `Punto`*
- *Aquí se define una estructura llamada `Punto`, que tiene dos propiedades: `x` y `y`, ambas de tipo `Double`. Estas propiedades representan las coordenadas del punto en un sistema de coordenadas 2D.*
1. *Método `mover(dx: dy:)`*
- *El método `mover` toma dos parámetros: `dx` y `dy`, que son los desplazamientos a aplicar a las coordenadas `x` y `y`respectivamente.*
- *La palabra clave `mutating` es crucial aquí. En Swift, las estructuras son tipos de valor, lo que significa que cuando creas una instancia de una estructura y la pasas a una función, se hace una copia de la estructura. El modificador `mutating` le dice a Swift que este método va a cambiar las propiedades de la instancia del tipo `Punto` sobre la que se llama, lo cual no sería posible de forma predeterminada en una estructura.*
- *El método actualiza las coordenadas `x` e `y` sumándoles los valores `dx` y `dy` respectivamente.*
1. *Uso de la estructura y el método*
- *Se crea una instancia de la estructura `Punto` llamada `punto1` con las coordenadas `(1.0, 2.0)`.*
- *Luego, se llama al método `mover(dx:dy:)` en `punto1`, pasando los valores `2.0` y `3.0`. Esto hace que las coordenadas de `punto1` se actualicen a `(3.0, 5.0)` (es decir, `x` se incrementa en 2.0 y `y` en 3.0).*
- *Finalmente, se imprime la nueva posición de `punto1`, que es `(3.0, 5.0)`.*
1. *Copia de la estructura `Punto`*
- *Se crea una nueva constante `punto2` que es una copia del valor de `punto1`. Como `Punto` es un tipo de valor (no una referencia), `punto2` es una copia independiente de `punto1`. Los cambios en `punto2` no afectarán a `punto1` y viceversa.*
- *Se imprime el valor de `punto2.x`, que es `3.0`. Dado que `punto2` es una copia de `punto1`, esta muestra las mismas coordenadas que tenía `punto1` después de moverlo. Sin embargo, si hubieras realizado cambios adicionales en `punto2`, estos no habrían afectado a `punto1`.*

*Resumen:*

- *La estructura `Punto` tiene dos propiedades (`x` y `y`) y un método `mover` que permite cambiar las coordenadas del punto.*
- *El método `mover` es `mutating`, lo que permite modificar las propiedades de la instancia del tipo `Punto`.*
- *Se crea una copia del valor de `punto1` en `punto2`, lo que significa que son independientes y modificar uno no afecta al otro.*
</aside>

# ***5. Cuándo usar Class o Struct***

- Usa `struct`:
    - Cuando los datos no necesitan ser compartidos entre múltiples partes del programa.
    - Para datos livianos, como coordenadas, tamaños o configuraciones.
    - Cuando buscas evitar problemas de concurrencia.
- Usa `class`:
    - Cuando necesitas herencia o un modelo orientado a objetos.
    - Si necesitas compartir referencias entre múltiples partes del programa.
    - Para manejar objetos complejos con ciclos de vida largos.

# ***6. Inicializadores***

En `struct` :

Si no defines un inicializador manual, Swift genera uno automático que usa los nombres de las propiedades.

```swift
struct Persona {
    var nombre: String
    var edad: Int
}

let persona1 = Persona(nombre: "Ana", edad: 25)
```

En `class`:

En clases, **debes** definir un inicializador si las propiedades no tienen valores predeterminados.

```swift
class Persona {
    var nombre: String
    var edad: Int

    init(nombre: String, edad: Int) {
        self.nombre = nombre
        self.edad = edad
    }
}

let persona1 = Persona(nombre: "Luis", edad: 30)
```

# ***7. Uso de herencia en Class***

Solo las clases permiten herencia:

```swift
class Vehiculo {
    var ruedas: Int
    init(ruedas: Int) {
        self.ruedas = ruedas
    }
}

class Carro: Vehiculo {
    var marca: String
    
    init(ruedas: Int, marca: String) {
        self.marca = marca
        super.init(ruedas: ruedas) // Llamada al inicializador de la clase base
    }
}
```

# ***8. Propiedades y Métodos***

Ambos son poderosos y se usan según las necesidades del proyecto. En general, prefiere `struct` por su simplicidad y seguridad, y recurre a `class` solo cuando sea estrictamente necesario.

Propiedades almacenadas:

```swift
struct Rectangulo {
    var largo: Double
    var ancho: Double
}
```

Propiedades computadas:

```swift
struct Rectangulo {
    var largo: Double
    var ancho: Double
    
    var area: Double { // Propiedad calculada
        return largo * ancho
    }
}
```

Métodos:

```swift
struct Contador {
    var valor: Int = 0
    
    mutating func incrementar() {
        valor += 1
    }
}
```

Inicializadores personalizados:

```swift
struct Persona {
    var nombre: String
    var edad: Int
    
    init(nombre: String) {
        self.nombre = nombre
        self.edad = 0 // Por defecto
    }
}
```

---