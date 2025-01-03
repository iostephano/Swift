# Concurrency

> Realizar operaciones asíncronas.
> 

# ***1. Introducción al modelo de concurrencia moderno de Swift***

El modelo moderno de concurrencia en Swift (introducido en Swift 5.5) está diseñado para simplificar el manejo de tareas concurrentes. Las principales características son:

- `async` y `await`: Para escribir código asíncrono de forma legible y secuencial.
- `Task` y `TaskGroup`: Para estructurar tareas concurrentes.
- `Actor`: Para gestionar estados compartidos de forma segura.
- `MainActor`: Para trabajar con actualizaciones en la interfaz de usuario (UI).
- Integración con APIs heredadas como Grand Central Dispatch (GCD).

# ***2. Ejemplo básico: Async y Await***

Características principales:

- `fetchUserData` y `fetchPostsData` son funciones asíncronas que simulan operaciones que toman tiempo.
- `loadUserDetails` coordina ambas operaciones y las ejecuta secuencialmente.

```swift
import Foundation

// Simula una tarea asíncrona como una llamada de red
func fetchUserData(userId: String) async -> String {
    try? await Task.sleep(nanoseconds: 2 * 1_000_000_000) // Espera 2 segundos
    return "Datos del usuario \(userId)"
}

func fetchPostsData(userId: String) async -> String {
    try? await Task.sleep(nanoseconds: 1 * 1_000_000_000) // Espera 1 segundo
    return "Posts del usuario \(userId)"
}

// Función que combina ambas operaciones
func loadUserDetails(userId: String) async {
    print("Cargando datos del usuario...")
    let userData = await fetchUserData(userId: userId)
    let postsData = await fetchPostsData(userId: userId)
    print("Completado: \(userData) y \(postsData)")
}

// Llamada a la función
Task {
    await loadUserDetails(userId: "123")
}
```

<aside>
📎

*Este código puede leerse como:*

*1. Importación de Foundation*

- *La importación de `Foundation` permite el uso de muchas funcionalidades útiles en Swift, como las operaciones asincrónicas, la manipulación de fechas y tiempos, y más.*

*2. Función `fetchUserData`* 

- *Objetivo: Esta función simula una llamada de red para obtener los datos de un usuario.*
- *Parámetro: `userId` (un identificador único de usuario).*
- `*async`: La función es asíncrona, lo que significa que puede ejecutarse en segundo plano sin bloquear el hilo principal.*
- `*await`: La palabra clave que se usa para esperar el resultado de una tarea asincrónica. En este caso, se espera 2 segundos.*
- `*Task.sleep(nanoseconds:)`: Simula un retraso en la ejecución, en este caso, la función esperará durante 2 segundos (2 segundos = 2 * 1,000,000,000 nanosegundos).*
- `*try?`: Se utiliza para capturar errores de forma opcional. En este caso, si la tarea de espera falla, el error se ignora (se hace de manera segura).*
- *Retorno: Devuelve un mensaje que contiene los "datos del usuario".*

*3. Función `fetchPostsData`*

- *Objetivo: Similar a la función anterior, esta función simula la obtención de publicaciones del usuario.*
- *Espera: En lugar de 2 segundos, esta función espera 1 segundo (1 segundo = 1 * 1,000,000,000 nanosegundos).*
- *Retorno: Devuelve un mensaje con los "posts del usuario".*

*4. Función `loadUserDetails`*

- *Objetivo: Esta función coordina ambas operaciones asincrónicas (`fetchUserData` y `fetchPostsData`).*
- *Flujo:*
    - *Se imprime el mensaje `"Cargando datos del usuario..."` para indicar que se está iniciando el proceso.*
    - *Se llama a `fetchUserData`, lo cual se hace de manera asíncrona. `await` garantiza que el código espere a que la tarea se complete antes de continuar.*
    - *Se llama a `fetchPostsData` de la misma manera. Aunque ambas operaciones son asíncronas, se ejecutan de manera secuencial en este caso.*
    - *Finalmente, se imprime un mensaje indicando que se han cargado los datos del usuario y sus publicaciones.*

*5. Llamada a `loadUserDetails`*

