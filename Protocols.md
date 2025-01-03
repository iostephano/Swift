# Protocols

> Definir los requisitos que deben implementar los tipos de conformidad.
> 

Los protocolos en Swift son una característica poderosa que define un conjunto de requisitos (propiedades, métodos o ambos) que una clase, estructura o enumeración debe implementar. Los protocolos son esenciales para estructurar código reutilizable, flexible y orientado a interfaces.

# ***1. Declaración de un Protocolo***

Un protocolo se declara usando la palabra clave `protocol`.

```swift
protocol Vehiculo {
    var velocidadMaxima: Int { get }
    var tipo: String { get set }
    func describir() -> String
}
```

- `velocidadMaxima` es una propiedad de solo lectura (`get`).
- `tipo` es una propiedad de lectura y escritura (`get set`).
- `describir()` es un método que debe ser implementado por las conformidades.

# ***2. Conformidad a Protocolos***

Las clases, estructuras o enumeraciones que implementen un protocolo deben cumplir todos sus requisitos.

```swift
struct Coche: Vehiculo {
    var velocidadMaxima: Int
    var tipo: String
    
    func describir() -> String {
        return "El \(tipo) alcanza hasta \(velocidadMaxima) km/h."
    }
}

let miCoche = Coche(velocidadMaxima: 200, tipo: "deportivo")
print(miCoche.describir())
// "El deportivo alcanza hasta 200 km/h."

```

<aside>
📎

*Este código puede leerse como:*

*1. Definición de la estructura `Coche`:*

- *Aquí se define una estructura llamada `Coche` que conforma un tipo de dato. Esta estructura adopta el protocolo`Vehiculo`. El protocolo `Vehiculo` podría definir ciertos requisitos (como propiedades o métodos) que deben ser implementados por cualquier tipo que lo adopte. Sin embargo, como no vemos la definición de `Vehiculo` en el código, asumimos que se trata de un protocolo que proporciona ciertas expectativas para las estructuras o clases que lo adoptan.*

*2. Propiedades de la estructura `Coche`:*

- *Dentro de la estructura `Coche`, se definen dos propiedades:*
    - `*velocidadMaxima`: de tipo `Int` (entero), que almacena la velocidad máxima que puede alcanzar el coche.*
    - `*tipo`: de tipo `String`, que describe el tipo de coche (por ejemplo, "deportivo", "sedán", etc.).*

*3. Método `describir()`:*

- *Este es un método dentro de la estructura `Coche`, llamado `describir`. Este método no recibe parámetros y retorna un `String`.*
- *Dentro del cuerpo del método, se usa interpolación de cadenas para construir un mensaje que describa el tipo de coche y su velocidad máxima.*
- `*\(tipo)` inserta el valor de la propiedad `tipo`, y `\(velocidadMaxima)` inserta el valor de la propiedad `velocidadMaxima` en el texto.*

*4. Creación de una instancia de `Coche`:*

- *Aquí se crea una instancia de la estructura `Coche` llamada `miCoche`:*
    - *Se asigna a `velocidadMaxima` el valor `200`, lo que significa que este coche puede alcanzar hasta 200 km/h.*
    - *Se asigna a `tipo` el valor `"deportivo"`, lo que indica que el coche es de tipo deportivo.*

*5. Llamada al método `describir()`:*

- *Finalmente, se llama al método `describir()` sobre la instancia `miCoche`. Este método devuelve una cadena de texto que describe el coche, y luego se imprime el resultado en la consola.*

*Resumen:*

- *La estructura `Coche` adopta un protocolo `Vehiculo` y tiene dos propiedades: `velocidadMaxima` y `tipo`.*
- *Tiene un método `describir()` que devuelve una descripción de las características del coche.*
- *Se crea una instancia de `Coche` con valores específicos para `velocidadMaxima` y `tipo`.*
- *El método `describir()` se llama para obtener una cadena que describe el coche y se imprime en la consola.*
- *Este código ilustra cómo se pueden usar estructuras, protocolos y métodos en Swift para modelar un objeto (en este caso, un coche) y luego interactuar con él.*
</aside>

# *3. Propiedades en Protocolos*

