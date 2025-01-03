# Basic Operators

> Realiza operaciones como asignación, aritmética, y comparación.
> 

# ***1. Operador de asignación***

El operador de asignación `(=)` se usa para asignar un valor. Al nombre del operando a la izquierda se le asigna el valor del operando a la derecha. En la expresión `a = b`, se inicializa o actualiza el valor de `a` con el valor de `b`:

```swift
let b = 10
var a = 5
 
a = b
// ahora, a es igual a 10
```

Si el lado derecho de la asignación es una tuples con múltiples valores, sus elementos se pueden descomponer en múltiples constantes o variables al mismo tiempo:

```swift
let (x, y) = (1, 2)
// x es igual a 1, y y es igual a 2
```

# ***2. Operadores aritméticos***

Swift soporta los 4 operadores aritméticos estándar para todos los tipos numéricos:

- Suma (+)
- Resta (-)
- Multiplicación (*)
- Division (/)

```swift
var suma = a + b
var resta = a - b
var multiplicacion = a * b
var division = a / b
```

Declaramos el valor de 2 variables y realizamos una operación de suma.

```swift
var a: Int = 5
var b: Int = 10

let suma = a + b
print(suma)   // 15
```

El operador de adición ( + ) también soporta la concatenación de cadenas:

```swift
print("My " + "House")   // My House
```

Debemos incluir los espacios de separación al final del primer texto ”My_”.

## ***2.1 Operador de residuo***

El operador de residuo (`%`) se usa para calcular el residuo de la división de dos valores enteros Int. En la expresión `a % b`, el operador de residuo calcula cuántas veces cabe `b` en `a` y devuelve el valor restante (conocido como residuo).

Sí es como funciona el operador de residuo. Para calcular `9 % 4`, primero se calcula cuántos `4`s caben en un `9`

Es posible insertar dos `4`s en un `9`, y el restante es 1 (la franja color anaranjado).

```swift
	9 % 4   //   Es igual 1
```

![image.png](image.png)

## ***2.2 Operador unario de resta***

El signo de un valor numérico se puede alternar con el prefijo (`-`), conocido como el operador unario de resta:

```swift
let four = 4
let minorFour = -four

// La constante "minorFour", ahora es igual a -4
```

## ***2.3 Operador unario de suma***

El operador unario de suma (`+`) simplemente devuelve el valor de su operando, sin ningún cambio:

```swift
let minorFour = -4
let four = +minorFour

// La constante "four", ahora es igual a 4
```

# ***3. Operadores de asignación compuesta***

Swift ofrece operadores de asignación compuesta, los cuales combinan asignación (`=`) con otra operación. Un ejemplo de esto es el operador de adición asignación (`+=`):

La expresión `a += 2` es la forma concisa de `a = a + 2`. Efectivamente, la adición y la asignación se combinan en un único operador que realiza ambas operaciones al mismo tiempo.

```swift
var a = 1
a += 2
// Ahora "a" es igual a 3
```

# ***4. Operadores de comparación***

Swift cuenta con los siguientes operadores de comparación:

- Igual que ( == )
- No igual que ( != )
- Mayor que ( > )
- Menor que ( < )
- Mayor o igual que ( >= )
- Menor o igual que ( <= )

Cada uno de los operadores de comparación devuelve un valor booleano, para indicar si un enunciado es verdadero `true` o falso `false`:

```swift
1 == 1   // true porque 1 es igual a 1
2 != 1   // true porque 2 no es igual a 1
2 > 1    // true porque 2 es mayor que 1
1 < 2    // true porque 1 es menor que 2
1 >= 1   // true porque 1 es mayor o igual a 1
2 <= 1   // false porque 2 no es menor o igual a 1
```

Puedes comparar dos tuples si estas tienen el mismo tipo y el mismo número de valores. Las tuples se comparan de izquierda a derecha, un valor a la vez, hasta que la comparación encuentra dos valores que no sean iguales. En tal caso, esos dos valores son comparados y el resultado de dicha comparación determinará el resultado general de la comparación de las tuples . Si todos los elementos de ambas tuples son iguales, entonces las tuples son consideradas iguales.

El mecanismo de comparación de izquierda a derecha en la primera línea. Dado que `1` es menor que `2`, `(1, "pantera")` es considerada menor que `(2, "manzana")`, independientemente de cualquier otro valor de las tuples . No importa que `"pantera"` no sea menor que `"manzana"`, porque la comparación ya ha sido determinada por los primeros elementos de los tuples . Sin embargo, cuando los primeros elementos de las tuples son iguales, sus segundos elementos sí son comparados; esto es lo que ocurre en las líneas segunda y tercera.

