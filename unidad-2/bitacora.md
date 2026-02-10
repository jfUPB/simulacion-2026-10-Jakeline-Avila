# Unidad 2

## Bitácora de proceso de aprendizaje



### Actividad 3

- Lo que tuve que hacer fue cambiar el constructor, crear un vector con los parámetros ya puestos.
- 
Código 
```js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    
    this.position = createVector(width / 2, height / 2);
  }

  show() {
    stroke(0);
    point(this.position.x, this.position.y);
  }

  step() {
    const choice = floor(random(4));

    if (choice === 0) {
      this.position.x++;
    } else if (choice === 1) {
      this.position.x--;
    } else if (choice === 2) {
      this.position.y++;
    } else {
      this.position.y--;
    }
    
  }
}

```

### Actividad 4
- ¿Qué resultado esperas obtener en el programa anterior?

R/= Que solamente se juegue con el vector.

- ¿Qué resultado obtuviste?

R/= El vector sí cambia pero pasa por referencia que es basicamente enviar una referencia del objeto a la memoria.

- Recuerda los conceptos de paso por valor y paso por referencia en programación.

R/=
- Paso por valor: Se copia el dato. Cambios dentro de la función no afectan al original.
- Paso por referencia: Se pasa una referencia al mismo objeto en memoria. Cambios dentro de la función sí afectan al original.

- ¿Qué tipo de paso se está realizando en el código?

R/= Paso por referencia, está modificando directamente position.

- ¿Qué aprendiste?

R/= Un p5.Vector puede ser modificado desde cualquier función que lo reciba.

### Actividad 5

¿Para qué sirve el método mag()? Nota que hay otro método llamado magSq(). ¿Cuál es la diferencia entre ambos? ¿Cuál es más eficiente?
¿Para qué sirve el método normalize()?
Te encuentras con un periodista en la calle y te pregunta ¿Para qué sirve el método dot()? ¿Qué le responderías en un frase?
El método dot() tiene una versión estática y una de instancia. ¿Cuál es la diferencia entre ambas?
Ahora el mismo periodista curioso de antes te pregunta si le puedes dar una intuición geométrica acerca del producto cruz. Entonces te pregunta ¿Cuál es la interpretación geométrica del producto cruz de dos vectores? Tu respuesta debe incluir qué pasa con la orientación y la magnitud del vector resultante.
¿Para que te puede servir el método dist()?
¿Para qué sirven los métodos normalize() y limit()?

### Actividad 6

``` js
let u = 0;
let velocito = 0.01;
let palla = 1;

function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(200);
  
  let v0 = createVector(50, 50);
  let v1 = createVector(300, 0);
  let v2 = createVector(0, 300);

  u += velocito * palla;
  if (u >= 1 || u <= 0) palla *= -1;

  let movingPoint = p5.Vector.lerp(v1, v2, u);

  drawArrow(v0, v1, "red");
  drawArrow(v0, v2, "blue");
  drawArrow(v0, movingPoint, "purple");
  drawArrow(p5.Vector.add(v0, v1), p5.Vector.sub(v2, v1), "green");
}

function drawArrow(base, vec, myColor) {
  push();
  stroke(myColor);
  strokeWeight(3);
  fill(myColor);
  translate(base.x, base.y);
  line(0, 0, vec.x, vec.y);
  rotate(vec.heading());
  let arrowSize = 7;
  translate(vec.mag() - arrowSize, 0);
  triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0);
  pop();
}

```

### Actividad 7

1. Cuál es el concepto del marco motion 101 y cómo se interpreta geométricamente.

R/= Motion 101 es un marco conceptual básico para describir el movimiento usando vectores. La idea central es que el movimiento se puede entender como la evolución de la posición de una partícula en el tiempo, y esa evolución se construye a partir de tres ingredientes fundamentales:

- Posición inicial

- Velocidad

- Aceleración

2. ¿Cómo se aplica motion 101 en el ejemplo?

R/= En el marco Motion 101, el movimiento se describe de forma básica mediante vectores, donde la posición de un objeto cambia al sumar su velocidad en cada instante de tiempo. En el ejemplo, el objeto Mover tiene un vector posición y un vector velocidad, y en cada frame la nueva posición se calcula con la instrucción this.position.add(this.velocity), lo que representa directamente el principio de Motion 101.

### Actividad 8

``` js
let anchor;
let position;
let velocity;
let acceleration;

let restLength = 220;   // longitud de la cuerda
let k = 0.01;           // rigidez del resorte
let damping = 0.98;

let drops = [];

function setup() {
  createCanvas(600, 600);
  background(255);

  anchor = createVector(width / 2, 40);
  position = createVector(width / 2 + 100, 300);
  velocity = createVector(0, 0);
  acceleration = createVector(0, 0);
}

function draw() {
  background(255, 30); // Fondo blanco con transparencia para efecto “fade” suave

  acceleration.mult(0); // Resetear fuerzas

  // -------- FUERZA DE CUERDA (SPRING) --------
  let force = p5.Vector.sub(position, anchor);
  let distance = force.mag();

  let stretch = distance - restLength;
  force.normalize();
  force.mult(-1 * k * stretch);

  acceleration.add(force);

  // -------- GRAVEDAD --------
  let gravity = createVector(0, 0.1);
  acceleration.add(gravity);

  // -------- ATRACCIÓN AL MOUSE --------
  let mouse = createVector(mouseX, mouseY);
  let mouseForce = p5.Vector.sub(mouse, position);

  let d = constrain(mouseForce.mag(), 20, 300);
  mouseForce.normalize();

  let strength = map(d, 20, 300, 0.05, 0.005);
  mouseForce.mult(strength);

  acceleration.add(mouseForce);

  // -------- MOTION 101 --------
  velocity.add(acceleration);
  velocity.mult(damping);
  position.add(velocity);

  // -------- DIBUJO CUERDA --------
  stroke(0, 30);
  line(anchor.x, anchor.y, position.x, position.y);

  // -------- CUBETA (partícula principal) --------
  noStroke();
  fill(0);
  circle(position.x, position.y, 14);

  // -------- GENERAR GOTAS DE PINTURA --------
  if (frameCount % 2 === 0) {
    drops.push(new Drop(position.x, position.y));
  }

  // -------- ACTUALIZAR Y MOSTRAR GOTAS --------
  for (let d of drops) {
    d.update();
    d.show();
  }
}

function mousePressed() {
  position.set(mouseX, mouseY);
  velocity.set(0, 0);
}

// -------- CLASE DROP --------
class Drop {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(random(-0.4, 0.4), random(1, 2));
    this.acceleration = createVector(0, 0.06);
    this.life = 255;
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.life -= 2;
  }

  show() {
    noStroke();
    fill(0, 18);
    circle(this.position.x, this.position.y, 4);
  }
}

```

## Bitácora de aplicación 



## Bitácora de reflexión





