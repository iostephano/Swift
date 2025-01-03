# Methods

> Definir y llamar a funciones que forman parte de una instancia o tipo.
> 

Los métodos son funciones asociadas a una clase, estructura o enumeración. Estas funciones permiten manipular y realizar acciones específicas sobre instancias de estos tipos o incluso sobre el propio tipo si se declaran como métodos estáticos.

# ***1. Tipos de Métodos***

## ***1.1 Métodos de instancia***

Son funciones que operan en una instancia específica de una clase, estructura o enumeración.

- Se accede mediante una instancia.
- Usan `self` para referirse a la propia instancia.

```swift
class Persona {
    var nombre: String
    var edad: Int
    
    init(nombre: String, edad: Int) {
        self.nombre = nombre
        self.edad = edad
    }
    
    // Método de instancia
    func saludar() -> String {
        return "Hola, me llamo \(self.nombre) y tengo \(self.edad) años."
    }
}

let persona = Persona(nombre: "Carlos", edad: 30)
print(persona.saludar()) // Hola, me llamo Carlos y tengo 30 años.
```

## ***1.2 Métodos estáticos o de tipo***

Son funciones que pertenecen al propio tipo, no a una instancia específica.

- Se declaran con la palabra clave `static` o `class`.
- Se llaman directamente desde el tipo.

```swift
class Calculadora {
    static func sumar(_ a: Int, _ b: Int) -> Int {
        return a + b
    }
}

let resultado = Calculadora.sumar(5, 7)
print(resultado) // 12
```

## ***1.3 Métodos mutantes (mutating)***

Se usan en estructuras o enumeraciones para modificar sus propiedades.

- Las estructuras y enumeraciones son tipos **inmutables por defecto**.
- Necesitan la palabra clave `mutating` para permitir cambios.

```swift
struct Contador {
    var valor: Int = 0
    
    mutating func incrementar() {
        valor += 1
    }
}

var contador = Contador()
contador.incrementar()
print(contador.valor) // 1
```

# ***2. Propiedades Computadas y Métodos Relacionados***

Las propiedades computadas pueden ser usadas junto con métodos para realizar cálculos o acciones específicas.

```swift
struct Rectangulo {
    var ancho: Double
    var alto: Double
    
    var area: Double {
        return ancho * alto
    }
    
    mutating func cambiarDimensiones(ancho: Double, alto: Double) {
        self.ancho = ancho
        self.alto = alto
    }
}

var rect = Rectangulo(ancho: 10, alto: 5)
print(rect.area) // 50
rect.cambiarDimensiones(ancho: 20, alto: 10)
print(rect.area) // 200
```

# ***3. Parámetros y Retorno en Métodos***

- Los métodos pueden aceptar parámetros y devolver valores, como cualquier función normal.
- Puedes usar nombres externos de parámetros para mayor claridad.

```swift
class Coche {
    var velocidad: Int = 0
    
    func acelerar(aumento: Int) {
        velocidad += aumento
    }
    
    func velocidadActual() -> String {
        return "La velocidad actual es \(velocidad) km/h."
    }
}

let coche = Coche()
coche.acelerar(aumento: 20)
print(coche.velocidadActual()) // La velocidad actual es 20 km/h.
```

# ***4. Métodos y Self***

- Dentro de los métodos de instancia, puedes usar `self` para referirte a la propia instancia.
- Esto es útil cuando necesitas diferenciar entre nombres de parámetros y propiedades.

```swift
class Animal {
    var nombre: String
    
    init(nombre: String) {
        self.nombre = nombre
    }
    
    func presentarse() {
        print("Soy un animal y me llamo \(self.nombre).")
    }
}

let gato = Animal(nombre: "Michi")
gato.presentarse() // Soy un animal y me llamo Michi.
```

# ***5. Encadenamiento de Métodos***

- Puedes invocar múltiples métodos en una misma línea si el método retorna la propia instancia (técnica llamada Method Chaining).

```swift
class Cadena {
    var texto: String = ""
    
    func agregar(_ str: String) -> Cadena {
        texto += str
        return self
    }
    
    func imprimir() {
        print(texto)
    }
}

let cadena = Cadena()
cadena.agregar("Hola, ").agregar("mundo!").imprimir()
// Hola, mundo!
```

# ***6. Configuraciones Adicionales***

## ***6.1 Sobrecarga de métodos***

Puedes definir múltiples métodos con el mismo nombre, pero diferentes parámetros.

```swift
class Matematicas {
    func sumar(_ a: Int, _ b: Int) -> Int {
        return a + b
    }
    
    func sumar(_ a: Double, _ b: Double) -> Double {
        return a + b
    }
}

let matematicas = Matematicas()
print(matematicas.sumar(5, 10))      // 15
print(matematicas.sumar(3.5, 2.5))  // 6.0
```

## ***6.2 Métodos predeterminados (default methods)***

Puedes proporcionar valores por defecto para parámetros.

```swift
class Bienvenida {
    func saludar(nombre: String = "Amigo") {
        print("¡Hola, \(nombre)!")
    }
}

let bienvenida = Bienvenida()
bienvenida.saludar()            // ¡Hola, Amigo!
bienvenida.saludar(nombre: "Luis") // ¡Hola, Luis!
```

***Conclusión***

Los métodos en Swift son fundamentales para encapsular comportamientos dentro de tipos. Con opciones como métodos de instancia, de tipo, mutantes, y con capacidades como sobrecarga y encadenamiento, puedes diseñar sistemas altamente flexibles y reutilizables.

---