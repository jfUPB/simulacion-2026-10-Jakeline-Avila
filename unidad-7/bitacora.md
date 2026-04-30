# Unidad 7

## Bitácora de proceso de aprendizaje

### Actividad 1

1. Revisé el yingyang, tunnel y smile.
2. La manipulación tipográfica le da más profundidad a la palabra, como el hecho de que nosotros al ver una palabra ya nos imaginamos a la cosa que se refiere. Este ejercicio ayuda que el cerebro la tenga mucho más fácil interpretarla. Incluyendo la creatividad y estética.
3. Fireball: Escribir fireball pero que la letra A salga disparada como si se tratara de una bola de fuego como las que tira Mario.
- Cámara: Que la tilde funcione como el flash y tome una foto del usuario.
4. Ambas me gustan pero siento que con la palabra cámara se puede explorar mucho más.

### Actividad 2

1. 
- Engine: Motor para hacer que algo funcione, como los motores de gráficos que manejan los renderizados.
- World: Mundo, el lugar donde están todos los objetos.
- Bodies: Objetos físicos con masa.
- Constraint: Conexión y restricción entre dos objetos.
- MouseConstraint: Permite interactuar con esa conexión usando el mouse.

2. Código, caja cayendo al suelo

``` js
let engine;
let world;
let box;
let ground;

function setup() {
  createCanvas(400, 400);

  engine = Matter.Engine.create();
  world = engine.world;

  box = Matter.Bodies.rectangle(200, 100, 50, 50);
  ground = Matter.Bodies.rectangle(200, 380, 400, 20, { isStatic: true });

  Matter.World.add(world, [box, ground]);
}

function draw() {
  background(220);
  Matter.Engine.update(engine);

  rectMode(CENTER);


  rect(box.position.x, box.position.y, 50, 50);


  rect(ground.position.x, ground.position.y, 400, 20);
}
```

Código arrastrar caja con el mouse:

``` js
let engine, world;
let box;
let mouseConstraint;

function setup() {
  createCanvas(400, 400);

  engine = Matter.Engine.create();
  world = engine.world;

  box = Matter.Bodies.rectangle(200, 200, 80, 80);

  let canvasMouse = Matter.Mouse.create(canvas.elt);
  let options = {
    mouse: canvasMouse
  };

  mouseConstraint = Matter.MouseConstraint.create(engine, options);

  Matter.World.add(world, [box, mouseConstraint]);
}

function draw() {
  background(220);
  Matter.Engine.update(engine);

  rectMode(CENTER);
  rect(box.position.x, box.position.y, 80, 80);
}
```

<img width="393" height="393" alt="image" src="https://github.com/user-attachments/assets/eb93b17f-bc4e-40ee-a21e-9c6f058a572b" />

<img width="393" height="383" alt="image" src="https://github.com/user-attachments/assets/c2f5b50b-2623-4154-b6cd-6afbe0b194a4" />

4. Me gustaría explorar los líquidos y los movimientos de arrastre, siempre me ha encantado ver la fluidez de los líquidos.

### Actividad 3

- Ejercicio de amplitud:

``` js
let song, amp;

function preload() {
  song = loadSound("mrbrightside.mp3");
}

function setup() {
  createCanvas(400, 400);
  amp = new p5.Amplitude();
  song.play();
}

function draw() {
  background(0);

  let level = amp.getLevel();
  let size = map(level, 0, 0.5, 50, 300);

  fill(255);
  ellipse(width/2, height/2, size);
}
```

- Uso p5.Amplitude() para obtener el nivel de volumen general en tiempo real. Este valor cambia constantemente y representa la intensidad global de la canción.

- Energía

``` js
let song, fft;

function preload() {
  song = loadSound("mrbrightside.mp3");
}

function setup() {
  createCanvas(400, 400);
  fft = new p5.FFT();
  song.play();
}

function draw() {
  let bass = fft.getEnergy("bass");

  if (bass > 180) {
    background(random(255), random(255), random(255));
  } else {
    background(0, 20); // leve rastro
  }
}
```
- Uso p5.FFT() y getEnergy("bass") para medir la energía en frecuencias bajas (bombo/bajo).

