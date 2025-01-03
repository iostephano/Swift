# Optional Chaining

> Acceda a los miembros de un valor opcional sin desempaquetar.
> 

El Optional Chaining en Swift es una forma segura y concisa de trabajar con valores opcionales. Permite acceder a propiedades, métodos y subscripts de un opcional solo si contiene un valor, devolviendo `nil` si el opcional es `nil`. 

Esto evita el uso de múltiples verificaciones para desempaquetar opcionales. 

Cuando se utiliza optional chaining, si el valor opcional es `nil`, toda la expresión devuelve `nil`. Si no es `nil`, la propiedad, método o subscript se evalúa y se devuelve su valor.

**Sintaxis**

La sintaxis usa el operador de encadenamiento opcional (`?`) después del nombre del opcional.

```swift
optionalValue?.property
optionalValue?.method()
optionalValue?[index]
```

# ***1. Acceso a Propiedades de un Opcional***

```swift
class Persona {
    var nombre: String?
}

var persona: Persona? = Persona()
persona?.nombre = "Juan"

// Sin optional chaining
if let p = persona, let n = p.nombre {
    print("El nombre es \(n)")
} else {
    print("No hay nombre")
}

// Con optional chaining
if let nombre = persona?.nombre {
    print("El nombre es \(nombre)")
} else {
    print("No hay nombre")
}
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición de la clase `Persona`*

*Aquí se define una clase llamada `Persona`. Esta clase tiene una propiedad `nombre` de tipo `String?`, lo que significa que `nombre` puede contener un valor de tipo `String` o puede ser `nil`. Es una propiedad opcional.*

*2. Creación de un objeto `persona` y asignación de valor*

`*var persona: Persona?` declara una variable opcional de tipo `Persona`. Inicialmente, la variable `persona` es `nil`.*

`*Persona()` crea una nueva instancia de la clase `Persona`, la cual se asigna a la variable `persona`. Por lo tanto, en este punto, `persona` deja de ser `nil` y se convierte en un objeto de tipo `Persona`.*

`*persona?.nombre = "Juan"` asigna el valor `"Juan"` a la propiedad `nombre` del objeto `persona`. Dado que `nombre`es opcional, el uso del operador `?.` asegura que solo se intentará acceder a `nombre` si `persona` no es `nil`. En este caso, como `persona` no es `nil`, el nombre se asigna correctamente.*

*3. Acceso sin "optional chaining" (usando optional binding)*

*En este bloque se usa el optional binding con el propósito de verificar si `persona` tiene un valor (es decir, no es `nil`) y si `persona.nombre` también tiene un valor (es decir, no es `nil`).*

`*if let p = persona` intenta "desenvolver" el valor opcional `persona`. Si `persona` no es `nil`, `p` recibirá el valor de `persona` (en este caso, una instancia de la clase `Persona`).*

*Si `persona` no es `nil`, entonces se verifica si `p.nombre` tiene un valor utilizando `if let n = p.nombre`. Si `nombre`tiene un valor (no es `nil`), entonces `n` recibirá ese valor y se ejecutará el bloque de código dentro del `if`.*

*Si ambos valores son no `nil`, el resultado será que se imprimirá el nombre: `"El nombre es Juan"`.*

*Si cualquiera de los valores es `nil` (es decir, si `persona` es `nil` o si `nombre` es `nil`), entonces se ejecutará el bloque `else`, y se imprimirá `"No hay nombre"`.*

*4. Acceso con "optional chaining"*

*Aquí se utiliza el optional chaining, que permite acceder de forma segura a las propiedades de un objeto opcional sin necesidad de hacer un `if let` por cada paso.*

`*persona?.nombre` intenta acceder a la propiedad `nombre` de `persona` solo si `persona` no es `nil`. Si `persona` es `nil`, entonces el resultado de `persona?.nombre` será `nil` automáticamente, y el bloque `else` se ejecutará.*

*Si `persona` no es `nil` y `nombre` tiene un valor no `nil`, entonces el valor de `nombre` se asignará a la constante `nombre`, y se imprimirá `"El nombre es Juan"`.*

*Si cualquiera de los valores es `nil`, se imprimirá `"No hay nombre"`.*

*Diferencia entre "optional binding" y "optional chaining"*

*Optional Binding (`if let`): Se utiliza para desenvuelver un valor opcional de manera explícita, verificando si el valor está presente antes de usarlo. Si cualquiera de las variables opcionales es `nil`, el bloque `else` se ejecuta.*

*Optional Chaining (`?.`): Permite acceder a propiedades, métodos o subscripts de un valor opcional de manera más compacta y segura. Si la variable opcional es `nil`, todo el encadenamiento devolverá `nil`, y no se ejecutará el bloque de código posterior al encadenamiento. No es necesario hacer un `if let` explícito.*

*Resumen*

*Sin Optional Chaining: Usamos `if let` para hacer un "desenvolvimiento" explícito de la variable `persona` y luego de la propiedad `nombre`. Esto nos da más control, pero requiere más código.*

*Con Optional Chaining: Usamos `?.` para acceder a la propiedad `nombre` de manera más compacta y directa, sin necesidad de hacer un "desenvolvimiento" manual de las variables opcionales. Es más limpio y cómodo, pero menos explícito en cuanto a la lógica de control.*

</aside>

# ***2. Llamadas a Métodos***

```swift
class Mascota {
    func ladrar() {
        print("¡Guau!")
    }
}

