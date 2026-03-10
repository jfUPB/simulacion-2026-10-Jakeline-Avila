# Unidad 4

## Bitácora de proceso de aprendizaje

### Actividad 1

Lo que más me llamó la atención de la obra de Memo Akten es la forma en que utiliza la tecnología y el movimiento para crear arte visual basado en principios científicos. En la serie Simple Harmonic Motion, el artista transforma conceptos de la física, como el movimiento armónico, en una experiencia visual dinámica y estética.

Me pareció interesante cómo patrones simples de movimiento pueden generar formas complejas y atractivas. Esto demuestra que las matemáticas y la física no solo sirven para explicar fenómenos naturales, sino que también pueden utilizarse como herramientas creativas en el arte digital.

Otro aspecto que me llamó la atención es la relación entre ciencia, arte y programación. La obra muestra cómo los algoritmos y las simulaciones pueden convertirse en medios de expresión artística, lo que abre nuevas posibilidades para explorar la creatividad mediante la tecnología.

En general, esta obra me hizo pensar en cómo los conceptos científicos pueden inspirar procesos creativos y en cómo el arte digital puede ayudarnos a visualizar fenómenos que normalmente solo entendemos de forma teórica.

### Actividad 2

1. Simulación sobre manejo de ángulos

¿Qué está pasando en la simulación? ¿Cuál es la interacción?
En la simulación se observa un objeto que rota alrededor del centro de la pantalla. La interacción consiste en que el sistema calcula un ángulo de rotación y, a partir de ese valor, los elementos gráficos giran. Esto permite visualizar cómo funciona la rotación en un sistema de coordenadas dentro de una animación.

¿Por qué se traslada el origen del sistema de coordenadas al centro de la pantalla?
Se hace para facilitar la rotación de los objetos. Si el origen está en el centro, los elementos pueden rotar alrededor de ese punto de manera más natural y simétrica. Si el origen estuviera en una esquina, la rotación sería más difícil de controlar y los cálculos serían más complejos.

¿Cuál es la relación entre el sistema de coordenadas y la función rotate()?
La función rotate() rota el sistema de coordenadas completo. Esto significa que todos los elementos que se dibujen después se orientarán según ese nuevo ángulo de rotación.

¿Por qué los elementos parecen dibujarse en (0,0)?
Los elementos se dibujan cerca del origen porque el sistema de coordenadas fue trasladado previamente al centro de la pantalla. De esta forma, dibujar cerca del punto (0,0) permite que el objeto gire alrededor de ese punto central.

¿Por qué los elementos rotan si en cada frame se dibuja lo mismo?
Porque antes de dibujar los elementos se aplica una transformación de rotación al sistema de coordenadas. Aunque el código que dibuja las figuras sea el mismo en cada frame, el sistema de coordenadas ya está rotado, lo que hace que los objetos aparezcan girando.

2. Simulación sobre orientación según el movimiento

¿Qué ocurre en el marco Motion 101?
En el marco Motion 101 se muestra cómo un objeto se mueve en la pantalla usando vectores de posición y velocidad. El objeto no solo se mueve, sino que también cambia su orientación para apuntar en la dirección en la que se está desplazando.

¿Qué hace la función heading()?
La función heading() obtiene el ángulo del vector de velocidad. Este ángulo indica la dirección hacia la que se mueve el objeto.

¿Qué hacen push() y pop()?
Estas funciones guardan y restauran el estado del sistema de transformaciones.

push() guarda la configuración actual del sistema de coordenadas.

pop() restaura esa configuración después de aplicar transformaciones como translate() o rotate().

Esto permite que las transformaciones solo afecten al objeto actual y no a los demás elementos que se dibujen después.

¿Qué hace rectMode(CENTER)?
Esta función cambia la forma en que se dibujan los rectángulos. Con CENTER, el rectángulo se dibuja desde su centro en lugar de desde la esquina superior izquierda. Esto facilita la rotación del objeto alrededor de su propio centro.

Relación entre el ángulo de rotación y el vector de velocidad
El vector de velocidad indica la dirección del movimiento del objeto. La función heading() convierte esa dirección en un ángulo. Luego, ese ángulo se usa en rotate(angle) para orientar el objeto en la misma dirección en la que se está moviendo.

Primero se traslada el sistema de coordenadas a la posición del objeto (translate). Después se aplica la rotación (rotate) basada en el ángulo del vector de velocidad. Finalmente se dibuja el objeto centrado en ese punto.

## Bitácora de aplicación 



## Bitácora de reflexión
