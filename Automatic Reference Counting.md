# Automatic Reference Counting

> Modelar la vida útil de los objetos y sus relaciones.
> 

Automatic Reference Counting (ARC) es una característica de Swift que se utiliza para gestionar la memoria de forma automática. ARC rastrea y gestiona la vida útil de las instancias de clases asegurándose de que no se desperdicien recursos y que las instancias se liberen cuando ya no se necesitan.

En Swift, las referencias fuertes son las que ARC utiliza para determinar si una instancia aún es necesaria. Cuando no hay más referencias fuertes hacia una instancia, ARC la libera automáticamente, recuperando la memoria que estaba utilizando.

# 1. Cómo funciona ARC

1. Asignación de referencias fuertes:
Cuando creas una instancia de una clase, ARC asigna un contador de referencia fuerte. Cada vez que otro objeto hace referencia a esa instancia, el contador aumenta.
2. Liberación de memoria:
Cuando una referencia fuerte se elimina, el contador disminuye. Si el contador llega a cero, ARC elimina la instancia.

Ejemplo básico de ARC

```swift
class Persona {
    let nombre: String

    init(nombre: String) {
        self.nombre = nombre
        print("\(nombre) ha sido inicializado")
    }

    deinit {
        print("\(nombre) ha sido liberado de memoria")
    }
}

var persona1: Persona? = Persona(nombre: "Juan") // Referencia fuerte creada
persona1 = nil 
// Contador de referencias llega a 0, la memoria es liberada
// Juan ha sido inicializado
// Juan ha sido liberado de memoria
```

<aside>
📎

*Este código puede leerse como:*

*1. Declaración de la clase `Persona`*

*Se define una clase llamada `Persona`.*

*Dentro de la clase, se declara una propiedad llamada `nombre` de tipo `String`. Esta propiedad es constante (se usa `let`), lo que significa que una vez asignado un valor a `nombre` dentro de la instancia de la clase, este valor no puede cambiar.*

*2. Inicializador (`init`)*

*Se define un inicializador (`init`) que recibe un parámetro `nombre` de tipo `String` para asignarlo a la propiedad `nombre` de la instancia.*

*Dentro del inicializador, se asigna el valor recibido en el parámetro `nombre` a la propiedad `nombre` de la instancia usando `self.nombre = nombre`.*

*Se imprime un mensaje en consola indicando que la persona ha sido inicializada, mostrando el valor de `nombre`.*

*3. Deinit (`deinit`)*

*Se define un deinicializador (`deinit`). Este bloque de código se ejecuta cuando el objeto es liberado de memoria (cuando su contador de referencias llega a cero).*

*En este caso, se imprime un mensaje indicando que la persona con el nombre especificado ha sido liberada de memoria.*

*4. Uso de la clase `Persona`*

*Se crea una instancia de la clase `Persona` y se asigna a la variable `persona1`. Esta variable es un opcional (`Persona?`), lo que significa que puede contener un valor `Persona` o ser `nil`.*

*La creación de la instancia invoca el inicializador, lo que lleva a que se imprima el mensaje: `"Juan ha sido inicializado"`.*

*Después, la variable `persona1` se establece a `nil`, lo que elimina la referencia fuerte al objeto `Persona`. Esto provoca que el objeto se marque para ser liberado de memoria.*

*5. Liberación de memoria*

*Como la referencia a `persona1` se ha eliminado, el contador de referencias del objeto `Persona` llega a 0, lo que significa que el objeto ya no está siendo retenido por ninguna parte del programa y es liberado de memoria.*

*En ese momento, se ejecuta el deinicializador, imprimiendo el mensaje: `"Juan ha sido liberado de memoria"`.*

*Resumen de la ejecución:*

*Se crea la instancia `persona1` con el nombre "Juan". Se imprime: `"Juan ha sido inicializado"`.*

*Se asigna `nil` a `persona1`, eliminando la referencia fuerte. El objeto `Persona` es liberado de memoria.*

*Se ejecuta el deinicializador, imprimiendo: `"Juan ha sido liberado de memoria"`.*

*Este código muestra cómo Swift maneja la memoria automática y la liberación de objetos cuando ya no hay referencias a ellos.*

</aside>

# ***2. Retain Cycles (Ciclos de Retención)***

Los ciclos de retención ocurren cuando dos instancias mantienen referencias fuertes entre sí, impidiendo que sus contadores lleguen a cero.

Ejemplo de ciclo de retención:

