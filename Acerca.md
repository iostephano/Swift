# Acerca

# ***1. Acerca de Swift 6***

Swift es un lenguaje de programación versátil y eficiente, diseñado para el desarrollo de software en diversas plataformas, incluyendo teléfonos y servidores. Combina características de seguridad, velocidad e interactividad, aprovechando la cultura de ingeniería de Apple y la comunidad de código abierto. Su compilador está optimizado para rendimiento, y el lenguaje facilita la creación de código gracias a su sintaxis clara y amigable, especialmente para principiantes.

Swift suprime muchos tipos comunes de errores de programación mediante la adopción de patrones de programación modernos:

- Las variables siempre se inicializan antes de ser usadas.
- Se verifican los índices de los array (vector, matriz, o arreglo) en busca de errores fuera de límites (out-of-bound errors).
- Se comprueba el desborde (overflow) de números enteros.
- Los opcionales aseguran que los valores nulos (`nil`) se manejen explícitamente.
- La memoria se gestiona automáticamente.
- El manejo de errores permite la recuperación controlada de fallas inesperadas.

# ***2. Compatibilidad de Versiones***

Este libro describe Swift 6, la versión predeterminada de Swift que se incluye en Xcode 16. Puedes usar el compilador de Swift 6 para construir código escrito en Swift 6, Swift 5, Swift 4.2 o Swift 4.

Cuando usas el compilador de Swift 6 para construir código que utiliza el modo de lenguaje de Swift 5, puedes aprovechar las nuevas características de Swift 6; están habilitadas por defecto o mediante un próximo flag de características. Sin embargo, para habilitar la verificación estricta de concurrencia, necesitas actualizar al modo de lenguaje de Swift 6.

Además, cuando usas Xcode 15.3 para construir código en Swift 4 y Swift 4.2, la mayoría de la funcionalidad de Swift 5 aún está disponible. Dicho esto, los siguientes cambios están disponibles solo para código que utiliza el modo de lenguaje de Swift 5:

- Las funciones que devuelven un tipo opaco requieren el runtime de Swift 5.1.
- La expresión `try?` no introduce un nivel adicional de opcionalidad a expresiones que ya devuelven opcionales.
- Las expresiones de inicialización de literales enteros grandes se infieren como del tipo entero correcto. Por ejemplo, `UInt64(0xffff_ffff_ffff_ffff)` evalúa al valor correcto en lugar de desbordarse.
- La concurrencia requiere el modo de lenguaje de Swift 5 y una versión de la biblioteca estándar de Swift que proporcione los tipos de concurrencia correspondientes. En plataformas de Apple, establece un objetivo de implementación de al menos iOS 13, macOS 10.15, tvOS 13, watchOS 6 o visionOS 1.

Un objetivo escrito en Swift 6 puede depender de un objetivo escrito en Swift 5, Swift 4.2 o Swift 4, y viceversa. Esto significa que, si tienes un proyecto grande dividido en múltiples frameworks, puedes migrar tu código a una versión de lenguaje más nueva un framework a la vez.

# ***3. Historial de Revisiones***

**2024-09-16 Actualizado para Swift 6**

- Se añadió la sección de preconcurrencia con información sobre la migración a la verificación de concurrencia estricta.
- Se añadió la sección Especificando el Tipo de Error con información sobre lanzar errores de un tipo específico.
- Actualizada la sección de Expresión de Expansión de Macros, ahora que cualquier macro puede ser utilizada como un valor por defecto para un parámetro.
- Se añadió información sobre el acceso a nivel de paquete al capítulo de Control de Acceso.

**2024-03-05 Actualizado para Swift 5.10**

- Se añadió información sobre protocolos anidados a la sección de Delegación.
- Se añadió información sobre deprecación en las secciones UIApplicationMain y NSApplicationMain.

**2023-12-11 Actualizado para Swift 5.9.2**

- Se añadió información sobre los modificadores de préstamo y consumo a la sección de Modificadores de Parámetros.
- Se añadió información en Declaración de Constantes y Variables sobre establecer el valor de una constante después de su declaración.
- Se añadió más información sobre tareas, grupos de tareas y cancelación de tareas al capítulo de Concurrencia.
- Se añadió información en el capítulo de Macros sobre la implementación de macros en un paquete Swift existente.
- Actualizada la sección adjunta, ahora que las macros de extensión han reemplazado a las macros de conformidad.
- Se añadió la sección de Despliegue Retrospectivo con información sobre el despliegue retrospectivo.

**2023-09-18 Actualizado para Swift 5.9**

