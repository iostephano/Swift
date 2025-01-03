# Type Casting

> Determine el tipo de tiempo de ejecución de un valor y déle información de tipo más específica.
> 

Es una técnica que permite verificar el tipo de un objeto o convertirlo a otro tipo dentro de una jerarquía de clases o protocolos. Esto se logra mediante los operadores **`is`** y **`as`**. Es particularmente útil cuando trabajas con tipos genéricos o colecciones heterogéneas como `[Any]`.

# ***1. Operadores principales de Type Casting***

- **`is`**: Se utiliza para comprobar si una instancia es de un tipo específico.
- **`as?`**: Realiza un casting condicional, devolviendo un valor opcional que contiene la instancia convertida si el casting es exitoso, o `nil` si no lo es.
- **`as!`**: Realiza un casting forzado y causa un error en tiempo de ejecución si falla. Úsalo solo cuando estés completamente seguro del tipo.

## *1.1 Comprobación de tipos con IS*

```swift
class Animal {}
class Perro: Animal {}
class Gato: Animal {}

let mascotas: [Animal] = [Perro(), Gato(), Perro()]

for mascota in mascotas {
    if mascota is Perro {
        print("Esta mascota es un Perro")
    } else if mascota is Gato {
        print("Esta mascota es un Gato")
    }
}
// Esta mascota es un Perro
// Esta mascota es un Gato
// Esta mascota es un Perro
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición de clases*

- `*class Animal {}`: Esta línea define una clase llamada `Animal`. Es una clase base, es decir, otras clases pueden heredar de ella.*
- `*class Perro: Animal {}`: Aquí estamos definiendo la clase `Perro`, que es una subclase de `Animal`. Esto significa que `Perro` hereda las características y comportamientos de la clase `Animal`.*
- `*class Gato: Animal {}`: De manera similar, `Gato` es otra subclase de `Animal`.*
- *Ambas clases, `Perro` y `Gato`, son especializaciones de `Animal`. Sin embargo, no tienen métodos ni propiedades definidas por el momento, solo heredan de la clase base `Animal`.*

*2. Creación de un arreglo de objetos*

- *Aquí estamos creando un arreglo llamado `mascotas` que es de tipo `[Animal]`. Esto significa que el arreglo puede contener cualquier objeto que sea una instancia de `Animal` o de sus subclases (como `Perro` o `Gato`).*
- `*Perro()` crea una nueva instancia de la clase `Perro`.*
- `*Gato()` crea una nueva instancia de la clase `Gato`.*
- *Otro `Perro()` crea una nueva instancia de la clase `Perro`.*
- *Entonces, el arreglo `mascotas` contendrá tres objetos: dos instancias de `Perro` y una instancia de `Gato`.*

*3. Iteración sobre el arreglo*

- *Aquí estamos iterando sobre cada objeto dentro del arreglo `mascotas` usando un ciclo `for-in`. En cada iteración, la variable `mascota` contiene un objeto del tipo `Animal` o sus subclases (`Perro` o `Gato`).*
- *Dentro del ciclo, se hace una comprobación de tipo usando la palabra clave `is`, que permite verificar si el objeto es una instancia de un tipo específico.*
    - `*if mascota is Perro`: Si `mascota` es una instancia de la clase `Perro` (o de una subclase de `Perro`), se ejecutará este bloque de código y se imprimirá el mensaje `"Esta mascota es un Perro"`.*
    - `*else if mascota is Gato`: Si `mascota` no es un `Perro`, pero es una instancia de `Gato` (o de una subclase de `Gato`), se ejecutará este bloque de código y se imprimirá el mensaje `"Esta mascota es un Gato"`.*

*4. Resultado esperado*

- *Dado el contenido del arreglo `mascotas`:*
- *El ciclo `for` iterará sobre los tres elementos de este arreglo y, en cada iteración, verificará el tipo del objeto:*
    - *El primer objeto es un `Perro`, por lo que se imprimirá: `"Esta mascota es un Perro"`.*
    - *El segundo objeto es un `Gato`, por lo que se imprimirá: `"Esta mascota es un Gato"`.*
    - *El tercer objeto es otro `Perro`, por lo que se imprimirá: `"Esta mascota es un Perro"`.*

*5. Salida en consola*

- *El resultado final será el siguiente:*
    
    *Esta mascota es un Perro
    Esta mascota es un Gato
    Esta mascota es un Perro*
    

*Resumen*

- *Este código ilustra cómo trabajar con clases y herencia en Swift. Utiliza la comprobación de tipo (`is`) para identificar si un objeto pertenece a una clase específica o a una de sus subclases dentro de un arreglo polimórfico.*
</aside>

## *1.2 Casting condicional con AS?*

```swift
class Vehiculo {}
class Coche: Vehiculo {
    var modelo: String
    init(modelo: String) {
        self.modelo = modelo
    }
}

let vehiculos: [Vehiculo] = [Coche(modelo: "Tesla"), Vehiculo()]

for vehiculo in vehiculos {
    if let coche = vehiculo as? Coche {
        print("Es un coche modelo \(coche.modelo)")
    } else {
        print("No es un coche")
    }
}
// Es un coche modelo Tesla
// No es un coche
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición de las clases*

