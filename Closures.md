# Closures

> Agrupar el código que se ejecuta juntos, sin crear una función con nombre.
> 

Los closures son bloques de código autocontenidos que puedes pasar y usar en tu código. Los closures tienen funcionalidades similares a las funciones, pero son más ligeros y flexibles. A menudo se usan como callbacks o para tareas que necesitan encapsular lógica para ser ejecutada posteriormente.

# ***1. Características de los Closures***

- Capturan y almacenan referencias a cualquier constante o variable del contexto donde fueron definidos.
- Son funciones anónimas, aunque pueden asignarse a una variable para ser reutilizados.
- Inferencia de tipos, lo que significa que Swift puede deducir su tipo basándose en el contexto.
- Sintaxis compacta, que se vuelve especialmente útil en combinaciones como `map`, `filter`, y `reduce`.

**Sintaxis:**

```swift
{ (parámetros) -> TipoDeRetorno in
    // Código
}
```

```swift
let sumaClosure = { (a: Int, b: Int) -> Int in
    return a + b
}
let resultado = sumaClosure(5, 3) // Resultado: 8
```

# ***2. Closures como Parámetros***

Pueden usarse como parámetros de funciones para personalizar su comportamiento.

```swift
func realizarOperacion(a: Int, b: Int, operacion: (Int, Int) -> Int) -> Int {
    return operacion(a, b)
}

let resultado = realizarOperacion(a: 10, b: 5) { (x, y) -> Int in
    return x * y
}
print(resultado) // Resultado: 50

```

<aside>
📎

*Este código puede leerse como:*

*1. Declaración de la función `realizarOperacion`*

- `*a` y `b`: son dos enteros que se pasan como parámetros a la función.*
- `*operacion`: es un parámetro que recibe una función (o closure). Esta función debe aceptar dos parámetros de tipo `Int` y devolver un `Int`.*
- `*> Int`: indica que la función `realizarOperacion` también devuelve un entero.*
- `*return operacion(a, b)`: ejecuta la función (o closure) `operacion` pasando `a` y `b` como argumentos, y retorna el resultado.*

*2. Llamada a `realizarOperacion` con una closure*

- `*a: 10` y `b: 5`: valores que se pasan a los parámetros `a` y `b`.*
- *Closure: `{ (x, y) -> Int in return x * y }` es una función anónima que se pasa como argumento. Desglosémosla:*
    - `*(x, y)`: define los parámetros de entrada de la closure, que corresponden a `a` y `b`.*
    - `*> Int`: especifica que la closure devuelve un entero.*
    - `*return x * y`: realiza la multiplicación de `x` e `y`.*

*Cuando se ejecuta, `realizarOperacion` reemplaza `operacion(a, b)` con `x * y`, lo que equivale a `10 * 5`.*

*3. Imprimir el resultado*

*El valor calculado es `10 * 5 = 50`, que se guarda en `resultado` y se imprime.*

</aside>

# *3. Optimización de Sintaxis (Trailing Closure)*

Cuando un closure es el último argumento, puedes colocarlo fuera de los paréntesis.

```swift
let numeros = [1, 2, 3, 4, 5]
let numerosDobles = numeros.map { $0 * 2 }
print(numerosDobles) // Resultado: [2, 4, 6, 8, 10]
```

<aside>
📎

*Este código puede leerse como:*

1. *Declaración del array `numeros`:*
- *Aquí se declara una constante llamada `numeros` y se le asigna un array que contiene los números enteros del 1 al 5.*

*2. Uso del método `map`:*

- *El método `map` se utiliza para transformar cada elemento del array original en un nuevo elemento, produciendo un nuevo array.*
- *Dentro de las llaves `{}`, se define la transformación que se aplicará a cada elemento.*
- `*$0` es una forma abreviada de referirse al primer (y único) argumento de la expresión en un cierre (closure).*
- *En este caso, cada elemento del array `numeros` se multiplica por 2, creando un nuevo array donde cada valor es el doble del correspondiente en `numeros`.*

*Ejemplo del proceso interno:*

- *Para el primer elemento, `1`: 1×2=2*
    
    *1×2=2*
    
- *Para el segundo elemento, `2`: 2×2=4*
    
    *2×2=4*
    
- *Y así sucesivamente.*
1. *Impresión del resultado*

*Finalmente, se imprime el contenido de `numerosDobles`, que es el nuevo array: `[2, 4, 6, 8, 10]`.*

</aside>

# *4. Closures que Capturan Valores*

Un closure puede capturar y modificar valores externos.

```swift
func contadorIncremental(inicio: Int) -> () -> Int {
    var total = inicio
    return {
        total += 1
        return total
    }
}

let contador = contadorIncremental(inicio: 10)
print(contador()) // 11
print(contador()) // 12
```

<aside>
📎

*Este código puede leerse como:*

1. *Definición de la función `contadorIncremental`*
- *Esta función toma un parámetro entero llamado `inicio`.*
- *Devuelve una closure (función anónima) que no recibe parámetros (`()`) pero devuelve un entero (`Int`).*

*2. Variable `total`*

- *Se define una variable `total` inicializada con el valor de `inicio`.*
- *Importante: Esta variable se encuentra dentro del alcance de la función, pero también estará accesible para la closure que se devuelve. Esto se llama captura de valores.*
1. *Closure devuelta*
- *Aquí se devuelve una closure.*
- *Esta closure tiene acceso a `total` gracias a la captura de contexto.*
- *Cada vez que se llame a esta closure:*
    
    *Incrementará `total` en 1 (`total += 1`).*
    
    *Retornará el valor actualizado de `total`.*
    
