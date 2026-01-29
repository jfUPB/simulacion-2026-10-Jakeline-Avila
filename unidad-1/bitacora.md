# Unidad 1

## Bitácora de proceso de aprendizaje

### Actividad 1

- La aleatoriedad en el arte generativo introduce sorpresa y diversidad, permitiendo que cada obra emerja como una variación única e impredecible dentro de un sistema de reglas diseñado por el artista, permitiendo tambien la exploración del arte mismo.

### Actividad 2

Código modificado: 

```
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  walker2 = new Walker();
  
  background(255);
}

function draw() {
  walker.step();
  walker.show();
  
  walker2.step();
  walker2.show();
  
  
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    stroke(0);
    circle(this.x, this.y, 50);
  }

  step() {
    const choice = floor(random(100));
    if (choice == 0) {
      this.x++;
    } else if (choice == 1) {
      this.x--;
    } else if (choice == 2) {
      this.y++;
    } else {
      this.y--;
    }
  }
}
```

- Una vez modificado el código, cambié la clase walker los valores y en el step el random a 7, esperaba que el punto se moviera de forma más variada e impredecible, ya que estaba aumentando el rango de valores aleatorios, manteniendo el comportamiento de una caminata aleatoria similar al ejemplo original. Pero en cambio solo cambió la dirección a la que iba que fue hacia arriba, siempre que lo ejecuto desde que hice los cambios solo va hacia arriba.

- No ocurrió exactamente lo que esperaba. Esto creo que sucedió porque al aumentar el rango de valores aleatorios sin equilibrar las condiciones.

### Actividad 3

- Una distribución uniforme es cuando los números salen repartidos por igual y cualquier valor puede aparecer con la misma probabilidad. Una distribución no uniforme es cuando algunos números salen más seguido que otros, haciendo que los resultados se acumulen más en ciertas partes, aunque siga siendo algo aleatorio.
```
 // The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  walker2 = new Walker();
  
  background(255);
}

function draw() {
  walker.step();
  walker.show();
  
  walker2.step();
  walker2.show();
  
  
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    stroke(0);
    circle(this.x, this.y, 50);
  }

  step() {
    const choice = floor(random(4));
    if (choice == 0) {
      this.x++;
    } else if (choice == 1) {
      this.x++;
    } else if (choice == 2) {
      this.y++;
    } else {
      this.y--;
    }
  }
}

```

### Actividad 4

https://editor.p5js.org/Jakeline-Avila/sketches/vczshUJTb

<img width="1895" height="834" alt="image" src="https://github.com/user-attachments/assets/36edb5ce-8259-44d8-956a-29bb971d496f" />


``` js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

function setup() {
  createCanvas(640, 240);
  background(255);
}
function draw() {
  //{!1} A normal distribution with mean 320 and standard deviation 60
  let x = randomGaussian(320, 60);
  let y = randomGaussian(120, 30);

  noStroke();
  fill(random(255), random(255), random(255), 20);

  let d = 20;
  let s = 5;

  
  square(x, y, s);
  square(x, y - d, s);
  square(x, y + d, s);
  circle(x - d, y, s);
  circle(x + d, y, s);
  circle(x - d, y - d, s);
  circle(x + d, y - d, s);
  circle(x - d, y + d, s);
  circle(x + d, y + d, s);
}

```

### Actividad 5

https://editor.p5js.org/Jakeline-Avila/sketches/h4cZb34vs
<img width="1918" height="890" alt="image" src="https://github.com/user-attachments/assets/76c425c8-d561-4595-a2c7-8a19acc93b04" />
- En este sketch se utiliza la técnica de Lévy flight para controlar el movimiento de las figuras, combinando desplazamientos pequeños la mayor parte del tiempo con saltos grandes ocasionales. Esta distribución permite simular un movimiento más natural y menos predecible que una caminata aleatoria uniforme, ya que genera zonas de acumulación visual interrumpidas por cambios bruscos de posición. El resultado esperado es un comportamiento dinámico y orgánico, donde el patrón se construye de manera irregular, aportando mayor riqueza visual y sensación de exploración dentro del canvas.

