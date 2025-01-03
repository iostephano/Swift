# Nested Types

> Definir tipos dentro del alcance de otro tipo.
> 

En Swift, los Nested Types (Tipos Anidados) permiten declarar clases, estructuras o enumeraciones dentro del contexto de otra clase, estructura o enumeración. Esto ayuda a organizar el código de manera lógica y modular, especialmente cuando un tipo solo tiene sentido en el contexto de otro.

# ***1. Casos de Uso Comunes***

- Agrupación Lógica: Si un tipo solo tiene relevancia dentro de otro tipo.
- Encapsulación: Para ocultar detalles de implementación de los tipos externos.
- Modelado jerárquico: Cuando los datos o comportamientos tienen una relación jerárquica.

# ***2. Básico de Tipos Anidados***

```swift
struct Contenedor {
    // Definimos un tipo anidado dentro de la estructura
    struct Elemento {
        var nombre: String
        var valor: Int
    }
    
    var elementos: [Elemento]
    
    mutating func agregarElemento(nombre: String, valor: Int) {
        let nuevoElemento = Elemento(nombre: nombre, valor: valor)
        elementos.append(nuevoElemento)
    }
}

// Uso del tipo anidado
var contenedor = Contenedor(elementos: [])
contenedor.agregarElemento(nombre: "Elemento1", valor: 10)
contenedor.agregarElemento(nombre: "Elemento2", valor: 20)

print(contenedor.elementos)
// [Elemento(nombre: "Elemento1", valor: 10), Elemento(nombre: "Elemento2", valor: 20)]
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición de la estructura `Contenedor`:*

- `*struct Contenedor`: Se define una estructura llamada `Contenedor`. Una estructura en Swift es un tipo de datos que puede contener propiedades y métodos.*
- `*struct Elemento`: Dentro de la estructura `Contenedor`, se define otra estructura llamada `Elemento`. Esta estructura tiene dos propiedades:*
    - `*nombre`: una cadena de texto (`String`), que representa el nombre del elemento.*
    - `*valor`: un número entero (`Int`), que representa el valor asociado con el elemento.*
- `*var elementos: [Elemento]`: La estructura `Contenedor` tiene una propiedad llamada `elementos`, que es un array de elementos (`Elemento`). Esto significa que un contenedor puede almacenar varios elementos.*
- `*mutating func agregarElemento(nombre: String, valor: Int)`: Este es un método de la estructura `Contenedor`, y está marcado con la palabra clave `mutating` porque modifica el estado del objeto (en este caso, agrega elementos al array `elementos`). El método recibe dos parámetros: `nombre` y `valor`, los cuales se usan para crear un nuevo `Elemento`. Luego, el nuevo elemento se agrega al array `elementos`.*

*2. Uso de la estructura `Contenedor`:*

- `*var contenedor = Contenedor(elementos: [])`: Se crea una instancia de la estructura `Contenedor` llamada `contenedor`. Inicialmente, el array `elementos` está vacío (`[]`).*
- `*contenedor.agregarElemento(nombre: "Elemento1", valor: 10)`: Se llama al método `agregarElemento` para agregar un nuevo `Elemento` con `nombre = "Elemento1"` y `valor = 10` al array `elementos` del `contenedor`.*
- `*contenedor.agregarElemento(nombre: "Elemento2", valor: 20)`: Se llama nuevamente al método `agregarElemento` para agregar otro `Elemento`, este con `nombre = "Elemento2"` y `valor = 20`.*
- `*print(contenedor.elementos)`: Finalmente, se imprime el contenido del array `elementos` del `contenedor`.*
- *El resultado será: [Elemento(nombre: "Elemento1", valor: 10), Elemento(nombre: "Elemento2", valor: 20)]*
- *Esto muestra que el contenedor ahora contiene dos elementos, cada uno con un nombre y valor asignados.*

*Resumen:*

- *El código define una estructura `Contenedor` que puede almacenar múltiples `Elemento`s. Cada `Elemento` tiene un nombre y un valor. A través del método `agregarElemento`, puedes agregar nuevos elementos al contenedor. El ejemplo crea un contenedor, le agrega dos elementos, y luego imprime los elementos almacenados en él.*
</aside>

# ***3. Tipos Anidados en Enumeraciones***

```swift
enum Juego {
    enum Nivel {
        case fácil
        case intermedio
        case difícil
    }
    