- Se añadió información sobre expresiones if y switch al capítulo de Flujo de Control y a la sección de Expresión Condicional.
- Se añadió el capítulo de Macros, con información sobre la generación de código en tiempo de compilación.
- Se amplió la discusión sobre opcionales en Lo Básico.
- Se añadió un ejemplo de concurrencia a Un Tour de Swift.
- Se añadió información sobre tipos de protocolo en caja al capítulo de Tipos de Protocolo Opacos y en Caja.
- Se añadió información sobre los métodos buildPartialBlock(first:) y buildPartialBlock(accumulated:next:) a la sección de Transformaciones de Resultados.
- Se añadió visionOS a las listas de plataformas en disponible y Bloque de Compilación Condicional.
- Se formateó la gramática formal para usar líneas en blanco para agrupar.

**2023-03-30 Actualizado para Swift 5.8**

- Se añadió la sección de Acciones Diferidas, mostrando defer fuera del manejo de errores.
- Se adoptó Swift-DocC para publicación.
- Correcciones menores y adiciones en todo.

**2022-09-12 Actualizado para Swift 5.7**

- Se añadió la sección de Tipos Sendable, con información sobre el envío de datos entre actores y tareas, y se añadió información sobre los atributos @Sendable y @unchecked a las secciones Sendable y unchecked.
- Se añadió la sección de Literales de Expresión Regular con información sobre la creación de expresiones regulares.
- Se añadió información sobre la forma corta de if-let a la sección de Vinculación Opcional.
- Se añadió información sobre #unavailable a la sección de Comprobación de Disponibilidad de API.

**2022-03-14 Actualizado para Swift 5.6**

- Actualizada la sección de Expresión de Miembro Explícito con información sobre el uso de #if alrededor de llamadas de métodos encadenados y otras expresiones postfix.
- Actualizado el estilo visual de las figuras en todo el documento.

**2021-09-20 Actualizado para Swift 5.5**

- Se añadió información sobre funciones asíncronas, tareas y actores al capítulo de Concurrencia, y a las secciones de Declaración de Actor, Funciones y Métodos Asíncronos, y Operador Await.
- Actualizada la sección de Identificadores con información sobre identificadores que comienzan con un guion bajo.

**2021-04-26 Actualizado para Swift 5.4**

- Se añadieron las secciones de Constructores de Resultados y resultBuilder con información sobre constructores de resultados.
- Se añadió la sección de Conversión Implícita a un Tipo de Puntero con información sobre cómo los parámetros in-out pueden convertirse implícitamente en punteros inseguros en una llamada de función.
- Actualizadas las secciones de Parámetros Variádicos y Declaración de Funciones, ahora que una función puede tener múltiples parámetros variádicos.
- Actualizada la sección de Expresión de Miembro Implícito, ahora que las expresiones de miembro implícitas pueden encadenarse.

***2020-09-16 Actualizado para Swift 5.3***

- Se añadió información sobre múltiples cierres finales a la sección de Cierres Finales, y se añadió información sobre cómo los cierres finales se emparejan con los parámetros a la sección de Expresión de Llamada de Función.
- Se añadió información sobre implementaciones sintetizadas de Comparable para enumeraciones a la sección de Adopción de un Protocolo Usando una Implementación Sintetizada.
- Se añadió la sección de Cláusulas Donde Contextuales ahora que se puede escribir una cláusula where genérica en más lugares.
- Se añadió la sección de Referencias Opcionales No Poseídas con información sobre el uso de referencias no poseídas con valores opcionales.
- Se añadió información sobre el atributo @main a la sección principal.
- Se añadió #filePath a la sección de Expresión Literal y se actualizó la discusión de #file.
- Actualizada la sección de Cierres que Escapan, ahora que los cierres pueden referirse a self implícitamente en más escenarios.
- Actualizadas las secciones de Manejo de Errores Usando Do-Catch y Declaraciones Do, ahora que una cláusula catch puede coincidir con múltiples errores.
- Se añadió más información sobre Any y se movió a la nueva sección Tipo Any.
- Actualizada la sección de Observadores de Propiedades, ahora que las propiedades perezosas pueden tener observadores.
- Actualizada la sección de Declaración de Protocolos, ahora que los miembros de una enumeración pueden cumplir con los requisitos de protocolo.
- Actualizada la sección de Observadores de Variables Almacenadas y Observadores de Propiedades para describir cuándo se llama al getter antes del observador.
- Actualizado el capítulo de Seguridad de Memoria para mencionar operaciones atómicas.

**2020-03-24 Actualizado para Swift 5.2**