1. *Creación de un contador*
- *Se llama a `contadorIncremental` con `inicio: 10`.*
- *La función devuelve una closure, que es asignada a la constante `contador`.*
- *Esta closure recuerda el valor de `total`, que inicialmente es 10.*
1. *Uso del contador*

*Llamas a `(contador())`* 

- *Dentro de la closure, `total` se incrementa en 1, pasando de 10 a 11.*
- *Luego, la closure devuelve 11, que se imprime.*

*Llamas a `(contador())` nuevamente*

- `*total` se incrementa otra vez, pasando de 11 a 12.*
- *La closure devuelve 12, que se imprime.*

*Conceptos clave*

- *Captura de valores:*
    - *La closure devuelta recuerda y mantiene el estado de la variable `total`, incluso después de que la función `contadorIncremental` haya terminado su ejecución.*
- *Closures como estado:*
    - *En este caso, la closure actúa como un contador que "recuerda" el valor previo y lo actualiza cada vez que se llama.*
- *Ejemplo de uso:*
    - *Este patrón es útil para implementar funciones que mantienen estados internos sin necesidad de usar clases u objetos.*
</aside>

# *5. Closures Escapantes*

Los closures escapantes son aquellos que pueden ejecutarse después de que la función que los recibe haya terminado.

Se marcan con `@escaping`.

```swift
var listaDeTareas: [() -> Void] = []

func agregarTarea(tarea: @escaping () -> Void) {
listaDeTareas.append(tarea)
}

agregarTarea {
print("Tarea 1 completada")
}

agregarTarea {
print("Tarea 2 completada")
}

for tarea in listaDeTareas {
tarea()
}
// Imprime:
// Tarea 1 completada
// Tarea 2 completada

```

<aside>
📎

*Este código puede leerse como:*

1. *Declaración de la variable `listaDeTareas`:*
- *Tipo: Es una lista (array) de funciones sin parámetros que no retornan nada (`() -> Void`).*
- *Propósito: Almacenar funciones que representan las tareas que se desean ejecutar más tarde.*
1. *Función `agregarTarea`:*
- *Parámetro `tarea`: Es una función (o closure) que se pasa como argumento.*
- *Palabra clave `@escaping`: Indica que el closure se guardará para ser ejecutado después, fuera del alcance de la función. Esto es necesario porque el closure se añade a `listaDeTareas`, que vive más allá del ciclo de vida de la función `agregarTarea`.*
1. *Uso de `agregarTarea`:*

*Aquí se crea un closure que imprime `"Tarea 1 completada"`, y este closure se pasa como argumento a `agregarTarea`. La función lo agrega a `listaDeTareas` , Lo mismo ocurre con la segunda llamada.*

1. *Ejecución de las tareas:*
- *Se recorre la lista de tareas con un bucle `for`.*
- *Cada elemento en `listaDeTareas` es un closure, y al invocar `tarea()` se ejecuta el código que contiene.*

*Resultado en consola:*

- *El primer closure imprime `"Tarea 1 completada"`.*
- *El segundo closure imprime `"Tarea 2 completada"`.*

*Este patrón es útil para almacenar y ejecutar acciones de forma diferida. Por ejemplo, en aplicaciones como gestores de tareas o eventos asíncronos, puedes acumular acciones a realizar y ejecutarlas en el momento adecuado.*

</aside>

# *6. Autoclosures*

Son closures implícitos que no requieren una sintaxis explícita al llamarlos. Su uso es común para operaciones diferidas o con condiciones.

```swift
func ejecutarSoloSi(_ condicion: Bool, tarea: @autoclosure () -> Void) {
    if condicion {
        tarea()
    }
}

ejecutarSoloSi(true, tarea: print("Condición cumplida"))
// Imprime: Condición cumplida

```

<aside>
📎

*Este código puede leerse como:*

1. *Declaración de la función*

*Argumentos:*

- `*condicion`: Es un parámetro de tipo `Bool` que determina si se ejecutará la tarea.*
- `*tarea`: Es un argumento que utiliza el atributo `@autoclosure`, lo que significa que la expresión que se pasa como argumento será automáticamente transformada en una clausura sin que el usuario tenga que escribir explícitamente `{}`.*

*¿Qué hace la función?*

- *Verifica si `condicion` es `true`.*
- *Si la condición es verdadera, se ejecuta la expresión proporcionada en `tarea`.*
1. *Uso del atributo `@autoclosure`* 

*El atributo `@autoclosure` convierte automáticamente una expresión en una clausura. Esto hace que el código sea más limpio y más fácil de leer. Sin este atributo, tendrías que escribir explícitamente la clausura al llamar a la función.*

*3. Ventajas de `@autoclosure`*

- *Hace que el código sea más limpio y legible.*
- *Permite posponer la evaluación de expresiones hasta que realmente se necesiten, lo cual puede mejorar el rendimiento en algunos casos.*

*4. Casos de uso comunes*

- *Validaciones condicionales.*
- *Implementaciones de operadores como `??` (Nil coalescing).*
- *Código donde quieres retrasar la ejecución de una expresión hasta que sea estrictamente necesaria.*
</aside>

***Usos Comunes***

1. *Callbacks en programación asíncrona (por ejemplo, en `URLSession` o `completion handlers`).*
2. *Procesamiento de colecciones (`map`, `filter`, `reduce`, etc.).*
3. *Configuración diferida.*
4. *Encapsular lógica temporal (como en temporizadores o tareas diferidas).*

---