- *Aquí defines una clase llamada `Vehiculo`. Esta es una clase base (o superclase) y no tiene propiedades ni métodos. Es simplemente una clase vacía que puede ser heredada por otras clases.*
- *Aquí defines una clase llamada `Coche`, que hereda de `Vehiculo`. La clase `Coche` tiene una propiedad `modelo`, que es un `String`, y un inicializador (`init`) que recibe un valor de modelo y lo asigna a la propiedad `modelo` de la instancia.*

*2. Creación del arreglo de vehículos*

- *Aquí estás creando un arreglo de tipo `[Vehiculo]` que contiene dos elementos:*
    - *El primer elemento es un objeto de tipo `Coche`, creado con el modelo `"Tesla"`.*
    - *El segundo elemento es un objeto de tipo `Vehiculo` (la clase base, sin ninguna propiedad ni inicialización).*
- *El tipo de todos los elementos es `Vehiculo`, pero uno es un `Coche` y el otro es un `Vehiculo` simple.*

*3. Iteración sobre los vehículos*

- *Este bloque de código recorre cada elemento del arreglo `vehiculos`. En cada iteración, el valor de `vehiculo` será de tipo `Vehiculo`. Dado que `Coche` hereda de `Vehiculo`, puedes intentar convertir (hacer "cast") ese objeto a `Coche` utilizando el operador `as?`, que es una conversión segura (si no se puede hacer el cast, el resultado es `nil`).*
- `*if let coche = vehiculo as? Coche`: Si el objeto `vehiculo` puede ser convertido a un `Coche`, entonces entra en el bloque `if`, donde `coche` es una constante que hace referencia a ese objeto como un `Coche`. Se imprime el modelo del coche utilizando `coche.modelo`.*
- `*else`: Si el objeto `vehiculo` no puede ser convertido a un `Coche` (es decir, si es un `Vehiculo` que no es un `Coche`), entonces se ejecuta el bloque `else`, donde se imprime que no es un coche.*
1. *Resultado del código*
- *Cuando ejecutas este código, el ciclo recorre el arreglo `vehiculos` que tiene dos elementos. En la primera iteración:*
    - *El elemento es un objeto de tipo `Coche` con el modelo `"Tesla"`. El `if let` puede hacer el cast correctamente, por lo que imprime:`"Es un coche modelo Tesla"`.*
- *En la segunda iteración:*
    - *El elemento es un objeto de tipo `Vehiculo`, no un `Coche`. Como no puede hacer el cast a `Coche`, se ejecuta el bloque `else` y se imprime:`"No es un coche"`.*

*Conclusión*

- *El código demuestra cómo puedes usar la herencia entre clases y cómo realizar un "type cast" condicional (`as?`) para verificar si un objeto de una superclase puede ser tratado como una instancia de una subclase. Esto es útil cuando trabajas con jerarquías de clases y necesitas determinar si un objeto específico es una instancia de una clase derivada antes de acceder a sus propiedades o métodos específicos.*
</aside>

## *1.3 Casting forzado con AS!*

```swift
let objeto: Any = "Swift es genial"

let mensaje = objeto as! String
print(mensaje)  // Swift es genial
```

**Nota:** Si el casting falla, el programa lanzará un error de tiempo de ejecución.

<aside>
📎

*Este código puede leerse como:*

*1. Declaración de `objeto`*

- `*let`: Se utiliza para declarar una constante (es decir, `objeto` no puede ser reasignado después de su declaración).*
- `*objeto`: Es el nombre de la constante.*
- `*Any`: Es un tipo en Swift que puede representar cualquier tipo de valor, ya sea un tipo de datos primitivo (como un número o un String) o un tipo personalizado. En este caso, `objeto` es declarado con el tipo `Any`, lo que significa que puede almacenar cualquier valor.*
- `*"Swift es genial"`: Es un valor de tipo `String`, que es lo que se está asignando a la constante `objeto`.*
- *Aquí, estamos asignando un `String` ("Swift es genial") a una variable cuyo tipo es `Any`. Aunque el valor es un `String`, su tipo en este contexto es `Any`, lo que lo hace más flexible pero también menos específico.*

*2. Conversión de tipo (casting)*

- `*objeto as! String`: Esto es una conversión forzada de tipo (force cast). Se está tratando de convertir el valor de `objeto`, que es de tipo `Any`, a un tipo más específico: `String`.*
- `*as!`: Este operador fuerza la conversión de tipo. Si el valor almacenado en `objeto` no es de tipo `String`, el programa lanzará un error en tiempo de ejecución (un crash). Por ejemplo, si `objeto` almacenara un número o un arreglo, esto causaría una falla.*
- *Es importante tener en cuenta que, en este caso, sabemos que `objeto` tiene un valor de tipo `String` (porque lo asignamos explícitamente como `"Swift es genial"`), por lo que la conversión es segura y no debería causar un error. Sin embargo, en un escenario real, deberíamos tener cuidado al usar `as!`, ya que si el tipo de `objeto`no es `String`, el programa se bloquearía.*