```swift
(1, "pantera") < (2, "manzana")  // true porque 1 es menor que 2; "pantera" y "manzana" no se comparan
(3, "manzana") < (3, "naranja")  // true porque 3 es igual a 3, y "manzana" es menor que "naranja"
(4, "perro") == (4, "perro")     // true porque 4 es igual a 4, y "perro" es igual a "perro"
```

Las tuples solo pueden ser comparadas mediante un determinado operador si dicho operador puede operar sobre cada valor de las respectivas tuples . Por ejemplo, como se demuestra en el código a continuación, resulta posible comparar dos tuples de tipo String, Int porque tanto los valores de tipo String como los de tipo Int pueden ser comparados mediante el operador `<`. Contrario a esto, dos tuples de tipo String, Int no pueden compararse mediante el operador `<` porque dicho operador no puede operar sobre valores de tipo Bool.

```swift
("azul", -1) < ("morado", 1)        // OK, evalúa a true
("azul", false) < ("morado", true)  // Error porque < no puede comparar valores booleanos
```

# ***5. Operador condicional ternario***

El operador condicional ternario es un operador especial, con tres operandos, el cual toma la forma `pregunta ? respuesta1 : respuesta2`. Es un atajo para evaluar una de las dos expresiones dependiendo si `pregunta` es verdadero o falso. Si el valor de `pregunta` es `true`, el operador evalúa `respuesta1` y devuelve su valor. De lo contrario, el operador evalúa `respuesta2` y devuelve su valor.

El operador condicional ternario es un atajo para el código a continuación:

```swift
if pregunta {
    respuesta1
} else {
    respuesta2
}
```

Acá tenemos un ejemplo, en el que se calcula la altura de la fila de una tabla. La altura de la fila debe ser 50 unidades más alta que la altura de su contenido, si la fila tiene un encabezado, y 20 unidades más alta si la fila no tiene un encabezado:

```swift
let alturaContenido = 40
let tieneEncabezado = true
let alturaFila = alturaContenido + (tieneEncabezado ? 50 : 20)
// alturaFila es igual a 90
```

<aside>
📎

*Este código puede leerse como:*

El código `let alturaFila = alturaContenido + (tieneEncabezado ? 50 : 20)` calcula la altura de una fila, sumando a `alturaContenido` un valor adicional dependiendo de si hay o no un encabezado. En este caso, como `tieneEncabezado` es `true`, se suma `50` (en lugar de `20`), lo que da como resultado que `alturaFila` sea igual a `90`.

</aside>

El ejemplo anterior es una forma concisa del código a continuación:

```swift
let alturaContenido = 40
let tieneEncabezado = true
let alturaFila: Int
 
if tieneEncabezado {
    alturaFila = alturaContenido + 50
} else {
    alturaFila = alturaContenido + 20
}
// alturaFila es igual a 90
```

El uso del operador condicional ternario en el primer ejemplo significa que a `alturaFila` se le puede asignar el valor correcto en una sola línea de código, lo cual es más conciso que el código utilizado en el segundo ejemplo.

El operador condicional ternario proporciona un atajo eficiente para decidir cuál de las dos expresiones considerar. Sin embargo, debes utilizar el operador condicional ternario con cuidado. Abusar de lo conciso puede resultar en un código difícil de leer. Evita combinar múltiples instancias del operador condicional ternario en un mismo enunciado compuesto.

# ***6. Operador nil-coalescing***

El operador nil-coalescing (`a ?? b`) extrae un opcional `a`, si este contiene un valor; o devuelve un valor predeterminado `b`, si `a` es `nil`. La expresión `a` siempre debe ser de tipo opcional. La expresión `b`debe coincidir con el tipo almacenado en `a`.

El operador nil-coalescing es una forma concisa del código a continuación:

```swift
let a: Int? = 5
let b: Int = 10
let result = a != nil ? a! : b // 5
```

<aside>
📎

*Este código puede leerse como:*

1. *Condición: `a != nil`*
    - *Esta es la condición que se evalúa. Verifica si `a` no es `nil`. En este caso, como `a` tiene el valor `5`, la condición `a != nil` es verdadera.*
2. *Resultado si la condición es verdadera: `a!`*
    - *Si `a` no es `nil` (como es el caso), se usa el valor de `a`. El `!` es un desempaquetado forzado que "extrae" el valor de `a` de su envoltorio opcional. Esto es seguro en este caso porque ya hemos comprobado que `a` no es `nil`.*
3. *Resultado si la condición es falsa: `b`*
    - *Si `a` fuera `nil` (lo cual no ocurre en este caso), el valor de `b` sería asignado a `result`.*

*Resumen:*

*En este caso, como `a` es un valor no `nil` (tiene el valor 5), la condición `a != nil` es verdadera, por lo que se desempaqueta el valor de `a` usando `a!` y ese valor se asigna a `result`.* 

</aside>

