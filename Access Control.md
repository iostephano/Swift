# Access Control

> Administre la visibilidad del código por declaración, archivo y módulo.
> 

En Swift, el Access Control es un mecanismo que permite controlar la visibilidad y el acceso a los componentes de un programa (como clases, estructuras, funciones, propiedades, etc.) desde otros módulos o archivos dentro de un mismo proyecto. Esta característica se utiliza para proteger el código y organizar la exposición de las funcionalidades.

# ***1. Niveles de Access Control en Swift***

1. `open`:
- El nivel más permisivo.
- Permite el acceso desde cualquier módulo, y también la sobrecarga o sobrescritura de clases y métodos.
- Usado principalmente para clases y métodos que están destinados a ser utilizados en otros módulos.

```swift
open class Animal {
    open func makeSound() {
        print("Generic sound")
    }
}

open class Dog: Animal {
    override open func makeSound() {
        print("Woof")
    }
}
```

1.  `public`:
- Permite el acceso desde cualquier módulo, pero no permite la sobrescritura de métodos o la herencia de clases.
- Es menos permisivo que `open` pero sigue permitiendo que se acceda desde otros módulos.

```swift
public class Car {
    public func drive() {
        print("The car is driving")
    }
}
```

1.  **** `internal` (por defecto):
- Es el nivel de acceso predeterminado.
- Permite el acceso dentro del mismo módulo (generalmente dentro de la misma aplicación o framework), pero no desde otros módulos.
- No se puede usar fuera del módulo en que está definido.

```swift
class Person {
    internal func walk() {
        print("Walking")
    }
}
```

1.  `fileprivate`:
- Limita el acceso a la entidad solo dentro del mismo archivo fuente.
- Es útil cuando se desea que diferentes partes del mismo archivo accedan a los mismos recursos sin exponerlos a otros archivo.

```swift
class Counter {
    private var count = 0

    fileprivate func increment() {
        count += 1
    }

    fileprivate func decrement() {
        count -= 1
    }
}
```

1. `private`:
- Restringe el acceso a la entidad dentro de la misma clase o estructura.
- El más restrictivo de todos los niveles de acceso.

```swift
class BankAccount {
    private var balance: Double = 0.0

    private func deposit(amount: Double) {
        balance += amount
    }

    func withdraw(amount: Double) {
        if balance >= amount {
            balance -= amount
        } else {
            print("Insufficient funds")
        }
    }
}
```

# ***2. Usos comunes de Access Control***

- **Encapsulación**: Se usa para ocultar detalles de implementación dentro de una clase o módulo, asegurando que solo se expongan las funcionalidades necesarias.
- **Modularidad**: Facilita el trabajo en equipos y con grandes proyectos, ya que se pueden definir interfaces públicas para las partes externas del código y mantener privadas las internas.
- **Seguridad**: Evita que otros módulos o componentes externos tengan acceso no autorizado a partes críticas del código.
- **Optimización**: Al restringir el acceso, el compilador puede hacer más optimizaciones de rendimiento porque tiene más certeza sobre qué partes del código son mutables y cuáles no.

Consideraciones

- Es importante elegir el nivel de acceso adecuado según el propósito de la clase o el método.
- Se debe evitar usar un acceso más permisivo del necesario, para mantener un diseño robusto y seguro.
- Los accesos más restrictivos, como `private` y `fileprivate`, son útiles para mantener el encapsulamiento y evitar que otras partes del código interfieran de manera inesperada.

Resumen

- `open`: Acceso completo (se puede sobrescribir y heredar).
- `public`: Acceso desde cualquier módulo, pero no se puede sobrescribir ni heredar.
- `internal`: Acceso solo dentro del mismo módulo (predeterminado).
- `fileprivate`: Acceso solo dentro del mismo archivo.
- `private`: Acceso solo dentro de la misma clase/estructura.

Cada uno tiene sus propios casos de uso según cómo quieras organizar tu código y exponer funcionalidades dentro de tu proyecto.

---