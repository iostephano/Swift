# Deinitialization

> Libere recursos que requieran limpieza personalizada.
> 

En Swift, Deinitialization es el proceso que ocurre cuando una instancia de una clase se elimina de la memoria. Esto se logra a través de un método especial llamado `deinit`. Este método se invoca automáticamente justo antes de que el sistema libere los recursos asociados con la instancia, permitiéndote realizar tareas de limpieza, como cerrar conexiones, liberar memoria manualmente asignada, o limpiar datos temporales.

# *1. Características clave de DEINIT*

1. Solo para clases: Los métodos de inicialización/desinicialización solo se aplican a clases, no a estructuras o enumeraciones.
2. Automático: El sistema lo invoca automáticamente; no se llama explícitamente.
3. No acepta parámetros: No puedes pasar valores al método `deinit`.

Ejemplo básico de `deinit`

```swift
class MyClass {
    var name: String
    
    init(name: String) {
        self.name = name
        print("\(name) ha sido inicializado.")
    }
    
    deinit {
        print("\(name) ha sido desinicializado.")
    }
}

// Crear y destruir instancias
if true {
    let objeto = MyClass(name: "Objeto1")
    // Al finalizar el bloque, la instancia será destruida
}
print("Fin del programa.")

// Objeto1 ha sido inicializado.
// Objeto1 ha sido desinicializado.
// Fin del programa.
```

<aside>
📎

*Este código puede leerse como:*

1. *Definición de la clase `MyClass`:*
    - *La clase tiene una propiedad llamada `name` de tipo `String`.*
    - *Hay dos métodos especiales:*
        - `*init(name: String)`: Es el constructor que inicializa la instancia de la clase. En este caso, asigna el valor de `name` al recibirlo como parámetro y muestra un mensaje en la consola indicando que el objeto ha sido inicializado.*
        - `*deinit`: Es el destructor, que se ejecuta automáticamente cuando la instancia de la clase es destruida (es decir, cuando su ciclo de vida termina). Aquí imprime un mensaje indicando que el objeto ha sido desinicializado.*
2. *Creación de una instancia:*
    - *Dentro de un bloque `if true`, se crea una instancia de `MyClass` llamada `objeto` con el nombre `"Objeto1"`. Al hacerlo, se ejecuta el método `init`, que imprime: Objeto1 ha sido inicializado.*
3. *Destrucción de la instancia:*

*Como `objeto` está declarado dentro de un bloque (delimitado por `{ }`), su alcance está limitado a ese bloque. Al final del bloque, el objeto se destruye automáticamente (porque ya no es necesario). En ese momento, se llama al método `deinit`, que imprime: Objeto1 ha sido desinicializado.*

1. *Fin del programa:*

*Después de que se destruye la instancia, el programa continúa ejecutándose y llega al final, donde imprime: Fin del programa.*

*5. Salida del programa:*

*El programa produce exactamente esta salida en la consola:*

*Objeto1 ha sido inicializado.
Objeto1 ha sido desinicializado.
Fin del programa.*

*Notas importantes:*

*Ciclo de vida de las instancias: En Swift, cuando un objeto ya no es referenciado por ninguna variable, el sistema lo destruye automáticamente. Esto se conoce como recolección automática de memoria (ARC, Automatic Reference Counting).*

`*if true`: Este bloque es una construcción artificial en este caso. Podrías usar cualquier otra estructura que delimite el alcance de una variable, como una función o un `do` block.*

</aside>

Ejemplo con manejo de recursos:

Un caso práctico podría ser cerrar una conexión de base de datos o liberar archivos

```swift
class FileHandler {
    let fileName: String
    
    init(fileName: String) {
        self.fileName = fileName
        print("Archivo \(fileName) abierto.")
    }
    
    deinit {
        print("Archivo \(fileName) cerrado.")
    }
}

// Uso de la clase
if true {
    let file = FileHandler(fileName: "datos.txt")
    // Operaciones con el archivo
}
print("Fin del programa.")
// Archivo datos.txt abierto.
// Archivo datos.txt cerrado.
// Fin del programa.
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición de la clase `FileHandler`:*

*Propiedad `fileName`:*

- *Es una constante (`let`) que almacena el nombre del archivo. Se asigna en el momento de la inicialización y no puede cambiar después.*

*Método `init` (inicializador):*

- *Este método se ejecuta automáticamente al crear una instancia de la clase.*
- *Recibe un parámetro `fileName` para inicializar la propiedad `fileName`.*
- *Imprime un mensaje indicando que el archivo ha sido abierto.*

*Método `deinit` (desinicializador):*

- *Este método se ejecuta automáticamente cuando la instancia de la clase se destruye, es decir, cuando su ciclo de vida termina.*
- *Imprime un mensaje indicando que el archivo ha sido cerrado.*

*2. Uso de la clase:*

*Dentro del bloque `if true`, se crea una instancia de la clase `FileHandler` llamada `file` con el nombre del archivo `"datos.txt"`.*

*Cuando se crea esta instancia:*

- *Se ejecuta el inicializador `init`, y se imprime: Archivo datos.txt abierto.*

*Al final del bloque (cuando termina su alcance):*

*La instancia `file` ya no es referenciada y se destruye automáticamente.*

*En ese momento, se ejecuta el desinicializador `deinit`, que imprime: Archivo datos.txt cerrado.*

*3. Fin del programa:*

*Una vez que el bloque `if true` termina, el programa sigue ejecutándose y finalmente imprime: Fin del programa.*

*Salida del programa:*

*El programa produce exactamente esta salida:*

*Archivo datos.txt abierto.
Archivo datos.txt cerrado.
Fin del programa.*

*Detalles importantes:*

*Ciclo de vida de las instancias:*

- *En Swift, las instancias se destruyen automáticamente cuando ya no son necesarias, gracias al sistema ARC (Automatic Reference Counting).*
- *En este caso, la variable `file` solo existe dentro del bloque `if true`. Al salir de este bloque, la instancia es liberada.*

*Aplicaciones prácticas:*

- *Esta técnica es útil para gestionar recursos como archivos, conexiones de red o memoria, asegurando que se liberen correctamente cuando ya no son necesarios.*

*Estructura del programa:*

- *El bloque `if true` no tiene un propósito funcional aquí; simplemente delimita el alcance de la variable `file`. Podría sustituirse por un `do` block o cualquier otra estructura*
</aside>

# **2. Consideraciones sobre ciclos de referencia**

Si usas referencias fuertes entre instancias de clases, puedes provocar ciclos de memoria y evitar que `deinit` se llame. Para evitar esto, se deben usar referencias débiles (`weak`) o sin dueño (`unowned`).

Ejemplo de un ciclo de referencia solucionado:

```swift
class Person {
    var name: String
    weak var pet: Pet? // Uso de `weak` para evitar el ciclo
    