El siguiente ejemplo, utiliza el operador nil-coalescing para elegir entre un nombre de color predeterminado y un nombre de color opcional, definido por el usuario:

```swift
let nombreColorPredeterminado = "rojo"
var nombreColorDefinidoPorUsuario: String?   // por defecto, resulta en nil
 
var nombreColorAUsar = nombreColorDefinidoPorUsuario ?? nombreColorPredeterminado
// nombreColorDefinidoPorUsuario es nil, por lo que a nombreColorAUsar
// se le asigna el valor predeterminado de "rojo"
```

<aside>
📎

*Este código puede leerse como:*

*La variable `nombreColorDefinidoPorUsuario` se define como un String opcional, con un valor predeterminado de nil. Como el tipo de `nombreColorDefinidoPorUsuario` es opcional, puedes usar el operador nil-coalescing para considerar su valor. En el ejemplo anterior, el operador es utilizado para determinar un valor inicial para una variable de tipo String llamada `nombreColorAUsar`. Dado que `nombreColorDefinidoPorUsuario` es nil,  la expresión `nombreColorDefinidoPorUsuario ?? nombreColorPredeterminado` devuelve el valor de `nombreColorPredeterminado`, es decir, rojo.*

</aside>

Si a `nombreColorDefinidoPorUsuario` le asignas un valor diferente a `nil` y ejecutas la verificación con el operador nil-coalescing nuevamente, el valor contenido por `nombreColorDefinidoPorUsuario`se usará en lugar del predeterminado:

```swift
nombreColorDefinidoPorUsuario = "verde"
 
nombreColorAUsar = nombreColorDefinidoPorUsuario ?? nombreColorPredeterminado
// nombreColorDefinidoPorUsuario no es nil, por lo que a nombreColorAUsar
// se le asigna "verde"
```

# ***7. Operadores de rango***

Swift incluye muchos operadores de rango, los cuales son maneras concisas de expresar un rango de valores.

## ***7.1 Operador de rango cerrado***

El operador de rango cerrado (`a...b`) define un rango que va de `a` a `b`, e incluye los valores `a` y `b`. El valor de `a` no debe ser mayor que el de `b`.

El operador de rango cerrado es útil al iterar sobre un rango, del cual se desean usar todos sus valores, como en el caso de un ciclo `for-in`:

```swift
for indice in 1...5 {
    print("\(indice) multiplicado por 5 es \(indice * 5)")
}
// 1 multiplicado por 5 es 5
// 2 multiplicado por 5 es 10
// 3 multiplicado por 5 es 15
// 4 multiplicado por 5 es 20
// 5 multiplicado por 5 es 25
```

## ***7.2 Operador de rango semiabierto***

El operador de rango semiabierto (`a..<b`) define un rango que va de `a` a `b`, pero que no incluye a `b`. Se considera semiabierto porque contiene su primer valor, pero no a su valor final. Al igual que con el operador de rango cerrado, el valor de `a` no debe ser mayor que el de `b`. Si el valor de `a` es igual a `b`, entonces el rango será un rango vacío.

Los rangos semiabiertos son particularmente útiles al trabajar con listas basadas en cero, como los arrays, donde resulta conveniente contar hasta (pero sin incluir) la longitud de la lista:

```swift
let nombres = ["Ana", "Alejandro", "Cindy", "Laura"]
let conteo = nombres.count
 
for i in 0..<conteo {
    print("La persona #\(i + 1) se llama \(nombres[i])")
}
// La persona #1 se llama Ana
// La persona #2 se llama Alejandro
// La persona #3 se llama Cindy
// La persona #4 se llama Laura
```

Observa que el array contiene cuatro elementos, pero `0..<conteo` solo cuenta hasta `3` (el índice del último elemento en el array), porque es un rango semiabierto.

## ***7.3 Rangos unilaterales***

El operador de rango cerrado cuenta con una forma alternativa para rangos que continúan lo más lejos posible en una dirección; por ejemplo, un rango que incluye todos los elementos de un array desde el índice 2 hasta el final del array . En estos casos, puedes omitir el valor en uno de los lados del operador. A este tipo de rangos se les denomina rangos unilaterales, porque el operador tiene un valor, solamente, en uno de los lados. 

```swift
for nombre in nombres[2...] {
    print(nombre)
}
// Cindy
// Laura
 
for nombre in nombres[...2] {
    print(nombre)
}
// Ana
// Alejandro
// Cindy
```

El operador de rango semiabierto también tiene una forma unilateral, donde solo se escribe su valor final. Al igual que cuando incluyes un valor en ambos lados, el valor final no forma parte del rango.

```swift
for nombre in nombres[..<2] {
    print(nombre)
}
// Ana
// Alejandro
```

