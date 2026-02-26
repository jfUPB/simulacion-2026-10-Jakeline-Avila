# Unidad 3
``` js

```
## Bitácora de proceso de aprendizaje
### Actividad 1

Después de ver la obra Magnetosphere de Robert Hodgin, sentí algo que no es tan común cuando uno mira una pantalla: asombro real. No es el asombro rápido de un video viral, sino uno más silencioso, más profundo. La obra parece viva. No es simplemente animación; es comportamiento. Es un sistema que responde, que evoluciona, que respira a través de fuerzas invisibles.

Lo que más me impactó es cómo trabaja con sistemas dinámicos. No “dibuja” cada movimiento; crea las condiciones para que el movimiento ocurra. Eso me hizo pensar en la diferencia entre controlar todo y diseñar reglas para que algo emerja. Hay algo casi filosófico ahí: el artista no impone una forma final, sino que permite que la forma se descubra en el proceso.

Mientras escuchaba su charla, no pude evitar conectar con la sensación que mencionas: vivimos en la inmediatez. Queremos el resultado sin atravesar el proceso. Pero lo que hace Hodgin es exactamente lo contrario. Su obra exige tiempo. Exige prueba y error. Exige frustración. Exige curiosidad. No parece alguien que busque “ganar” algo inmediato, sino alguien que explora.

### Actividad 2

En la actividad anterior, la aceleración era casi un capricho creativo. Yo decidía hacia dónde y cuánto se movía el objeto. Pero al introducir fuerzas, el movimiento deja de ser arbitrario y empieza a tener coherencia interna. Ya no es solo estética; es sistema.

La segunda ley de Newton aparece como un puente entre física y arte generativo.

Lo que más me hizo pensar fue esta línea:

``` js
this.acceleration.mult(0);
```
Al principio parece innecesaria. ¿Por qué borrar la aceleración justo después de usarla?

Pero si no la reiniciamos, la aceleración se acumula indefinidamente. Es decir, las fuerzas de un frame seguirían afectando todos los siguientes frames. Sería como si el viento soplara una sola vez y el objeto acelerara para siempre.

Multiplicar por cero no es un “borrón porque sí”. Es una decisión conceptual:
cada frame es un nuevo presente.

Lo que más me impacta es cómo algo tan pequeño —reiniciar un vector, copiar un objeto— cambia por completo el comportamiento del sistema.

En arte generativo, las decisiones invisibles son las más importantes.

Un mult(0) puede ser la diferencia entre un sistema controlado y uno caótico.
Un mal manejo de referencias puede romper la lógica física del mundo que estamos creando.

También me doy cuenta de algo: estamos diseñando leyes. No solo animaciones. Estamos construyendo pequeños universos con reglas internas consistentes.

### Actividad 3

#### Fricción
``` js
let movers = [];

function setup() {
  createCanvas(600, 400);
  for (let i = 0; i < 15; i++) {
    movers.push(new Mover(random(width), random(height)));
  }
}

function draw() {
  background(10, 10, 20, 40);

  for (let m of movers) {
    let friction = m.vel.copy();
    friction.mult(-1);
    friction.setMag(0.02);
    m.applyForce(friction);

    m.update();
    m.show();
  }
}

class Mover {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D().mult(random(2, 5));
    this.acc = createVector();
  }

  applyForce(f) {
    this.acc.add(f);
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
  }

  show() {
    noStroke();
    fill(200, 200, 255);
    circle(this.pos.x, this.pos.y, 6);
  }
}
``` js
let movers = [];

function setup() {
  createCanvas(600, 400);
  for (let i = 0; i < 8; i++) {
    movers.push(new Mover(random(width), random(height)));
  }
}

function draw() {
  background(15, 20, 30);

  for (let m of movers) {
    // gravedad para que haya movimiento constante
    m.applyForce(createVector(0, 0.2));

    m.update();
    m.bounce();
    m.show();
  }
}