    enum Resultado {
        case victoria
        case derrota
        case empate
    }
    
    var nivel: Nivel
    var resultado: Resultado
}

// Crear una instancia usando los tipos anidados
let partida = Juego(nivel: .intermedio, resultado: .victoria)
print(partida.nivel)      // intermedio
print(partida.resultado)  // victoria
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición de la enum principal (`Juego`):*

- *En esta parte del código, tenemos la declaración de un enum principal llamado `Juego`. Dentro de `Juego`, hay dos enums anidados: `Nivel` y `Resultado`.*
- `*Nivel`: Define los niveles de dificultad de un juego. Tiene tres casos posibles:*
    - `*fácil*`
    - `*intermedio*`
    - `*difícil*`
- `*Resultado`: Define los posibles resultados de una partida. Tiene tres casos posibles:*
    - `*victoria*`
    - `*derrota*`
    - `*empate*`
- *Además de estos enums, dentro de `Juego` hay dos propiedades:*
    - `*nivel`: Es una propiedad de tipo `Nivel`, que almacenará el nivel de dificultad de una partida.*
    - `*resultado`: Es una propiedad de tipo `Resultado`, que almacenará el resultado de la partida.*

*2. Creación de una instancia de `Juego`:*

- *En esta línea de código, se crea una instancia de la estructura `Juego`, llamada `partida`. El constructor de `Juego` requiere dos parámetros:*
    - `*nivel`: Se le asigna el valor `.intermedio`, que hace referencia al caso `intermedio` dentro del enum `Nivel`.*
    - `*resultado`: Se le asigna el valor `.victoria`, que hace referencia al caso `victoria` dentro del enum `Resultado`.*
- *Así, la instancia `partida` representa un juego con nivel "intermedio" y resultado "victoria".*

*3. Impresión de los valores:*

- *Finalmente, se imprimen los valores de las propiedades `nivel` y `resultado` de la instancia `partida`.*
    - `*partida.nivel` imprimirá el valor de la propiedad `nivel`, que es `.intermedio`.*
    - `*partida.resultado` imprimirá el valor de la propiedad `resultado`, que es `.victoria`.*

*Resumen:*

- *El código define una estructura `Juego` con dos enums anidados (`Nivel` y `Resultado`) que representan el nivel de dificultad y el resultado de una partida, respectivamente. Luego, crea una instancia de `Juego` con un nivel intermedio y un resultado de victoria, y finalmente imprime esos valores.*
</aside>

# ***4. Anidación en Clases***

```swift
class Biblioteca {
    class Libro {
        var titulo: String
        var autor: String
        
        init(titulo: String, autor: String) {
            self.titulo = titulo
            self.autor = autor
        }
    }
    
    private var libros: [Libro] = []
    
    func agregarLibro(titulo: String, autor: String) {
        let nuevoLibro = Libro(titulo: titulo, autor: autor)
        libros.append(nuevoLibro)
    }
    
    func listarLibros() {
        for libro in libros {
            print("\(libro.titulo) por \(libro.autor)")
        }
    }
}

// Uso de la clase anidada
let biblioteca = Biblioteca()
biblioteca.agregarLibro(titulo: "El Principito", autor: "Antoine de Saint-Exupéry")
biblioteca.agregarLibro(titulo: "1984", autor: "George Orwell")
biblioteca.listarLibros()
// Salida:
// El Principito por Antoine de Saint-Exupéry
// 1984 por George Orwell
```

<aside>
📎

*Este código puede leerse como:*

*1. Clase `Libro` (Clase anidada)*

- *Propiedades: La clase `Libro` tiene dos propiedades: `titulo` y `autor`, ambas de tipo `String`. Estas propiedades almacenan la información del título y el autor del libro.*
- *Inicializador (`init`): El inicializador toma dos parámetros, `titulo` y `autor`, y asigna estos valores a las propiedades correspondientes usando `self`. El uso de `self` es necesario para distinguir las propiedades de la clase de los parámetros del inicializador.*

