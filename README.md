# Antipatrones de Diseño

Integrantes:

- Brayan Alejandro Puentes Camargo - 20181020044
- Jhonnatan Guillermo Ruiz Bautista - 20181020034 
- Juan Camilo Ramírez Rátiva - 20181020089

## Anti-patrón Gota

### También conocido como: The Blob, The God Class

Se encuentra en diseños donde una clase monopoliza el procesamiento y otras clases principalmente encapsulan datos. Este Anti-patrón se caracteriza por un diagrama de clases compuesto por una única clase de controlador compleja rodeada de clases de datos simples. El problema clave aquí es que la mayoría de las responsabilidades se asignan a una sola clase.

En general, la Gota es un diseño de procedimental, aunque puede representarse mediante notaciones de objetos e implementarse en lenguajes orientados a objetos. Un diseño de procedimental separa los procesos de los datos, mientras que un diseño orientado a objetos fusiona los modelos de proceso y de datos, junto con las particiones.

La Gota contiene la mayor parte de los procesos y los demás objetos contienen los datos. Las arquitecturas con la Gota han separado los procesos de los datos; en otras palabras, son arquitecturas más de estilo procedimental que orientadas a objetos.

La Gota puede ser el resultado de una asignación de requisitos inadecuada. Por ejemplo, La Gota puede ser un módulo de software al que se le asignan responsabilidades que se superponen a la mayoría de las otras partes del sistema para el control o la gestión del sistema.

La Gota también es con frecuencia el resultado de un desarrollo iterativo en el que el código de prueba evoluciona con el tiempo hasta convertirse en un prototipo y, finalmente, en un sistema de producción. Esto a menudo se ve agravado por el uso de lenguajes de programación centrados principalmente en GUI, como Visual Basic, que permiten que una forma simple evolucione su funcionalidad y, por lo tanto, su propósito, durante el desarrollo incremental o la creación de prototipos.

La asignación de responsabilidades no se reparte durante la evolución del sistema, de modo que un módulo se vuelve predominante. La Gota suele ir acompañada de código innecesario (Anti-patrón Código Muerto), lo que dificulta la diferenciación entre la funcionalidad útil de la clase Gota y el código que ya no se usa.


### Síntomas

- Clase única con una gran cantidad de atributos, operaciones o ambos. Una clase con 60 o más atributos y operaciones generalmente indica la presencia de la Gota
- Una colección dispar de operaciones y atributos no relacionados encapsulados en una sola clase. Una falta general de cohesión de los atributos y operaciones es típica de este anti-patrón.
- Una sola clase de controlador con clases de objetos de datos simples asociadas.
- Ausencia de diseño orientado a objetos. Un bucle principal del programa dentro de la clase Gota asociado con objetos de datos relativamente pasivos. La clase controlador a menudo encapsula casi toda la funcionalidad de la aplicación, al igual que un programa principal.
- Un diseño heredado migrado que no se ha refactorizado correctamente en una arquitectura orientada a objetos.

### Consecuencias

- La Gota compromete las ventajas inherentes de un diseño orientado a objetos. Por ejemplo, limita la capacidad de modificar el sistema sin afectar la funcionalidad de otros objetos encapsulados. Las modificaciones a la clase Gota afectan el software extenso dentro de la encapsulación. También es probable que las modificaciones en otros objetos del sistema tengan un impacto en el software de la Gota.
- La clase Gota suele ser demasiado compleja para su reutilización y prueba. Puede ser ineficaz o introducir una complejidad excesiva al reutilizar la Gota para subconjuntos de su funcionalidad.
- La clase Gota puede ser costosa de cargar en la memoria, ya que usa recursos excesivos, incluso para operaciones simples.

### Causas

- Falta de una arquitectura orientada a objetos. Es posible que los diseñadores no tengan una comprensión adecuada de los principios orientados a objetos. Alternativamente, el equipo puede carecer de las habilidades de abstracción adecuadas.
- Falta de (alguna) arquitectura. La ausencia de definición de los componentes del sistema, sus interacciones y el uso específico de los lenguajes de programación seleccionados. Esto permite que los programas evolucionen de manera ad-hoc porque los lenguajes de programación se utilizan para fines distintos a los previstos.
- Falta de aplicación de la arquitectura. A veces, este anti-patrón crece accidentalmente, incluso después de que se planeó una arquitectura razonable. Esto puede ser el resultado de una revisión arquitectónica inadecuada a medida que se lleva a cabo el desarrollo. Esto es especialmente frecuente en los equipos de desarrollo nuevos en la orientación a objetos.
- Intervención demasiado limitada. En proyectos iterativos, los desarrolladores tienden a agregar pequeñas piezas de funcionalidad a las clases trabajadoras existentes, en lugar de agregar nuevas clases o revisar la jerarquía de clases para una asignación de responsabilidades más efectiva.
- Desastre especificado. A veces, la Gota resulta de la forma en que se especifican los requisitos. Si los requisitos dictan una solución de procedimiento, entonces se pueden realizar compromisos de arquitectura durante el análisis de requisitos que son difíciles de cambiar. Definir la arquitectura del sistema como parte del análisis de requisitos suele ser inapropiado y, a menudo, conduce a este anti-patrón, o algo peor.