class Mover {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D().mult(5);
    this.acc = createVector();
    this.friction = 0.95; // pérdida de energía
  }

  applyForce(f) {
    this.acc.add(f);
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
  }

  bounce() {
    if (this.pos.x > width || this.pos.x < 0) {
      this.vel.x *= -this.friction;
    }
    if (this.pos.y > height || this.pos.y < 0) {
      this.vel.y *= -this.friction;
    }
  }

  show() {
    fill(150, 200, 255);
    noStroke();
    circle(this.pos.x, this.pos.y, 12);
  }
}
```
``` js
let movers = [];

function setup() {
  createCanvas(600, 400);
  for (let i = 0; i < 6; i++) {
    movers.push(new Mover(random(width), random(50)));
  }
}

function draw() {
  background(0);

  stroke(255);
  line(0, height - 20, width, height - 20); // suelo

  for (let m of movers) {
    m.applyForce(createVector(0, 0.4)); // gravedad

    // fricción SOLO en el suelo
    if (m.pos.y > height - 20) {
      let friction = m.vel.copy();
      friction.mult(-1);
      friction.setMag(0.2);
      m.applyForce(friction);
    }

    m.update();
    m.edges();
    m.show();
  }
}

class Mover {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = createVector(random(-3, 3), 0);
    this.acc = createVector();
  }

  applyForce(f) {
    this.acc.add(f);
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
  }

  edges() {
    if (this.pos.y > height - 20) {
      this.pos.y = height - 20;
      this.vel.y *= -0.6;
    }
  }

  show() {
    fill(255, 120, 120);
    noStroke();
    circle(this.pos.x, this.pos.y, 16);
  }
}
```
#### Resistencia al aire y fluidos
``` js
let balls = [];

function setup() {
  createCanvas(600, 400);
  for (let i = 0; i < 8; i++) {
    balls.push(new Ball(random(width), random(-100, 0), random(1, 3)));
  }
}

function draw() {
  background(230);

  // agua
  noStroke();
  fill(100, 150, 255, 150);
  rect(0, height / 2, width, height / 2);

  for (let b of balls) {
    let gravity = createVector(0, 0.2 * b.mass);
    b.applyForce(gravity);

    // SOLO dentro del agua hay drag fuerte
    if (b.pos.y > height / 2) {
      let speed = b.vel.mag();
      let dragMag = 0.1 * speed * speed;

      let drag = b.vel.copy();
      drag.mult(-1);
      drag.setMag(dragMag);
      b.applyForce(drag);
    }

    b.update();
    b.show();
  }
}

class Ball {
  constructor(x, y, m) {
    this.pos = createVector(x, y);
    this.vel = createVector();
    this.acc = createVector();
    this.mass = m;
  }

  applyForce(f) {
    this.acc.add(p5.Vector.div(f, this.mass));
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
  }

  show() {
    fill(50);
    circle(this.pos.x, this.pos.y, this.mass * 12);
  }
}
```
``` js
let balls = [];

function setup() {
  createCanvas(600, 400);
  for (let i = 0; i < 8; i++) {
    balls.push(new Ball(random(width), random(-100, 0), random(1, 3)));
  }
}

function draw() {
  background(230);

  // agua
  fill(100, 150, 255, 150);
  noStroke();
  rect(0, height / 2, width, height / 2);

  for (let b of balls) {
    // gravedad
    let gravity = createVector(0, 0.2 * b.mass);
    b.applyForce(gravity);

    if (b.pos.y > height / 2) {
      // DRAG en el agua
      let speed = b.vel.mag();
      let dragMag = 0.1 * speed * speed;

      let drag = b.vel.copy();
      drag.mult(-1);
      drag.setMag(dragMag);
      b.applyForce(drag);

      // flotabilidad (hacia arriba)
      let buoyancy = createVector(0, -0.15 * b.mass);
      b.applyForce(buoyancy);
    }

    b.update();
    b.show();
  }
}

class Ball {
  constructor(x, y, m) {
    this.pos = createVector(x, y);
    this.vel = createVector(0, 0);
    this.acc = createVector();
    this.mass = m;
  }

  applyForce(f) {
    this.acc.add(p5.Vector.div(f, this.mass));
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
  }

  show() {
    fill(255, 120, 120);
    circle(this.pos.x, this.pos.y, this.mass * 14);
  }
}
```
``` js
let drops = [];
let glass;