- `*Task {}`: Crea una nueva tarea asincrónica que se ejecuta de manera concurrente con el resto del código.*
- `*await loadUserDetails(userId: "123")`: Dentro de la tarea, se llama a la función `loadUserDetails` pasando el ID del usuario `"123"`. El uso de `await` asegura que el programa espere a que se completen todas las operaciones asincrónicas antes de continuar.*
- *Flujo completo del programa:*
    - *La tarea principal comienza al ejecutar `Task {}`.*
    - *Se invoca la función `loadUserDetails` con el ID del usuario `"123"`.*
    - *Dentro de `loadUserDetails`, se inicia la carga de los datos del usuario con la función `fetchUserData`, que espera 2 segundos.*
    - *Después, se llama a `fetchPostsData`, que espera 1 segundo.*
    - *Una vez que ambas tareas han finalizado, se imprime el mensaje con los resultados de ambas funciones.*
    - *Lo que verías en la consola:*
    - *Cargando datos del usuario...
    Completado: Datos del usuario 123 y Posts del usuario 123*

*Resumen:*

- *Este código demuestra cómo manejar tareas asíncronas en Swift utilizando `async` y `await`, y cómo esperar los resultados de varias operaciones de manera secuencial, sin bloquear el hilo principal. La simulación de retrasos con `Task.sleep`ayuda a emular el comportamiento de una llamada de red o cualquier operación que requiera esperar un tiempo determinado.*
</aside>

# ***3. Ejecución concurrente con Async let***

Si las operaciones no dependen entre sí, se pueden ejecutar en paralelo usando `async let`.

***Ventajas***

- Las tareas `userData` y `postsData` se ejecutan en paralelo.
- `await` asegura que ambas finalicen antes de combinar sus resultados.

```swift
func loadUserDetailsConcurrently(userId: String) async {
    print("Cargando datos del usuario de forma concurrente...")

    async let userData = fetchUserData(userId: userId)
    async let postsData = fetchPostsData(userId: userId)

    let (user, posts) = await (userData, postsData)
    print("Completado: \(user) y \(posts)")
}

// Llamada a la función
Task {
    await loadUserDetailsConcurrently(userId: "123")
}
```

<aside>
📎

*Este código puede leerse como:*

1. *Definición de la Función `loadUserDetailsConcurrently`*
- *La función `loadUserDetailsConcurrently` está marcada como `async`, lo que significa que es una función asíncrona, es decir, puede ejecutar tareas en segundo plano (sin bloquear el hilo principal) y devolver un resultado en algún momento en el futuro.*
- *El parámetro de la función es un `userId` de tipo `String`, que será utilizado para recuperar información sobre el usuario y sus publicaciones.*

*2. Mensajes de depuración:*

- *Esta línea imprime un mensaje para indicar que el proceso de carga de datos está comenzando.*

*3. Operaciones asíncronas concurrentes:*

- *Las líneas anteriores están declarando dos variables asíncronas (`userData` y `postsData`) mediante `async let`.*
- `*fetchUserData(userId:)` es una función que recupera la información del usuario (probablemente desde una base de datos o una API).*
- `*fetchPostsData(userId:)` es una función que recupera las publicaciones asociadas al usuario.*
- *Ambas funciones (`fetchUserData` y `fetchPostsData`) se ejecutan de manera concurrente, lo que significa que se inician al mismo tiempo, sin esperar que una termine antes de comenzar la otra. Esto mejora la eficiencia, ya que no se bloquea el programa mientras espera los resultados de ambas.*

*4. Esperar los resultados:*

- *Aquí se usa `await` para esperar a que ambas tareas (`userData` y `postsData`) finalicen.*
- `*await` hace que el código espere el resultado de las dos tareas concurrentes y las combine en una tupla `(user, posts)`.*
- `*user` será el resultado de `fetchUserData(userId:)` (probablemente la información del usuario).*
- `*posts` será el resultado de `fetchPostsData(userId:)` (probablemente una lista de publicaciones del usuario).*

*5. Impresión del resultado final:*

- *Una vez que ambas tareas se han completado y se ha obtenido el resultado, se imprime un mensaje de éxito que incluye la información del usuario y las publicaciones.*