Los rangos unilaterales se pueden utilizar en otros contextos, no solo en los subscripts. No puedes iterar sobre un rango unilateral que omita un primer valor, ya que no estaría claro donde debe comenzar la iteración. Aunque sí puedes iterar en un rango unilateral que omita su valor final; sin embargo, como el rango continúa indefinidamente, asegúrate de agregar una condición final explícita para el ciclo. También puedes verificar si un rango unilateral contiene un valor en particular, como se muestra en el código a continuación.

```swift
let rango = ...5
 
rango.contains(7)   // false
rango.contains(4)   // true
rango.contains(-1)  // true
```

# ***8. Operadores lógicos***

Los operadores lógicos modifican o combinan los valores lógicos booleanos `true` y `false`.

- NO (NOT) lógico (`!`)
- Y (AND) lógico (`&&`)
- O (OR) lógico (`||`)

## ***8.1 Operador lógico NO***

El operador lógico NO (`!`) invierte un valor booleano, de manera que `true` se convierte en `false` y `false` se convierte en `true`.

```swift
let entradaPermitida = false
 
if !entradaPermitida {
    print("ACCESO DENEGADO")
}
// Imprime "ACCESO DENEGADO"
```

<aside>
📎

*Este código puede leerse como:*

*La expresión `if !entradaPermitida` se puede leer como «si no entrada permitida». La línea subsiguiente solo se ejecuta si «no entrada permitida» es true; es decir, si `entradaPermitida` es false.*

</aside>

## ***8.2 Operador lógico Y***

El operador lógico Y (`&&`) crea expresiones lógicas, en donde ambos valores deben ser `true` para que toda la expresión sea `true`.

Si cualquiera de los dos valores es `false`, toda la expresión será `false`. De hecho, si el primer valor es `false`, el segundo valor ni siquiera será evaluado, ya que no será posible que este haga que la expresión sea `true`. Esto se conoce como evaluación cortocircuito.

Este ejemplo considera dos valores de tipo Bool y solo permite el acceso si ambos valores son `true`:

```swift
let ingresoCodigoPuerta = true
let aproboEscanerDeRetina = false
 
if ingresoCodigoPuerta && aproboEscanerDeRetina {
    print("¡Bienvenida!")
} else {
    print("ACCESO DENEGADO")
}
// Imprime "ACCESO DENEGADO"
```

## ***8.3 Operador lógico O***

El operador lógico O (`||`) es un operador interfijo formado por dos barras verticales. Se usa para crear expresiones lógicas, en las cuales solo uno de los dos valores tiene que ser `true` para que toda la expresión sea `true`.

En el siguiente ejemplo, el primer valor booleano `tieneLlaveDeLaPuerta` es `false`, pero el segundo valor `conoceClaveMaestra` es `true`. Dado que un valor es `true`, toda la expresión evalúa a `true`, y se permite el acceso:

```swift
let tieneLlaveDeLaPuerta = false
let conoceClaveMaestra = true
 
if tieneLlaveDeLaPuerta || conoceClaveMaestra {
    print("¡Bienvenida!")
} else {
    print("ACCESO DENEGADO")
}
// Imprime "¡Bienvenida!"
```

## ***8.4 Combinación de operadores lógicos***

Puedes combinar múltiples operadores lógicos para crear expresiones compuestas más largas:

```swift
if ingresoCodigoPuerta && aproboEscanerDeRetina || tieneLlaveDeLaPuerta || conoceClaveMaestra {
    print("¡Bienvenida!")
} else {
    print("ACCESO DENEGADO")
}
// Imprime "¡Bienvenida!"
```

Este ejemplo usa múltiples operadores `&&` y `||` para crear una expresión compuesta más larga. Sin embargo, los operadores `&&` y `||` siguen teniendo dos operandos solamente, por lo que son, en realidad, tres expresiones pequeñas unidas entre sí.

## ***8.5 Paréntesis explícitos***

Algunas veces resulta conveniente incluir paréntesis aunque no sea estrictamente necesario, para hacer que la intención de una expresión compleja sea más fácil de leer. En el ejemplo anterior (acceso a la puerta), es útil agregar paréntesis alrededor de la primera parte de la expresión compuesta para hacer que su intención sea explícita:

```swift
if (ingresoCodigoPuerta && aproboEscanerDeRetina) || tieneLlaveDeLaPuerta || conoceClaveMaestra {
    print("¡Bienvenida!")
} else {
    print("ACCESO DENEGADO")
}
// Imprime "¡Bienvenida!"
```

Los paréntesis dejan en claro que los dos primeros valores se consideran como parte de un posible estado, aparte, en la lógica general. El resultado de la expresión compuesta no cambia, pero la intención general es más clara para el lector. Siempre elige la legibilidad sobre la brevedad; usa paréntesis donde estos ayuden a hacer tus intenciones claras.

---