function setup() {
  createCanvas(600, 400);
  glass = {
    x: width / 2 - 80,
    y: 150,
    w: 160,
    h: 200
  };

  for (let i = 0; i < 15; i++) {
    drops.push(new Drop(random(width), random(-200, 0)));
  }
}

function draw() {
  background(240);

  // vaso
  noFill();
  stroke(0);
  rect(glass.x, glass.y, glass.w, glass.h);

  // agua
  noStroke();
  fill(100, 150, 255, 120);
  rect(glass.x, glass.y + 40, glass.w, glass.h - 40);

  for (let d of drops) {
    let gravity = createVector(0, 0.3);
    d.applyForce(gravity);

    // DRAG dentro del agua
    if (
      d.pos.x > glass.x &&
      d.pos.x < glass.x + glass.w &&
      d.pos.y > glass.y + 40 &&
      d.pos.y < glass.y + glass.h
    ) {
      let speed = d.vel.mag();
      let dragMag = 0.12 * speed * speed; // drag más fuerte

      let drag = d.vel.copy();
      drag.mult(-1);
      drag.setMag(dragMag);
      d.applyForce(drag);
    }

    d.update();

    // quedarse en el fondo del vaso
    if (
      d.pos.x > glass.x &&
      d.pos.x < glass.x + glass.w &&
      d.pos.y > glass.y + glass.h - 5
    ) {
      d.pos.y = glass.y + glass.h - 5;
      d.vel.mult(0); // se detiene
    }

    d.show();
  }
}

class Drop {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = createVector(0, 0);
    this.acc = createVector();
  }

  applyForce(f) {
    this.acc.add(f);
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);

    // respawn si se pierde
    if (this.pos.y > height + 50) {
      this.pos.y = random(-100, 0);
      this.vel.mult(0);
    }
  }

  show() {
    fill(50);
    noStroke();
    circle(this.pos.x, this.pos.y, 6);
  }
}
```

#### Atracción
``` js
let sun;
let planets = [];
let G = 1.5;

function setup() {
  createCanvas(600, 400);
  sun = new Attractor(width / 2, height / 2, 40);

  for (let i = 0; i < 6; i++) {
    planets.push(new Planet(random(width), random(height)));
  }
}

function draw() {
  background(10, 10, 30);

  sun.show();

  for (let p of planets) {
    let force = sun.attract(p);
    p.applyForce(force);
    p.update();
    p.show();
  }
}

class Planet {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = createVector(0, 0);
    this.acc = createVector();
    this.mass = 2;
  }

  applyForce(f) {
    this.acc.add(p5.Vector.div(f, this.mass));
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
  }

  show() {
    fill(200, 200, 255);
    noStroke();
    circle(this.pos.x, this.pos.y, 10);
  }
}

class Attractor {
  constructor(x, y, m) {
    this.pos = createVector(x, y);
    this.mass = m;
  }

  attract(obj) {
    let force = p5.Vector.sub(this.pos, obj.pos);
    let d = constrain(force.mag(), 20, 150);
    let strength = (G * this.mass * obj.mass) / (d * d);
    force.setMag(strength);
    return force;
  }

  show() {
    fill(255, 180, 50);
    noStroke();
    circle(this.pos.x, this.pos.y, this.mass);
  }
}
```
``` js
let particles = [];
let G = 2;

function setup() {
  createCanvas(600, 400);
  for (let i = 0; i < 20; i++) {
    particles.push(new Particle());
  }
}

function draw() {
  background(0);

  // atractor visible
  fill(255, 80, 80);
  circle(mouseX, mouseY, 30);

  for (let p of particles) {
    let attractor = createVector(mouseX, mouseY);
    let force = p5.Vector.sub(attractor, p.pos);

    let d = constrain(force.mag(), 10, 200);
    let strength = G / (d * d);
    force.setMag(strength * 50);

    p.applyForce(force);
    p.update();
    p.show();
  }
}

class Particle {
  constructor() {
    this.pos = createVector(random(width), random(height));
    this.vel = createVector();
    this.acc = createVector();
  }

