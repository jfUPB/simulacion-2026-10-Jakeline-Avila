# Unidad 6

## Bitácora de proceso de aprendizaje
### Actividad 1

En esta actividad analicé el trabajo del artista generativo Tyler Hobbs, centrándome en cómo sus obras no son solo imágenes, sino sistemas de decisiones visuales. La primera pieza que elegí corresponde a composiciones basadas en flow fields, donde múltiples líneas recorren el espacio siguiendo direcciones suaves y continuas. La composición no tiene un centro definido, sino que se distribuye de manera uniforme en todo el plano, generando equilibrio a partir de la acumulación. La densidad varía en distintas zonas, creando áreas más cargadas y otras más abiertas, lo que aporta profundidad visual. El movimiento es fluido y orgánico, como si las líneas estuvieran guiadas por corrientes invisibles. El uso del color suele ser limitado, lo que permite enfocarse en la estructura y el comportamiento del sistema. El ritmo surge de la repetición de líneas con pequeñas variaciones, produciendo un efecto hipnótico.


Estas decisiones visuales me parecen potentes porque logran transformar un sistema matemático en una imagen que se percibe como natural y viva. Aunque detrás hay reglas precisas, el resultado evoca fenómenos como el viento, el agua o incluso patrones biológicos. A partir de esto, mi hipótesis es que la pieza está construida mediante un campo de flujo generado con ruido, posiblemente Perlin Noise, donde cada punto del espacio define una dirección. Las líneas funcionan como partículas que siguen ese campo paso a paso, partiendo de posiciones iniciales aleatorias y avanzando según ciertas reglas de velocidad, longitud y variación.
La segunda pieza que seleccioné pertenece a la serie Fidenza, también de Tyler Hobbs. En este caso, la composición es más estructurada, con formas que parecen bloques o cintas que se organizan en el espacio como si fueran caminos. A diferencia de los flow fields más simples, aquí hay una sensación de organización por regiones, donde algunas zonas son más densas y otras más abiertas. El movimiento sigue siendo fluido, pero se percibe más controlado, generando una especie de “arquitectura blanda”. El color juega un rol mucho más importante, con paletas cuidadosamente seleccionadas que crean contraste y jerarquía. El ritmo es más complejo, alternando entre orden y variación, y las formas se repiten pero nunca de manera idéntica.


Lo que hace potente esta segunda obra es la combinación entre lo orgánico y lo estructurado. Se percibe como un sistema que está entre lo natural y lo diseñado, lo que genera una tensión interesante. Mi hipótesis es que esta pieza también se basa en flow fields, pero incorpora capas adicionales de reglas, como la subdivisión del espacio en regiones y algoritmos que determinan cómo se rellenan esas áreas con formas. Probablemente incluye parámetros relacionados con el grosor de las formas, la curvatura, la paleta de color y la forma en que los elementos interactúan entre sí.
En conjunto, el trabajo de Tyler Hobbs demuestra cómo una obra generativa surge de un sistema de reglas que controla aspectos como el movimiento, la densidad y la variación. Lo más interesante es que pequeños cambios en esas reglas pueden producir resultados muy distintos, manteniendo al mismo tiempo una coherencia visual reconocible.

### Actividad 2

Un agente autónomo es una entidad que puede moverse y tomar decisiones por sí misma dentro de un sistema. A diferencia de un objeto pasivo, no solo responde a fuerzas externas, sino que tiene cierto “comportamiento” definido por reglas internas. Por ejemplo, un agente puede decidir hacia dónde moverse, evitar obstáculos o seguir a otros agentes. En este sentido, no es simplemente un punto que se desplaza, sino un sistema con lógica propia que interpreta su entorno y actúa en consecuencia.

Una steering force (fuerza de dirección) es el mecanismo que permite a ese agente ajustar su movimiento para cumplir un objetivo. No es una fuerza física en el sentido tradicional, sino una fuerza calculada que guía al agente hacia un comportamiento específico, como llegar a un punto, escapar de algo o alinearse con otros. Estas fuerzas suelen combinarse entre sí, generando movimientos complejos a partir de reglas relativamente simples.

La diferencia entre una steering force y una fuerza externa como la gravedad radica en su origen y propósito. Fuerzas como la gravedad, el viento o la fricción son externas al objeto y afectan su movimiento de manera pasiva, sin “intención”. En cambio, una steering force es interna al agente y está orientada a un objetivo o comportamiento. Mientras la gravedad siempre atrae hacia abajo de forma constante, una steering force puede cambiar dinámicamente dependiendo de lo que el agente “quiera hacer”, como moverse hacia un objetivo o evitar colisiones.