*6. Ejecución de la función con `Task`*

- *Este bloque crea una nueva tarea asíncrona utilizando `Task {}`. Dentro de esta tarea se llama a la función `loadUserDetailsConcurrently` pasando un `userId` (en este caso `"123"`).*
- *La tarea es iniciada inmediatamente, y la función se ejecuta de manera asíncrona dentro del bloque.*

*Resumen:*

- *Este código está diseñado para cargar la información de un usuario y sus publicaciones de manera concurrente, es decir, ambas operaciones (`fetchUserData` y `fetchPostsData`) se ejecutan al mismo tiempo. Al usar `async let`, se mejora la eficiencia ya que no se espera que una tarea termine antes de iniciar la otra. Cuando ambas tareas terminan, se esperan los resultados usando `await`, y luego se imprime el resultado.*

*Beneficios de este enfoque:*

- *Concurrencia: Ambas tareas se ejecutan al mismo tiempo, lo que reduce el tiempo total de espera.*
- *Código limpio y fácil de leer: La sintaxis de `async let` hace que el código sea más legible y manejable en comparación con otras técnicas de concurrencia.*
</aside>

# ***4. Uso de Taskgroup para múltiples tareas dinámicas***

Cuando no sabes cuántas tareas necesitas por adelantado, puedes usar `TaskGroup`.

- `TaskGroup` permite agregar tareas dinámicamente.
- `for await` recolecta los resultados a medida que las tareas finalizan.

```swift
func fetchMultipleUsers(userIds: [String]) async -> [String] {
    await withTaskGroup(of: String.self) { group in
        for userId in userIds {
            group.addTask {
                await fetchUserData(userId: userId)
            }
        }

        var results: [String] = []
        for await result in group {
            results.append(result)
        }
        return results
    }
}

// Llamada con varios IDs de usuario
Task {
    let results = await fetchMultipleUsers(userIds: ["101", "102", "103"])
    print("Resultados: \(results)")
}
```

<aside>
📎

*Este código puede leerse como:*

1. *Definición de la Función `fetchMultipleUsers(userIds:)`*
- `*userIds: [String]`: Esta función toma como parámetro una lista de identificadores de usuario (IDs) de tipo `String`.*
- `*async`: La función es asíncrona, lo que significa que puede realizar tareas de larga duración sin bloquear el hilo principal.*
- `*> [String]`: La función retorna un arreglo de cadenas (`[String]`), que en este caso sería una lista de resultados, probablemente datos de los usuarios.*

*2. Uso de `withTaskGroup`*

- `*withTaskGroup(of: String.self)`: `withTaskGroup` es una construcción que permite ejecutar tareas concurrentes. En este caso, el tipo de los resultados que devolverán las tareas dentro del grupo es `String`, que se refiere al tipo de datos que devolverá la función `fetchUserData` (probablemente información sobre cada usuario).*
- `*group.addTask { ... }`: En este bloque, se agregan tareas al grupo. Para cada `userId` en el arreglo de usuarios, se llama a `fetchUserData(userId:)` de manera asíncrona. Cada tarea se ejecutará de manera independiente y concurrente.*
- `*await fetchUserData(userId: userId)`: Se llama a la función `fetchUserData` (presumiblemente otra función asíncrona que obtiene datos de un usuario) para obtener la información de cada usuario en paralelo.*

*3. Recolección de resultados*

- `*var results: [String] = []`: Se crea un arreglo vacío donde se almacenarán los resultados de las tareas concurrentes.*
- `*for await result in group`: Esto es un ciclo que espera a que cada tarea dentro del `group` termine y recoja el resultado. Debido a la naturaleza asíncrona, `await` asegura que el código espere a que cada tarea termine antes de continuar con el siguiente resultado.*
- `*results.append(result)`: A medida que se obtienen los resultados de las tareas, se agregan al arreglo `results`.*
- `*return results`: Finalmente, después de que todas las tareas hayan completado y los resultados hayan sido recolectados, la función devuelve el arreglo de resultados.*

*4. Llamada a la función*

