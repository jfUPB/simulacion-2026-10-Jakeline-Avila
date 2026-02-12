# Unidad 2

## Bitácora de proceso de aprendizaje
### Actividad 1

<img width="1107" height="1012" alt="image" src="https://github.com/user-attachments/assets/ace78b90-b3c3-4c4b-9403-69aec7f5b438" />


- En esta exploración de artistas que trabajan con vectores, movimiento y animación generativa, el proyecto que más me llamó la atención fue “Beary Bear” de Raven Kwok. Me impactó especialmente la forma en que las partículas construyen la figura del oso a través del movimiento, generando una sensación de vida y fluidez constante.

- Lo que más me gustó fue cómo el desplazamiento de los puntos parece responder a fuerzas invisibles, lo que sugiere el uso de vectores, velocidad y aceleración como parte fundamental de la obra. No se percibe como una animación tradicional, sino como un sistema dinámico donde cada partícula contribuye a la forma general sin perder su autonomía.

- Además, me parece muy interesante la relación entre arte, programación y física que plantea este tipo de trabajos. La obra demuestra cómo conceptos matemáticos pueden convertirse en experiencias visuales poéticas, logrando que la tecnología no solo sea funcional sino también expresiva.

### Actividad 2

- La suma de vectores en p5.js se realiza usando métodos propios del objeto p5.Vector, como add(). En el ejemplo, position.add(velocity); actualiza la posición de la pelota sumando la velocidad en cada frame, es decir, se suman las coordenadas X y Y de ambos vectores para generar el movimiento.

- La línea position = position + velocity; no funciona porque los vectores en p5.js son objetos, no números. El operador + no suma sus componentes, por lo que es necesario usar funciones específicas como add() para realizar correctamente la operación.

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

- El método mag() sirve para saber qué tan largo es un vector. magSq() hace lo mismo pero sin sacar la raíz cuadrada, por eso es más rápido cuando solo se quiere comparar tamaños.

- El método normalize() sirve para dejar el vector con tamaño 1 pero sin cambiar hacia dónde apunta.

- El método dot() sirve para saber si dos vectores van en la misma dirección o no.

- La diferencia entre el dot() normal y el estático es que uno se usa desde un vector (v1.dot(v2)) y el otro recibe los dos vectores directamente (p5.Vector.dot(v1,v2)).

- El producto cruz da un vector perpendicular a los otros dos; la dirección depende del orden en que los pongas y el tamaño indica qué tan “abiertos” están.

- El método dist() sirve para medir la distancia entre dos puntos o vectores.

- normalize() ayuda a mantener la dirección y limit() sirve para que un vector no se pase de cierta velocidad o tamaño.

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

- ¿Cómo funciona lerp() y lerpColor()?

- lerp() significa “mezclar” entre dos cosas. En vectores: p5.Vector.lerp(v1, v2, u) te da un punto “entre” v1 y v2.

- Si u = 0 → te da v1
- Si u = 1 → te da v2
- Si u = 0.5 → te da justo la mitad
 Si u va cambiando con el tiempo, ese punto se mueve de v1 a v2 (y si lo haces rebotar, va y vuelve).

lerpColor() hace lo mismo pero con colores: mezcla un color con otro según u.

- u = 0 → color A
- u = 1 → color B
- u = 0.5 → mezcla 50/50

- ¿Cómo se dibuja una flecha con drawArrow()?

drawArrow(base, vec, color) dibuja una flecha así:
Mueve el origen al punto base con translate(base.x, base.y).
Dibuja la línea principal desde (0,0) hasta (vec.x, vec.y).
Gira todo para que apunte en la dirección del vector con rotate(vec.heading()).
Se mueve casi al final de la línea con translate(vec.mag() - arrowSize, 0).
Dibuja la punta con un triángulo (triangle(...)).

### Actividad 7

1. Cuál es el concepto del marco motion 101 y cómo se interpreta geométricamente.

R/= Motion 101 es un marco conceptual básico para describir el movimiento usando vectores. La idea central es que el movimiento se puede entender como la evolución de la posición de una partícula en el tiempo, y esa evolución se construye a partir de tres ingredientes fundamentales:

- Posición inicial

- Velocidad

- Aceleración

2. ¿Cómo se aplica motion 101 en el ejemplo?

R/= En el marco Motion 101, el movimiento se describe de forma básica mediante vectores, donde la posición de un objeto cambia al sumar su velocidad en cada instante de tiempo. En el ejemplo, el objeto Mover tiene un vector posición y un vector velocidad, y en cada frame la nueva posición se calcula con la instrucción this.position.add(this.velocity), lo que representa directamente el principio de Motion 101.

### Actividad 8

- Cuando probé aceleración constante, el movimiento se volvió cada vez más rápido en la misma dirección. Se siente como si el objeto tuviera un impulso fijo que lo empuja todo el tiempo.

- Con aceleración aleatoria, el movimiento fue impredecible y más orgánico. El objeto cambia de dirección constantemente, dando la sensación de algo más natural o caótico.

- Cuando usé aceleración hacia el mouse, el objeto parecía “perseguir” el cursor. Se genera un efecto interactivo interesante porque el movimiento responde directamente a mi posición, haciendo que el sistema se sienta vivo.