var perro: Mascota? = Mascota()
perro?.ladrar()  // Imprime "¡Guau!"

perro = nil
perro?.ladrar()  // No hace nada porque el valor es nil
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición de la clase `Mascota`*

*Aquí defines una clase llamada `Mascota`.*

*La clase tiene un método llamado `ladrar()`, que cuando se invoca, imprime el texto `"¡Guau!"` en la consola.*

*Este es un comportamiento básico de una clase con un método que solo realiza una acción (imprimir un mensaje).*

*2. Creación de una instancia opcional de `Mascota`*

*Aquí defines una variable `perro` de tipo `Mascota?`. El signo de interrogación (`?`) indica que la variable es opcional, lo que significa que puede contener un valor de tipo `Mascota` o puede ser `nil` (es decir, que no apunte a ninguna instancia).*

*Se crea una instancia de `Mascota()` y se asigna a `perro`. Por lo tanto, en este momento, `perro` no es `nil` y contiene una instancia de la clase `Mascota`.*

*3. Llamada al método `ladrar()` de la instancia de `Mascota`*

*Aquí se llama al método `ladrar()` de la variable `perro`.*

*El operador de encadenamiento opcional `?.` se usa para invocar el método solo si `perro` no es `nil`.*

- *Si `perro` tiene un valor (es decir, si no es `nil`), se ejecuta el método `ladrar()` y se imprime `"¡Guau!"`.*
- *Si `perro` fuera `nil`, no se ejecutaría el método y simplemente no sucedería nada.*

*En este caso, como `perro` contiene una instancia de `Mascota`, el método `ladrar()` se ejecuta y se imprime `"¡Guau!"`.*

*4. Asignación de `nil` a `perro`*

*Aquí se asigna `nil` a la variable `perro`. Esto hace que `perro` deje de apuntar a una instancia de `Mascota` y, en su lugar, ahora sea `nil`.*

*5. Llamada a `ladrar()` cuando `perro` es `nil`*

*Nuevamente se intenta llamar al método `ladrar()` sobre `perro`.*

*Debido a que ahora `perro` es `nil`, el encadenamiento opcional `?.` evita la ejecución del método. Como resultado, no se hace nada y no se imprime ningún mensaje en la consola.*

- *Si `perro` no fuera `nil`, el método `ladrar()` se ejecutaría normalmente.*
- *En este caso, como `perro` es `nil`, el código simplemente "salta" la llamada al método sin realizar ninguna acción.*

*Resumen*

*Primera llamada (`perro?.ladrar()` cuando `perro` no es `nil`): El método `ladrar()` se ejecuta y se imprime `"¡Guau!"`.*

*Segunda llamada (`perro?.ladrar()` cuando `perro` es `nil`): No sucede nada, ya que `perro` es `nil` y el operador `?.` previene la ejecución del método en caso de que la variable sea `nil`.*

</aside>

# ***3. Encadenamiento de Opcionales Anidados***