  applyForce(f) {
    this.acc.add(f);
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
  }

  show() {
    fill(200);
    circle(this.pos.x, this.pos.y, 6);
  }
}
```
``` js
let blackHole;
let stars = [];
let G = 3;

function setup() {
  createCanvas(600, 400);
  blackHole = createVector(width / 2, height / 2);

  for (let i = 0; i < 60; i++) {
    stars.push(new Star());
  }
}

function draw() {
  background(5, 5, 15, 40);

  // agujero negro
  fill(0);
  stroke(200);
  circle(blackHole.x, blackHole.y, 40);

  for (let s of stars) {
    let force = p5.Vector.sub(blackHole, s.pos);
    let d = constrain(force.mag(), 10, 200);

    let strength = G / (d * d);
    force.setMag(strength * 80);

    s.applyForce(force);
    s.update();
    s.show();

    // desaparecen si caen
    if (d < 20) {
      s.pos = createVector(random(width), random(height));
      s.vel.mult(0);
    }
  }
}

class Star {
  constructor() {
    this.pos = createVector(random(width), random(height));
    this.vel = p5.Vector.random2D();
    this.acc = createVector();
  }

  applyForce(f) {
    this.acc.add(f);
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
  }

  show() {
    stroke(150, 200, 255);
    point(this.pos.x, this.pos.y);
  }
}
```
### 
## Bitácora de aplicación 

### Actividad 4

Mi obra generativa cuenta la historia de un cohete que atraviesa distintas etapas de un viaje cósmico: exploración, peligro y renacimiento. En lugar de narrar la historia de forma lineal, el sistema generativo permite que emerja a partir de las fuerzas físicas que gobiernan el comportamiento de los elementos visuales.

- En la primera fase, el cohete navega por el espacio rodeado de estrellas y partículas cósmicas. Aquí predominan fuerzas suaves: una leve resistencia al movimiento y campos de repulsión entre el cohete y las partículas, que generan una sensación de flujo y exploración.

- En la segunda fase, el sistema introduce una fuerza dominante: la atracción gravitacional de un agujero negro. Esta fuerza altera radicalmente la aceleración de todos los elementos, generando órbitas, trayectorias curvas y una sensación de pérdida de control. Las partículas forman discos de acreción y el cohete intenta escapar de una fuerza imposible de evitar.

- Finalmente, en la fase de aterrizaje, la historia cambia de tono. La gravedad se invierte hacia una dirección estable y aparece resistencia de fluido al entrar en el agua. La velocidad se amortigua progresivamente, simbolizando un aterrizaje suave y un renacimiento después del caos.

La narrativa emerge directamente de las reglas físicas del sistema:

- Atracción gravitacional → peligro y colapso

- Resistencia al fluido → calma y amortiguación

- Campos de repulsión → interacción con el entorno

La interactividad se implementa permitiendo al usuario controlar la dirección del cohete con el mouse, modificando directamente las fuerzas aplicadas. Además, el usuario puede cambiar entre fases del viaje usando el teclado, alterando el conjunto de reglas físicas activas en el sistema.

#### Código

#### Sketch.js

``` js
  ellipse(0, 0, 85);
  pop();
}

function drawSky() {
  for (let i = 0; i < height; i++) {
    let inter = map(i, 0, height, 0, 1);
    let c = lerpColor(color(135, 206, 235), color(255, 255, 255), inter);
    stroke(c);
    line(0, i, width, i);
  }
}

function drawWater() {
  noStroke();
  // Back layer
  fill(0, 80, 180, 100);
  beginShape();
  vertex(0, height);
  for (let x = 0; x <= width; x += 20) {
    let y = height - 110 + sin(frameCount * 0.03 + x * 0.01) * 8;
    vertex(x, y);
  }
  vertex(width, height);
  endShape(CLOSE);

  // Front layer
  fill(0, 120, 255, 180);
  beginShape();
  vertex(0, height);
  for (let x = 0; x <= width; x += 20) {
    let y = height - 120 + sin(frameCount * 0.05 + x * 0.02) * 10;
    vertex(x, y);
  }
  vertex(width, height);
  endShape(CLOSE);
}
```
#### Controls.js
``` js
function keyPressed() {
  let k = key.toLowerCase();
  if (k === 't') initBlackHole();
  if (k === 'a') initLanding();
  if (k === 's') initSpace();
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}

