# Unidad 5
## Bitácora de proceso de aprendizaje
### Actividad 1

Capa de comportamiento

Cada partícula tiene propiedades que se dividen en estado físico y estado vital. El estado físico está compuesto por la posición, la velocidad y la aceleración, ya que estas determinan cómo se mueve la partícula en el espacio. El estado vital está representado por el lifespan, que define cuánto tiempo permanece activa. Una partícula “muere” cuando su lifespan llega a cero o es menor, y esta muerte es gradual, ya que el valor disminuye poco a poco en cada frame, generando un efecto de desvanecimiento. En cada actualización se aplica el patrón Motion 101: la velocidad se modifica con la aceleración, la posición se actualiza con la velocidad y finalmente se reduce el lifespan, integrando así movimiento y ciclo de vida en un mismo sistema.

Capa de estructura

Las partículas son creadas por el sistema, generalmente dentro del draw, lo que permite una emisión continua en el tiempo. El mismo sistema es quien decide cuándo eliminarlas, verificando si están “muertas” mediante una condición como isDead(). El array se recorre en orden inverso al momento de eliminar partículas para evitar errores de índice; si se recorriera de forma normal (de inicio a fin), al eliminar un elemento los índices cambiarían y se podrían saltar partículas o generar comportamientos inesperados. Si no se eliminaran nunca las partículas, el sistema acumularía cada vez más objetos en memoria, lo que provocaría una caída progresiva del rendimiento y del frame rate, pudiendo incluso llegar a congelar la ejecución.

Capa de visualización

Visualmente, cada partícula se representa generalmente como una forma simple, como un círculo dibujado con ellipse(), acompañado de transparencia. El tiempo de vida (lifespan) está directamente conectado con la apariencia visual, ya que se utiliza para controlar la opacidad del color, haciendo que la partícula se desvanezca a medida que se acerca a su muerte. Si se quisiera cambiar la representación visual, por ejemplo usar líneas en lugar de círculos, solo sería necesario modificar la función de dibujo, mientras que las propiedades físicas, la lógica de actualización y el sistema de vida y muerte permanecerían intactos, evidenciando la separación entre visualización, comportamiento y estructura.

### Actividad 2

En este ejemplo, la gestión de partículas deja de hacerse directamente en el ciclo principal y se encapsula dentro de una entidad llamada emisor. Cada emisor se encarga de crear, actualizar y eliminar sus propias partículas, lo que permite una mejor organización del sistema.

El programa principal ahora maneja una colección de emisores, mientras que cada emisor contiene su propia colección de partículas, formando una estructura jerárquica de dos niveles.

Este enfoque introduce el concepto de sistema de sistemas, donde múltiples entidades autónomas administran su propio estado, ciclo de vida y comportamiento frente a fuerzas, facilitando la escalabilidad y modularidad del sistema

### Actividad 3

En este ejemplo, las distintas subclases de partículas comparten una estructura y comportamiento base definidos por la clase principal. Todas poseen atributos como posición, velocidad, aceleración y tiempo de vida, y siguen el mismo ciclo de actualización mediante métodos comunes. Sin embargo, se diferencian en su representación visual, ya que cada subclase puede redefinir la forma en que se muestra, lo que introduce variedad sin alterar la lógica fundamental del sistema.

Resulta fundamental que el emisor no necesite conocer el tipo específico de partícula que está gestionando. Esto se debe a que todas las partículas responden a la misma interfaz de comportamiento, lo que permite tratarlas de manera uniforme. Gracias a esto, el sistema se vuelve más flexible y extensible, ya que el emisor únicamente ejecuta y evalúa el estado de cada partícula sin depender de su implementación concreta.

Si se quisiera agregar un nuevo tipo de partícula, bastaría con crear una nueva subclase que herede de la clase base y, si es necesario, redefinir ciertos métodos como el de visualización. No sería necesario modificar la lógica del emisor ni el funcionamiento general del sistema, lo que evidencia una correcta separación de responsabilidades y un diseño escalable.

En comparación con el ejemplo anterior, la lógica del emisor y el mecanismo de eliminación de partículas permanecen sin cambios. La modificación se introduce exclusivamente en la capa de las partículas, donde se aplica herencia y polimorfismo para diversificar el comportamiento visual. Esto demuestra que es posible ampliar las capacidades del sistema sin alterar su estructura central.

### Actividad 4
Fuerzas globales vs. locales

En el Example 4.6, la gravedad se define en el ciclo principal como un vector constante. Esta fuerza es aplicada por el emisor a todas las partículas mediante el método applyForce(). Por lo tanto, se trata de una fuerza global, ya que afecta a todas las partículas por igual, sin depender de condiciones individuales.

En el Example 4.7, además de la gravedad, se introduce una nueva fuerza generada por un objeto llamado repeller. La diferencia principal es que la gravedad sigue siendo una fuerza global, mientras que la fuerza del repeller es local, ya que depende de la posición relativa entre cada partícula y el repeller. La gravedad “vive” en el sistema global (ciclo principal), mientras que la lógica del repeller está encapsulada dentro de su propia entidad.

La fuerza del repeller depende de la distancia entre la partícula y el repeller, siguiendo una relación inversamente proporcional al cuadrado de la distancia. Esto modela un principio físico similar a las leyes de atracción o repulsión gravitacional/electrostática, donde la intensidad de la fuerza disminuye con la distancia.

Es importante notar que la clase Particle no cambia entre los ejemplos 4.6 y 4.7. Esto implica que las partículas no necesitan conocer el origen de las fuerzas que reciben, lo que evidencia una clara separación entre el comportamiento interno de las partículas y las fuerzas externas que actúan sobre ellas.

| Aspecto                           | 4.2      | 4.4      | 4.5      | 4.6             | 4.7                        |
| --------------------------------- | -------- | -------- | -------- | --------------- | -------------------------- |
| ¿Quién crea partículas?           | draw()   | Emitter  | Emitter  | Emitter         | Emitter                    |
| ¿Hay clase Emitter?               | ❌ No     | ✅ Sí     | ✅ Sí     | ✅ Sí            | ✅ Sí                       |
| ¿Hay herencia?                    | ❌ No     | ❌ No     | ✅ Sí     | ❌ No            | ❌ No                       |
| ¿Hay fuerzas externas?            | ❌ No     | ❌ No     | ❌ No     | ✅ Sí (gravedad) | ✅ Sí (gravedad + repeller) |
| ¿Hay interacción entre elementos? | ❌ No     | ❌ No     | ❌ No     | ❌ No            | ✅ Sí (repeller-partículas) |
| ¿Cómo mueren las partículas?      | lifespan | lifespan | lifespan | lifespan        | lifespan                   |
Se decidió modificar el comportamiento de las fuerzas en el Example 4.7, específicamente aumentando la intensidad de la repulsión del repeller.

Para lograr esto, se modificó la línea dentro de la clase Repeller:

this.power = 150;

por un valor mayor, por ejemplo:

this.power = 300;

También podría modificarse la fórmula de fuerza en el método repel() para hacer la repulsión más intensa o más suave.
## Bitácora de aplicación 


## Bitácora de reflexión
