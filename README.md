# Antipatrones de Diseño

Integrantes:

- Brayan Alejandro Puentes Camargo - 20181020044
- Jhonnatan Guillermo Ruiz Bautista - 20181020034 
- Juan Camilo Ramírez Rátiva - 20181020089

## Antipatrón Lava Flow

<p align= "Justify">Este antipatrón de diseño lava flow, ocurre cuando el software es recibido antes de su finalización o sin contar con las pruebas completas para su ejecucion y este al ser entregado, no puede modificar sus caracteristicas, imitando la analogia de cuando la lava que sale de un volcán se seca.</p>

<p align= "Justify">Este antipatron se catacteriza por estar esparcido en versiones antiguas del software de manera inamovible, ya que no existe una clara identificación sobre como interactúa estos fragmentos del código con el software como tal, causa de una mal estructura y documentación </p>

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