function initSpace() {
  rockets = [new Rocket(createVector(width * 0.8, height / 2))];
  stars = Array.from({ length: 800 }, () => new Star());
  cosmicParticles = Array.from({ length: 150 }, () => new CosmicParticle());
  clouds = []; // Clear clouds
  biolumParticles = [];
  accretionParticles = [];
  phase = "SPACE";
}

function initBlackHole() {
  blackHole = { pos: createVector(width / 2, height / 2), mass: 8000 };
  accretionParticles = Array.from({ length: 300 }, () => new AccretionParticle());
  cosmicParticles = [];
  if (rockets.length > 0) {
    const orbitRadius = 200;
    rockets[0].pos = createVector(width / 2 + orbitRadius, height / 2);
    rockets[0].vel = createVector(0, -6.3);
  }
  phase = "BLACK_HOLE";
}

function initLanding() {
  cosmicParticles = [];
  clouds = Array.from({ length: 6 }, () => new Cloud()); // Init clouds
  if (rockets.length > 0) {
    rockets[0].pos = createVector(width / 2, -100);
    rockets[0].vel = createVector(0, 2);
  }
  phase = "LANDING";
}
```

####  Objects.js
``` js
class Rocket {
  constructor(pos) {
    this.pos = pos;
    this.vel = createVector(0, 0);
    this.acc = createVector(0, 0);
  }
  applyForce(f) { this.acc.add(f); }
  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
  }
  display() {
    push();
    translate(this.pos.x, this.pos.y);
    rotate(this.vel.heading() + PI / 2);
    if (frameCount % 2 === 0) {
      noStroke();
      fill(255, 100, 0, 200);
      triangle(-5, 20, 5, 20, 0, 35 + random(10));
      fill(255, 200, 0, 150);
      triangle(-3, 20, 3, 20, 0, 28 + random(5));
    }
    stroke(200);
    strokeWeight(1.5);
    fill(240);
    rectMode(CENTER);
    rect(0, 0, 12, 30, 5, 5, 2, 2);
    fill(200, 0, 0);
    triangle(-6, -15, 6, -15, 0, -25);
    fill(150);
    triangle(-6, 5, -12, 15, -6, 15);
    triangle(6, 5, 12, 15, 6, 15);
    fill(100, 200, 255);
    ellipse(0, -5, 6);
    pop();
  }
}

class Star {
  constructor() {
    this.pos = createVector(random(width), random(height));
    this.depth = random(0.1, 1);
    this.size = random(1, 3);
    this.twinkle = random(TWO_PI);
  }
  update(rocket) {
    this.pos.x -= 0.5 * this.depth;
    if (rocket) {
      let d = dist(this.pos.x, this.pos.y, rocket.pos.x, rocket.pos.y);
      if (d < 150) {
        let away = p5.Vector.sub(this.pos, rocket.pos);
        away.setMag(0.8);
        this.pos.add(away);
      }
    }
    if (this.pos.x < 0) this.pos.x = width;
    if (this.pos.y < 0) this.pos.y = height;
    if (this.pos.y > height) this.pos.y = 0;
  }
  display() {
    let alpha = 150 + sin(frameCount * 0.05 + this.twinkle) * 100;
    fill(255, alpha);
    noStroke();
    ellipse(this.pos.x, this.pos.y, this.size * this.depth);
  }
}