*2. Clase `Biblioteca`*

- *Propiedades: La clase `Biblioteca` tiene una propiedad privada llamada `libros`, que es un arreglo de objetos `Libro`. Al ser privada (`private`), solo es accesible dentro de la clase `Biblioteca`, lo que ayuda a proteger el estado interno de la clase.*
- *Método `agregarLibro`: Este método permite agregar libros a la biblioteca. Toma dos parámetros (`titulo` y `autor`), crea un nuevo objeto `Libro` usando estos valores, y luego lo agrega al arreglo `libros`.*
- *Método `listarLibros`: Este método recorre el arreglo `libros` y, para cada libro, imprime su título y autor en la consola en el formato: "Título por Autor".*
1. *Uso de las clases:*
- *Creación de una instancia de `Biblioteca`: Se crea una instancia de la clase `Biblioteca` llamada `biblioteca`.*
- *Agregar libros: Se agregan dos libros a la biblioteca usando el método `agregarLibro`. El primer libro tiene como título "El Principito" y autor "Antoine de Saint-Exupéry". El segundo libro es "1984" de "George Orwell".*
- *Listar libros: Se llama al método `listarLibros`, que imprime la lista de libros en la biblioteca. El resultado sería:*

*Resumen:*

- *Este código crea una biblioteca que puede almacenar libros, cada uno con un título y un autor, y luego muestra los libros almacenados. La clase `Libro` es anidada dentro de la clase `Biblioteca`, lo que significa que solo puede ser utilizada dentro de esa clase, aunque en este caso es simplemente una forma de organizar mejor el código.*
</aside>

# ***5. Acceso a Tipos Anidados***

Para acceder a un tipo anidado desde fuera de su contenedor, se utiliza la notación de punto:

```swift
let tipoAnidado = Contenedor.Elemento(nombre: "Nuevo", valor: 5)
print(tipoAnidado) // Elemento(nombre: "Nuevo", valor: 5)

```

<aside>
📎

*Este código puede leerse como:*

1. Instancia`let tipoAnidado = Contenedor.Elemento(nombre: "Nuevo", valor: 5)`
- En esta línea se está creando una instancia de un tipo de datos llamado `Elemento`. Sin embargo, `Elemento` está anidado dentro de una estructura o clase llamada `Contenedor`.
- La sintaxis `Contenedor.Elemento` indica que `Elemento` es un tipo (probablemente una estructura o clase) que está definido dentro de otro tipo llamado `Contenedor`. Esto es una forma de organización en Swift, donde puedes tener tipos de datos anidados (es decir, un tipo dentro de otro tipo).
- La instancia de `Elemento` se crea con dos parámetros:
    - `nombre: "Nuevo"`: El parámetro `nombre` recibe el valor `"Nuevo"`.
    - `valor: 5`: El parámetro `valor` recibe el valor `5`.
- El resultado de esta línea es que se crea una instancia de `Elemento` con el nombre `"Nuevo"` y el valor `5`, y esta instancia se guarda en la variable `tipoAnidado`.
1. Print
- Aquí se imprime el contenido de `tipoAnidado` en la consola.
- El valor que se imprime será una descripción del objeto `tipoAnidado`. En este caso, el objeto es una instancia de `Elemento`, y Swift proporciona una representación textual del mismo. El valor impreso es:
- Esto significa que el objeto `tipoAnidado` es una instancia de la estructura o clase `Elemento` con los valores correspondientes para las propiedades `nombre` y `valor`.

Resumen:

- El código crea un tipo anidado `Elemento` dentro de `Contenedor` y lo inicializa con un nombre y un valor.
- Luego, imprime la instancia creada de `Elemento`, mostrando sus propiedades.
- Este tipo de estructura es común cuando se desea organizar y agrupar tipos de datos relacionados en Swift, y la anidación permite tener una jerarquía clara de cómo se organizan los tipos.
</aside>

***Conclusión***

Los Nested Types en Swift son una herramienta poderosa para organizar código relacionado, reducir el desorden y mejorar la claridad. Son especialmente útiles en casos donde la relación entre tipos es jerárquica o lógica.

---