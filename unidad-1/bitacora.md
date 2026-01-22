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

## Bitácora de aplicación 


## Bitácora de reflexión