Los protocolos pueden requerir propiedades, que pueden ser de solo lectura (`get`) o de lectura y escritura (`get set`).

```swift
protocol Contador {
    var cuenta: Int { get set }
    var descripcion: String { get }
}
```

# ***4. Métodos en Protocolos***

Los métodos en protocolos no tienen cuerpo; solo se declara su firma.

```swift
protocol Saludable {
    func comer()
    func hacerEjercicio(duracion: Int)
}
```

El protocolo tiene dos métodos:

- `comer()`: Este es un método que no recibe parámetros ni devuelve nada (es un método vacío). Cualquier tipo que adopte el protocolo `Saludable` debe implementar este método y definir cómo debe "comer".
- `hacerEjercicio(duracion: Int)`: Este método tiene un parámetro llamado `duracion`, que es un valor de tipo `Int`. El método también no devuelve ningún valor (es void). Al igual que el método `comer()`, cualquier tipo que adopte el protocolo debe implementar cómo se debe "hacer ejercicio" y utilizar el parámetro `duracion` para especificar cuánto tiempo debe durar el ejercicio.

```swift
class Persona: Saludable {
    func comer() {
        print("Comiendo comida saludable...")
    }
    
    func hacerEjercicio(duracion: Int) {
        print("Ejercitándome por \(duracion) minutos.")
    }
}
```

En este ejemplo, la clase `Persona` adopta el protocolo `Saludable`, lo que obliga a la clase a implementar los métodos `comer()` y `hacerEjercicio(duracion:)` para cumplir con la definición del protocolo.

***Resumen***

- El protocolo `Saludable` define dos métodos (`comer()` y `hacerEjercicio(duracion:)`), pero no proporciona implementaciones concretas.
- Las clases o estructuras que adoptan este protocolo deben proporcionar sus propias implementaciones para esos métodos.
- El protocolo ayuda a garantizar que cualquier tipo que lo adopte tenga la capacidad de "comer" y "hacer ejercicio" de alguna manera.

# ***5. Requisitos Inicializadores***

Los protocolos pueden requerir inicializadores.

```swift
protocol Inicializable {
    init(nombre: String)
}

class Mascota: Inicializable {
    var nombre: String
    
    required init(nombre: String) {
        self.nombre = nombre
    }
}
```

<aside>
📎

*Este código puede leerse como:*

*1. El `protocol Inicializable`:*

- *Un protocolo en Swift define un conjunto de métodos y propiedades que una clase, estructura o enumeración debe implementar para cumplir con ese protocolo. Este protocolo define que cualquier tipo que se conforme a `Inicializable` debe tener un inicializador que acepte un parámetro de tipo `String` (en este caso, un `nombre`).*

*2. La clase `Mascota`:*

- *Ahora, la clase `Mascota` se conforma al protocolo `Inicializable`. Esto significa que debe implementar el inicializador definido por el protocolo, es decir, el inicializador `init(nombre: String)`:*
    - `*var nombre: String`: Declara una propiedad llamada `nombre` de tipo `String`. Esta propiedad almacenará el nombre de la mascota.*
    - `*required init(nombre: String)`: El inicializador es marcado con la palabra clave `required`, lo cual es una característica importante en Swift. Esto significa que todas las subclases de `Mascota` deben implementar este inicializador (si heredan de `Mascota`). Si no estuviera marcado con `required`, solo sería necesario para la clase base, pero la palabra clave asegura que cualquier subclase de `Mascota` también deberá implementarlo.*
    - *El inicializador recibe un argumento de tipo `String` (`nombre`), y dentro de él, asigna el valor de `nombre` a la propiedad `nombre` de la instancia.*

*3. Relación entre el protocolo y la clase:*

- *El protocolo `Inicializable` define que cualquier tipo que lo conforme debe tener un inicializador que acepte un `String`.*
- *La clase `Mascota` se ajusta a este protocolo implementando el inicializador requerido. De esta manera, garantiza que puede ser inicializada con un nombre, como se espera del protocolo.*

*Resumen:*

- *Este código muestra cómo usar un protocolo para definir un contrato de inicialización, y cómo una clase puede adoptar ese contrato e implementarlo. La palabra clave `required` asegura que cualquier subclase también deberá tener el inicializador que recibe un `String`.*
</aside>