    init(name: String) {
        self.name = name
    }
    
    deinit {
        print("\(name) ha sido desinicializado.")
    }
}

class Pet {
    var name: String
    unowned var owner: Person // Uso de `unowned` aquí
    
    init(name: String, owner: Person) {
        self.name = name
        self.owner = owner
    }
    
    deinit {
        print("Mascota \(name) ha sido desinicializada.")
    }
}

// Creación de instancias
if true {
    let person = Person(name: "Juan")
    let dog = Pet(name: "Fido", owner: person)
    person.pet = dog
}
// Al final del bloque, ambos objetos serán liberados

// Mascota Fido ha sido desinicializada.
// Juan ha sido desinicializado.
```

<aside>
📎

*Este código puede leerse como:*

*1. Clase `Person`:*

*Propiedades:*

- `*name`: Una propiedad de tipo `String` que almacena el nombre de la persona.*
- `*pet`: Una referencia débil (`weak`) a un objeto de tipo `Pet`.*
    - *Esto significa que `Person` no retiene fuertemente a su mascota. Si no hay otra referencia al objeto `Pet`, se liberará automáticamente de la memoria.*

*Métodos:*

- `*init(name:)`: Inicializa el nombre de la persona.*
- `*deinit`: Se ejecuta automáticamente cuando la instancia de `Person` es liberada, imprimiendo un mensaje.*

*2. Clase `Pet`:*

*Propiedades:*

- `*name`: Una propiedad de tipo `String` que almacena el nombre de la mascota.*
- `*owner`: Una referencia no retenida (`unowned`) a un objeto de tipo `Person`.*
    - *Esto indica que la mascota asume que su dueño siempre existirá mientras la mascota esté viva. Si el objeto dueño desaparece antes que la mascota, habrá un error.*

*Métodos:*

- `*init(name:owner:)`: Inicializa el nombre de la mascota y su relación con el dueño.*
- `*deinit`: Se ejecuta automáticamente cuando la instancia de `Pet` es liberada, imprimiendo un mensaje.*

*3. Creación de instancias:*

*Dentro del bloque `if true`:*

- *Se crea una instancia de `Person` llamada `person` con el nombre `"Juan"`.*
- *Se crea una instancia de `Pet` llamada `dog` con el nombre `"Fido"`, cuyo dueño es `person`.*
- *Se establece una relación mutua: `person.pet = dog`.*

*Esto establece una referencia fuerte (`strong`) de `dog` hacia `person` y una referencia débil (`weak`) de `person` hacia `dog`.*

*4. Liberación de memoria:*

*Al salir del bloque `if true`:*

- *La referencia a `person` y `dog` desaparece.*
- `*dog` tiene una referencia `unowned` a `person`, que no impide que este sea liberado.*
- `*person` tiene una referencia `weak` a `dog`, lo que tampoco impide que este sea liberado.*
- *Ambos objetos se liberan automáticamente, y se ejecutan sus respectivos desinicializadores (`deinit`).*
1. *Salida esperada:*

*Cuando las instancias se destruyen, los desinicializadores imprimen:* 

*Mascota Fido ha sido desinicializada.
Juan ha sido desinicializado.*

1. *Detalles clave:*

*Evitar ciclos de referencia fuertes:*

- *Si `pet` tuviera una referencia fuerte (`strong`) a `Person`, y `Person` tuviera una referencia fuerte a `Pet`, habría un ciclo de referencia. Esto impediría que ambos objetos se liberen, causando una fuga de memoria.*

*Uso de `weak`:*

- *Se utiliza cuando la relación es opcional y el objeto puede desaparecer (como una persona que puede o no tener mascota).*

*Uso de `unowned`:*

- *Se utiliza cuando se garantiza que el objeto referido existirá durante la vida útil del que lo contiene (como una mascota que siempre tiene un dueño mientras esté viva).*
</aside>

# ***3. Comparación de Weak y Unowned***

| Característica | `weak` | `unowned` |
| --- | --- | --- |
| Tipo de referencia | Débil | No retenida |
| Valor opcional | Siempre opcional (`?`) | No opcional |
| Uso | Cuando el objeto puede desaparecer | Cuando el objeto siempre existirá |

---