- `*Task { ... }`: Aquí se está creando una tarea asíncrona que se ejecutará de manera independiente. La tarea es creada porque la función `fetchMultipleUsers` es asíncrona y se debe llamar desde un contexto que permita esperar a su resultado (por ejemplo, dentro de una vista en SwiftUI o una función asíncrona).*
- `*let results = await fetchMultipleUsers(userIds: ["101", "102", "103"])`: Se invoca la función `fetchMultipleUsers` pasando tres IDs de usuario (`"101"`, `"102"`, y `"103"`), y se espera su resultado.*
- `*print("Resultados: \(results)")`: Una vez que se obtienen los resultados, estos se imprimen en la consola.*

*Resumen:*

- *Este código utiliza `withTaskGroup` para ejecutar de forma concurrente múltiples solicitudes asíncronas a la función `fetchUserData` con diferentes IDs de usuario. Cada tarea se ejecuta en paralelo, lo que permite que la función obtenga los datos de varios usuarios al mismo tiempo, mejorando el rendimiento y reduciendo el tiempo de espera en comparación con un enfoque secuencial. Los resultados de todas las tareas se recolectan y se devuelven en un solo arreglo.*

*Ventajas del enfoque:*

- *Eficiencia: El uso de concurrencia mejora el rendimiento al ejecutar múltiples tareas al mismo tiempo.*
- *Escalabilidad: Puede manejar un número variable de IDs de usuario, y el código se adapta fácilmente para tareas adicionales.*
</aside>

# ***5. Manejo seguro de estados compartidos con Actor***

Un `Actor` asegura que el acceso a sus propiedades sea seguro en un entorno concurrente.

***Ventajas***

- Solo una tarea puede acceder a las propiedades del `actor` a la vez.
- Evita condiciones de carrera automáticamente.

```swift
actor Counter {
    private var value = 0

    func increment() {
        value += 1
    }

    func getValue() -> Int {
        return value
    }
}

let counter = Counter()

Task {
    await counter.increment()
    await counter.increment()
    print("Valor actual: \(await counter.getValue())")
}
```

<aside>
📎

*Este código puede leerse como:*

*1. Definición del actor `Counter`*

- *Actor: En Swift, un `actor` es un tipo especial de objeto que está diseñado para proteger su estado interno de condiciones de carrera en entornos concurrentes. Esto significa que, dentro de un `actor`, solo una tarea puede acceder a sus propiedades o métodos en un momento dado. Los actores proporcionan seguridad de datos sin necesidad de usar semáforos o otras técnicas de sincronización tradicionales.*
- `*private var value = 0`: Aquí se define una propiedad privada `value` que será utilizada para llevar un conteo de algún valor (inicialmente 0).*
- *Método `increment()`: Esta función incrementa el valor de `value` en 1. Los métodos de un `actor` pueden ser llamados de forma asíncrona desde tareas concurrentes, pero el acceso al valor se maneja de forma segura gracias al modelo de actores.*
- *Método `getValue()`: Este método devuelve el valor actual de la propiedad `value`. Dado que `Counter` es un actor, si se llama desde un contexto concurrente, el acceso a `value` está protegido, lo que evita condiciones de carrera.*

*2. Creación de una instancia del actor*

- *Aquí, creamos una instancia de `Counter` llamada `counter`. Debido a que `Counter` es un actor, esta instancia es gestionada de manera especial para garantizar que las operaciones sobre su estado sean seguras en un entorno concurrente.*

*3. Tarea Asíncrona (`Task`)*

- `*Task`: Se crea una tarea asíncrona utilizando la palabra clave `Task`. En el contexto de Swift, `Task` se utiliza para ejecutar código de manera concurrente (en un hilo diferente o de manera asíncrona).*
- `*await counter.increment()`: Este código invoca el método `increment()` del actor `counter`. Como se trata de un actor, el `await` se utiliza para esperar de manera segura que el `increment()` termine antes de proceder. Esto asegura que el acceso al estado del actor esté correctamente sincronizado.*
- `*await counter.increment()`: Se incrementa de nuevo el valor de `counter`.*
- `*await counter.getValue()`: Aquí, obtenemos el valor actual de `counter`. El uso de `await` es necesario porque `getValue()` es un método de un actor, y el acceso a propiedades de actores también es asíncrono.*
- `*print("Valor actual: \(await counter.getValue())")`: Finalmente, imprimimos el valor actual de `counter`después de los dos incrementos. El valor impreso será 2, ya que `counter` comenzó en 0 y luego se incrementó dos veces.*