# ***6. Extensiones de Protocolos***

Puedes extender protocolos para proporcionar implementaciones predeterminadas para sus métodos o propiedades.

```swift
extension Saludable {
    func hacerEjercicio(duracion: Int) {
        print("Ejercicio predeterminado: \(duracion) minutos.")
    }
}
```

Esto es útil para evitar que todas las conformidades tengan que implementar ciertos métodos.

<aside>
📎

*Este código puede leerse como:*

*1. Extensión*

- *La palabra clave `extension` en Swift se utiliza para agregar funcionalidades adicionales a una clase, estructura o protocolo existente, sin modificar el código original de dicha clase o protocolo.*
- *En este caso, la extensión se está aplicando a algo llamado `Saludable`, que podría ser un protocolo o una clase (en este código no está claro qué es exactamente, pero puede ser cualquiera de las dos).*

*2. Función `hacerEjercicio(duracion:)`*

- *La función `hacerEjercicio(duracion:)` se agrega a `Saludable`. Esta función toma un parámetro de tipo `Int`, que representa la duración del ejercicio en minutos.*
- *Luego, se imprime un mensaje en la consola que indica que se está haciendo un ejercicio, y se muestra la duración en minutos que se pasó como argumento.*
    - `*print("Ejercicio predeterminado: \(duracion) minutos.")` es la forma en que se hace una interpolación de cadenas en Swift, donde el valor de `duracion` se inserta en el texto de la cadena.*
</aside>

# ***7. Delegación***

La delegación es un patrón común donde un protocolo define un conjunto de tareas que un delegado (otra clase o estructura) implementa.

```swift
protocol ProtocoloDelegado {
    func tareaFinalizada()
}

class ClasePrincipal {
    var delegado: ProtocoloDelegado?
    
    func iniciarTarea() {
        print("Tarea en progreso...")
        delegado?.tareaFinalizada()
    }
}

class DelegadoConcreto: ProtocoloDelegado {
    func tareaFinalizada() {
        print("¡Tarea finalizada!")
    }
}

let principal = ClasePrincipal()
let delegado = DelegadoConcreto()
principal.delegado = delegado
principal.iniciarTarea()
// "Tarea en progreso..."
// "¡Tarea finalizada!"
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición del Protocolo (`ProtocoloDelegado`)*

- *Qué es un protocolo: Un protocolo es una especificación que define un conjunto de métodos y propiedades que una clase, estructura o enumeración debe implementar para cumplir con ese protocolo. En este caso, el protocolo `ProtocoloDelegado` exige que cualquier clase que lo adopte implemente el método `tareaFinalizada()`.*
- *Método requerido: Cualquier clase que adopte `ProtocoloDelegado` debe proporcionar una implementación de `tareaFinalizada()`, que no toma parámetros ni devuelve nada (es un método vacío).*

*2. Definición de la clase principal (`ClasePrincipal`)*

- *Propiedad `delegado`:*
    - `*delegado: ProtocoloDelegado?` es una propiedad opcional de tipo `ProtocoloDelegado`. Es decir, `delegado` puede ser una instancia de cualquier clase que haya adoptado el protocolo `ProtocoloDelegado`, pero también puede ser `nil` si no se asigna ningún delegado.*
- *Método `iniciarTarea()`:*
    - *Este método simula que se está llevando a cabo una tarea. Primero, imprime el mensaje `"Tarea en progreso..."`.*
    - *Después, llama al método `tareaFinalizada()` en el delegado. La llamada es opcional (`delegado?.tareaFinalizada()`), lo que significa que solo se ejecutará si `delegado` no es `nil`. Si no se asignó un delegado, este paso no hará nada (por eso se usa el operador `?`).*

*3. Definición de la clase que actúa como delegado (`DelegadoConcreto`)*

- *Adopción del protocolo:*
    - *La clase `DelegadoConcreto` adopta el protocolo `ProtocoloDelegado`, por lo que debe implementar el método `tareaFinalizada()`.*
    - *En este caso, `tareaFinalizada()` simplemente imprime el mensaje `"¡Tarea finalizada!"`.*

*4. Creación de instancias y ejecución del código*

- *Creación de una instancia de `ClasePrincipal`:*
    - `*let principal = ClasePrincipal()` crea un objeto de la clase `ClasePrincipal`. Este objeto tiene una propiedad `delegado` que, en principio, está `nil`.*
- *Creación de una instancia de `DelegadoConcreto`:*
    - `*let delegado = DelegadoConcreto()` crea un objeto de la clase `DelegadoConcreto`, que implementa el protocolo `ProtocoloDelegado`.*
- *Asignación del delegado:*
    - `*principal.delegado = delegado` asigna la instancia de `DelegadoConcreto` al delegado de `ClasePrincipal`. Ahora, cuando se llame al método `tareaFinalizada()`, se ejecutará la implementación de `DelegadoConcreto`.*
- *Llamada al método `iniciarTarea()`:*
    - `*principal.iniciarTarea()` llama al método que inicia la tarea. Esto hace que se imprima el mensaje `"Tarea en progreso..."`, y luego llama al método `tareaFinalizada()` en el delegado, lo que imprimirá `"¡Tarea finalizada!"`.*

*Resumen del flujo*

- *Creación de la clase `ClasePrincipal`: Tiene una propiedad `delegado` que se utiliza para delegar la tarea finalizada.*
- *Creación de la clase `DelegadoConcreto`: Implementa el protocolo `ProtocoloDelegado` y proporciona su propia versión del método `tareaFinalizada()`.*
- *Asignación del delegado: Se asigna una instancia de `DelegadoConcreto` a la propiedad `delegado` de `ClasePrincipal`.*
- *Ejecución del método `iniciarTarea()`: Se imprime `"Tarea en progreso..."`, y luego se invoca `tareaFinalizada()` en el delegado, lo que imprime `"¡Tarea finalizada!"`.*
- *Este patrón de delegación es muy útil para manejar eventos o acciones que deben ser gestionadas por otras clases, sin que la clase principal necesite saber exactamente cómo se manejan esos eventos, simplemente delegando la responsabilidad.*
</aside>

# ***8. Protocolos con Asociated Types***

Los protocolos pueden incluir tipos asociados para ser más genéricos.

```swift
protocol Contenedor {
    associatedtype Item
    func agregar(_ item: Item)
    func obtenerTodos() -> [Item]
}