```swift
class Direccion {
    var ciudad: String?
}

class Usuario {
    var direccion: Direccion?
}

var usuario = Usuario()
usuario.direccion = Direccion()
usuario.direccion?.ciudad = "Milán"

// Accediendo a propiedades opcionales anidadas
if let ciudad = usuario.direccion?.ciudad {
    print("La ciudad es \(ciudad)")
} else {
    print("No hay ciudad")
}
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición de la clase `Direccion`*

*La clase `Direccion` tiene una propiedad `ciudad`, que es de tipo opcional `String?`.*

*El tipo `String?` significa que esta propiedad puede contener un valor de tipo `String`, o puede ser `nil` (no tener valor).*

*2. Definición de la clase `Usuario`*

*La clase `Usuario` tiene una propiedad `direccion`, que es de tipo opcional `Direccion?`.*

*Esto significa que un objeto de tipo `Usuario` puede tener una instancia de `Direccion` o puede no tener ninguna (es decir, puede ser `nil`).*

*3. Creación e inicialización de un objeto `Usuario`*

*Se crea una instancia de `Usuario` llamada `usuario`.*

*Luego, se asigna una nueva instancia de `Direccion` a la propiedad `direccion` del usuario.*

*Después, se intenta asignar el valor `"Milán"` a la propiedad `ciudad` de la instancia de `Direccion` dentro de `usuario`.*

*El operador `?.` se utiliza para acceder a la propiedad `ciudad` de manera segura. Esto significa que si `usuario.direccion` es `nil`, no se intentará acceder a `ciudad` y el programa no fallará.*

*4. Acceso seguro a las propiedades opcionales anidadas*

*El bloque `if let` intenta desempaquetar la propiedad opcional `ciudad` de forma segura.*

*Si `usuario.direccion` no es `nil` y `ciudad` tiene un valor (es decir, no es `nil`), entonces el valor de `ciudad` se asigna a la constante `ciudad` y se ejecuta el bloque `if`, imprimiendo el valor de la ciudad.*

*Si alguna de las propiedades opcionales (`usuario.direccion` o `ciudad`) es `nil`, el bloque `else` se ejecuta, imprimiendo `"No hay ciudad"`.*

*Resultado de ejecución*

*Dado que se asigna `"Milán"` a la propiedad `ciudad` en el paso anterior, el valor de `ciudad` no es `nil`. Por lo tanto, el programa ejecutará el bloque `if` y mostrará en la consola: La ciudad es Milán.*

*Resumen del código:*

*Clases: Se definen dos clases, `Direccion` (que tiene una propiedad opcional `ciudad`) y `Usuario` (que tiene una propiedad opcional `direccion`).*

*Propiedades opcionales: Tanto `direccion` como `ciudad` son opcionales, lo que significa que pueden ser `nil`.*

*Acceso seguro: El operador `?.` se usa para acceder de manera segura a las propiedades opcionales sin causar errores si alguna de ellas es `nil`.*

*Desempaquetado opcional: Se utiliza `if let` para desempaquetar de manera segura la propiedad `ciudad` y acceder a su valor solo si no es `nil`.*

*Este enfoque es común en Swift para manejar valores opcionales sin causar fallos en el programa, lo que ayuda a evitar errores de desreferenciación de punteros nulos (lo que podría ocurrir en otros lenguajes).*

</aside>

# ***4. Subscripts***

```swift
var diccionario: [String: [String]]? = ["frutas": ["manzana", "pera"]]
let primeraFruta = diccionario?["frutas"]?.first
print(primeraFruta ?? "No hay fruta")  // Imprime "manzana"
```

<aside>
📎

*Este código puede leerse como:*

1. *Declaración de `diccionario`:*

*Aquí se está declarando una variable llamada `diccionario` de tipo opcional `[String: [String]]?`. Esto significa que `diccionario` es un diccionario que tiene como clave un `String` y como valor un arreglo de `String`. Es opcional porque tiene el signo de interrogación (`?`), lo que indica que puede ser `nil`.*

*Luego, se le asigna un valor que es un diccionario con una sola entrada: la clave `"frutas"`, y su valor correspondiente es un arreglo de frutas `["manzana", "pera"]`.*

1. *Acceso a un valor del diccionario:*

*En esta línea estamos accediendo al valor del diccionario con la clave `"frutas"`. Sin embargo, como `diccionario`es opcional, usamos el operador de encadenamiento opcional `?` para acceder de manera segura. Si `diccionario` es `nil`, no se ejecutará el resto de la cadena de accesos y el resultado será `nil`.*

*El valor asociado a la clave `"frutas"` es un arreglo de strings (`["manzana", "pera"]`), por lo que luego se utiliza `.first` para obtener el primer elemento del arreglo. El operador `?.` se usa para encadenar el acceso de manera segura, ya que si el arreglo es `nil` o está vacío, el resultado será `nil` y no generará un error.*

1. *Impresión del valor:*

*Aquí, estamos imprimiendo el valor de `primeraFruta`. Si `primeraFruta` es `nil`, se imprimirá el valor que se encuentra después del operador `??`, que en este caso es el string `"No hay fruta"`.*

*Como `primeraFruta` es opcional, si el diccionario tiene la clave `"frutas"` y el arreglo no está vacío, `primeraFruta` tendrá un valor (en este caso `"manzana"`).*

*Como resultado, se imprimirá `"manzana"`, ya que es el primer elemento del arreglo asociado a la clave `"frutas"`.*

*Resumen:*

*Este código está trabajando con un diccionario opcional de tipo `[String: [String]]?`, y está tratando de acceder al primer elemento del arreglo asociado a la clave `"frutas"`. Si encuentra ese valor, imprime el primer elemento (en este caso `"manzana"`). Si no encuentra ese valor, imprime `"No hay fruta"`. En este caso específico, como el diccionario está correctamente definido y contiene el arreglo `["manzana", "pera"]`, se imprimirá `"manzana"`.*

</aside>

***Ventajas***

- Código más limpio: Reduce la necesidad de desempaquetar opcionales manualmente.
- Seguridad: Previene errores al intentar acceder a propiedades o métodos en valores `nil`.
- Concisión: Permite encadenar múltiples niveles de opcionales de forma compacta.

***Conclusión***

- El optional chaining es una herramienta esencial en Swift para trabajar con opcionales de manera segura y elegante. Se usa siempre que no sea necesario manejar explícitamente el valor `nil` con lógica adicional.

---