### Actividad 4
<img width="1084" height="920" alt="image" src="https://github.com/user-attachments/assets/d7825dd9-5eef-4d64-bfd7-403c5c67ad95" />
- He vinculado un cuerpo circular de Matter.js a la palabra "BALL". He creado un sistema de partículas simple para representar el "FIRE".
- Implementé un vector de fuerza de atracción. La bola no sigue al mouse de forma rígida, sino que es atraída por una fuerza física, lo que permite movimientos curvos y fluidos.
Relación Audio-Física:
El bajo expande el radio de la bola visualmente.
El agudo modifica el shadowBlur (el resplandor) de la tipografía.
Evaluación de la prueba:
- Lo que funcionó: La fluidez del movimiento y la integración del brillo con los agudos crean una atmósfera muy inmersiva.
- A mejorar: Debo ajustar la fricción del aire (frictionAir) porque a veces la bola se mueve demasiado rápido y cuesta ver la palabra con claridad. También planeo hacer que el rastro de fuego sea más denso cuando el volumen suba.


## Bitácora de aplicación 

Elegí la frase "Yin Yang" para explorar el concepto de la dualidad y el equilibrio dinámico. No quería que fuera una imagen estática, sino una pieza que mostrara cómo los opuestos (luz/oscuridad, orden/caos) se filtran y se transforman el uno en el otro. La pieza es un ciclo narrativo que viaja desde el vacío blanco hasta el símbolo de equilibrio, pasando por estados de inversión visual.

2. Visual: Utilizo el contraste absoluto de blanco y negro. La tipografía Serif aporta una sensación de tradición y caligrafía, mientras que el símbolo geométrico representa la perfección matemática del equilibrio.
Comportamental:
- Fase Yin: La tinta negra "llueve" y actúa como un filtro que revela el blanco oculto tras las letras negras. Es un comportamiento de revelación por contacto.
- Fase de Equilibrio: El movimiento es rotatorio, circular y eterno, simulando la órbita de los elementos en el universo.
- Viscosidad: La física de la tinta no es rígida; las partículas se atraen y se repelen como un fluido viscoso (mercurio o petróleo).

3. <img width="1864" height="1131" alt="image" src="https://github.com/user-attachments/assets/5c406ddd-9332-407e-9a98-fd99e41c18c1" />
<img width="250" height="250" alt="image" src="https://github.com/user-attachments/assets/6450d2be-bb92-491d-bdf8-28622746b8a8" />
<img width="520" height="280" alt="image" src="https://github.com/user-attachments/assets/84d667f3-8112-48b7-8b16-501cd8700bfd" />

4. <img width="1572" height="862" alt="image" src="https://github.com/user-attachments/assets/226b7b42-b7e1-4f8f-a175-c7b02909ffe0" />
<img width="1667" height="877" alt="Captura de pantalla 2026-04-30 123937" src="https://github.com/user-attachments/assets/8d85475c-8d69-4fef-8bd8-d3534a80b541" />
<img width="1495" height="851" alt="image" src="https://github.com/user-attachments/assets/d35a8efc-515c-431e-bcab-7b2f1fa2c696" />

6. Mapa de Decisiones (Relación Forma-Física-Audio)
- Tipografía: Serif para denotar peso histórico y espiritual.
- Física (Matter.js):
Gravedad Cero: Para permitir que las manchas floten como en un líquido.
Fricción de Aire Alta: Para que los movimientos sean suaves y no erráticos.
Constraints: Uso de fuerzas magnéticas para que las partículas formen el símbolo rotatorio.
- Audio (p5.FFT):
Bajos (Bass): Controlan la escala (la palabra "respira") y la vibración del símbolo.
Energía General: Dicta la intensidad con la que los Kanjis caen.
- Interacción:
Mouse: Arrastre de fluido (fricción dirigida).
Teclado (1-5): Salto entre estados narrativos.
Espacio: Aceleración (Turbo) de la rotación, simbolizando el aumento de energía.

7. Mapa de Interpretación (Ejecución en Vivo)
La obra se ejecuta como una performance en cuatro actos:
Inicio: Pantalla blanca, calma inicial. Se activa el audio y empieza la "lluvia de tinta". El intérprete usa el mouse para "revolver" la tinta sobre las letras.
Transición: Al llegar al clímax sonoro, el texto se disuelve para formar el símbolo sagrado.
Inversión: El universo se vuelve negro y la luz (tinta blanca) cae sobre el vacío, invirtiendo la percepción inicial.
Cierre: El símbolo regresa en su forma opuesta, cerrando el ciclo eterno del Yin y el Yang.