class Caja<T>: Contenedor {
    private var items: [T] = []
    
    func agregar(_ item: T) {
        items.append(item)
    }
    
    func obtenerTodos() -> [T] {
        return items
    }
}

let caja = Caja<String>()
caja.agregar("Manzana")
print(caja.obtenerTodos()) // ["Manzana"]
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición del `protocol Contenedor`*

- `*protocol Contenedor`: Aquí estamos definiendo un protocolo llamado `Contenedor`. Un protocolo es un conjunto de métodos y propiedades que un tipo (clase, estructura o enumeración) puede adoptar para cumplir con un contrato específico.*
- `*associatedtype Item`: Esta es una característica del protocolo llamada `associatedtype`. La palabra clave `associatedtype` define un tipo genérico que será determinado más tarde por los tipos que adopten el protocolo. En este caso, `Item` será el tipo de los elementos que el contenedor manejará (por ejemplo, `String`, `Int`, etc.).*
- `*func agregar(_ item: Item)`: Este es un método obligatorio que debe ser implementado por cualquier tipo que adopte el protocolo `Contenedor`. El método recibe un elemento de tipo `Item` y no retorna nada (es `void`).*
- `*func obtenerTodos() -> [Item]`: Este es otro método obligatorio que debe ser implementado. Este método debe retornar una lista (`array`) de elementos del tipo `Item`.*

*2. Definición de la clase `Caja`*

