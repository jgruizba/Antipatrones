# Antipatrones de Diseño

Integrantes:

- Brayan Alejandro Puentes Camargo - 20181020044
- Jhonnatan Guillermo Ruiz Bautista - 20181020034 
- Juan Camilo Ramírez Rátiva - 20181020089

## Antipatrón Lava Flow

Este antipatrón de diseño lava flow, ocurre cuando el software es recibido antes de su finalización o sin contar con las pruebas completas para su ejecucion y este al ser entregado, no puede modificar sus caracteristicas, imitando la analogia de cuando la lava que sale de un volcán se seca.

Este antipatron se catacteriza por estar esparcido en versiones antiguas del software de manera inamovible, ya que no existe una clara identificación sobre como interactúa estos fragmentos del código con el software como tal, causa de una mal estructura y documentación 

### Síntomas de Software:

- Interfaces obsoletas, con ninguna participación y puestos en archivos de cabecera.
- Variables y fragmentos de código sin justificación, de manera sistemática.
- Conjunto de líneas de código o objetos que no tienen forma clara sobre su funcionalidad ni previa documentación.

### Causas típicas:

- El software comúnmente que presentan Lava Flow han sido desarrollados por un único desarrollador, y no en trabajos conjuntos.
- El software puede contener muchos métodos de prueba para evaluar funcionalidades del sistema
- Código elaborado a las carreras, que no fue documentando ni verificado
- Falta de patrones de diseño, sin alguna orientación o arquitectura
- Múltiples parches de correcciones al sistema

### Consecuencias:

- Si los niveles de Lava Flow en el software tienen un crecimiento considerable, este programa se vuelve no documentable, lo que hace que entender su funcionamiento parezca como descifrar un código encriptado.

- El diseño del programa pierde su diseño orientado a objetos, perdiendo consigo la modularidad, convirtiendo al software en un gran inconveniente para su mantenimiento, reutilización e implementación.

### Solución:

- Para evitar este anti patrón, lo primero es partir del inicio del código de manera correcta, y en caso de que este software este en mantenimiento, lo mejor es hacer una correcta documentación, recuperando el desarrollo de la estructura del software.

- Durante las transiciones de las actualizaciones del software es necesario que las partes desactualizadas sean borradas o en su caso, reemplazadas con el fin de evitar el código muerto.

## Patron Spaghetti code

- es un anti-patrón definido por un código que está mal estructurado, es confuso y difícil de entender, que contiene todo tipo de ramificaciones, como excepciones, condiciones y bucles de envoltura. Anteriormente, el operador goto era el principal aliado de este anti-patrón.

- Los programadores que escriben código espagueti generalmente aprendieron a codificar en un lenguaje no estructurado como BASIC, y nunca se molestaron en actualizar sus conocimientos técnicos cuando progresaron a lenguajes más serios. 


### Causas:

- **Rápido y sucio**
por lo generarl es difícil evitar situaciones en las que es necesario preparar una solución rápida y sucia. pero esto por sí solo no va a crear este anti-patrón. Sin embargo, cuando deja que este tipo de soluciones se acumule, se llega a este patron donde tendra muy poca clarida el codigo y sera muy extenso.

### Consecuencias:

- debido a que es un codigo poco flexible se torna muy dificil realizar un cambios a dicho codigo por lo que a veses es mejor comenzar desde cero debido a que  se necesita menos tiempo para reconstruir la solución que para comprenderla y modificarla.

### Solución

- La refactorización es la mejor solución, pero una onza de prevención vale una libra de curación, por lo que el nombre, la estructura y las revisiones adecuadas para los estándares del equipo evitarán que su código se vuelva espaguetizado.  

## Antipatron Fantasma (Poltergeist)

Los fantasmas son clases con responsabilidades y roles limitados que desempeñar en el sistema; por lo tanto, su ciclo de vida efectivo es bastante breve. Los fantasmas desordenan los diseños de software, creando abstracciones innecesarias; son excesivamente complejos, difíciles de entender y difíciles de mantener.

Este anti-patrón es típico en los casos en que los diseñadores familiarizados con el modelado de procesos pero nuevos en el diseño orientado a objetos definen arquitecturas. En este anti-patrón, es posible identificar una o más clases de apariciones fantasmales que aparecen solo brevemente para iniciar alguna acción en otra clase más permanente. Normalmente los fantasmas se inventan como clases de controlador que existen sólo para invocar métodos de otras clases, generalmente en una secuencia predeterminada. Suelen ser obvios porque sus nombres a menudo contienen el sufijo _manager o _controller.

El anti-patrón fantasma suele ser intencional por parte de algún arquitecto novato que realmente no comprende el concepto orientado a objetos. Las clases de poltergeist constituyen malos artefactos de diseño por tres razones clave:

- Son innecesarios, por lo que desperdician recursos cada vez que "aparecen".
- Son ineficientes porque utilizan varias rutas de navegación redundantes.
- Se interponen en el camino del diseño orientado a objetos adecuado al saturar innecesariamente el modelo de objetos.

### Sintomas y consecuencias

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

### Solución
Los Cazafantasmas resuelven los fantasmas eliminándolos por completo de la jerarquía de clases. Sin embargo, después de su eliminación, la funcionalidad que fue "proporcionada" por el poltergeist debe ser reemplazada. Esto es fácil con un simple ajuste para corregir la arquitectura.

La clave es mover las acciones de control inicialmente encapsuladas en Poltergeist a las clases relacionadas que invocaron.