### Solución

La solución implica una forma de refactorización. La clave es alejar el comportamiento de la Gota. Puede ser apropiado reasignar el comportamiento a algunos de los objetos de datos encapsulados de manera que estos objetos sean más capaces y la Gota menos compleja. El método para refactorizar las responsabilidades se describe a continuación:

1. Identificar o categorizar atributos y operaciones relacionados de acuerdo con los contratos. Estos contratos deben ser cohesivos en el sentido de que todos se relacionan directamente con un enfoque, comportamiento o función común dentro del sistema general. Por ejemplo, un diagrama de arquitectura de un sistema de biblioteca se representa con una clase Gota potencial llamada LIBRARY.

En el ejemplo que se muestra en la figura, la clase LIBRARY encapsula la suma total de todas las funciones del sistema. Por lo tanto, el primer paso es identificar conjuntos cohesivos de operaciones y atributos que representan contratos. En este caso, podríamos recopilar operaciones relacionadas con la gestión de catálogos, como Sort_Catalog y Search_Catalog.

También podríamos identificar todas las operaciones y atributos relacionados con elementos individuales, como Print_Item, Delete_Item, etc.

![alt text](https://github.com/jgruizba/Antipatrones/blob/master/Blow_ex_sol_a.png)

![alt text](https://github.com/jgruizba/Antipatrones/blob/master/Blow_ex_sol_b.png)

2. El segundo paso es buscar "hogares naturales" para estas colecciones de funcionalidad basadas en contratos y luego migrarlas allí. En este ejemplo, recopilamos operaciones relacionadas con catálogos y las migramos de la clase LIBRARY y las trasladamos a la clase CATALOG.

Hacemos lo mismo con las operaciones y atributos relacionados con los artículos, moviéndolos a la clase ITEM. Esto simplifica la clase LIBRARY y hace que las clases ITEM y CATALOG sean más que simples tablas de datos encapsulados. El resultado es un mejor diseño orientado a objetos.

![alt text](https://github.com/jgruizba/Antipatrones/blob/master/Blow_ex_sol_c.png)

3. El tercer paso es eliminar todas las asociaciones indirectas "acopladas a distancia" o redundantes. En el ejemplo, la clase ITEM está inicialmente acoplada de forma remota a la clase LIBRARY en que cada elemento realmente pertenece a un CATALOG, que a su vez pertenece a una LIBRARY.

4. A continuación, cuando sea apropiado, migramos asociados a clases derivadas a una clase base común. En el ejemplo, una vez que se ha eliminado el acoplamiento lejano entre las clases LIBRARY y ITEM, debemos migrar los ITEM a los CATALOG, como se muestra en la siguiente figura.

![alt text](https://github.com/jgruizba/Antipatrones/blob/master/Blow_ex_sol_d.png)

## Anti-patrón Fantasma

### También conocido como: Poltergeist, Gypsy

Los fantasmas son clases con responsabilidades y roles limitados que desempeñar en el sistema; por lo tanto, su ciclo de vida efectivo es bastante breve. Los fantasmas desordenan los diseños de software, creando abstracciones innecesarias; son excesivamente complejos, difíciles de entender y difíciles de mantener.

Este anti-patrón es típico en los casos en que los diseñadores familiarizados con el modelado de procesos pero nuevos en el diseño orientado a objetos definen arquitecturas. En este anti-patrón, es posible identificar una o más clases de apariciones fantasmales que aparecen solo brevemente para iniciar alguna acción en otra clase más permanente. Normalmente los fantasmas se inventan como clases de controlador que existen sólo para invocar métodos de otras clases, generalmente en una secuencia predeterminada. Suelen ser obvios porque sus nombres a menudo contienen el sufijo _manager o _controller.

El anti-patrón fantasma suele ser intencional por parte de algún arquitecto novato que realmente no comprende el concepto orientado a objetos. Las clases fantasma constituyen malos artefactos de diseño por tres razones clave:

- Son innecesarios, por lo que desperdician recursos cada vez que "aparecen".
- Son ineficientes porque utilizan varias rutas de navegación redundantes.
- Se interponen en el camino del diseño orientado a objetos adecuado al saturar innecesariamente el modelo de objetos.

### Síntomas y Consecuencias

- Rutas de navegación redundantes.
- Asociaciones transitorias.
- clases sin estado.
- Clases y objetos temporales, de corta duración.
- Clases de operación única que existen solo para "inicializar" o "invocar" otras clases a través de asociaciones temporales.
- Clases con nombres de operaciones "similares a controles" como start_process_alpha.

### Causas

- Falta de arquitectura orientada a objetos. "Los diseñadores no conocen la orientación a objetos".
Herramienta incorrecta para el trabajo.
- Contrariamente a la opinión popular, el enfoque orientado a objetos no es necesariamente la solución adecuada para cada trabajo. Como decía una vez un cartel: "No hay forma correcta de hacer lo incorrecto".
Es decir, si la orientación a objetos no es la herramienta adecuada, no hay una forma correcta de implementarla.
- Desastre especificado. La administración a veces realiza compromisos de arquitectura durante el análisis de requisitos. Esto es inapropiado y, a menudo, conduce a problemas como este.

### Ejemplo

Considere el ejemplo de un sistema de enlatado de melocotón en la siguiente figura.

![alt text](https://github.com/jgruizba/Antipatrones/blob/master/Polt_ex_sol.png)

Vemos que la clase PEACH_CANNER_CONTROLLER es un Fantasma porque:
- Tiene rutas de navegación redundantes a todas las demás clases del sistema.
- Todas sus asociaciones son transitorias.
- No tiene estado.
- Es una clase temporal de corta duración que aparece solo para invocar otras clases a través de asociaciones temporales.

En este ejemplo, si eliminamos la clase fantasma, las clases restantes pierden la capacidad de interactuar. Ya no hay ningún orden de procesos. Por lo tanto, debemos colocar dicha capacidad de interacción en la jerarquía restante. Es necesario agregar ciertas operaciones a cada proceso de manera que las clases individuales interactúen y procesen los resultados.

![alt text](https://github.com/jgruizba/Antipatrones/blob/master/Polt_ex_pro.png)

### Solución
Los Caza-fantasmas resuelven los fantasmas eliminándolos por completo de la jerarquía de clases. Sin embargo, después de su eliminación, la funcionalidad que fue "proporcionada" por el fantasma debe ser reemplazada. Esto es fácil con un simple ajuste para corregir la arquitectura.

La clave es mover las acciones de control inicialmente encapsuladas en el fantasma a las clases relacionadas.

## Anti-patrón Código Muerto

### También conocido como: Lava Flow

Este anti-patrón de diseño ocurre cuando el software es recibido antes de su finalización o sin contar con las pruebas completas para su ejecución y este al ser entregado, no puede modificar sus características, imitando la analogía de cuando la lava que sale de un volcán se seca.

Este anti-patrón se caracteriza por estar esparcido en versiones antiguas del software de manera inamovible, ya que no existe una clara identificación sobre como interactúa estos fragmentos del código con el software como tal, causa de una mal estructura y documentación 

### Síntomas

- Interfaces obsoletas, con ninguna participación y puestos en archivos de cabecera.
- Variables y fragmentos de código sin justificación, de manera sistemática.
- Conjunto de líneas de código o objetos que no tienen forma clara sobre su funcionalidad ni previa documentación.

### Causas típicas:

- El software comúnmente que presentan código muerto han sido desarrollados por un único desarrollador, y no en trabajos conjuntos.
- El software puede contener muchos métodos de prueba para evaluar funcionalidades del sistema
- Código elaborado a las carreras, que no fue documentando ni verificado
- Falta de patrones de diseño, sin alguna orientación o arquitectura
- Múltiples parches de correcciones al sistema

### Consecuencias:

- Si los niveles de código muerto en el software tienen un crecimiento considerable, este programa se vuelve díficil de documentar, lo que hace que entender su funcionamiento parezca como descifrar un código encriptado.

- El diseño del programa pierde su diseño orientado a objetos, perdiendo consigo la modularidad, convirtiendo al software en un gran inconveniente para su mantenimiento, reutilización e implementación.

### Solución:

- Para evitar este anti patrón, lo primero es partir del inicio del código de manera correcta, y en caso de que este software este en mantenimiento, lo mejor es hacer una correcta documentación, recuperando el desarrollo de la estructura del software.

- Durante las transiciones de las actualizaciones del software es necesario que las partes desactualizadas sean borradas o en su caso, reemplazadas con el fin de evitar el código muerto.

## Anti-patrón Código Espagueti

### También conocido como: Spaghetti Code

- es un anti-patrón definido por un código que está mal estructurado, es confuso y difícil de entender, que contiene todo tipo de ramificaciones, como excepciones, condiciones y bucles de envoltura. Anteriormente, el operador Goto era el principal aliado de este anti-patrón.

- Los programadores que escriben código espagueti generalmente aprendieron a codificar en un lenguaje no estructurado como BASIC, y nunca se molestaron en actualizar sus conocimientos técnicos cuando progresaron a lenguajes más serios. 


### Causas:

**Rápido y sucio:** Por lo general es difícil evitar situaciones en las que es necesario preparar una solución rápida y sucia. pero esto por sí solo no va a crear este anti-patrón. Sin embargo, cuando deja que este tipo de soluciones se acumule, se llega a este patrón donde tendrá muy poca claridad el código y sera muy extenso.

### Consecuencias:

- Debido a que es un código poco flexible se torna muy difícil realizar un cambios a dicho código por lo que a veces es mejor comenzar desde cero debido a que  se necesita menos tiempo para reconstruir la solución que para comprenderla y modificarla.

### Solución

- La refactorización es la mejor solución, pero una onza de prevención vale una libra de curación, por lo que el nombre, la estructura y las revisiones adecuadas para los estándares del equipo evitarán que su código se vuelva espaguetizado.  

### Referencias

- [https://sourcemaking.com/antipatterns/software-development-antipatterns](https://sourcemaking.com/antipatterns/software-development-antipatterns)
