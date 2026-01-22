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
  function setup() {
  createCanvas(100, 100);
  background(200);
}

function draw() {
  noStroke();
  fill(0, 10);

  // Distribución NO uniforme, favorece la derecha
  let x = randomGaussian(70, 15);
  let y = 25;
  circle(x, y, 5);

  // Gaussian con poca dispersión
  x = randomGaussian(50, 1);
  y = 50;
  circle(x, y, 5);

  // Gaussian con mayor dispersión
  x = randomGaussian(50, 10);
  y = 75;
  circle(x, y, 5);
}
```

### Actividad 4


## Bitácora de aplicación 


## Bitácora de reflexión