```swift
class Persona {
    let nombre: String
    var mascota: Mascota?

    init(nombre: String) {
        self.nombre = nombre
    }

    deinit {
        print("\(nombre) ha sido liberado de memoria")
    }
}

class Mascota {
    let nombre: String
    var dueño: Persona?

    init(nombre: String) {
        self.nombre = nombre
    }

    deinit {
        print("\(nombre) ha sido liberado de memoria")
    }
}

var juan: Persona? = Persona(nombre: "Juan")
var perro: Mascota? = Mascota(nombre: "Fido")

juan?.mascota = perro
perro?.dueño = juan

juan = nil
perro = nil // Ciclo de retención: ni Persona ni Mascota son liberadas
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición de las clases
Clase `Persona`*

*La clase `Persona` tiene dos propiedades:*

- `*nombre`: una constante (`let`) que guarda el nombre de la persona.*
- `*mascota`: una propiedad opcional de tipo `Mascota?`. Esto significa que la persona puede tener una mascota, pero no necesariamente.*

*El inicializador `init` recibe un `nombre` como parámetro y asigna ese valor a la propiedad `nombre` de la instancia.*

*El método `deinit` es el destructor de la clase y se ejecuta cuando una instancia de `Persona` es liberada de memoria. En este caso, imprime un mensaje indicando que la persona ha sido liberada de memoria.*

*Clase `Mascota`*

*La clase `Mascota` es muy similar a la clase `Persona`:*

- `*nombre`: una constante que guarda el nombre de la mascota.*
    - `*dueño`: una propiedad opcional de tipo `Persona?`, lo que indica que una mascota puede tener un dueño (persona), pero no necesariamente.*

*Al igual que en `Persona`, el inicializador asigna un valor a la propiedad `nombre` de la mascota.*

*El `deinit` imprime un mensaje cuando una instancia de `Mascota` es liberada de memoria.*

*2. Creación de objetos y asignación de relaciones*

*Se crean dos objetos:*

- `*juan`: una instancia de `Persona` con el nombre "Juan".*
- `*perro`: una instancia de `Mascota` con el nombre "Fido".*

*Luego, se establece una relación entre ellos:*

- *Se asigna `perro` a la propiedad `mascota` de `juan`, lo que significa que Juan tiene una mascota llamada "Fido".*
- *Se asigna `juan` a la propiedad `dueño` de `perro`, lo que significa que la mascota "Fido" tiene un dueño llamado Juan.*

*3. Liberación de memoria y ciclo de retención*

*Aquí, se intenta liberar los objetos:*

*Se establece `juan = nil`, lo que debería liberar la instancia de `Persona` llamada "Juan".*

*Se establece `perro = nil`, lo que debería liberar la instancia de `Mascota` llamada "Fido".*

*Sin embargo, no se liberan estas instancias de memoria debido a un ciclo de retención.*

*4. Explicación del ciclo de retención*

*El ciclo de retención ocurre porque tanto `juan` como `perro` tienen referencias fuertes entre sí:*

`*juan` tiene una referencia fuerte a `perro` a través de la propiedad `mascota`.*

`*perro` tiene una referencia fuerte a `juan` a través de la propiedad `dueño`.*

*En Swift, las referencias fuertes (como las de las propiedades) incrementan el contador de retenciones del objeto, lo que evita que se liberen de memoria. Esto significa que, aunque establezcas `juan = nil` y `perro = nil`, los objetos no se liberarán porque ambos mantienen una referencia mutua y fuerte entre sí.*

*5. Resultado esperado*

*Debido al ciclo de retención:*

*Ni `Persona` ni `Mascota` son liberadas de memoria cuando se establecen `juan = nil` y `perro = nil`.*

*En lugar de que el `deinit` se ejecute y los objetos sean liberados, el ciclo de retención mantiene a ambos objetos en memoria.*

*6. Solución al ciclo de retención*

*Para solucionar el ciclo de retención, puedes usar referencias débiles (`weak`) o referencias no retenidas (`unowned`) para romper la referencia mutua. Por ejemplo, en lugar de usar `var dueño: Persona?` en la clase `Mascota`, podrías cambiarlo a:* 

```swift
var dueño: Persona?
```

*Para que no se mantenga una fuerte referencia circular.*

*De esta forma, cuando se establezca `juan = nil`, `perro` podrá ser liberado correctamente y viceversa.*

</aside>

# ***3. Referencias débiles (weak) y sin propietario (unowned)***

Para evitar ciclos de retención, puedes usar `weak` o `unowned`:

- `weak`: La referencia puede ser nula y no incrementa el contador de referencias.
- `unowned`: La referencia nunca será nula y no incrementa el contador, pero puede causar un error si se accede a una referencia que ya ha sido liberada.

Ejemplo con `weak`:

```swift
class Persona {
    let nombre: String
    var mascota: Mascota?

    init(nombre: String) {
        self.nombre = nombre
    }

    deinit {
        print("\(nombre) ha sido liberado de memoria")
    }
}

class Mascota {
    let nombre: String
    weak var dueño: Persona? // Solución al ciclo de retención

