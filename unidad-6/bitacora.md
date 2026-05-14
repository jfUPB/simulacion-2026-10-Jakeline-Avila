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

### Concepto visual:

1. Canción escogida: Headlock
2. Me gustaria transmitir la tranquila desesperación de la canción junto con la intensa lucha al cambio, la comodidad tóxica y el estancamiento emocional. Se utiliza la metáfora del líquido como un elemento que fluye pero que a la vez atrapa (un "headlock" o llave de lucha). La visual evoluciona de formas líquidas cohesivas hacia una fragmentación puntillista y finalmente a una estructura topográfica sólida, representando el proceso de endurecimiento y cristalización de las emociones.

### Moodboard o referencias
<img width="740" height="416" alt="image" src="https://github.com/user-attachments/assets/2b7c1d5c-a08f-4a1d-b419-4c8791ba1348" />
<img width="800" height="480" alt="image" src="https://github.com/user-attachments/assets/0042b277-1fb5-4968-834c-17b25dd61388" />
<img width="480" height="270" alt="image" src="https://github.com/user-attachments/assets/96c8eead-1378-48b1-84be-93597693c516" />
<img width="800" height="480" alt="image" src="https://github.com/user-attachments/assets/2f3fa803-1d96-46f4-af8b-01a4fd38a201" />
<img width="626" height="470" alt="image" src="https://github.com/user-attachments/assets/4225092c-af7c-4132-99a8-6b1a492623c6" />

### Bocetos

<img width="1131" height="1599" alt="image" src="https://github.com/user-attachments/assets/aadc3a32-9426-43ed-a9d2-4650fc289d18" />

<img width="1131" height="1599" alt="image" src="https://github.com/user-attachments/assets/e5b8ae6a-e12c-4968-bd6f-26edff064f26" />

<img width="1131" height="1599" alt="image" src="https://github.com/user-attachments/assets/d50fb1b4-d53e-4007-b898-8f78dee410b2" />
<img width="1131" height="1599" alt="image" src="https://github.com/user-attachments/assets/c1ee712a-3fbd-4b32-8706-27882ee630b6" />
<img width="1131" height="1599" alt="image" src="https://github.com/user-attachments/assets/09496560-ad5b-4005-9712-5ae6cfed5234" />

<img width="1131" height="1599" alt="image" src="https://github.com/user-attachments/assets/d70cf2bd-1798-47bf-97b5-eca0d3fbc7cd" />


### Mapa de decisiones

- Paleta Blanco y Negro (Minimalismo Limpio): Para enfatizar el contraste entre el vacío y la forma sin distracciones de color.
- Metaballs (Lógica Líquida): Elegidos por su capacidad de fusionarse y separarse, representando relaciones o estados de ánimo que se pegan y se rompen.
- Faux 3D (Montañas): Añade peso visual y una sensación de "terreno difícil" durante la fase final de la canción.

### Mapa de integración

- Mouse (Movimiento): Perturba el flujo de las partículas.
- Mouse (Click/Drag): Cambia la fuerza de repulsión a atracción. Permite "arrastrar" y estirar las líneas como si fueran materia física.
- Teclas 1, 2, 3, 4: Selector manual de estados (1: Líquido, 2: Puntos, 3: Montañas, 4: Caleidoscopio). Permite al intérprete sincronizarse con la narrativa musical de forma libre.
- Barra Espaciadora: Modo de "Baja Densidad". Reduce el sistema al mínimo para acompañar silencios o momentos de susurro.
- Tecla R: Reset/Modo Automático.

### Justificación del algoritmo escogido

- Flow Fields (Perlin Noise): Se eligieron campos de flujo porque Headlock no se siente como un comportamiento de grupo (flocking), sino como una corriente inevitable que arrastra al espectador.
- Shaders (GLSL): Se utilizaron para lograr una estética de alta resolución y efectos de distorsión (glitch/3D) que serían imposibles de procesar en tiempo real solo con la CPU del navegador.

### Explicación de la relación audio-visual.

- Bajos (Bass): Controlan la velocidad de los agentes y la escala de los metaballs. A más bajo, el sistema se "infla" y se agita.
- Agudos (Treble): Controlan el "temblor" de las líneas. Los sonidos agudos de la voz o los platillos causan una micro-vibración nerviosa en la visual.
- FFT (Energía): Determina la densidad de las curvas de nivel.
### Evidencia IA
- Asistente Técnico: Utilicé la IA para la materialización de los Shaders (GLSL) en WebGL y para depurar errores de compilación complejos (como el error de fwidth y versiones de WebGL 2.0).
- Iteración: La IA ayudó a pulir la física de "arrastre" del mouse.
- Autoría: El concepto de las 5 fases, la selección de la canción, la estética minimalista y la dirección narrativa ("Error de sistema" -> "Montañas") son de mi autoría exclusiva.