``` js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com
let x;
let y;

function setup() {
  createCanvas(640, 240);
  background(255);

  x = width / 2;
  y = height / 2;
}

function draw() {
  noStroke();
  fill(random(255), random(255), random(255), 20);

  let d = 20;
  let s = 12;

  square(x, y, s);

  square(x, y - d, s);
  square(x, y + d, s);

  circle(x - d, y, s);
  circle(x + d, y, s);

  circle(x - d, y - d, s);
  circle(x + d, y - d, s);
  circle(x - d, y + d, s);
  circle(x + d, y + d, s);

  let r = random(1);
  let xstep, ystep;

  if (r < 0.01) {
    // 1% de probabilidad de salto grande
    xstep = random(-100, 100);
    ystep = random(-100, 100);
  } else {
    // movimiento pequeño la mayor parte del tiempo
    xstep = random(-2, 2);
    ystep = random(-2, 2);
  }

  x += xstep;
  y += ystep;

  // mantener dentro del canvas
  x = constrain(x, 0, width);
  y = constrain(y, 0, height);
}


```

### Actividad 6
https://editor.p5js.org/Jakeline-Avila/sketches/5MZu_Yvbo

<img width="1764" height="762" alt="image" src="https://github.com/user-attachments/assets/ec63bd9d-720e-498e-bcb3-c056d4dc7e04" />

- En este sketch se utiliza ruido Perlin para generar un movimiento continuo y suave, a diferencia del ruido aleatorio que produce cambios bruscos e impredecibles. El ruido Perlin permite que los valores varíen de forma gradual en el tiempo, lo que se traduce en trayectorias más orgánicas y naturales dentro del canvas. En esta visualización, el Perlin noise controla los desplazamientos pequeños del objeto, creando fluidez y coherencia en el movimiento, mientras que los saltos ocasionales rompen ligeramente esa continuidad. El resultado esperado es un patrón visual más armónico, con transiciones suaves y una sensación de movimiento constante, similar a fenómenos naturales como corrientes, viento o desplazamientos orgánicos.
- 
``` js
let x;
let y;

let xoff = 0;
let yoff = 1000;

function setup() {
  createCanvas(640, 240);
  background(255);

  x = width / 2;
  y = height / 2;
}

function draw() {
  noStroke();
  fill(random(255), random(255), random(255), 20);

  let d = 20;
  let s = 12;

  square(x, y, s);
  square(x, y - d, s);
  square(x, y + d, s);
  circle(x - d, y, s);
  circle(x + d, y, s);
  circle(x - d, y - d, s);
  circle(x + d, y - d, s);
  circle(x - d, y + d, s);
  circle(x + d, y + d, s);

  let r = random(1);
  let xstep, ystep;

  if (r < 0.01) {
    // Lévy flight: salto grande ocasional
    xstep = random(-100, 100);
    ystep = random(-100, 100);
  } else {
    // Movimiento suave con Perlin Noise
    let nx = noise(xoff);
    let ny = noise(yoff);

    xstep = map(nx, 0, 1, -2, 2);
    ystep = map(ny, 0, 1, -2, 2);

    xoff += 0.01;
    yoff += 0.01;
  }

  x += xstep;
  y += ystep;

  x = constrain(x, 0, width);
  y = constrain(y, 0, height);
}

```

## Bitácora de aplicación 
### Actividad 7

https://editor.p5js.org/Jakeline-Avila/sketches/u9AM8Q_zK

- Esta obra es un lyric video generativo donde el texto de la canción se convierte en el principal elemento visual y se comporta como un sistema dinámico. Las palabras no siguen una animación predefinida, sino que se mueven y transforman en tiempo real mediante la combinación de ruido Perlin, aleatoriedad y saltos tipo Lévy flight.
``` js
// Actividad 07 – Obra generativa
// Lyric video generativo con Lévy flight, Perlin Noise y aleatoriedad

let lyrics = [
  "Caramelldansen",
  "U-u-u-yeah!",
  "Ooh ooh ooh ah ah",
  "So dance on and on",
  "Dum dee dum"
];

let currentWord = 0;

// posición del texto
let x, y;

// offsets para Perlin Noise
let xoff = 0;
let yoff = 1000;

// modo caos (fondo tipo epilepsia)
let chaosMode = true;

function setup() {
  createCanvas(640, 360);
  background(0);
  textAlign(CENTER, CENTER);
  rectMode(CENTER);

  x = width / 2;
  y = height / 2;
}

function draw() {
  // FONDO
  if (chaosMode) {
    background(
      random(255),
      random(255),
      random(255),
      120
    );
  } else {
    background(0, 20); // modo acumulativo
  }

  // MOVIMIENTO: Perlin + Lévy flight
  let r = random(1);
  let xstep, ystep;

  if (r < 0.02) {
    // Lévy flight → salto brusco + cambio de palabra
    xstep = random(-200, 200);
    ystep = random(-120, 120);
    currentWord = (currentWord + 1) % lyrics.length;
  } else {
    // Movimiento fluido con ruido Perlin
    let nx = noise(xoff);
    let ny = noise(yoff);

    xstep = map(nx, 0, 1, -3, 3);
    ystep = map(ny, 0, 1, -3, 3);

    xoff += 0.01;
    yoff += 0.01;
  }

  x += xstep;
  y += ystep;

  // mantener dentro del canvas
  x = constrain(x, 0, width);
  y = constrain(y, 0, height);

  // DIBUJO DEL TEXTO
  push();
  translate(x, y);
  rotate(random(-0.2, 0.2));

  let txtSize = map(mouseX, 0, width, 24, 72);
  textSize(txtSize);

  fill(
    random(255),
    random(255),
    random(255),
    180
  );

  text(lyrics[currentWord], 0, 0);
  pop();
}

// INTERACCIÓN
function mousePressed() {
  // Forzar salto tipo Lévy
  x += random(-250, 250);
  y += random(-150, 150);
}

function keyPressed() {
  // Activar / desactivar caos visual
  chaosMode = !chaosMode;
}

```