8. Relación Audio-Comportamiento
La pieza "escucha" la canción Zhongli Theme. Los golpes de percusión (bajos) provocan una expansión física de las letras, como si la palabra tuviera un pulso cardíaco. En la fase del símbolo, los bajos activan una vibración sutil que hace que la tinta parezca estar viva y bajo tensión, reaccionando directamente a la potencia de la música.

9. Uso Explícito de IA como Materializador
Autoría Conceptual (Mía): Yo definí la palabra, la estructura de 5 fases, la idea del filtro de inversión (negro+negro=blanco), la inclusión de Kanjis y la lógica de la "lámpara de lava".
IA (Apoyo Técnico): Utilicé la IA para:
Escribir el código de los Shaders (GLSL) para lograr la textura de tinta rasgada con ruido aleatorio.
Resolver la matemática compleja de los arc() y erase() para que el símbolo del Yin Yang fuera geométricamente perfecto.
Optimizar la integración de Matter.js con el modo WEBGL de p5.js, asegurando el centrado absoluto en pantalla completa.
<img width="1523" height="143" alt="image" src="https://github.com/user-attachments/assets/21aef833-8d56-4052-a709-4d523fa372ca" />

10.Codigo:

Sketch.js:
``` js
let motor, mundo, blobs = [], kanjis = [], miFuente, miSonido, miAnalizador;
let miShader, pgText, pgInk;
let iniciado = false, fase = 1, rotacion = 0;
let modoManual = false; 
let listaKanjis = ["和", "平", "乱", "阴", "阳", "心", "道"]; 

// --- PARÁMETROS DE AJUSTE ---
let intensidadVibracion = 2; 
let velocidadNormal = 0.018; 
let velocidadTurbo = 0.12;   
let velocidadActual = 0.018;

function preload() {
  miFuente = loadFont('Serif.ttf'); 
  miSonido = loadSound('Zhongli.mp3');
  miShader = loadShader('shader.vert', 'shader.frag');
}

function setup() {
  pixelDensity(1);
  // WEBGL: El centro del lienzo es (0,0)
  createCanvas(windowWidth, windowHeight, WEBGL);
  
  // Buffers 2D: El centro es (width/2, height/2)
  pgText = createGraphics(width, height);
  pgInk = createGraphics(width, height);

  motor = Matter.Engine.create();
  mundo = motor.world;
  mundo.gravity.y = 0;

  // Inicializar lluvia (Fase 1 y 3)
  for (let i = 0; i < 15; i++) crearBlob(random(width), random(-height, height));
  
  // Inicializar Kanjis (Fase 2 y 4)
  for (let i = 0; i < 10; i++) {
    let b = Matter.Bodies.circle(random(width), random(-height, 0), 30, {
      frictionAir: 0.06, collisionFilter: { group: -1 }
    });
    kanjis.push({ cuerpo: b, txt: random(listaKanjis), offset: random(1000) });
    Matter.World.add(mundo, b);
  }
  miAnalizador = new p5.FFT();
}

function crearBlob(x, y) {
  let r = random(120, 280);
  let b = Matter.Bodies.circle(x, y, r/4, { frictionAir: 0.05, collisionFilter: { group: -1 } });
  let obj = { cuerpo: b, radio: r, offset: random(1000) };
  blobs.push(obj);
  Matter.World.add(mundo, b);
}

function draw() {
  if (!iniciado) {
    resetShader(); 
    background(255); 
    fill(0); 
    textAlign(CENTER, CENTER);
    textFont(miFuente); 
    textSize(width * 0.02); 
    text("HAZ CLIC PARA COMENZAR\n(Doble clic para Pantalla Completa)\n\nCONTROLES:\n1-5: Cambiar Fases | A: Automático | Espacio: TURBO", 0, 0);
    return;
  }

  Matter.Engine.update(motor);
  miAnalizador.analyze();
  let bajos = miAnalizador.getEnergy("bass");
  let fMusica = map(bajos, 0, 255, 0.9, 1.35); 
  
  // --- GESTIÓN DE FASES ---
  let tiempo = miSonido.currentTime();
  let duracion = miSonido.duration();

  if (!modoManual) {
    if (tiempo > 0 && !miSonido.isPlaying() && tiempo >= duracion - 0.5) fase = 5; 
    else if (tiempo < 20) fase = 1;
    else if (tiempo < 47) fase = 2;
    else if (tiempo < 86) fase = 3; // 1:26 = 86s
    else fase = 4;
  }

  // Turbo giro con Espacio
  let vTarget = keyIsDown(32) ? velocidadTurbo : velocidadNormal;
  velocidadActual = lerp(velocidadActual, vTarget, 0.1);
  rotacion += velocidadActual; 

  pgText.clear();
  pgInk.clear();

  if (fase === 1 || fase === 3 || fase === 5) {
    // --- LÓGICA DE TEXTO (Buffers 2D usan width/2 como centro) ---
    pgText.fill(255); pgText.textAlign(CENTER, CENTER);
    pgText.textFont(miFuente);
    if (fase === 5) {
      pgText.textSize(height * 0.06);
      pgText.text("hecho por jakeline avila - yin yang", pgText.width/2, pgText.height/2);
    } else {
      pgText.textSize(height * 0.18 * fMusica);
      pgText.text("YIN YANG", pgText.width/2, pgText.height/2);
    }

    // --- LLUVIA DE TINTA ---
    pgInk.fill(255); pgInk.noStroke();
    for (let b of blobs) {
      let pos = b.cuerpo.position;
      Matter.Body.translate(b.cuerpo, { x: sin(frameCount * 0.02 + b.offset) * 2, y: 3 });
      if (pos.y > height + 200) Matter.Body.setPosition(b.cuerpo, { x: random(width), y: -200 });
      if (mouseIsPressed && dist(mouseX, mouseY, pos.x, pos.y) < 150) {
        Matter.Body.setVelocity(b.cuerpo, { x: (mouseX - pmouseX)*0.6, y: (mouseY - pmouseY)*0.6 });
      }
      pgInk.ellipse(pos.x, pos.y, b.radio * fMusica);
    }
  } 
  else {
    // --- FASE 2 Y 4: SÍMBOLO Y KANJIS ---
    pgInk.fill(255); pgInk.textAlign(CENTER, CENTER); pgInk.textSize(60 * fMusica);
    for (let k of kanjis) {
      let pos = k.cuerpo.position;
      Matter.Body.translate(k.cuerpo, { x: sin(frameCount*0.01 + k.offset), y: 2 });
      if (pos.y > height + 100) Matter.Body.setPosition(k.cuerpo, { x: random(width), y: -100 });
      if (mouseIsPressed && dist(mouseX, mouseY, pos.x, pos.y) < 80) {
        Matter.Body.setVelocity(k.cuerpo, { x: (mouseX-pmouseX)*0.6, y: (mouseY-pmouseY)*0.6 });
      }
      pgInk.text(k.txt, pos.x, pos.y);
    }

    // Dibujo del Símbolo centrado en pgInk
    pgInk.push();
    let shake = map(bajos, 180, 255, 0, intensidadVibracion, true);
    pgInk.translate(pgInk.width/2 + random(-shake, shake), pgInk.height/2 + random(-shake, shake));
    pgInk.rotate(rotacion); pgInk.scale(fMusica);
    let R = height * 0.35;
    pgInk.fill(255); pgInk.noStroke();
    pgInk.ellipse(0, 0, R * 2);
    pgInk.erase();
    pgInk.arc(0, 0, R * 2, R * 2, HALF_PI, -HALF_PI); 
    pgInk.ellipse(0, -R/2, R); pgInk.noErase();
    pgInk.fill(255); pgInk.ellipse(0, R/2, R);
    pgInk.noFill(); pgInk.stroke(255); pgInk.strokeWeight(8); 
    pgInk.ellipse(0, 0, R * 2);
    pgInk.arc(0, -R/2, R, R, HALF_PI, -HALF_PI);
    pgInk.arc(0, R/2, R, R, -HALF_PI, HALF_PI);
    pgInk.fill(255); pgInk.noStroke();
    pgInk.ellipse(0, -R/2, R/4);
    pgInk.erase();
    pgInk.ellipse(0, R/2, R/4);
    pgInk.noErase();
    pgInk.pop();

    for (let b of blobs) {
      Matter.Body.setVelocity(b.cuerpo, { 
        x: (width/2 - b.cuerpo.position.x) * 0.05, y: (height/2 - b.cuerpo.position.y) * 0.05 
      });
    }
  }

  // --- APLICAR SHADER (Centrado para WEBGL) ---
  shader(miShader);
  miShader.setUniform('uText', pgText);
  miShader.setUniform('uInk', pgInk);
  
  let valInv = 0.0;
  if (fase === 2) valInv = 1.0;
  else if (fase === 3) valInv = 2.0;
  else if (fase === 4) valInv = 3.0;
  else if (fase === 5) valInv = 0.0;
  
  miShader.setUniform('uInversion', valInv);
  miShader.setUniform('uTime', millis()/1000.0);
  
  // En WEBGL el rect(0,0) se dibuja centrado si el modo es CENTER
  rectMode(CENTER);
  rect(0, 0, width, height);
}

function keyPressed() {
  if (key === '1') { fase = 1; modoManual = true; }
  if (key === '2') { fase = 2; modoManual = true; }
  if (key === '3') { fase = 3; modoManual = true; }
  if (key === '4') { fase = 4; modoManual = true; }
  if (key === '5') { fase = 5; modoManual = true; }
  if (key === 'a' || key === 'A') { modoManual = false; } 
}

function doubleClicked() {
  let fs = fullscreen();
  fullscreen(!fs);
}

function mousePressed() {
  if (!iniciado) { userStartAudio(); miSonido.play(); iniciado = true; }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
  pgText.resizeCanvas(windowWidth, windowHeight);
  pgInk.resizeCanvas(windowWidth, windowHeight);
}
```
``` js
precision highp float;
varying vec2 vTexCoord;
uniform sampler2D uText;  
uniform sampler2D uInk;   
uniform float uInversion; // 0: F1, 1: F2, 2: F3, 3: F4
uniform float uTime;

float random (vec2 st) {
    return fract(sin(dot(st.xy, vec2(12.9898,78.233))) * 43758.5453123);
}

void main() {
  vec2 uv = vec2(vTexCoord.x, 1.0 - vTexCoord.y);
  float n = random(uv + uTime * 0.01) * 0.04;
  
  float textMask = texture2D(uText, uv).a;
  float inkMask = texture2D(uInk, uv + n).a;
  
  float t = step(0.5, textMask);
  float edgeNoise = random(uv * 12.0) * 0.12;
  float i = smoothstep(0.45 - edgeNoise, 0.55, inkMask);
  
  vec3 finalCol;
  
  if (uInversion < 0.5) { // FASE 1: Yin Lluvia (Fondo Blanco)
    if (t > 0.1 && i > 0.1) finalCol = vec3(1.0); 
    else if (t > 0.1 || i > 0.1) finalCol = vec3(0.0);
    else finalCol = vec3(1.0);
  } 
  else if (uInversion < 1.5) { // FASE 2: Yang Símbolo (Fondo Negro)
    finalCol = mix(vec3(0.0), vec3(1.0), i);
  } 
  else if (uInversion < 2.5) { // FASE 3: Yang Lluvia (Fondo Negro)
    if (t > 0.1 && i > 0.1) finalCol = vec3(0.0); 
    else if (t > 0.1 || i > 0.1) finalCol = vec3(1.0);
    else finalCol = vec3(0.0);
  }
  else { // FASE 4: Yin Símbolo (Fondo Blanco)
    finalCol = mix(vec3(1.0), vec3(0.0), i);
  }

  gl_FragColor = vec4(finalCol, 1.0);
}
```

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

11. Link: https://editor.p5js.org/Jakeline-Avila/sketches/yf83920E1

12. <img width="1272" height="990" alt="image" src="https://github.com/user-attachments/assets/6db56304-aea6-401d-811e-483666e79841" />
<img width="1248" height="1008" alt="image" src="https://github.com/user-attachments/assets/7753756e-68c3-4180-a342-e163f36712c4" />
<img width="1266" height="958" alt="image" src="https://github.com/user-attachments/assets/ea3523b5-1585-4453-94d5-9d1b70a60fb8" />
<img width="1225" height="1008" alt="image" src="https://github.com/user-attachments/assets/7ff8ebd8-3da9-4594-a204-c2d36ceed737" />

## Bitácora de reflexión
