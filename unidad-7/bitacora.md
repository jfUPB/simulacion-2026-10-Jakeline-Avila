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


## Bitácora de reflexión