*3. Imprimir el mensaje*

- *Esta línea simplemente imprime el valor de la constante `mensaje` en la consola.*
- *Como `mensaje` ahora es de tipo `String`, se imprimirá el texto `"Swift es genial"`.*

*Resumen*

- *Este código crea una constante `objeto` de tipo `Any` y le asigna un valor de tipo `String`. Luego, convierte explícitamente el valor almacenado en `objeto` a `String` usando el operador `as!`, y finalmente imprime el valor de `mensaje` en la consola.*
</aside>

## *1.4 Uso de ANY y ANYOBJECT con Type Casting*

```swift
let items: [Any] = [42, "Hola", 3.14, Coche(modelo: "Ford")]

for item in items {
    if let numero = item as? Int {
        print("Es un número entero: \(numero)")
    } else if let texto = item as? String {
        print("Es un texto: \(texto)")
    } else if let coche = item as? Coche {
        print("Es un coche modelo \(coche.modelo)")
    } else {
        print("Tipo desconocido")
    }
}
// Es un número entero: 42
// Es un texto: Hola
// Es un tipo desconocido
// Es un coche modelo Ford
```

<aside>
📎

*Este código puede leerse como:*

*1. Declaración del arreglo `items`*

- *Se declara una constante `items` que es un arreglo de elementos de tipo `Any`.*
    - `*Any` es un tipo en Swift que puede contener cualquier tipo de valor. Puede ser un número, una cadena, un objeto, etc.*
    - *Este arreglo contiene cuatro elementos:*
        - `*42`: un número entero (`Int`).*
        - `*"Hola"`: una cadena de texto (`String`).*
        - `*3.14`: un número decimal (`Double`).*
        - `*Coche(modelo: "Ford")`: una instancia de la clase `Coche`.*

*2. Ciclo `for` para recorrer los elementos del arreglo*

- *El ciclo `for` recorre todos los elementos en el arreglo `items` uno por uno.*
- *En cada iteración, el valor del elemento se guarda en la constante `item`.*

*3. Comprobación de tipos usando `if let` y `as?`*

- *Dentro del ciclo `for`, se utiliza una serie de sentencias `if let` con el operador `as?` para intentar hacer una conversión de tipo segura. Vamos a verlo por partes:*
    - *a) Comprobación de si el elemento es un número entero (`Int`)*
        - `*item as? Int` intenta convertir el valor de `item` a un `Int`.*
        - *Si `item` es efectivamente un número entero, se ejecuta el bloque dentro de este `if`, y se imprime un mensaje con el valor de `numero`.*
    - *b) Comprobación de si el elemento es una cadena de texto (`String`)*
        - *Si el elemento no era un `Int`, se intenta convertirlo a un `String` usando `item as? String`.*
        - *Si la conversión es exitosa, se ejecuta el bloque correspondiente e imprime el valor del texto.*
    - *c) Comprobación de si el elemento es un objeto de tipo `Coche`*
        - *Si el elemento no era ni un `Int` ni un `String`, se intenta convertir a un objeto de tipo `Coche` con `item as? Coche`.*
        - *Si la conversión es exitosa, se ejecuta este bloque y se imprime el modelo del coche.*
    - *d) Manejo de tipos desconocidos*
        - *Si el elemento no coincide con ninguno de los tipos anteriores (ni `Int`, ni `String`, ni `Coche`), se entra en esta sección y se imprime "Tipo desconocido".*

*4. Suposición sobre la clase `Coche`*

- *Para que este código funcione, es necesario que exista una definición de la clase `Coche`, que podría verse algo así:*
    
    ```swift
    class Coche {
        var modelo: String
        
        init(modelo: String) {
            self.modelo = modelo
        }
    }
    ```
    
- *En este caso, `Coche` es una clase que tiene una propiedad `modelo` (de tipo `String`). En el arreglo, se crea una instancia de esta clase con el modelo `"Ford"`.*
1. *Resumen del flujo*
- *El ciclo recorre los elementos en `items`.*
- *En cada iteración, intenta determinar el tipo del elemento mediante el operador de conversión segura `as?`.*
- *Si el tipo es reconocido (como `Int`, `String` o `Coche`), realiza una acción específica (como imprimir un mensaje).*
- *Si el tipo no es reconocido, imprime "Tipo desconocido".*
1. *Salida esperada*
- *El programa imprimirá lo siguiente:*
    
    *Es un número entero: 42
    Es un texto: Hola
    Tipo desconocido
    Es un coche modelo Ford*
    
1. *Detalles adicionales*
- *Si quieres agregar más tipos a manejar en el futuro, podrías agregar más bloques `else if` para comprobar otros tipos (como `Double`, `Bool`, etc.).*
- *El uso de `as?` permite evitar errores en tiempo de ejecución si el tipo no coincide, y si la conversión falla, simplemente se pasa al siguiente bloque.*
</aside>

***Consejos***

- Usa `as?` en lugar de `as!` siempre que sea posible para evitar errores en tiempo de ejecución.
- El Type Casting es una herramienta poderosa, pero úsala de manera razonable para mantener el código claro y seguro.

---