- `*class Caja<T>: Contenedor`: Aquí estamos definiendo una clase genérica llamada `Caja`. La clase adopta el protocolo `Contenedor` y tiene un tipo genérico `T`, que reemplazará a `Item` en el protocolo `Contenedor`. Esto significa que, cuando se cree una instancia de `Caja`, el tipo `T` puede ser cualquier tipo, por ejemplo, `String`, `Int`, etc.*
- `*private var items: [T] = []`: Dentro de la clase, declaramos una propiedad privada llamada `items` que es un arreglo de tipo `T`. Este arreglo guardará los elementos que se agreguen a la caja.*
- `*func agregar(_ item: T)`: Este es el método que implementa la función `agregar` del protocolo `Contenedor`. Recibe un elemento de tipo `T` y lo agrega al arreglo `items` usando `append`.*
- `*func obtenerTodos() -> [T]`: Este es el método que implementa la función `obtenerTodos` del protocolo `Contenedor`. Retorna todos los elementos que están almacenados en el arreglo `items` (es decir, un arreglo de tipo `[T]`).*

*3. Creación de una instancia de `Caja` y uso de los métodos*

- `*let caja = Caja<String>()`: Aquí estamos creando una instancia de `Caja` con el tipo `String`. Es decir, `T` se ha sustituido por `String`. Ahora, `Caja` está diseñada para almacenar elementos de tipo `String`.*
- `*caja.agregar("Manzana")`: Usamos el método `agregar` para agregar el elemento `"Manzana"` al contenedor `caja`. Este método toma un `String` y lo añade al arreglo `items` de la caja.*
- `*print(caja.obtenerTodos())`: Finalmente, llamamos al método `obtenerTodos` para obtener todos los elementos dentro de la caja. Como solo hemos agregado `"Manzana"`, se imprimirá el arreglo `["Manzana"]`.*

*Resumen*

- *Este código muestra cómo trabajar con protocolos genéricos en Swift. El protocolo `Contenedor` define los métodos que deben ser implementados por cualquier tipo que lo adopte, mientras que la clase `Caja` adopta este protocolo y lo implementa de manera genérica, permitiendo que el contenedor almacene cualquier tipo de elemento (`T`). En este caso, hemos usado `String`, pero podríamos haber usado cualquier otro tipo.*
</aside>

# ***9. Uso en Colecciones***

Puedes usar protocolos como tipos para colecciones.

```swift
let vehiculos: [Vehiculo] = [
    Coche(velocidadMaxima: 120, tipo: "sedán"),
    Coche(velocidadMaxima: 150, tipo: "SUV")
]

for vehiculo in vehiculos {
    print(vehiculo.describir())
}
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición del arreglo de vehículos*

- `*let vehiculos: [Vehiculo]`: Aquí estamos creando una constante llamada `vehiculos` que contiene un arreglo (`[Vehiculo]`). Este arreglo está compuesto por elementos de tipo `Vehiculo`. Este tipo de datos puede ser una clase, estructura o protocolo.*
- `*Coche(velocidadMaxima: 120, tipo: "sedán")`: Estamos instanciando un objeto de tipo `Coche`. La clase `Coche`tiene un inicializador que requiere dos parámetros: `velocidadMaxima` (un número entero) y `tipo` (un String). En este caso, el primer coche tiene una velocidad máxima de 120 km/h y su tipo es "sedán".*
- `*Coche(velocidadMaxima: 150, tipo: "SUV")`: Aquí estamos creando otro objeto de tipo `Coche`, con una velocidad máxima de 150 km/h y tipo "SUV".*
- *Es importante que la clase `Coche` sea una subclase (o conformante) del tipo `Vehiculo`, ya que estamos creando un arreglo de objetos `Vehiculo`, pero usando instancias específicas de `Coche`.*

*2. Iteración sobre el arreglo de vehículos*

- `*for vehiculo in vehiculos`: Este es un bucle `for-in` que recorre cada elemento del arreglo `vehiculos`. En cada iteración, la variable `vehiculo` tomará el valor de un elemento dentro del arreglo (un objeto de tipo `Coche`, en este caso).*
- `*vehiculo.describir()`: Dentro del bucle, para cada objeto `vehiculo`, se llama al método `describir()`. Este método probablemente pertenece a la clase `Vehiculo` o la clase `Coche`, y su objetivo es devolver una descripción del vehículo. El método `describir()` debe estar implementado en alguna de las clases involucradas, y la llamada a este método genera una salida, que probablemente sea un `String`.*
- `*print(vehiculo.describir())`: Finalmente, el resultado del método `describir()` (que debería ser un `String`) se imprime en la consola.*

*Resumen:*

- *Se crea un arreglo de vehículos (`vehiculos`), compuesto por dos objetos de tipo `Coche` con distintas propiedades (`velocidadMaxima` y `tipo`).*
- *Se itera sobre cada objeto dentro del arreglo `vehiculos`.*
- *En cada iteración, se llama al método `describir()` de cada vehículo y se imprime el resultado.*
</aside>

# ***10. Protocolos Compuestos***

Un tipo puede conformar múltiples protocolos a la vez.

```swift
protocol Volador {
    func volar()
}

