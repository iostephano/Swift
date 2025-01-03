# Properties

> Acceda a valores almacenados y calculados que forman parte de una instancia o tipo.
> 

Las properties (propiedades) son variables o constantes asociadas a una clase, estructura o enumeración. Estas permiten almacenar valores y definir comportamientos personalizados al acceder o modificar esos valores.

# ***1. Tipos de propiedades***

## ***1.1 Propiedades almacenadas (Stored Properties)***

Son las que almacenan un valor constante o variable como parte de una instancia.

```swift
struct Persona {
    var nombre: String // Variable: puede cambiar.
    let edad: Int       // Constante: no puede cambiar una vez asignada.
}

var persona = Persona(nombre: "Ana", edad: 30)
persona.nombre = "María" // Cambia porque es `var`
// persona.edad = 31      // Error porque es `let`
```

## *1.2 Propiedades calculadas (Computed Properties)*

No almacenan valores directamente, sino que calculan un valor cada vez que se accede a ellas.

```swift
struct Rectangulo {
    var ancho: Double
    var altura: Double
    var area: Double {
        return ancho * altura // Calcula cada vez que se accede.
    }
}

let rectangulo = Rectangulo(ancho: 5, altura: 10)
print(rectangulo.area) // Output: 50.0
```

## ***1.3 Propiedades de clase (Type Properties)***

Pertenecen a la clase o estructura, no a una instancia específica. Se declaran con `static` o `class`.

```swift
class Configuracion {
    static var version = "1.0" // Propiedad estática
}

print(Configuracion.version) // Output: 1.0
```

# ***2. Observadores de propiedades***

Los property observers permiten realizar acciones antes o después de cambiar el valor de una propiedad. Se usan con `willSet` y `didSet`.

```swift
class Contador {
    var valor: Int = 0 {
        willSet {
            print("El valor cambiará a \(newValue)")
        }
        didSet {
            print("El valor cambió de \(oldValue) a \(valor)")
        }
    }
}

let contador = Contador()
contador.valor = 10
// Salida:
// El valor cambiará a 10
// El valor cambió de 0 a 10
```

# ***3. Lazy Properties***

Son propiedades almacenadas cuya inicialización se retrasa hasta que se acceden por primera vez. Se declaran con `lazy`. Útil cuando el valor requiere mucho procesamiento o depende de otros valores.

```swift
class DatosPesados {
    init() {
        print("Cargando datos...")
    }
}

class Gestor {
    lazy var datos = DatosPesados() // Inicialización retrasada
}

let gestor = Gestor() // No se imprime nada
let _ = gestor.datos // Aquí se inicializa "Cargando datos..."
```

**Nota**: Las propiedades `lazy` solo pueden declararse como variables (`var`).

# ***4. Sintaxis con propiedades de acceso personalizado***

Puedes configurar `get` y `set` para propiedades calculadas. Si `set` no se declara, la propiedad será de solo lectura.

```swift
struct Punto {
    private var _x: Double = 0.0
    var x: Double {
        get { _x }
        set { _x = max(0, newValue) } // Solo permite valores positivos
    }
}

var punto = Punto()
punto.x = -10
print(punto.x) // Output: 0
```

# ***5. Métodos y propiedades***

Las propiedades pueden interactuar con métodos para ofrecer más funcionalidad.

```swift
class Contador {
    var cuenta: Int = 0

    func incrementar() {
        cuenta += 1
    }

    func reiniciar() {
        cuenta = 0
    }
}

var miContador = Contador()
miContador.incrementar()
print(miContador.cuenta) // Output: 1
```

# ***6. Modificadores de propiedades***

Los modificadores de acceso en Swift controlan el nivel de visibilidad y accesibilidad de las propiedades, métodos y otros elementos dentro de un programa.

## ***6.1. Private y Public***

Estos modificadores controlan el acceso a las propiedades de una clase, estructura o enumeración.

- `private`: Restringe el acceso a la propiedad o método solo al contexto en el que está declarado. Esto significa que solo se puede acceder desde la misma clase o estructura.
- `public`: Permite el acceso desde cualquier lugar del programa, incluso desde otros módulos (si el módulo está importado). Es la opción más abierta.

```swift
class Persona {
    private var nombre: String = "Oculto" // Solo accesible dentro de la clase.
    public var edad: Int = 0              // Accesible desde cualquier lugar.
}

let p = Persona()
// print(p.nombre) // Error: 'nombre' es privado
print(p.edad)      // Output: 0
```

## ***6.2 Final***

El modificador `final` evita que una propiedad, método o clase sea sobrescrita o heredada.

- Métodos y propiedades `final`: No pueden ser sobrescritos en una subclase.
- Clases `final`: Evitan que sean subclasificadas.

**Ejemplo Método Final**:

```swift
class Vehiculo {
    final func arrancar() {
        print("El vehículo está arrancando.")
    }
}

class Coche: Vehiculo {
    // No es posible sobrescribir el método 'arrancar' porque es 'final'.
    // override func arrancar() { }
}
```

**Ejemplo Clases Final**:

```swift
final class Animal {
    var nombre: String = "Sin nombre"
}

// No se puede heredar de 'Animal' porque es 'final'.
// class Perro: Animal { }
```

## ***6.3 Otros Modificadores de Acceso***

Swift también proporciona otros modificadores para casos específicos:

- `internal` (predeterminado): Hace que las propiedades sean accesibles dentro del mismo módulo, pero no fuera de él.
- `fileprivate`: Restringe el acceso a las propiedades dentro del mismo archivo fuente.
- `open`: Similar a `public`, pero permite que las clases y métodos puedan ser heredados y sobrescritos desde otros módulos.

Ejemplo (Comparativa):

```swift
class Ejemplo {
    private var privado = "Solo dentro de la clase"
    fileprivate var archivoPrivado = "Solo dentro del archivo"
    internal var interno = "Accesible en el módulo"
    public var publico = "Accesible en cualquier lugar"
    open var abierto = "Accesible y heredable desde cualquier lugar"
}
```

***Conclusión***

Elegir el modificador adecuado depende de tus necesidades de encapsulación y seguridad en tu código. En general:

- Usa `private` para propiedades internas o sensibles que no deberían ser accesibles desde el exterior.
- Usa `public` o `open` para elementos que necesitan ser utilizados ampliamente o extendidos en otros módulos.
- Usa `final` cuando quieras evitar modificaciones o subclases no deseadas.

---