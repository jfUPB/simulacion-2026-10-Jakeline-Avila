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
``` js
let brushes = [];
let currentBrush;

let x, y;          // posición
let xoff = 0;      // Perlin Noise offsets
let yoff = 1000;

function preload() {
  // Cargar imágenes como pinceles (sube tus imágenes a Assets)
  brushes.push(loadImage('0.png'));
  brushes.push(loadImage('Dimitri.png'));
  brushes.push(loadImage('Dimitri2.jpg'));
  brushes.push(loadImage('Dimitri3.jpg'));
  
  // El primer pincel inicial
  currentBrush = brushes[0];
}

function setup() {
  createCanvas(640, 360);
  background(random(255));      
  imageMode(CENTER);
  
  // posición inicial al centro
  x = width / 2;
  y = height / 2;
}

function draw() {
  // movimiento Lévy flight + Perlin Noise
  let r = random(1);
  let xstep, ystep;

  if (r < 0.01) {
    // salto grande ocasional
    xstep = random(-100, 100);
    ystep = random(-100, 100);
  } else {
    // movimiento suave con Perlin Noise
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

  // rotación aleatoria suave
  push();
  translate(x, y);
  rotate(map(noise(xoff), 0, 1, -PI/6, PI/6));
  
  // tamaño aleatorio para más efecto generativo
  let size = random(30, 60);
  
  // dibujar el pincel actual
  image(currentBrush, 0, 0, size, size);
  pop();
}

// Cambiar pincel cuando se presiona cualquier tecla
function keyPressed() {
  currentBrush = random(brushes);
}

```


## Bitácora de reflexión