- En general entendí que la aceleración es clave porque define cómo cambia el movimiento; dependiendo de cómo se calcule, el comportamiento puede verse ordenado, caótico o interactivo

  
## Bitácora de aplicación 
### Actividad 9

- 1) Concepto de la obra generativa

Mi obra es una pieza generativa en tiempo real donde un “péndulo” (una partícula principal unida a un ancla por una cuerda/resorte) se mueve con física básica y va dejando un rastro de “gotas de tinta/pintura” que caen y se acumulan en el espacio. La idea es mezclar un comportamiento controlado (tensión del resorte + gravedad) con una fuerza interactiva (atracción al mouse), para que el usuario sienta que está “guiando” el movimiento pero nunca lo controla por completo.

- Regla de aceleración aplicada (Motion 101):

La aceleración se calcula como la suma de fuerzas:

- Fuerza tipo resorte (cuerda elástica hacia el ancla)
- Gravedad constante hacia abajo
- Atracción al mouse (dependiente de la distancia)

Luego se aplica Motion 101:

- velocity += acceleration
- position += velocity y un damping para que no se vuelva infinito y se sienta más “orgánico”.

- Por qué lo elegí / qué me evoca:
Lo pensé como una exploración artística de equilibrio entre orden y caos: la cuerda y la gravedad generan una dinámica “natural”, y el mouse introduce intención humana.

``` js
let anchor;
let position;
let velocity;
let acceleration;

let restLength = 220; // longitud de la cuerda
let k = 0.01;         // rigidez del resorte
let damping = 0.98;

let drops = [];
let trail;            // capa donde SÍ se acumula el rastro
let fade = 5;         // 5 = borra suave / 0 = no borra (acumula)

function setup() {
  createCanvas(600, 600);

  // Capa para el rastro (solo gotas)
  trail = createGraphics(width, height);
  trail.background(255);

  anchor = createVector(width / 2, 40);
  position = createVector(width / 2 + 100, 300);
  velocity = createVector(0, 0);
  acceleration = createVector(0, 0);

  textFont("monospace");
}

function draw() {
  // Canvas principal: limpio completo para que la "cubeta" NO deje estela fea
  background(255);

  // Capa trail: se borra según fade (si fade=0, NO borra nada)
  trail.noStroke();
  trail.fill(255, fade);
  trail.rect(0, 0, width, height);

  // Reset fuerzas
  acceleration.mult(0);

  // -------- FUERZA DE CUERDA (SPRING / HOOKE) --------
  let force = p5.Vector.sub(position, anchor);
  let distance = force.mag();
  let stretch = distance - restLength;

  force.normalize();
  force.mult(-1 * k * stretch);
  acceleration.add(force);

  // -------- GRAVEDAD --------
  acceleration.add(createVector(0, 0.1));

  // -------- ATRACCIÓN AL MOUSE (más fuerte cerca) --------
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

  // -------- GENERAR GOTAS (dibujan en trail) --------
  if (frameCount % 2 === 0) {
    drops.push(new Drop(position.x, position.y));
  }

  for (let dr of drops) {
    dr.update();
    dr.show(trail); // <- dibuja en la capa
  }
  drops = drops.filter((dr) => dr.life > 0);

  // Pegar la capa sobre el canvas
  image(trail, 0, 0);

  // -------- DIBUJO CUERDA (sin rastro) --------
  stroke(0, 40);
  line(anchor.x, anchor.y, position.x, position.y);

  // -------- CUBETA / PARTÍCULA PRINCIPAL (sin rastro) --------
  noStroke();
  fill(0);
  circle(position.x, position.y, 14);

  // HUD simple
  noStroke();
  fill(0);
  text("B: toggle fade | fade=" + fade + "  (0=acumula)", 10, 20);
}

function mousePressed() {
  position.set(mouseX, mouseY);
  velocity.set(0, 0);
}

function keyPressed() {
  // Toggle entre rastro suave y acumulación total
  if (key === "b" || key === "B") {
    fade = (fade === 0) ? 5 : 0;
  }

  // (Opcional) limpiar todo con 'c'
  if (key === "c" || key === "C") {
    trail.background(255);
    drops = [];
  }
}

// -------- CLASE DROP --------
class Drop {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(random(-0.4, 0.4), random(1, 2));
    this.acceleration = createVector(0, 0.06);
    this.life = 180; // se usa como opacidad (más vida = más visible)
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.life -= 2;
  }

  show(layer) {
    layer.noStroke();
    layer.fill(0, this.life);          // se desvanece con la vida
    layer.circle(this.position.x, this.position.y, 5);
  }
}

```
Link: https://editor.p5js.org/Jakeline-Avila/sketches/xIDuxBhzS

<img width="904" height="936" alt="image" src="https://github.com/user-attachments/assets/bb75d804-fa82-41d6-ab6d-9417ae93a038" />
<img width="808" height="753" alt="image" src="https://github.com/user-attachments/assets/f56b3539-79df-4d9d-935b-b8cd9cea13a6" />
<img width="849" height="896" alt="image" src="https://github.com/user-attachments/assets/ae4b44de-a23b-4a8f-b953-b7f021c845a9" />
<img width="885" height="923" alt="image" src="https://github.com/user-attachments/assets/e2a6f6dc-1ab9-4cab-ad2e-ef744d0c72ea" />

## Bitácora de reflexión