*Resumen:*

- *Actor: `Counter` es un actor que encapsula el valor `value` y proporciona métodos seguros para manipularlo en un entorno concurrente.*
- *Tarea asíncrona (`Task`): Se utiliza para ejecutar tareas concurrentes que interactúan con el actor `Counter`.*
- `*await`: Se utiliza para esperar que las operaciones sobre el actor finalicen, garantizando la seguridad de los datos.*

*Concurrencia en Swift*

- *El uso de actores ayuda a manejar la concurrencia en Swift de manera más fácil y segura. Cuando se accede a las propiedades de un actor desde diferentes hilos o tareas, Swift garantiza que solo una tarea pueda modificar el estado del actor en un momento dado. Esto previene errores comunes en programas concurrentes, como las condiciones de carrera.*

*Salida del código*

- *Cuando ejecutas este código, la salida será: Valor actual: 2*
- *Esto se debe a que `increment()` se llamó dos veces, incrementando el valor de 0 a 2.*
</aside>

# ***6. Uso del Main Actor para actualizar la UI***

Las actualizaciones de la interfaz de usuario deben ocurrir en el hilo principal. Puedes usar `MainActor` para asegurarlo.

***Beneficios***

- El decorador `@MainActor` asegura que todas las modificaciones de `userData` ocurran en el hilo principal.
- Ideal para integraciones con SwiftUI.

```swift
import SwiftUI

@MainActor
class ViewModel: ObservableObject {
    @Published var userData: String = ""

    func loadUserData() async {
        let data = await fetchUserData(userId: "123")
        userData = data // Actualización en el hilo principal
    }
}

struct ContentView: View {
    @StateObject private var viewModel = ViewModel()

    var body: some View {
        VStack {
            Text(viewModel.userData)
                .padding()

            Button("Cargar datos") {
                Task {
                    await viewModel.loadUserData()
                }
            }
        }
    }
}
```

# ***7. Ejemplo avanzado: Progresión y cancelación***

Se puede manejar la cancelación de tareas y el progreso de forma explícita.

***Características***

- `Task.checkCancellation` verifica si se solicitó la cancelación.
- Puedes controlar el tiempo de ejecución y finalizar una tarea de forma anticipada.

```swift
func downloadFile() async throws -> String {
    for i in 1...10 {
        try Task.checkCancellation() // Verifica si la tarea ha sido cancelada
        print("Descargando: \(i * 10)%")
        try? await Task.sleep(nanoseconds: 500_000_000) // Simula progreso
    }
    return "Descarga completada"
}

Task {
    do {
        let result = try await downloadFile()
        print(result)
    } catch {
        print("La tarea fue cancelada")
    }
}

// Cancelar la tarea después de 2 segundos
Task {
    try? await Task.sleep(nanoseconds: 2 * 1_000_000_000)
    Task.current?.cancel()
}
```

<aside>
📎

*Este código puede leerse como:*

1. *Función `downloadFile()`*
- `*async throws`: La función `downloadFile` es asíncrona (`async`) y puede lanzar errores (`throws`). Esto indica que la función puede ser ejecutada de manera asíncrona (en segundo plano) y también puede generar errores durante su ejecución.*
- `*for i in 1...10`: El ciclo `for` simula la descarga dividiendo la tarea en 10 pasos. Cada paso representa un 10% de la descarga total.*
- `*try Task.checkCancellation()`: Este es un punto de control donde se verifica si la tarea ha sido cancelada antes de continuar. Si la tarea ha sido cancelada, se lanzará un error de cancelación (`CancellationError`). Esto es útil para permitir que las tareas asíncronas se interrumpan de manera limpia y segura cuando sea necesario.*
- `*print("Descargando: \(i * 10)%")`: Simula la descarga mostrando el progreso (10%, 20%, ..., 100%).*
- `*try? await Task.sleep(nanoseconds: 500_000_000)`: Esta línea simula un retardo de 0.5 segundos (500,000,000 nanosegundos) entre cada paso de la descarga. Esto simula el tiempo que tardaría una descarga real.*
- `*return "Descarga completada"`: Si la tarea no ha sido cancelada antes de completar el ciclo, se devuelve un mensaje indicando que la descarga ha terminado.*