- Se añadió información sobre pasar un camino clave en lugar de un cierre a la sección de Expresión de Camino Clave.
- Se añadió la sección de Métodos con Nombres Especiales con información sobre azúcar sintáctico que permite a instancias de clases, estructuras y enumeraciones ser utilizadas con sintaxis de llamada de función.
- Actualizada la sección de Opciones de Subscript, ahora que los subscripts admiten parámetros con valores por defecto.
- Actualizada la sección de Tipo Self, ahora que Self puede ser usado en más contextos.
- Actualizada la sección de Opcionales Desenvueltos Implícitamente para dejar claro que un valor opcional desenvuelto implícitamente puede ser usado como un valor opcional o no opcional.

**2019-09-10 Actualizado para Swift 5.1**

- Se añadió información sobre funciones que especifican un protocolo al que su valor de retorno se ajusta, en lugar de proporcionar un tipo de retorno nombrado específico, al capítulo de Tipos de Protocolo Opacos y en Caja.
- Se añadió información sobre envoltorios de propiedades a la sección de Envoltorios de Propiedades.
- Se añadió información sobre enumeraciones y estructuras que están congeladas para la evolución de la biblioteca a la sección de congelación.
- Se añadieron las secciones de Funciones con un Retorno Implícito y Declaración de Getter Corto con información sobre funciones que omiten el retorno.
- Se añadió información sobre el uso de subscripts en tipos a la sección de Subscripts de Tipo.
- Actualizada la sección de Patrón de Caso de Enumeración, ahora que un patrón de caso de enumeración puede coincidir con un valor opcional.
- Actualizada la sección de Inicializadores por Miembros para Tipos de Estructura, ahora que los inicializadores por miembros admiten omitir parámetros para propiedades que tienen un valor por defecto.
- Se añadió información sobre miembros dinámicos que se buscan por camino clave en tiempo de ejecución a la sección dynamicMemberLookup.
- Se añadió macCatalyst a la lista de entornos de destino en Bloque de Compilación Condicional.
- Actualizada la sección de Tipo Self, ahora que Self puede ser usado para referirse al tipo introducido por la declaración actual de clase, estructura o enumeración.

**2019-03-25 Actualizado para Swift 5.0**

- Se añadió la sección de Delimitadores de Cadenas Extendidas y se actualizó la sección de Literales de Cadenas con información sobre delimitadores de cadenas extendidos.
- Se añadió la sección dynamicCallable con información sobre cómo llamar dinámicamente a instancias como funciones usando el atributo dynamicCallable.
- Se añadieron las secciones unknown y Switching Over Future Enumeration Cases con información sobre cómo manejar futuros casos de enumeración en declaraciones switch usando el atributo de caso switch unknown.
- Se añadió información sobre el camino clave de identidad (\.self) a la sección de Exp

# ***4. Glosario de Términos***