class CosmicParticle {
  constructor() {
    this.pos = createVector(random(width), random(height));
    this.vel = createVector(random(-0.5, 0.5), random(-0.5, 0.5));
    const colors = [
      color(0, 255, 255, 150), color(255, 0, 255, 150),
      color(0, 255, 100, 150), color(100, 100, 255, 150),
      color(255, 200, 0, 150)
    ];
    this.color = random(colors);
    this.size = random(2, 5);
    this.twinkle = random(TWO_PI);
  }
  update(rocket) {
    this.pos.add(this.vel);
    this.pos.x -= 0.2;
    if (rocket) {
      let d = dist(this.pos.x, this.pos.y, rocket.pos.x, rocket.pos.y);
      if (d < 200) {
        let away = p5.Vector.sub(this.pos, rocket.pos);
        away.setMag(0.3);
        this.pos.add(away);
      }
    }
    if (this.pos.x < 0) this.pos.x = width;
    if (this.pos.x > width) this.pos.x = 0;
    if (this.pos.y < 0) this.pos.y = height;
    if (this.pos.y > height) this.pos.y = 0;
  }
  display() {
    let alpha = 100 + sin(frameCount * 0.03 + this.twinkle) * 50;
    noStroke();
    fill(red(this.color), green(this.color), blue(this.color), alpha);
    ellipse(this.pos.x, this.pos.y, this.size);
    fill(red(this.color), green(this.color), blue(this.color), alpha * 0.3);
    ellipse(this.pos.x, this.pos.y, this.size * 2);
  }
}

class BiolumParticle {
  constructor(pos) {
    this.pos = pos.copy();
    this.vel = createVector(random(1, 3), random(-1, 1));
    this.acc = createVector();
    this.life = 255;
  }
  applyForce(f) { this.acc.add(f); }
  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
    this.life -= 4;
  }
  display() {
    noStroke();
    fill(0, 255, 255, this.life);
    ellipse(this.pos.x, this.pos.y, 3);
  }
}

class AccretionParticle {
  constructor() {
    let angle = random(TWO_PI);
    let r = random(150, 400);
    this.pos = createVector(width / 2 + cos(angle) * r, height / 2 + sin(angle) * r);
    this.vel = createVector(-sin(angle), cos(angle)).mult(random(2, 5));
    this.acc = createVector();
    this.life = 255;
    this.isDead = false;
  }
  applyForce(f) { this.acc.add(f); }
  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
    let d = dist(this.pos.x, this.pos.y, width / 2, height / 2);
    if (d < 50) this.isDead = true;
    this.life -= 0.5;
    if (this.life < 0) this.isDead = true;
  }
  display() {
    noStroke();
    let c = lerpColor(color(255, 100, 0), color(150, 0, 255), map(this.life, 0, 255, 1, 0));
    fill(red(c), green(c), blue(c), 150);
    ellipse(this.pos.x, this.pos.y, 2);
  }
}

class Cloud {
  constructor() {
    this.pos = createVector(random(width), random(height * 0.5));
    this.size = random(40, 100);
    this.speed = random(0.2, 0.8);
  }

  update() {
    this.pos.x += this.speed;
    if (this.pos.x > width + this.size) {
      this.pos.x = -this.size;
      this.pos.y = random(height * 0.5);
    }
  }

  display() {
    noStroke();
    fill(255, 230);
    ellipse(this.pos.x, this.pos.y, this.size, this.size * 0.6);
    ellipse(this.pos.x + this.size * 0.3, this.pos.y + this.size * 0.1, this.size * 0.8, this.size * 0.5);
    ellipse(this.pos.x - this.size * 0.3, this.pos.y + this.size * 0.1, this.size * 0.8, this.size * 0.5);
  }
}
```

#### Physics.js
``` js
function getAttraction(a, b, mass) {
  let force = p5.Vector.sub(a, b);
  let d = constrain(force.mag(), 50, 400);
  force.normalize();
  force.mult(mass / (d * d));
  return force;
}
```
#### Link del proyecto
- https://editor.p5js.org/Jakeline-Avila/sketches/N4rpZ-AGF

#### Capturas de pantalla

<img width="1068" height="803" alt="image" src="https://github.com/user-attachments/assets/0d75fd1f-1e40-4d50-921d-20f38578f328" />
<img width="1106" height="961" alt="image" src="https://github.com/user-attachments/assets/777e6bdb-20bc-435f-9548-a22a61f2932e" />
<img width="1049" height="982" alt="image" src="https://github.com/user-attachments/assets/1a5cdfee-2a53-49c3-ab8a-4604844893ed" />





## Bitácora de reflexión

