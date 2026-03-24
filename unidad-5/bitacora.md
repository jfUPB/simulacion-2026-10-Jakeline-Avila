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



## Bitácora de aplicación 


## Bitácora de reflexión