1. **Xcode**: El entorno de desarrollo integrado (IDE) oficial de Apple para el desarrollo de aplicaciones iOS y macOS. Incluye herramientas para escribir, compilar, probar y depurar código.
2. **Swift**: Un lenguaje de programación creado por Apple para el desarrollo de aplicaciones iOS y macOS. Es conocido por ser seguro, rápido y fácil de leer.
3. **Objective-C**: Un lenguaje de programación utilizado históricamente para el desarrollo de aplicaciones iOS. Aunque Swift es el lenguaje preferido actualmente, Objective-C sigue siendo relevante para mantener y actualizar aplicaciones más antiguas.
4. **Storyboard**: Una interfaz visual dentro de Xcode que permite a los desarrolladores diseñar y organizar la interfaz de usuario (UI) de una aplicación iOS mediante un sistema de arrastrar y soltar.
5. **Interface Builder**: Una herramienta en Xcode que permite a los desarrolladores diseñar interfaces gráficas de usuario. Se puede utilizar con Storyboards o archivos XIB.
6. **UIKit**: Un framework que proporciona las herramientas necesarias para construir y gestionar la interfaz de usuario de las aplicaciones iOS. Incluye controles, ventanas y vistas estándar.
7. **Cocoa Touch**: Un conjunto de bibliotecas de desarrollo que incluye UIKit y otros frameworks necesarios para crear aplicaciones en iOS.
8. **Auto Layout**: Un sistema dentro de Xcode para crear interfaces de usuario que se adapten automáticamente a diferentes tamaños de pantalla y orientaciones de dispositivos.
9. **Simulator**: Una herramienta dentro de Xcode que permite a los desarrolladores probar aplicaciones iOS en diferentes modelos de dispositivos sin necesidad de hardware físico.
10. **Provisioning Profile**: Un archivo que permite a los desarrolladores instalar y ejecutar aplicaciones en dispositivos iOS físicos durante el proceso de desarrollo y prueba. También es necesario para la distribución de aplicaciones.
11. **App Store Connect**: Una plataforma web de Apple donde los desarrolladores pueden gestionar sus aplicaciones, incluidas las pruebas beta, las descripciones de la App Store y las versiones publicadas.
12. **TestFlight**: Un servicio de Apple que permite a los desarrolladores distribuir versiones beta de sus aplicaciones a testers antes de lanzar una versión final.
13. **ARC (Automatic Reference Counting)**: Una característica de gestión de memoria en Swift y Objective-C que automáticamente mantiene un recuento de referencias de objetos y libera la memoria cuando los objetos ya no son necesarios.
14. **Delegate**: Un patrón de diseño en el desarrollo iOS donde un objeto delega la responsabilidad de ciertas acciones o eventos a otro objeto.
15. **MVC (Model-View-Controller)**: Un patrón de diseño ampliamente utilizado en el desarrollo iOS que separa la lógica de la aplicación en tres componentes: Model (modelo), View (vista) y Controller (controlador).
16. **Singleton**: Un patrón de diseño que asegura que una clase tenga solo una instancia y proporcione un punto de acceso global a ella.
17. **IBAction**: Un término utilizado en Xcode para conectar elementos de la interfaz de usuario a métodos en el código que responden a eventos, como pulsaciones de botones.
18. **IBOutlet**: Un término utilizado en Xcode para conectar elementos de la interfaz de usuario a variables en el código que permiten interactuar con esos elementos desde el código.
19. **NS (NextStep)**: Prefijo que se utiliza en muchas clases y funciones de las bibliotecas de Cocoa, derivado del sistema operativo NeXTSTEP en el que se basan macOS e iOS.
20. **ViewController**: Una clase fundamental en UIKit que gestiona una pantalla completa de contenido en una aplicación iOS. Cada vista tiene un controlador que maneja la lógica de la interfaz de usuario y la interacción del usuario.
21. **Core Data**: Un framework de Apple para gestionar el almacenamiento persistente de datos en aplicaciones iOS. Proporciona una solución completa para almacenar datos en una base de datos SQLite y gestionarlos mediante un modelo de objetos.
22. **Core Animation**: Un framework que permite crear animaciones complejas y fluidas en aplicaciones iOS con una mínima cantidad de código.
23. **Core Location**: Un framework que proporciona servicios para determinar la ubicación del dispositivo y gestionar datos de ubicación en aplicaciones iOS.
24. **Core Graphics**: Un framework que proporciona herramientas para el dibujo de gráficos bidimensionales y el manejo de imágenes en aplicaciones iOS.
25. **Core Motion**: Un framework que accede a los datos del acelerómetro, giroscopio y otros sensores de movimiento del dispositivo para detectar y responder a los movimientos del dispositivo.
26. **APNS (Apple Push Notification Service)**: Un servicio que permite a los desarrolladores enviar notificaciones push a los dispositivos iOS.
27. **Sandboxing**: Una técnica de seguridad que aísla las aplicaciones en su propio entorno controlado para evitar que accedan a recursos no autorizados en el dispositivo.
28. **Entitlements**: Configuraciones que especifican los permisos y capacidades de una aplicación, como el acceso a iCloud, notificaciones push y más.
29. **Keychain**: Un servicio de iOS para almacenar de manera segura información sensible como contraseñas y datos de autenticación.
30. **View Hierarchy**: La estructura de vistas (views) organizadas en una jerarquía, donde cada vista puede tener una o más sub-vistas. Es fundamental para el diseño y la disposición de la interfaz de usuario.
31. **Restoration ID**: Un identificador utilizado para restaurar el estado de una vista o vista controladora durante el proceso de reanudación de una aplicación.
32. **SceneDelegate**: Introducido en iOS 13, maneja las escenas de una aplicación, permitiendo que las aplicaciones gestionen múltiples ventanas independientes.
33. **Multitasking**: La capacidad de iOS para ejecutar múltiples aplicaciones de manera simultánea y permitir la transición entre ellas sin perder el estado actual de cada aplicación.
34. **App Extension**: Un componente que permite a una aplicación ofrecer funcionalidades específicas a otras aplicaciones y partes del sistema operativo, como widgets y extensiones de teclado.
35. **Background Fetch**: Una capacidad que permite a las aplicaciones descargar y procesar contenido en segundo plano para mantener la información actualizada.
36. **Combine**: Un framework de Apple que facilita la gestión de eventos asincrónicos mediante la combinación de flujos de datos y el manejo de valores de forma reactiva.
37. **SceneKit**: Un framework para la creación y manipulación de gráficos 3D y escenas en aplicaciones iOS.
38. **SpriteKit**: Un framework para el desarrollo de juegos 2D, proporcionando herramientas para manejar gráficos, físicas y animaciones.
39. **ARKit**: Un framework que permite desarrollar aplicaciones de realidad aumentada (AR) en dispositivos iOS.
40. **Metal**: Un framework de bajo nivel que proporciona acceso directo a la GPU, permitiendo a los desarrolladores crear gráficos y cálculos altamente eficientes para aplicaciones y juegos.
41. **Handoff**: Una funcionalidad que permite a los usuarios comenzar una actividad en un dispositivo Apple y continuarla en otro sin interrupciones.
42. **Touch ID**: Tecnología de reconocimiento de huellas dactilares utilizada para la autenticación en dispositivos iOS.
43. **Face ID**: Tecnología de reconocimiento facial utilizada para la autenticación en dispositivos iOS.
44. **Provisioning Portal**: Parte de App Store Connect, donde los desarrolladores gestionan certificados, perfiles de aprovisionamiento y dispositivos registrados.
45. **App Groups**: Una característica que permite a las aplicaciones compartir datos y recursos con otras aplicaciones del mismo desarrollador.
46. **Universal Links**: Enlaces que, cuando se tocan, abren la aplicación iOS correspondiente en lugar de un navegador web, mejorando la integración de enlaces profundos.
47. **Deep Linking**: Técnica para dirigir a los usuarios a un contenido específico dentro de una aplicación desde una URL externa.
48. **Retina Display**: Tecnología de pantalla de alta resolución utilizada en dispositivos Apple para proporcionar imágenes más nítidas y claras.
49. **Gestures**: Interacciones táctiles reconocidas por iOS, como toques, deslizamientos, pellizcos y rotaciones, que se utilizan para controlar la interfaz de usuario.
50. **View Controller Lifecycle**: El ciclo de vida de un controlador de vista, incluyendo métodos como `viewDidLoad`, `viewWillAppear`, `viewDidAppear`, `viewWillDisappear` y `viewDidDisappear`, que gestionan la creación, presentación y eliminación de vistas.
51. **IBInspectable**: Un atributo que permite exponer propiedades de una clase a Interface Builder, permitiendo la configuración de estas propiedades directamente desde el storyboard o archivo XIB.
52. **IBDesignable**: Un atributo que permite que una vista personalizada se renderice en Interface Builder, mostrando su apariencia en tiempo real mientras se diseña la interfaz.
53. **GCD (Grand Central Dispatch)**: Una tecnología de Apple para realizar tareas concurrentes de manera eficiente, utilizando colas para gestionar hilos en segundo plano.
54. **Concurrency**: La capacidad de un programa para gestionar múltiples tareas al mismo tiempo, mejorando el rendimiento y la capacidad de respuesta de las aplicaciones.
55. **Asynchronous Programming**: Un estilo de programación que permite realizar operaciones que pueden tardar en completarse sin bloquear la ejecución del programa, utilizando técnicas como callbacks, promesas y async/await.
56. **Tuple**: Una colección ordenada de valores en Swift que puede contener diferentes tipos de datos. Se utiliza para agrupar múltiples valores en una sola unidad.
57. **Optional**: Un tipo en Swift que puede contener un valor o `nil`, utilizado para manejar la ausencia de un valor de manera segura.
58. **Closure**: Un bloque de código que puede ser pasado y ejecutado más tarde, capturando y almacenando referencias a variables y constantes del contexto en el que se define.
59. **Protocol**: Una especificación en Swift que define un conjunto de métodos, propiedades y otros requisitos que una clase, estructura o enumeración debe implementar.
60. **Extension**: Una característica en Swift que permite añadir nuevas funcionalidades a una clase, estructura, enumeración o protocolo existente sin necesidad de modificar su código original.
61. **Enum (Enumerations)**: Un tipo de datos en Swift que define un grupo de valores relacionados y permite trabajar con ellos de una manera segura y predecible.
62. **Struct (Structure)**: Un tipo de datos en Swift que define un grupo de propiedades y métodos que trabajan juntos, similar a una clase pero con semántica de valor en lugar de referencia.
63. **Property Wrapper**: Una característica en Swift que permite agregar lógica adicional a las propiedades mediante la definición de un tipo que encapsula la lógica de almacenamiento y acceso.
64. **Combine Framework**: Un framework que proporciona una manera declarativa para trabajar con valores que cambian con el tiempo, utilizando flujos de datos reactivos.
65. **WidgetKit**: Un framework que permite crear widgets para la pantalla de inicio de iOS, proporcionando información y acceso rápido a funcionalidades de la aplicación.
66. **SwiftUI**: Un framework declarativo para construir interfaces de usuario en todas las plataformas de Apple. Utiliza una sintaxis declarativa que permite describir la interfaz y su comportamiento.
67. **CloudKit**: Un framework que facilita el almacenamiento y sincronización de datos de la aplicación en la nube, permitiendo el acceso a datos compartidos entre múltiples dispositivos.
68. **iBeacon**: Una tecnología de Apple que permite a los dispositivos iOS detectar y reaccionar a señales de balizas Bluetooth de baja energía (BLE) en proximidad.
69. **In-App Purchase (IAP)**: Un mecanismo que permite a los usuarios comprar contenido adicional o funcionalidades dentro de una aplicación iOS.
70. **HealthKit**: Un framework que permite a las aplicaciones acceder y compartir datos de salud y fitness del usuario.
71. **HomeKit**: Un framework que permite a las aplicaciones controlar dispositivos y sistemas de automatización del hogar.
72. **SiriKit**: Un framework que permite integrar la funcionalidad de Siri en las aplicaciones, permitiendo a los usuarios interactuar con las aplicaciones mediante comandos de voz.
73. **MapKit**: Un framework que proporciona una interfaz para incorporar mapas y funciones de localización en las aplicaciones iOS.
74. **AVFoundation**: Un framework que proporciona una interfaz para trabajar con medios audiovisuales, incluyendo la reproducción, grabación y edición de audio y video.
75. **SceneKit**: Un framework para crear gráficos y animaciones 3D, proporcionando herramientas para construir y gestionar escenas tridimensionales.
76. **SpriteKit**: Un framework que facilita la creación de juegos 2D, proporcionando un motor de gráficos, físicas y animaciones.
77. **CallKit**: Un framework que permite integrar servicios de llamadas VoIP en la interfaz nativa de llamadas de iOS.
78. **Core ML**: Un framework que permite integrar modelos de aprendizaje automático (machine learning) en las aplicaciones iOS.
79. **Natural Language**: Un framework que proporciona herramientas para procesar y analizar texto en lenguaje natural, incluyendo el análisis de sentimiento, el reconocimiento de entidades y más.
80. **Vision**: Un framework que proporciona herramientas para realizar tareas de procesamiento de imágenes y análisis de video, como la detección de caras, objetos y texto.
81. **RealityKit**: Un framework para desarrollar aplicaciones de realidad aumentada, proporcionando herramientas avanzadas para el renderizado, animación y física en AR.
82. **Metal Performance Shaders (MPS)**: Un framework que proporciona una colección de funciones altamente optimizadas para realizar operaciones comunes en gráficos y cálculos científicos utilizando la GPU.
83. **App Clips**: Una funcionalidad que permite a los usuarios acceder a una parte de la funcionalidad de una aplicación sin tener que descargar e instalar la aplicación completa.
84. **Apple Pay**: Un servicio de pagos móviles y cartera digital de Apple que permite a los usuarios realizar pagos en persona, en aplicaciones y en la web utilizando dispositivos iOS.
85. **Accessibility**: Conjunto de características y herramientas que permiten a los desarrolladores crear aplicaciones que sean utilizables por personas con discapacidades.
86. **Sign in with Apple**: Un sistema de autenticación que permite a los usuarios iniciar sesión en aplicaciones y sitios web utilizando su ID de Apple, proporcionando una forma segura y privada de autenticación.
87. **Core Bluetooth**: Un framework que permite a las aplicaciones iOS interactuar con dispositivos Bluetooth de baja energía (BLE).
88. **CarPlay**: Una funcionalidad que permite integrar la interfaz y funcionalidades de una aplicación iOS con el sistema de infoentretenimiento de un vehículo compatible.
89. **Haptic Feedback**: Tecnología que utiliza vibraciones para proporcionar respuestas táctiles al usuario, mejorando la interacción con la aplicación.
90. **Provisional Profile**: Un archivo que contiene permisos y configuraciones necesarias para la distribución de una aplicación iOS a dispositivos específicos para pruebas.
91. **Bitcode**: Una representación intermedia del código fuente de una aplicación que Apple puede optimizar y recompilar para diferentes arquitecturas de dispositivos.
92. **XCConfig**: Archivos de configuración que permiten definir configuraciones de compilación reutilizables y fáciles de gestionar para proyectos de Xcode.
93. **XCUnit Test**: Un marco de pruebas unitarias integrado en Xcode que permite a los desarrolladores escribir y ejecutar pruebas para verificar el comportamiento del código.
94. **UITest**: Un marco de pruebas de interfaz de usuario integrado en Xcode que permite automatizar la interacción con la interfaz de una aplicación para verificar su comportamiento.
95. **Fastlane**: Una herramienta de automatización para la distribución de aplicaciones iOS y Android, que facilita la gestión de certificados, perfiles de aprovisionamiento, compilaciones y envíos a la App Store.
96. **Carthage**: Un gestor de dependencias para proyectos iOS que permite integrar bibliotecas de terceros de una manera simple y ligera.
97. **CocoaPods**: Un gestor de dependencias para proyectos iOS que facilita la integración de bibliotecas de terceros en el proyecto.
98. **Swift Package Manager (SPM)**: Una herramienta para gestionar la distribución de código Swift y su integración en proyectos, facilitando la gestión de dependencias y la modularización del código.
99. **Playground**: Un entorno interactivo en Xcode que permite a los desarrolladores experimentar con código Swift en tiempo real y ver los resultados inmediatamente.
100. **@objc**: Un atributo en Swift que expone métodos y propiedades a Objective-C, permitiendo la interoperabilidad entre Swift y Objective-C.
101. **Module**: Un grupo de código que se puede compilar de forma independiente y se puede importar en otros proyectos, facilitando la reutilización y la modularidad del código.
102. **Resilience**: Un concepto en Swift que permite la evolución del código de una biblioteca sin romper la compatibilidad binaria con el código que la utiliza.
103. **WWDC (Worldwide Developers Conference)**: La conferencia anual de Apple donde se presentan nuevas tecnologías, herramientas y frameworks para desarrolladores.
104. **On-Demand Resources**: Recursos que se descargan y se utilizan bajo demanda en lugar de incluirse en la instalación inicial de la aplicación, reduciendo el tamaño de la aplicación y mejorando la experiencia del usuario.
105. **Dynamic Framework**: Un tipo de framework que se carga en tiempo de ejecución y puede ser compartido entre múltiples aplicaciones.
106. **Static Framework**: Un tipo de framework que se vincula en tiempo de compilación y se incluye directamente en la aplicación, lo que resulta en un mayor tamaño de la aplicación pero menor complejidad en tiempo de ejecución.
107. **App Groups**: Permiten a las aplicaciones y extensiones compartir datos y recursos entre sí de manera segura.
108. **URL Scheme**: Un método para abrir una aplicación iOS específica desde otra aplicación o un enlace web, permitiendo la comunicación y la transferencia de datos entre aplicaciones.
109. **Background Modes**: Modos que permiten a las aplicaciones realizar ciertas tareas en segundo plano, como reproducir audio, recibir ubicaciones GPS y manejar eventos de red.
110. **Application State**: Los diferentes estados en los que puede estar una aplicación iOS, como activa, inactiva, en segundo plano, suspendida y finalizada.
111. **UserDefaults**: Una interfaz para almacenar datos simples y persistentes, como configuraciones y preferencias de usuario.
112. **Plist (Property List)**: Un formato de archivo utilizado por iOS para almacenar datos estructurados como configuraciones y preferencias.
113. **App Thinning**: Un conjunto de técnicas para optimizar el tamaño de la aplicación y mejorar la instalación y la ejecución en dispositivos iOS, incluyendo el uso de Slicing, Bitcode y On-Demand Resources.
114. **Simctl**: Una herramienta de línea de comandos para gestionar el simulador de iOS, permitiendo la creación, gestión y control de dispositivos simulados.
115. **Dynamic Type**: Una característica de iOS que permite a los usuarios ajustar el tamaño del texto en las aplicaciones para mejorar la legibilidad.
116. **Localization**: El proceso de adaptar una aplicación para diferentes idiomas y regiones, incluyendo la traducción de texto y el ajuste de formatos de fecha, hora y números.
117. **Internationalization (i18n)**: El proceso de diseñar y preparar una aplicación para que pueda ser localizada fácilmente en diferentes idiomas y regiones.
118. **Touch Bar**: Una pantalla táctil interactiva situada en el teclado de algunos modelos de MacBook Pro, que permite añadir controles contextuales específicos para la aplicación.
119. **User Interface (UI)**: El conjunto de elementos visuales y de interacción que permiten a los usuarios interactuar con una aplicación.
120. **Human Interface Guidelines (HIG)**: Las directrices de Apple para diseñar interfaces de usuario que sean intuitivas, coherentes y accesibles.
121. **Split View Controller**: Un controlador de vista que gestiona una interfaz de usuario de pantalla dividida, comúnmente utilizado en aplicaciones de iPad para mostrar dos vistas al mismo tiempo.
122. **Tab Bar Controller**: Un controlador de vista que gestiona una interfaz de usuario con una barra de pestañas en la parte inferior, permitiendo la navegación entre diferentes secciones de la aplicación.
123. **Navigation Controller**: Un controlador de vista que gestiona una interfaz de usuario basada en una pila de vistas, permitiendo la navegación hacia adelante y hacia atrás entre vistas.
124. **Table View**: Un componente de interfaz de usuario que muestra una lista de elementos en una columna única, utilizado comúnmente para mostrar datos en una forma estructurada.
125. **Collection View**: Un componente de interfaz de usuario que muestra una colección de elementos en un diseño personalizable, permitiendo diseños de cuadrícula, lista y otros.
126. **Core Spotlight**: Un framework que permite indexar y buscar contenido dentro de una aplicación, integrándose con la búsqueda del sistema de iOS.
127. **Data Protection**: Una característica de seguridad en iOS que utiliza cifrado para proteger los datos almacenados en el dispositivo.
128. **Signpost**: Una herramienta de diagnóstico que permite a los desarrolladores marcar eventos específicos en el tiempo y analizar el rendimiento de la aplicación.
129. **XCTest**: El framework de pruebas de Apple que permite escribir y ejecutar pruebas unitarias, de rendimiento y de interfaz de usuario.
130. **SFSafariViewController**: Un controlador de vista que permite mostrar contenido web dentro de una aplicación utilizando la interfaz de Safari, proporcionando una experiencia de navegación web segura y familiar.
131. **WKWebView**: Un componente de interfaz de usuario que permite integrar y renderizar contenido web dentro de una aplicación utilizando el motor de navegación de Safari.
132. **PassKit**: Un framework que permite a las aplicaciones gestionar tarjetas de pago, entradas, cupones y otros tipos de pases en la aplicación Wallet.
133. **MediaPlayer**: Un framework que proporciona interfaces para reproducir y controlar contenido multimedia, como música y videos.
134. **EventKit**: Un framework que permite a las aplicaciones acceder y gestionar eventos y recordatorios del calendario del usuario.
135. **Multipeer Connectivity**: Un framework que permite la comunicación y el intercambio de datos entre dispositivos cercanos mediante Wi-Fi, Bluetooth y redes peer-to-peer.
136. **Game Center**: Una plataforma de servicios de juegos en línea de Apple que permite a los desarrolladores integrar funcionalidades como tablas de clasificación, logros y partidas multijugador.
137. **Reality Composer**: Una herramienta que permite crear y probar experiencias de realidad aumentada sin necesidad de escribir código, utilizando una interfaz visual intuitiva.
138. **MetricKit**: Un framework que proporciona métricas y diagnósticos del rendimiento y uso de la aplicación, ayudando a los desarrolladores a identificar y resolver problemas.
139. **CloudKit Dashboard**: Una interfaz web que permite a los desarrolladores gestionar y supervisar la base de datos de CloudKit utilizada por sus aplicaciones.
140. **Custom URL Scheme**: Una técnica que permite a las aplicaciones abrir y comunicarse con otras aplicaciones utilizando URLs personalizados.
141. **Deep Linking**: Un método para dirigir a los usuarios a una ubicación específica dentro de una aplicación desde una URL externa, mejorando la navegación y la experiencia del usuario.
142. **Siri Shortcuts**: Funcionalidades que permiten a los usuarios realizar tareas rápidas en las aplicaciones mediante comandos de voz a Siri.
143. **Core NFC**: Un framework que permite a las aplicaciones leer etiquetas NFC (Near Field Communication) para interactuar con el mundo físico.
144. **AudioToolbox**: Un framework que proporciona interfaces para la reproducción, grabación y manipulación de audio en aplicaciones iOS.
145. **AVKit**: Un framework que proporciona una interfaz para la reproducción de contenido audiovisual, incluyendo la integración con el sistema de reproducción nativo de iOS.
146. **CryptoKit**: Un framework que proporciona interfaces para realizar operaciones criptográficas seguras, como el cifrado y la generación de firmas digitales.
147. **Network Extension**: Un framework que permite a las aplicaciones crear y gestionar extensiones de red personalizadas, como VPNs y filtros de contenido.
148. **Push Notifications**: Mensajes enviados desde un servidor a una aplicación iOS, permitiendo la comunicación y actualización de información en tiempo real.
149. **Launch Screen**: Una pantalla inicial que se muestra mientras la aplicación está cargando, proporcionando una transición suave y mejorando la experiencia del usuario.
150. **NSPersistentContainer**: Una clase que encapsula el código de configuración de Core Data y simplifica la creación y gestión del stack de Core Data.