Estas ideas son especialmente útiles para diseñar comportamiento visual porque permiten crear sistemas que parecen vivos o inteligentes, sin necesidad de animar cada detalle manualmente. En lugar de definir trayectorias fijas, se establecen reglas de comportamiento, y el movimiento emerge de la interacción entre los agentes y su entorno. Esto es clave en el arte generativo y en simulaciones, ya que permite producir resultados complejos, orgánicos y variados a partir de principios simples, generando una sensación de naturalidad y dinamismo en las composiciones visuales.

### Actividad 3

El campo de flujo está construido como una grilla bidimensional que divide el espacio en celdas. En cada celda se almacena un vector que define una dirección. Estos vectores suelen generarse con funciones de ruido como Perlin Noise, lo que permite que las direcciones cambien de manera suave y continua en el espacio.

Cada celda del campo representa una dirección de movimiento preferida. El vector contenido en ella actúa como una guía local, como si fuera una corriente o un viento que influye en los agentes que pasan por esa zona. En conjunto, todas las celdas forman una estructura invisible que organiza el movimiento global.

Un agente usa su posición para consultar el campo transformando sus coordenadas en índices de la grilla. Es decir, convierte su posición en pantalla a una posición dentro del arreglo de celdas y accede al vector correspondiente a ese lugar.

El vector obtenido se convierte en una decisión de movimiento al ser interpretado como una fuerza deseada. El agente calcula una fuerza de dirección comparando ese vector con su velocidad actual, limita esa fuerza mediante un valor máximo y luego actualiza su velocidad y su posición. Este comportamiento se relaciona con modelos como Boids algorithm.

Entre los parámetros más importantes del sistema se encuentra la resolución, que define el tamaño de cada celda y el nivel de detalle del campo. También son importantes el maxspeed, que limita la velocidad de los agentes, y el maxforce, que controla qué tan rápido pueden cambiar de dirección. La cantidad de agentes influye directamente en la densidad y complejidad del patrón visual.

Como modificación, aumenté la resolución del campo, haciendo que las celdas fueran más pequeñas. Esto produjo un movimiento más detallado y turbulento, con trayectorias más complejas y menos uniformes. El resultado visual se volvió más dinámico, aunque perdió algo de coherencia global.

Este algoritmo produce un movimiento fluido y orgánico, similar a fenómenos naturales como corrientes de agua o viento. Las trayectorias son continuas y generan una sensación de flujo constante.

Visualmente, sugiere sensaciones de calma cuando el movimiento es suave, pero también puede generar una impresión de complejidad o caos controlado cuando hay mucha variación en el campo.

Este tipo de sistema funcionaría bien con música ambient o electrónica suave. Por ejemplo, podría acompañar composiciones de Brian Eno, donde el flujo visual refuerza la atmósfera continua y envolvente del sonido.

### Actividad 4

El flocking es un sistema basado en reglas simples que cada agente sigue de manera local, pero que en conjunto producen un comportamiento colectivo complejo. Este modelo está inspirado en el comportamiento de grupos de animales y se formaliza en algoritmos como el Boids algorithm.

La regla de separación hace que cada agente evite acercarse demasiado a los demás. Si detecta vecinos muy próximos, genera una fuerza para alejarse. Esto evita que los agentes se superpongan y mantiene una distancia mínima entre ellos.

La alineación consiste en que cada agente intenta igualar su dirección de movimiento con la de sus vecinos cercanos. Para hacerlo, calcula el promedio de las velocidades de los agentes cercanos y ajusta su dirección hacia ese promedio. Esto genera movimientos coordinados.

La cohesión hace que los agentes tiendan a acercarse entre sí. Cada agente calcula el centro de masa de sus vecinos y se dirige suavemente hacia ese punto. Esta regla mantiene unido al grupo.

Estas reglas están controladas por varios parámetros. Entre los más importantes están los pesos de cada comportamiento (separación, alineación y cohesión), que determinan la influencia de cada regla. También son importantes el radio de percepción, que define qué tan lejos puede ver un agente a sus vecinos, y parámetros físicos como maxspeed y maxforce, que limitan la velocidad y la capacidad de giro.

Como modificación, aumenté el peso de la separación y reduje el de cohesión. El efecto visual fue que los agentes se volvieron más independientes y el grupo se dispersó. Se generaron espacios vacíos entre ellos y el movimiento se volvió menos compacto y más fragmentado.

El comportamiento emergente en este caso fue disperso y algo nervioso. Los agentes evitaban constantemente a los demás, lo que producía trayectorias más erráticas. En contraste, cuando la cohesión es alta, el sistema tiende a ser más compacto y estable, mientras que un buen equilibrio entre las tres reglas produce un movimiento fluido.

El flocking genera una atmósfera visual orgánica y viva. Da la sensación de estar observando un sistema natural, como una bandada de aves o un banco de peces, donde cada elemento responde a los demás en tiempo real.