*2. Tarea principal que ejecuta `downloadFile()`*

- `*Task { ... }`: Esto crea una tarea asíncrona en el hilo de ejecución actual. Dentro de este bloque, se realiza la llamada a la función `downloadFile`.*
- `*do { ... } catch { ... }`: Se utiliza un bloque `do-catch` para manejar cualquier error que pueda ocurrir durante la ejecución de la tarea. Si la función `downloadFile` lanza un error (por ejemplo, si la tarea es cancelada), se captura en el bloque `catch`.*
- `*let result = try await downloadFile()`: La función `downloadFile` se llama y espera su resultado. Si se completa con éxito, el mensaje "Descarga completada" se almacena en la variable `result` y se imprime en consola.*
- `*catch { print("La tarea fue cancelada") }`: Si la tarea se cancela (por ejemplo, si se lanza un error de cancelación), se captura y se imprime el mensaje "La tarea fue cancelada".*

*3. Tarea que cancela la tarea de descarga*

- `*Task { ... }`: Esto crea una nueva tarea asíncrona que se ejecutará en paralelo con la tarea de descarga.*
- `*try? await Task.sleep(nanoseconds: 2 * 1_000_000_000)`: Esta línea simula un retardo de 2 segundos (2,000,000,000 nanosegundos). Después de esperar 2 segundos, la tarea procederá a cancelar la tarea de descarga.*
- `*Task.current?.cancel()`: Esta línea cancela la tarea en ejecución actual. En este caso, la tarea principal que estaba descargando el archivo se cancela después de 2 segundos.*
1. *Flujo de ejecución*
- *Se inicia la tarea de descarga llamando a `downloadFile()`.*
- *La descarga simula un proceso dividido en 10 partes, mostrando el progreso en cada paso.*
- *Después de 2 segundos, se inicia otra tarea que cancela la tarea de descarga.*
- *En el ciclo de la descarga, la función `checkCancellation()` verifica si la tarea ha sido cancelada en cada iteración. Si es así, se lanza un error de cancelación.*
- *Si la tarea es cancelada, el bloque `catch` en la tarea principal captura el error y muestra el mensaje "La tarea fue cancelada".*
- *Si la descarga no es cancelada, se completa y muestra "Descarga completada".*
1. *Resultado Esperado en Consola:*
- *Después de ejecutar el código, el flujo sería:*
- *En el primer ciclo de la descarga, el progreso (10%) se imprime.*
- *Después de 2 segundos, la tarea es cancelada, y el flujo salta al bloque `catch` que imprime "La tarea fue cancelada".*
- *Este es el comportamiento esperado debido a la cancelación de la tarea después de 2 segundos de ejecución.*

*Resumen:*

- *Este código muestra cómo manejar tareas asíncronas en Swift, verificando la cancelación de tareas y cómo simular una operación (en este caso, una descarga) que se puede interrumpir. La cancelación de tareas es útil cuando se necesita gestionar operaciones que podrían tomar un tiempo prolongado o que deben ser detenidas por alguna razón, como cambios en el estado de la aplicación o la interacción del usuario.*
</aside>

# ***8. Uso de DispatchQueue (modelo antiguo)***

DispatchQueue y GCD (Grand Central Dispatch):

- Es una API tradicional para manejar tareas concurrentes usando colas.

***Explicación***

- `DispatchQueue.global` ejecuta código en un hilo de fondo.
- `DispatchQueue.main` asegura que la actualización de la interfaz de usuario ocurra en el hilo principal.

```swift
import Foundation

DispatchQueue.global(qos: .background).async {
    let result = "Tarea en segundo plano"
    DispatchQueue.main.async {
        print("Resultado: \(result) en el hilo principal")
    }
}
```

---