    init(nombre: String) {
        self.nombre = nombre
    }

    deinit {
        print("\(nombre) ha sido liberado de memoria")
    }
}

var juan: Persona? = Persona(nombre: "Juan")
var perro: Mascota? = Mascota(nombre: "Fido")

juan?.mascota = perro
perro?.dueño = juan

juan = nil // Persona liberada
perro = nil // Mascota liberada
// Juan ha sido liberado de memoria
// Fido ha sido liberado de memoria
```

<aside>
📎

*Este código puede leerse como:*

*1. Clase `Persona`*

*Propiedades:*

- `*nombre`: una constante de tipo `String`, que almacena el nombre de la persona.*
- `*mascota`: una propiedad opcional de tipo `Mascota?`. Se trata de una referencia a un objeto de tipo `Mascota`, que puede ser `nil` (es decir, la persona no tiene mascota en un momento dado).*

*Inicializador:*

- *El método `init(nombre: String)` es el inicializador de la clase. Recibe un nombre como parámetro y lo asigna a la propiedad `nombre`.*

*Desinicializador:*

- *El método `deinit` se llama automáticamente cuando el objeto es liberado de la memoria. En este caso, imprime un mensaje indicando que la persona ha sido liberada de la memoria.*

*2. Clase `Mascota`*

*Propiedades:*

- `*nombre`: una constante de tipo `String`, que almacena el nombre de la mascota.*
- `*dueño`: una propiedad opcional de tipo `Persona?`, que es una referencia débil (`weak`). Esta referencia apunta al objeto `Persona` que es dueño de la mascota.*
    - *La palabra clave `weak` es importante para evitar ciclos de retención (circular references), que ocurren cuando dos objetos se mantienen mutuamente en memoria, evitando que el sistema libere la memoria de los objetos. Usar `weak` significa que la referencia no aumenta el conteo de referencias fuertes y, por lo tanto, no previene la liberación de memoria de los objetos asociados.*

*Inicializador:*

- *El método `init(nombre: String)` recibe un nombre como parámetro y lo asigna a la propiedad `nombre`.*

*Desinicializador:*

- *El método `deinit` se llama cuando el objeto es liberado de la memoria, y en este caso, imprime un mensaje indicando que la mascota ha sido liberada de la memoria.*

*3. Creación y vinculación de objetos*

*Se crean dos objetos: uno de tipo `Persona` (Juan) y otro de tipo `Mascota` (Fido).*

*Luego, se establece la relación entre ellos:*

- `*juan?.mascota = perro`: La persona (Juan) tiene una mascota (Fido).*
- `*perro?.dueño = juan`: La mascota (Fido) tiene un dueño (Juan).*

*4. Liberación de memoria*

*Al poner `juan` y `perro` en `nil`, ambos objetos se desreferencian y deberían ser liberados de la memoria.*

- *Juan: El objeto `Persona` es liberado, lo que invoca el `deinit` de la clase `Persona`, imprimiendo "Juan ha sido liberado de memoria".*
- *Fido: El objeto `Mascota` también se libera, invocando el `deinit` de la clase `Mascota`, lo que imprime "Fido ha sido liberado de memoria".*

*5. Evitar ciclo de retención*

*En este código, se evita un ciclo de retención gracias a la palabra clave `weak` en la propiedad `dueño` de la clase `Mascota`. Sin el `weak`, ambos objetos (`Persona` y `Mascota`) se referirían mutuamente, lo que impediría que ambos fueran liberados de la memoria cuando ya no hay más referencias fuertes hacia ellos, resultando en una fuga de memoria.*

*Al usar `weak` en `dueño`, la propiedad `dueño` no incrementa el conteo de referencias, permitiendo que tanto `juan` como `perro` puedan ser liberados correctamente cuando se pone `nil` en sus referencias.*

*Resultado final*

*Cuando el código se ejecuta, los objetos son liberados correctamente de la memoria:*

*Juan ha sido liberado de memoria
Fido ha sido liberado de memoria*

*Resumen*

*Este código muestra cómo manejar relaciones entre objetos de manera segura en Swift, utilizando referencias débiles (`weak`) para evitar ciclos de retención y garantizar que la memoria se libere adecuadamente cuando los objetos ya no sean necesarios.*

</aside>

# ***4. Usos comunes de ARC***

1. Gestión de objetos complejos:
En aplicaciones con jerarquías de objetos, ARC asegura que los recursos no se queden en memoria más tiempo del necesario.
2. Evitar fugas de memoria:
Al identificar ciclos de retención con herramientas como Instruments y utilizando referencias débiles, se evita el desperdicio de memoria.
3. Desarrollo de aplicaciones eficientes:
ARC elimina la necesidad de liberar memoria manualmente, como ocurre en lenguajes como C o C++.

---