## Bitácora de reflexión

### Actividad 8



// Describe la diferencia fundamental entre la aleatoriedad generada por random() y la apariencia de aleatoriedad del Ruido Perlin (noise()). ¿En qué tipo de situación usarías cada una?

- Describe la diferencia fundamental entre la aleatoriedad generada por random() y la apariencia de aleatoriedad del Ruido Perlin (noise()). ¿En qué tipo de situación usarías cada una?

R/= La diferencia más importante es que random() genera valores completamente independientes, mientras que noise() genera valores correlacionados entre sí. ¿Cómo así? pues basicamente random cada número no tiene relación con el anterior y ruido perlin da apariencia de aletoriedad, pero en realidad los valores cambian de forma suave y continua.

Cuando usaría cada uni? Usaría random cuando quiero sorpresa, irregularidad o caos, como posiciones totalmente dispersas y noise cuando quiero movimientos mas naturales como desplazamientos suaves.

// Explica con tus palabras qué es una distribución de probabilidad. ¿Qué diferencia visual produce una caminata aleatoria con una distribución uniforme versus una con una distribución normal?

- Explica con tus palabras qué es una distribución de probabilidad. ¿Qué diferencia visual produce una caminata aleatoria con una distribución uniforme versus una con una distribución normal?

R/= Una distribución de probabilidad describe qué tan probable es que ocurran ciertos valores dentro de un conjunto de posibilidades. La diferencia visual entre ambas caminatas es que la distribución uniforme todos los pasos tienen la misma probabilidad mientras que la normal los pasos pequeños son más frecuentes que los grandes, el movimiento se concentra alrededor de una zona y se ve más suave y natural.

- ¿Cuál es el papel de la aleatoriedad en el arte generativo? Menciona al menos dos funciones distintas que cumple

R/= Es clave debido a que introduce variación, cada ejecución de la obra puede producir un resultado distinto aunque el código sea el mismo. También permite exploración de parte del artista podiendo jugar con el algoritmo.

- Piensa en tu obra final (Actividad 07). Describe uno de los conceptos de aleatoriedad que usaste y explica por qué fue una elección adecuada para lograr el efecto que buscabas.

R/= En mi obra utilicé una combinación de Ruido Perlin y Lévy flight. El Ruido Perlin controla el movimiento suave del texto, haciendo que se desplace de forma continua y orgánica. De manera ocasional, se activa un salto tipo Lévy flight, que produce desplazamientos bruscos y cambia la palabra mostrada.

Esta elección fue adecuada porque genera un contraste entre estabilidad y sorpresa. Además, el uso de random() en el color, la rotación y el fondo aporta energía visual y refuerza el carácter caótico del lyric video.

- ¿Qué es un “paseo” o “caminata” (walk) en el contexto de la simulación? ¿Qué característica particular tiene una caminata de tipo “Lévy flight”?

R/= Un paseo o caminata (walk) en simulación es un proceso donde un objeto se mueve paso a paso, y cada nueva posición depende de la anterior, normalmente usando reglas aleatorias.

Una caminata tipo Lévy flight se caracteriza porque combina muchos pasos pequeños con saltos grandes ocasionales, lo que produce movimientos impredecibles pero con patrones.