<img width="730" height="208" alt="Captura de pantalla 2026-04-16 123856" src="https://github.com/user-attachments/assets/1a56157e-47d2-4e96-b032-eb386f0785ec" />
<img width="727" height="249" alt="Captura de pantalla 2026-04-16 123825" src="https://github.com/user-attachments/assets/5fcbeb62-32b9-43b5-8cea-8870b19ac78d" />



### Codigo fuente

#### Skecth.js
``` js
let particles = [];
const numParticles = 30;
let flowField = [];
const scl = 40;
let cols, rows;
let zoff = 0;
let liquidShader;
let song;
let fft;
let started = false;

let songTimer = 0;
let songDur = 0;
let phase = 1; 
let transitionLevel = 0;
let targetDensity = 1.0;
let currentDensity = 1.0;
let isGlitching = false;
let glitchTimer = 0;
let smoothTreble = 0;
let manualMode = false;

function preload() {
  // Asegúrate de subir el archivo Headlock.mp3 a tu editor
  song = loadSound('Headlock.mp3'); 
  liquidShader = loadShader('shader.vert', 'shader.frag');
}

function setup() {
  createCanvas(windowWidth, windowHeight, WEBGL);
  pixelDensity(1);
  noCursor();
  
  cols = floor(width / scl);
  rows = floor(height / scl);

  // Inicializar el arreglo de flujo
  for (let i = 0; i < rows; i++) {
    flowField[i] = [];
  }

  for (let i = 0; i < numParticles; i++) {
    particles.push(new Particle());
  }
  fft = new p5.FFT();
}

function keyPressed() {
  if (key === ' ') targetDensity = (targetDensity === 1.0) ? 0.2 : 1.0;
  if (key === '1') { phase = 1; manualMode = true; isGlitching = false; }
  if (key === '2') { phase = 2; manualMode = true; isGlitching = false; }
  if (key === '3') { phase = 3; manualMode = true; isGlitching = false; }
  if (key === '4') { phase = 4; manualMode = true; isGlitching = false; }
  if (key === 'r' || key === 'R') { manualMode = false; glitchTimer = 0; }
}

function mousePressed() {
  if (!started && song.isLoaded()) {
    userStartAudio();
    song.play();
    started = true;
    songDur = song.duration();
    
    // --- ESTO ACTIVA EL FULLSCREEN AL INICIAR ---
    let fs = fullscreen();
    fullscreen(!fs);
  }
}

function draw() {
  background(0);
  if (!started) {
    fill(255);
    textAlign(CENTER);
    text("Haz click para iniciar sistema", 0, 0);
    return;
  }

  songTimer = song.currentTime();
  currentDensity = lerp(currentDensity, targetDensity, 0.05);

  // CONTROL DE FASES AUTOMÁTICO
  if (!manualMode) {
    if (songTimer > 72.0 && songTimer < 104.0) {
      if (phase !== 2) {
        isGlitching = true;
        glitchTimer++;
        if (glitchTimer > 60) { isGlitching = false; phase = 2; }
      }
    } else if (songTimer >= 104.0 && songTimer < 140.0) {
      phase = 3; isGlitching = false;
    } else if (songTimer >= 140.0 && songTimer < (songDur - 10)) {
      phase = 4; isGlitching = false;
    } else if (songTimer >= (songDur - 10)) {
      phase = 5; targetDensity = 0.0;
      isGlitching = (songTimer < (songDur - 8));
    } else {
      phase = 1; isGlitching = false;
    }
  }

  // Transiciones
  if (phase === 1) transitionLevel = lerp(transitionLevel, 0.0, 0.05);
  if (phase === 2) transitionLevel = lerp(transitionLevel, 1.0, 0.04);
  if (phase === 3) transitionLevel = lerp(transitionLevel, 2.0, 0.02);
  if (phase === 4) transitionLevel = lerp(transitionLevel, 3.0, 0.05);
  if (phase === 5) transitionLevel = lerp(transitionLevel, 4.0, 0.05);

  fft.analyze();
  let bass = fft.getEnergy("bass") / 255;
  let treble = fft.getEnergy("treble") / 255;
  smoothTreble = lerp(smoothTreble, treble, 0.2);
  
  zoff += 0.0004 + bass * 0.001;

  // RELLENAR EL CAMPO DE FLUJO
  for (let y = 0; y < rows; y++) {
    for (let x = 0; x < cols; x++) {
      let angle = noise(x * 0.1, y * 0.1, zoff) * TWO_PI * 4;
      let v = p5.Vector.fromAngle(angle);
      v.setMag(0.1 + bass * 0.5); 
      flowField[y][x] = v;
    }
  }

  particles.forEach(p => {
    p.follow(flowField);
    if (phase === 2 || phase === 4) p.separate(particles); 
    p.update(bass);
    p.edges();
  });

  if (liquidShader) {
    shader(liquidShader);
    liquidShader.setUniform('uResolution', [width, height]);
    liquidShader.setUniform('uBass', bass);
    liquidShader.setUniform('uTreble', smoothTreble);
    liquidShader.setUniform('uMouse', [mouseX / width, 1.0 - (mouseY / height)]);
    liquidShader.setUniform('uTime', millis() / 1000.0);
    liquidShader.setUniform('uTransition', transitionLevel);
    liquidShader.setUniform('uDensity', currentDensity);
    liquidShader.setUniform('uIsGlitching', isGlitching ? 1.0 : 0.0);
    liquidShader.setUniform('uMousePressed', mouseIsPressed ? 1.0 : 0.0);

    let particlePositions = [];
    for(let p of particles) {
      particlePositions.push(p.pos.x / width, 1.0 - (p.pos.y / height));
    }
    liquidShader.setUniform('uParticles', particlePositions);
    rect(-width/2, -height/2, width, height);
  }

  if (isGlitching) drawGlitchOverlays();
  if (phase === 5 && currentDensity < 0.05) drawTextFinal();
}

function drawGlitchOverlays() {
  push();
  noStroke();
  let w = width * 0.4;
  for(let i=0; i<3; i++){
    if(i==0) fill(255, 0, 80, 150);
    if(i==1) fill(0, 255, 255, 150);
    if(i==2) fill(255);
    let ox = random(-10, 10);
    let oy = random(-10, 10);
    rect(-w/2 + ox, -20 + oy, w, 40);
    rect(random(-width/2, width/2), random(-height/2, height/2), random(width), 2);
  }
  pop();
}

function drawTextFinal() {
  push();
  resetShader();
  noStroke();
  textAlign(CENTER, CENTER);
  textFont('monospace');
  let fade = map(songTimer, songDur - 8, songDur, 0, 255);
  fill(255, fade);
  textSize(width * 0.05);
  text("HEADLOCK", 0, -40);
  textSize(width * 0.015);
  fill(200, fade);
  text("Imogen Heap", 0, 10);
  fill(150, fade);
  textSize(width * 0.012);
  text("Visuales hechas por Jakeline Avila", 0, 80);
  pop();
}

class Particle {
  constructor() {
    this.pos = createVector(random(width), random(height));
    this.vel = createVector(random(-1, 1), random(-1, 1));
    this.acc = createVector(0, 0);
    this.maxSpeed = 0.8; 
  }

  follow(vectors) {
    let x = floor(this.pos.x / scl);
    let y = floor(this.pos.y / scl);
    if (vectors[y] && vectors[y][x]) {
      this.acc.add(vectors[y][x]);
    }
    
    let d = dist(this.pos.x, this.pos.y, mouseX, mouseY);
    if (d < 300) {
      let target = createVector(mouseX, mouseY);
      let force = p5.Vector.sub(this.pos, target);
      if (mouseIsPressed) {
        force = p5.Vector.sub(target, this.pos);
        force.setMag(0.5);
      } else {
        force.setMag(0.15);
      }
      this.acc.add(force);
    }
  }

  separate(others) {
    let steer = createVector(0, 0);
    let count = 0;
    for (let o of others) {
      let d = dist(this.pos.x, this.pos.y, o.pos.x, o.pos.y);
      if (d > 0 && d < 180) { 
        let diff = p5.Vector.sub(this.pos, o.pos);
        diff.normalize();
        diff.div(d);
        steer.add(diff);
        count++;
      }
    }
    if (count > 0) {
      steer.div(count);
      steer.setMag(1.5);
      this.acc.add(steer);
    }
  }

  update(bass) {
    this.vel.add(this.acc);
    this.vel.limit(this.maxSpeed + bass * 4); 
    this.pos.add(this.vel);
    this.acc.mult(0);
  }

  edges() {
    if (this.pos.x > width) this.pos.x = 0;
    if (this.pos.x < 0) this.pos.x = width;
    if (this.pos.y > height) this.pos.y = 0;
    if (this.pos.y < 0) this.pos.y = height;
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
  cols = floor(width / scl);
  rows = floor(height / scl);
  flowField = [];
  for (let i = 0; i < rows; i++) {
    flowField[i] = [];
  }
}

```

