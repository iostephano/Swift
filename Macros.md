# Macros

> Utilice macros para generar código en tiempo de compilación.
> 

Las macros en Swift son una funcionalidad introducida en Swift 5.9 que permite generar código de forma dinámica durante la compilación. Esto facilita tareas repetitivas, asegura consistencia y puede optimizar el rendimiento al generar código específico en lugar de depender de soluciones genéricas o en tiempo de ejecución.

Las macros en Swift son particularmente útiles para:

- Automatizar la creación de código repetitivo.
- Validar código en tiempo de compilación.
- Mejorar la claridad del código al reducir redundancia.
- Implementar funcionalidades personalizadas basadas en anotaciones.

# ***1. Tipos de Macros en Swift***

- Expression Macros: Transforman expresiones y devuelven un nuevo valor.
- Declaration Macros: Generan nuevas declaraciones, como funciones, propiedades o estructuras.
- Freestanding Macros: No están asociadas a ningún elemento del código y pueden usarse de manera libre.

## *1.1 Macro de Propiedades Automáticas*

Supongamos que queremos evitar escribir repetidamente getters y setters para propiedades.

```swift
@AddPropertyWrapper
struct Usuario {
    var nombre: String
    var apellido: String
}
```

Definición de la macro:

```swift
macro AddPropertyWrapper: DeclarationMacro {
    static func expand(declaration: some DeclSyntax) -> DeclSyntax {
        // Genera automáticamente los getters y setters
    }
}
```

<aside>
📎

*Este código puede leerse como:*

*1. `macro AddPropertyWrapper: DeclarationMacro`*

- `*macro`: Esto indica que estamos declarando una macro. Las macros en Swift permiten modificar o generar código de manera automática en tiempo de compilación, lo que facilita tareas repetitivas o la adición de comportamientos específicos en el código.*
- `*AddPropertyWrapper`: Es el nombre de la macro. En este caso, parece que la macro está diseñada para añadir un "Property Wrapper" (un envoltorio de propiedad), que es un patrón común en Swift utilizado para agregar lógica adicional a una propiedad sin modificar directamente su tipo o acceso.*
- `*DeclarationMacro`: Especifica que la macro está relacionada con declaraciones, como `var`, `let`, o `func`. Este tipo de macro puede intervenir en declaraciones de propiedades o funciones.*

*2. `static func expand(declaration: some DeclSyntax) -> DeclSyntax`*

- `*static func expand`: Define un método estático llamado `expand`. Este método es responsable de modificar o generar código, en este caso, para las propiedades o declaraciones pasadas a la macro.*
- `*declaration: some DeclSyntax`: Este parámetro recibe una declaración que implementa el protocolo `DeclSyntax`. En Swift, `DeclSyntax` es una estructura que representa una declaración en el código, como una declaración de propiedad, clase o función. Aquí, `declaration` se refiere a una declaración que puede ser una propiedad de una clase, estructura, etc.*
    - `*some`: El uso de `some` implica que el tipo específico no se conoce de manera explícita, pero se sabe que es un tipo que cumple con el protocolo `DeclSyntax`.*
- `*> DeclSyntax`: El método devuelve una nueva declaración modificada, que también debe ser del tipo `DeclSyntax`. Esto significa que la macro tiene la capacidad de modificar una declaración existente, probablemente agregando un getter y un setter para una propiedad.*

*3. `// Genera automáticamente los getters y setters`*

- *Este comentario sugiere que la finalidad principal de la macro es generar automáticamente los getters y setterspara una propiedad, lo cual es un comportamiento común cuando se usan property wrappers en Swift.*
1. *¿Qué hace la macro en este contexto?*
- *Aunque el cuerpo de la macro (`expand`) está vacío en el ejemplo, podemos hacer algunas suposiciones basadas en el nombre y el contexto:*
    - `*AddPropertyWrapper` parece ser una macro destinada a envolver una propiedad en un property wrapper.*
    - *Generar los getters y setters automáticamente: Esto sugiere que la macro agregará automáticamente los métodos de acceso (`get` y `set`) a la propiedad, lo que podría ser útil si se quiere modificar cómo se accede o establece el valor de una propiedad (por ejemplo, validando o modificando valores antes de asignarlos).*
</aside>

## ***1.2 Macro para Logs Automáticos***

Podemos usar una macro para registrar automáticamente las entradas y salidas de una función.

```swift
@Log
func saludar(nombre: String) -> String {
    return "Hola, \(nombre)!"
}
```

Salida esperada:

```swift
func saludar(nombre: String) -> String {
    print("Entrando a la función con parámetro nombre=\(nombre)")
    let resultado = "Hola, \(nombre)!"
    print("Saliendo de la función con resultado=\(resultado)")
    return resultado
}
```

Definición de la macro:

```swift
macro Log: DeclarationMacro {
    static func expand(declaration: some DeclSyntax) -> DeclSyntax {
        // Inserta logs antes y después de la ejecución de la función.
    }
}
```

## ***1.3 Macro para Validación***

Podemos usar macros para validar propiedades.

```swift
@Validate(range: 1...100)
var porcentaje: Int
```

Salida esperada:

Esta macro puede generar automáticamente un setter que asegure que el valor de `porcentaje` esté siempre en el rango especificado.

Definición simplificada:

```swift
macro Validate(range: ClosedRange<Int>): PropertyMacro {
    static func expand(declaration: some DeclSyntax) -> DeclSyntax {
        // Agrega un setter que valida el rango
    }
}
```

# ***2. Uso Práctico***

Las macros son útiles para:

- Reducir código repetitivo, como conformidades a protocolos.
- Crear validaciones o registros automáticamente.
- Generar configuraciones dinámicas en frameworks personalizados.

---