Este algoritmo funciona especialmente bien en relación con música que tenga estructura colectiva o rítmica, como electrónica, techno suave o incluso música orquestal con crescendos. También puede acompañar piezas donde la intensidad varía, ya que los parámetros del flocking pueden ajustarse para reflejar cambios en la energía sonora.

### Actividad 5

El sistema de flow fields produce un movimiento continuo y guiado por una estructura invisible. Los agentes siguen direcciones definidas en el espacio, lo que genera trayectorias suaves y fluidas, similares a corrientes. En cambio, el flocking, basado en el Boids algorithm, produce un movimiento colectivo que emerge de la interacción entre agentes, generando agrupaciones dinámicas y comportamientos más impredecibles.


En términos de control visual, los flow fields ofrecen un mayor control global, ya que el diseñador define directamente el campo vectorial que los agentes siguen. Esto permite diseñar patrones específicos con bastante precisión. Por otro lado, el flocking tiene un control más indirecto: se ajustan parámetros, pero el resultado final depende de la interacción entre múltiples agentes, lo que lo hace menos predecible.
Respecto al nivel de emergencia, el flocking presenta un grado más alto, ya que el comportamiento global no está predefinido sino que surge de reglas simples como separación, alineación y cohesión. En los flow fields, aunque hay cierta complejidad, el comportamiento está más determinado por la estructura del campo.


En cuanto a la atmósfera visual, los flow fields suelen generar sensaciones de fluidez, calma o hipnosis, especialmente cuando las transiciones son suaves. El flocking, en cambio, puede generar sensaciones más vivas y orgánicas, como sistemas naturales en movimiento, que pueden variar entre lo armónico y lo caótico dependiendo de los parámetros.
En relación con una pieza musical, los flow fields funcionan bien con música ambient o continua, donde no hay cambios bruscos y se busca una experiencia envolvente. El flocking se adapta mejor a músicas con ritmo, variaciones o energía colectiva, ya que puede reflejar cambios de intensidad mediante el comportamiento del grupo.


Entre las ventajas de los flow fields está su capacidad de generar composiciones visuales controladas y estéticamente coherentes. Sin embargo, su limitación es que pueden volverse predecibles si el campo no cambia. El flocking, por su parte, tiene la ventaja de producir comportamientos ricos y dinámicos, pero su limitación es la dificultad para controlar exactamente el resultado visual.


Si quisiera diseñar visuales para una canción contemplativa, usaría flow fields, ya que permiten generar movimientos suaves, continuos y envolventes. Para una canción agresiva, elegiría flocking con parámetros que generen tensión y caos, aprovechando su capacidad de producir comportamientos intensos. En el caso de una canción melancólica, optaría por flow fields con movimientos lentos y direcciones suaves, que refuercen una sensación introspectiva. Finalmente, para una canción eufórica, usaría flocking, ya que el movimiento colectivo dinámico puede transmitir energía, expansión y entusiasmo.

## Bitácora de aplicación 


1. Canción escogida: Headlock
2. Me gustaria transmitir la tranquila desesperación de la canción junto con la intensa lucha al cambio, la comodidad tóxica y el estancamiento emocional.
3. 
<img width="740" height="416" alt="image" src="https://github.com/user-attachments/assets/2b7c1d5c-a08f-4a1d-b419-4c8791ba1348" />
<img width="800" height="480" alt="image" src="https://github.com/user-attachments/assets/0042b277-1fb5-4968-834c-17b25dd61388" />

```
let particles = [];
let scale = 0.002;
let t = 0;

function setup() {
  createCanvas(windowWidth, windowHeight);
  background(0);

  // muchas partículas para generar flujo continuo
  for (let i = 0; i < 5000; i++) {
    particles.push(new Particle());
  }
}

function draw() {
  // no limpiamos completamente → acumulación líquida
  fill(0, 15);
  noStroke();
  rect(0, 0, width, height);

  for (let p of particles) {
    p.update();
    p.show();
  }

  t += 0.005;
}

class Particle {
  constructor() {
    this.pos = createVector(random(width), random(height));
    this.prev = this.pos.copy();
    this.vel = createVector(0, 0);
  }

  update() {
    this.prev = this.pos.copy();

    // campo fluido suave
    let angle =
      noise(this.pos.x * scale, this.pos.y * scale, t) *
      TWO_PI *
      2;

    let force = p5.Vector.fromAngle(angle);

    this.vel.add(force);
    this.vel.limit(1.5);
    this.pos.add(this.vel);

    // wrap edges
    if (this.pos.x < 0) this.pos.x = width;
    if (this.pos.x > width) this.pos.x = 0;
    if (this.pos.y < 0) this.pos.y = height;
    if (this.pos.y > height) this.pos.y = 0;
  }

  show() {
    stroke(255, 180);
    strokeWeight(0.6);
    line(this.prev.x, this.prev.y, this.pos.x, this.pos.y);
  }
}
```

## Bitácora de reflexión
