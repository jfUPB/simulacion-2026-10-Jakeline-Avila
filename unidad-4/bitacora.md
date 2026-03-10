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


### Actividad 3

Práctica de movimiento y rotación

En esta actividad desarrollé una simulación de un vehículo que puede moverse por la pantalla usando las teclas de flecha. El objetivo era aplicar los conceptos de vectores, rotación y traslación para que el vehículo no solo se moviera, sino que también apuntara en la dirección de su movimiento.

Proceso de creación

Primero definí las variables principales del vehículo: posición, velocidad y aceleración. Estas variables permiten controlar el movimiento del objeto en la pantalla. La posición indica dónde está el vehículo, la velocidad indica hacia dónde se está moviendo y la aceleración se usa para modificar la velocidad cuando se presionan las teclas.

Después programé la interacción con el teclado. Utilicé las flechas izquierda y derecha para aplicar aceleración al vehículo en esas direcciones. Cada vez que se presiona una tecla, se modifica la aceleración y esta se suma a la velocidad para producir el movimiento.

Luego implementé la rotación del vehículo. Para lograr que el triángulo apuntara en la dirección del movimiento, utilicé el ángulo del vector de velocidad. Este ángulo se usa con la función de rotación para orientar el vehículo correctamente.

También utilicé las funciones de transformación del sistema de coordenadas. Primero trasladé el sistema de coordenadas a la posición del vehículo y luego apliqué la rotación. Después dibujé el triángulo centrado en ese punto para que girara correctamente.

Resultados y aprendizaje

Al final logré que el vehículo se moviera por la pantalla y que el triángulo siempre apuntara hacia la dirección en la que se desplaza. Esto me ayudó a entender mejor cómo funcionan los vectores de movimiento y cómo las transformaciones como translate y rotate afectan el dibujo de los objetos.

Esta actividad también me permitió comprender la importancia de organizar bien las transformaciones para controlar correctamente la posición y la orientación de los elementos en una simulación.

### Actividad 4

Relación con el marco Motion 101

En esta actividad analicé la simulación Motion 101 con fuerzas para entender cómo se integran los conceptos de movimiento con la aplicación de fuerzas.

Identificación de Motion 101

El marco Motion 101 describe el modelo básico de movimiento utilizando tres variables principales: posición, velocidad y aceleración. En cada frame de la simulación, la aceleración se suma a la velocidad y la velocidad se suma a la posición para actualizar el movimiento del objeto.

Modificación al agregar fuerzas acumulativas

Cuando se agregan fuerzas acumulativas al modelo Motion 101 es necesario modificar la forma en que se maneja la aceleración. En lugar de asignar directamente un valor a la aceleración, las fuerzas se acumulan en la aceleración durante cada frame.

Después de actualizar la velocidad, la aceleración debe reiniciarse a cero. Esto se hace porque las fuerzas solo deben aplicarse durante el frame actual. Si no se reinicia, las fuerzas se seguirían acumulando continuamente y el movimiento no sería correcto.

Identificación del Attractor

En la simulación aparece un objeto llamado Attractor, que representa un punto que ejerce una fuerza de atracción sobre el vehículo o partícula. Este objeto generalmente está ubicado en el centro o en una posición fija de la pantalla.

Para cambiar su color se puede modificar la función que lo dibuja, cambiando el valor de fill() dentro de su método display().

Ejemplo:
``` js

fill(255, 0, 0); // rojo
ellipse(this.position.x, this.position.y, this.mass*2);

```
Uso de los atributos dragging y rollover

El Attractor tiene dos atributos importantes:

dragging: indica si el objeto está siendo arrastrado con el mouse.

rollover: indica si el mouse está pasando sobre el objeto.

Aunque estos atributos existen, en la simulación no se están modificando. Para activarlos se pueden usar funciones de interacción con el mouse de p5.js como:

mousePressed()

mouseReleased()

mouseDragged()

mouseMoved()

Por ejemplo:

Detectar cuando el mouse está sobre el attractor:

``` js
let d = dist(mouseX, mouseY, this.position.x, this.position.y);
if (d < this.mass) {
  this.rollover = true;
} else {
  this.rollover = false;
}

Permitir arrastrar el attractor:

function mousePressed() {
  if (attractor.rollover) {
    attractor.dragging = true;
  }
}

function mouseReleased() {
  attractor.dragging = false;
}

function mouseDragged() {
  if (attractor.dragging) {
    attractor.position.x = mouseX;
    attractor.position.y = mouseY;
  }
}
```

Con estas modificaciones, el attractor podría cambiar de color cuando el cursor pase sobre él y también moverse por la pantalla al arrastrarlo con el mouse.

Reflexión

Esta actividad me ayudó a comprender mejor cómo integrar fuerzas en el modelo Motion 101 y cómo las simulaciones pueden volverse interactivas utilizando eventos del mouse. También entendí cómo organizar el código para que los objetos tengan comportamientos más dinámicos dentro de la simulación.

## Bitácora de aplicación 



## Bitácora de reflexión