Shader.frag
``` js
precision highp float;
varying vec2 vTexCoord;
uniform vec2 uResolution;
uniform vec2 uParticles[30];
uniform float uBass;
uniform float uTreble;
uniform vec2 uMouse;
uniform float uTime;
uniform float uTransition; 
uniform float uDensity;
uniform float uIsGlitching;
uniform float uMousePressed;

float pattern(vec2 st, float size, float spacing) {
    return step(spacing, length(fract(st * size) - 0.5));
}
float random(vec2 st) {
    return fract(sin(dot(st.xy, vec2(12.9898,78.233))) * 43758.5453123);
}
vec2 kaleidoscope(vec2 st, float segments) {
    vec2 p = st - 0.5;
    float r = length(p);
    float a = atan(p.y, p.x);
    float tau = 6.283185;
    a = mod(a, tau/segments);
    a = abs(a - tau/segments/2.0);
    return vec2(cos(a), sin(a)) * r + 0.5;
}

void main() {
    vec2 st = vTexCoord;
    
    if (uTreble > 0.45) {
       st.x += (random(vec2(uTime, st.y)) - 0.5) * 0.007 * uTreble;
    }

    if (uTransition > 2.0) {
        float kTransition = clamp(uTransition - 2.0, 0.0, 1.0);
        st = mix(st, kaleidoscope(st, 6.0), kTransition);
    }

    if(uIsGlitching > 0.5) {
        st.x += (random(vec2(uTime, st.y)) - 0.5) * 0.12;
    }

    float sum = 0.0;
    for (int i = 0; i < 30; i++) {
        vec2 p = uParticles[i];
        float d = distance(st, p);
        sum += (0.0008 * uDensity) / (pow(d, 2.0) + 0.0001);
    }

    float mRad = 0.15 + (uMousePressed * 0.35);
    float mStr = 0.15 + (uMousePressed * 0.45);
    sum += smoothstep(mRad, 0.0, distance(st, uMouse)) * mStr;

    float freq = 45.0 + uBass * 20.0;
    float p1 = smoothstep(0.0, 0.1, sin(sum * freq - uTime * 1.8)) * smoothstep(0.1, 0.12, sum);

    float p2 = 0.0;
    if(sum > 0.6) p2 = pattern(st, 180.0, 0.4);
    else if (sum > 0.3) p2 = (random(st + uTime) > 0.8) ? 1.0 : 0.0;
    else if (sum > 0.1) p2 = pattern(st, 320.0, 0.05);

    float f3 = 75.0 + uBass * 10.0;
    float h = sin(sum * f3 - uTime * 0.4);
    float p3 = step(0.5, h) * smoothstep(0.05, 0.1, sum);

    float res = 0.0;
    if (uTransition <= 1.0) res = mix(p1, p2, clamp(uTransition, 0.0, 1.0));
    else if (uTransition <= 2.0) res = mix(p2, p3, clamp(uTransition - 1.0, 0.0, 1.0));
    else res = p2; 

    if (uTransition > 3.0) res *= (1.0 - clamp(uTransition - 3.0, 0.0, 1.0));
    if(uIsGlitching > 0.5 && random(vec2(uTime)) > 0.85) res = 1.0 - res;

    gl_FragColor = vec4(vec3(res), 1.0);
}
```
Shader.vert
``` js
precision highp float;
attribute vec3 aPosition;
attribute vec2 aTexCoord;
varying vec2 vTexCoord;

void main() {
  vTexCoord = aTexCoord;
  vec4 positionVec4 = vec4(aPosition, 1.0);
  positionVec4.xy = positionVec4.xy * 2.0 - 1.0;
  gl_Position = positionVec4;
}
```

#### Link de la actividad
https://editor.p5js.org/Jakeline-Avila/sketches/fzgEIbT6H

#### Capturas de pantalla

Fase 1
<img width="2559" height="1439" alt="Captura de pantalla 2026-04-16 124455" src="https://github.com/user-attachments/assets/f449cd88-555f-42e9-aa53-e2e194d386f4" />

Fase 2
<img width="2559" height="1439" alt="Captura de pantalla 2026-04-16 124502" src="https://github.com/user-attachments/assets/feab7a4c-9c12-416b-b266-e6dcf6cc9837" />

Fase 3
<img width="2552" height="1439" alt="Captura de pantalla 2026-04-16 124507" src="https://github.com/user-attachments/assets/1eb162e9-3399-4167-99da-6d77bf0b2fcc" />

Fase 4
<img width="2559" height="1439" alt="Captura de pantalla 2026-04-16 124517" src="https://github.com/user-attachments/assets/b5643ef5-db20-4920-8e4d-3d8b41c46cd3" />

## Bitácora de reflexión
