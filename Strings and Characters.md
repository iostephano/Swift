# Strings and Characters

> Almacena y manipula textos.
> 

# ***1. Literales de cadena***

Puedes incluir valores predeterminados de tipo String en tu código como «literales de cadena». Un literal de cadena es una secuencia de caracteres encerrada en comillas dobles (`"`)

Usa un literal de cadena como el valor inicial para una constante o variable.

```swift
let algunaCadena = "Un valor cualquiera para un literal de cadena"
```

Swift infiere un valor de tipo String para la constante `algunaCadena` ya que esta se inicializó con un valor literal de cadena.

## ***1.1 Literales de cadena de varias líneas***

Si tu literal de cadena necesita múltiples líneas, usa un literal de cadena de varias líneas: una secuencia de caracteres rodeada por tres comillas dobles (`"""`)

```swift
let cita = """
El Conejo Blanco se puso sus lentes. «¿Por dónde debo empezar,
con la venia de Su Majestad?», preguntó.
 
«Empieza por el principio», dijo el rey con gravedad, «y sigue
hasta llegar al final; allí te detienes.
"""
```

Cuando tu código fuente incluya saltos de línea dentro de un literal de cadena de varias líneas, dichos saltos de línea también formarán parte del valor de la cadena. Si quieres usar saltos de línea para hacer que tu código fuente resulte más legible, pero no quieres que estos formen parte parte del valor de la cadena, escribe una barra invertida (`\`) al final de cada línea.

```swift
let citaModificada = """
El Conejo Blanco se puso sus lentes. «¿Por dónde debo empezar, \
con la venia de Su Majestad?», preguntó.
 
«Empieza por el principio», dijo el rey con gravedad, «y sigue \
hasta llegar al final; allí te detienes."
"""
```

## ***1.2 Caracteres especiales en literales de cadena***

Los literales de cadena pueden incluir los siguientes caracteres especiales:

- Los caracteres especiales de escape: `\0` (carácter nulo), `\\` (barra invertida), `\t` (tabulador), `\n`(salto de línea), `\r` (retorno de carro), `\"` (comilla doble) y `\'` (comilla simple).
- Un valor escalar Unicode arbitrario, escrito como `\u{_n_}`, donde `n` es un número hexadecimal, de uno a ocho dígitos Unicode.

El código a continuación muestra cuatro ejemplos de estos caracteres especiales. La constante `palabrasSabias` contiene dos comillas dobles de escape.

Las constantes `signoDolar`, `corazonNegro`, y `corazonBrillante` demuestran el formato escalar de Unicode.

```swift
let palabrasSabias = "\"La imaginación es más importante que el conocimiento.\" — Einstein"
// "La imaginación es más importante que el conocimiento." — Einstein
let signoDolar = "\u{24}"           // $,  Escalar Unicode U+0024
let corazonNegro = "\u{2665}"       // ♥,  Escalar Unicode U+2665
let corazonBrillante = "\u{1F496}"  // 💖, Escalar Unicode U+1F496
```

# ***2. Inicializando una cadena vacía***

Para crear una cadena vacía como punto inicial para construir una cadena más larga, bien puedes asignar un literal de cadena vacío a una variable o inicializar una nueva instancia del tipo String  mediante sintaxis de inicializador.

```swift
var cadenaVacia = ""            // literal de cadena vacío
var otraCadenaVacia = String()  // sintaxis de inicializador
// Estas dos cadenas están vacías y son equivalentes entre sí.
```

Verifica si un valor de tipo String está vacío, al evaluar su propiedad booleana `.isEmpty`

```swift
if cadenaVacia.isEmpty {
    print("Nada que ver por aquí.")
}
// Imprime "Nada que ver por aquí."
```

# ***3. Mutabilidad de una cadena***

Para indicar si una cadena en particular puede ser modificada (es decir, para hacerla «mutable»), puedes asignarla a una variable (en cuyo caso, podrá ser modificada), o a una constante (en cuyo caso, no podrá ser modificada).

```swift
var cadenaVariable = "Caballo"
 
cadenaVariable += " y carruaje"
// Ahora, cadenaVariable es "Caballo y carruaje"
 
let cadenaConstante = "Highlander"
 
cadenaConstante += " y otro Highlander"
// Esto resulta en un error en tiempo de compilación:
// una cadena constante no puede ser modificada
```

# ***4. Trabajando con caracteres***

Puedes crear una constante o variable individual de tipo Character a partir de un literal de cadena, con un solo carácter, agregando una anotación de tipo Character.

```swift
let signoDeExclamacion: Character = "!"
```

Los valores de tipo String se pueden construir pasando un array de valores de tipo Character como un argumento para su inicializador.

```swift
let caracteresGato: [Character] = ["¡", "G", "a", "t", "o", "!", " ", "🐱"]
let cadenaGato = String(caracteresGato)
 
print(cadenaGato)
// Imprime "¡Gato! 🐱"
```

Puedes acceder a los valores individuales de tipo Character en una cadena al iterar sobre la misma mediante un ciclo `for-in` .

```swift
for caracter in "¡Perro! 🐶" {
    print(caracter)
}
// ¡
// P
// e
// r
// r
// o
// !
//
// 🐶
```

# ***5. Concatenación de cadenas y caracteres***

Puedes juntar (o «concatenar») valores de tipo String con el operador de adición (`+`) para crear una nueva cadena.

```swift
let cadena1 = "Buenos"
let cadena2 = " días"
var saludo = cadena1 + cadena2
// Ahora, saludo es igual a "Buenos días"
```

También puedes agregar un valor de tipo String a una variable existente, de tipo String mediante el operador de adición-asignación (`+=`).

```swift
var instruccion = "deletrea la palabra"
instruccion += cadena2
// Ahora, instruccion es igual a "deletrea la palabra días"
```

Si estás usando literales de cadena de varias líneas para componer las líneas de una cadena más larga, querrás que cada línea de la cadena finalice con un salto de línea, incluyendo la última línea.

Puedes agregar un valor de tipo Character a una variable String usando el método `.append()` del tipo String:

```swift
let punto: Character = "."
 
saludo.append(punto)
// Ahora, saludo es igual a "Buenos días."
```

```swift
let malComienzo = """
    uno
    dos
    """
let final = """
    tres
    """
 
print(malComienzo + final)
// Imprime dos líneas:
// uno
// dostres
 
let buenComienzo = """
    uno
    dos
 
    """
 
print(buenComienzo + final)
// Imprime tres líneas:
// uno
// dos
// tres
```

# ***6. Interpolación de cadenas***

La interpolación de cadenas es una forma de crear nuevos valores de tipo String a partir de la combinación de constantes, variables, literales, y expresiones, al incluir sus valores en un literal de cadena. Puedes usar la interpolación de cadenas tanto para literales de cadena de una sola línea como para aquellos de varias líneas. Cada elemento que quieras insertar en el literal de cadena, va rodeado por paréntesis y precedido por una barra invertida (`\`):

```swift
let multiplicador = 3
let mensaje = "\(multiplicador) por 2.5 es \(Double(multiplicador) * 2.5)"
// mensaje es "3 por 2.5 es 7.5"
```

<aside>
📎

*Este código puede leerse como:*

1. *El valor de `multiplicador` se inserta en un literal de cadena como `\(multiplicador)`. Este marcador de posición («placeholder») es reemplazado por el valor real de `multiplicador` al momento de evaluar la interpolación de cadenas para crear una nueva cadena.*
2. *El valor de `multiplicador` también forma parte de una expresión más larga, más adelante en la cadena. Esta expresión calcula el valor de `Double(multiplicador) * 2.5` e inserta el resultado (`7.5`) en la cadena. En este caso, la expresión se escribe como `\(Double(multiplicador) * 2.5)` a la hora de incluirla en el literal de cadena.*
</aside>

Puedes usar delimitadores de cadena extendidos para crear cadenas que contengan caracteres que, de otra manera, serían tratados como interpolación de cadenas.

```swift
print(#"Escribe una cadena interpolada en Swift usando \(multiplicador)."#)
// Imprime "Escribe una cadena interpolada en Swift usando \(multiplicador)."
```

# ***7. Unicode***

Unicode es un estándar internacional para codificar, representar, y procesar texto en diferentes sistemas de escritura. Unicode permite representar casi cualquier carácter de cualquier idioma en una forma estandarizada, así como leer y escribir esos caracteres desde y hacia una fuente externa, como un archivo de texto o una página web. Los tipos String y Character de Swift son totalmente compatibles con Unicode.

# ***8. Conteo de caracteres***

Para obtener la cuenta de valores tipo Character en una cadena, usa la propiedad `.count` de la cadena:

```swift
let animalesDomesticos = "Gato 🐈, Perro 🐕, Vaca 🐄, Caballo 🐎"
 
print("animalesDomesticos tiene \(animalesDomesticos.count) caracteres")
// Imprime "animalesDomesticos tiene 34 caracteres"
```

# ***9. Comparación de cadenas***

Swift ofrece tres formas de comparar valores textuales: igualdad de cadenas y caracteres, igualdad de prefijo, e igualdad de sufijo.

## ***9. 1 Igualdad de cadenas y caracteres***

La igualdad de cadenas y caracteres se verifica mediante los operadores «igual que» (`==`) y «no igual que» (`!=`).

```swift
let frase = "Somos muy parecidos. Tú y yo."
let mismaFrase = "Somos muy parecidos. Tú y yo."
 
if frase == mismaFrase {
    print("Estas dos cadenas son consideradas iguales.")
}
// Imprime "Estas dos cadenas son consideradas iguales."
```

## ***9.2 Igualdad de prefijo y sufijo***

Para verificar si una cadena tiene un prefijo o sufijo de cadena en particular, llama a los métodos `hasPrefix(_:)` y `hasSuffix(_:)` de la cadena, ambos de los cuales toman un solo argumento de tipo Character y devuelven un valor booleano.

Los ejemplos a continuación consideran un array de cadenas que representan las ubicaciones de las escenas de los dos primeros actos de la obra de Shakespeare, «Romeo y Julieta»:

```swift
let romeoYJulieta = [
    "Acto 1 Escena 1: Verona. Una plaza pública.",
    "Acto 1 Escena 2: La mansión Capuleto.",
    "Acto 1 Escena 3: Un cuarto en la mansión Capuleto.",
    "Acto 1 Escena 4: Una calle afuera de la mansión Capuleto.",
    "Acto 1 Escena 5: El Gran Salón en la mansión Capuleto.",
    "Acto 2 Escena 1: Afuera de la mansión Capuleto.",
    "Acto 2 Escena 2: El jardín de Capuleto.",
    "Acto 2 Escena 3: Afuera de la celda del hermano Lorenzo.",
    "Acto 2 Escena 4: Una calle en Verona.",
    "Acto 2 Escena 5: La mansión Capuleto.",
    "Acto 2 Escena 6: La celda del hermano Lorenzo."
]
```

Puedes usar el método `.hasPrefix()` con el array `romeoYJulieta` para contar el número de escenas en el Acto 1 de la obra:

```swift
var conteoDeEscenasDelActo1 = 0
 
for escena in romeoYJulieta {
    if escena.hasPrefix("Acto 1 ") {
        conteoDeEscenasDelActo1 += 1
    }
}
 
print("Hay \(conteoDeEscenasDelActo1) escenas en el Acto 1.")
// Imprime "Hay 5 escenas en el Acto 1."
```

De manera similar, usa el método `.hasSuffix()` para contar el número de escenas que tienen lugar en o cerca de la mansión Capuleto y de la celda del hermano Lorenzo:

```swift
var conteoMansion = 0
var conteoCelda = 0
 
for escena in romeoYJulieta {
    if escena.hasSuffix("mansión Capuleto.") {
        conteoMansion += 1
    } else if escena.hasSuffix("celda del hermano Lorenzo.") {
        conteoCelda += 1
    }
}
 
print("\(conteoMansion) escenas en la mansión; \(conteoCelda) escenas en la celda")
// Imprime "6 escenas en la mansión; 2 escenas en la celda"
```

---