protocol Nadador {
    func nadar()
}

struct Superheroe: Volador, Nadador {
    func volar() {
        print("Volando alto.")
    }
    
    func nadar() {
        print("Nadando rápido.")
    }
}
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición de protocolos:*

- *En Swift, un protocolo es un conjunto de métodos y propiedades que pueden ser adoptados por clases, estructuras (structs) o enumeraciones (enums). Los protocolos no implementan los métodos, solo los definen, y cualquier tipo que adopte un protocolo debe implementar esos métodos (si no tiene una implementación predeterminada).*
- *Protocolo `Volador`:*
    - *Aquí defines un protocolo llamado `Volador`. Este protocolo requiere que cualquier tipo que lo adopte implemente el método `volar()`, que no tiene cuerpo (es solo una firma de la función).*
    - `*func volar()` significa que cualquier tipo que adopte el protocolo `Volador` debe tener una función llamada `volar()` que no recibe parámetros y no devuelve nada.*
- *Protocolo `Nadador`:*
    - *De manera similar al protocolo `Volador`, defines otro protocolo llamado `Nadador`. Este protocolo exige que cualquier tipo que lo adopte implemente el método `nadar()`, que también tiene solo la firma, sin cuerpo.*
    - `*func nadar()` significa que cualquier tipo que adopte el protocolo `Nadador` debe implementar una función llamada `nadar()`.*

*2. Definición de la estructura `Superheroe`:*

- *Aquí defines una estructura llamada `Superheroe`, que adopta ambos protocolos: `Volador` y `Nadador`. Esto significa que la estructura `Superheroe` debe implementar todos los métodos que exigen esos protocolos. En este caso, los métodos `volar()` y `nadar()`.*
    - `*Superheroe` adopta el protocolo `Volador` al poner `Volador` después de los dos puntos (`:`) y también adopta el protocolo `Nadador`.*
- *Dentro de la estructura `Superheroe`, implementas ambos métodos:*
    - `*func volar()`: Esta función imprime el mensaje "Volando alto." cuando se llama.*
    - `*func nadar()`: Esta función imprime el mensaje "Nadando rápido." cuando se llama.*

*3. Creación de una instancia de `Superheroe`:*

- *A continuación, podrías crear una instancia de `Superheroe` y llamar a los métodos `volar()` y `nadar()`:*
- *Al llamar a `volar()` en la instancia `heroe`, se ejecuta el código dentro de la función `volar()` definida en `Superheroe`, lo cual imprime "Volando alto.". De manera similar, al llamar a `nadar()`, se imprime "Nadando rápido.".*

*Resumen:*

- *Protocolos (`Volador`, `Nadador`) definen los métodos que cualquier tipo debe implementar.*
- *Estructura `Superheroe` adopta ambos protocolos y proporciona las implementaciones de los métodos `volar()` y `nadar()`.*
- *Puedes crear una instancia de `Superheroe` y llamar a estos métodos, lo que da como resultado las impresiones "Volando alto." y "Nadando rápido.".*
- *Este código es un buen ejemplo de cómo usar protocolos en Swift para garantizar que una estructura (o clase) cumpla con ciertas funcionalidades, en este caso, la habilidad de volar y nadar.*
</aside>

***Resumen***

- Declarar: `protocol NombreProtocolo { ... }`
- Conformidad: `struct/clase NombreClase: NombreProtocolo { ... }`
- Extensiones: `extension NombreProtocolo { ... }`
- Usar como tipo: `var variable: NombreProtocolo`

---