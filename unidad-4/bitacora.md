# Unidad 4

## Bitácora de proceso de aprendizaje

### Actividad 1

Lo que más me llamó la atención de la obra de Memo Akten es la forma en que utiliza la tecnología y el movimiento para crear arte visual basado en principios científicos. En la serie Simple Harmonic Motion, el artista transforma conceptos de la física, como el movimiento armónico, en una experiencia visual dinámica y estética.

Me pareció interesante cómo patrones simples de movimiento pueden generar formas complejas y atractivas. Esto demuestra que las matemáticas y la física no solo sirven para explicar fenómenos naturales, sino que también pueden utilizarse como herramientas creativas en el arte digital.

Otro aspecto que me llamó la atención es la relación entre ciencia, arte y programación. La obra muestra cómo los algoritmos y las simulaciones pueden convertirse en medios de expresión artística, lo que abre nuevas posibilidades para explorar la creatividad mediante la tecnología.

En general, esta obra me hizo pensar en cómo los conceptos científicos pueden inspirar procesos creativos y en cómo el arte digital puede ayudarnos a visualizar fenómenos que normalmente solo entendemos de forma teórica.

### Actividad 2

1. Simulación sobre manejo de ángulos

¿Qué está pasando en la simulación? ¿Cuál es la interacción?
En la simulación se observa un objeto que rota alrededor del centro de la pantalla. La interacción consiste en que el sistema calcula un ángulo de rotación y, a partir de ese valor, los elementos gráficos giran. Esto permite visualizar cómo funciona la rotación en un sistema de coordenadas dentro de una animación.

¿Por qué se traslada el origen del sistema de coordenadas al centro de la pantalla?
Se hace para facilitar la rotación de los objetos. Si el origen está en el centro, los elementos pueden rotar alrededor de ese punto de manera más natural y simétrica. Si el origen estuviera en una esquina, la rotación sería más difícil de controlar y los cálculos serían más complejos.

¿Cuál es la relación entre el sistema de coordenadas y la función rotate()?
La función rotate() rota el sistema de coordenadas completo. Esto significa que todos los elementos que se dibujen después se orientarán según ese nuevo ángulo de rotación.

¿Por qué los elementos parecen dibujarse en (0,0)?
Los elementos se dibujan cerca del origen porque el sistema de coordenadas fue trasladado previamente al centro de la pantalla. De esta forma, dibujar cerca del punto (0,0) permite que el objeto gire alrededor de ese punto central.

¿Por qué los elementos rotan si en cada frame se dibuja lo mismo?
Porque antes de dibujar los elementos se aplica una transformación de rotación al sistema de coordenadas. Aunque el código que dibuja las figuras sea el mismo en cada frame, el sistema de coordenadas ya está rotado, lo que hace que los objetos aparezcan girando.

2. Simulación sobre orientación según el movimiento

¿Qué ocurre en el marco Motion 101?
En el marco Motion 101 se muestra cómo un objeto se mueve en la pantalla usando vectores de posición y velocidad. El objeto no solo se mueve, sino que también cambia su orientación para apuntar en la dirección en la que se está desplazando.

¿Qué hace la función heading()?
La función heading() obtiene el ángulo del vector de velocidad. Este ángulo indica la dirección hacia la que se mueve el objeto.

¿Qué hacen push() y pop()?
Estas funciones guardan y restauran el estado del sistema de transformaciones.

push() guarda la configuración actual del sistema de coordenadas.

pop() restaura esa configuración después de aplicar transformaciones como translate() o rotate().

Esto permite que las transformaciones solo afecten al objeto actual y no a los demás elementos que se dibujen después.

¿Qué hace rectMode(CENTER)?
Esta función cambia la forma en que se dibujan los rectángulos. Con CENTER, el rectángulo se dibuja desde su centro en lugar de desde la esquina superior izquierda. Esto facilita la rotación del objeto alrededor de su propio centro.

Relación entre el ángulo de rotación y el vector de velocidad
El vector de velocidad indica la dirección del movimiento del objeto. La función heading() convierte esa dirección en un ángulo. Luego, ese ángulo se usa en rotate(angle) para orientar el objeto en la misma dirección en la que se está moviendo.

Primero se traslada el sistema de coordenadas a la posición del objeto (translate). Después se aplica la rotación (rotate) basada en el ángulo del vector de velocidad. Finalmente se dibuja el objeto centrado en ese punto.


### Actividad 3

Práctica de movimiento y rotación

En esta actividad desarrollé una simulación de un vehículo que puede moverse por la pantalla usando las teclas de flecha. El objetivo era aplicar los conceptos de vectores, rotación y traslación para que el vehículo no solo se moviera, sino que también apuntara en la dirección de su movimiento.

Proceso de creación

Primero definí las variables principales del vehículo: posición, velocidad y aceleración. Estas variables permiten controlar el movimiento del objeto en la pantalla. La posición indica dónde está el vehículo, la velocidad indica hacia dónde se está moviendo y la aceleración se usa para modificar la velocidad cuando se presionan las teclas.

Después programé la interacción con el teclado. Utilicé las flechas izquierda y derecha para aplicar aceleración al vehículo en esas direcciones. Cada vez que se presiona una tecla, se modifica la aceleración y esta se suma a la velocidad para producir el movimiento.

Luego implementé la rotación del vehículo. Para lograr que el triángulo apuntara en la dirección del movimiento, utilicé el ángulo del vector de velocidad. Este ángulo se usa con la función de rotación para orientar el vehículo correctamente.

También utilicé las funciones de transformación del sistema de coordenadas. Primero trasladé el sistema de coordenadas a la posición del vehículo y luego apliqué la rotación. Después dibujé el triángulo centrado en ese punto para que girara correctamente.

Resultados y aprendizaje

Al final logré que el vehículo se moviera por la pantalla y que el triángulo siempre apuntara hacia la dirección en la que se desplaza. Esto me ayudó a entender mejor cómo funcionan los vectores de movimiento y cómo las transformaciones como translate y rotate afectan el dibujo de los objetos.

Esta actividad también me permitió comprender la importancia de organizar bien las transformaciones para controlar correctamente la posición y la orientación de los elementos en una simulación.

### Actividad 4

Relación con el marco Motion 101

En esta actividad analicé la simulación Motion 101 con fuerzas para entender cómo se integran los conceptos de movimiento con la aplicación de fuerzas.

Identificación de Motion 101

El marco Motion 101 describe el modelo básico de movimiento utilizando tres variables principales: posición, velocidad y aceleración. En cada frame de la simulación, la aceleración se suma a la velocidad y la velocidad se suma a la posición para actualizar el movimiento del objeto.

Modificación al agregar fuerzas acumulativas

Cuando se agregan fuerzas acumulativas al modelo Motion 101 es necesario modificar la forma en que se maneja la aceleración. En lugar de asignar directamente un valor a la aceleración, las fuerzas se acumulan en la aceleración durante cada frame.

Después de actualizar la velocidad, la aceleración debe reiniciarse a cero. Esto se hace porque las fuerzas solo deben aplicarse durante el frame actual. Si no se reinicia, las fuerzas se seguirían acumulando continuamente y el movimiento no sería correcto.

Identificación del Attractor

En la simulación aparece un objeto llamado Attractor, que representa un punto que ejerce una fuerza de atracción sobre el vehículo o partícula. Este objeto generalmente está ubicado en el centro o en una posición fija de la pantalla.

Para cambiar su color se puede modificar la función que lo dibuja, cambiando el valor de fill() dentro de su método display().

Ejemplo:
``` js

fill(255, 0, 0); // rojo
ellipse(this.position.x, this.position.y, this.mass*2);

```
Uso de los atributos dragging y rollover

El Attractor tiene dos atributos importantes:

dragging: indica si el objeto está siendo arrastrado con el mouse.

rollover: indica si el mouse está pasando sobre el objeto.

Aunque estos atributos existen, en la simulación no se están modificando. Para activarlos se pueden usar funciones de interacción con el mouse de p5.js como:

mousePressed()

mouseReleased()

mouseDragged()

mouseMoved()

Por ejemplo:

Detectar cuando el mouse está sobre el attractor:

``` js
let d = dist(mouseX, mouseY, this.position.x, this.position.y);
if (d < this.mass) {
  this.rollover = true;
} else {
  this.rollover = false;
}

Permitir arrastrar el attractor:

function mousePressed() {
  if (attractor.rollover) {
    attractor.dragging = true;
  }
}

function mouseReleased() {
  attractor.dragging = false;
}

function mouseDragged() {
  if (attractor.dragging) {
    attractor.position.x = mouseX;
    attractor.position.y = mouseY;
  }
}
```

Con estas modificaciones, el attractor podría cambiar de color cuando el cursor pase sobre él y también moverse por la pantalla al arrastrarlo con el mouse.

Reflexión

Esta actividad me ayudó a comprender mejor cómo integrar fuerzas en el modelo Motion 101 y cómo las simulaciones pueden volverse interactivas utilizando eventos del mouse. También entendí cómo organizar el código para que los objetos tengan comportamientos más dinámicos dentro de la simulación.

### Actividad 5

1. Relación entre r, θ con x y y

En coordenadas polares:

r es la distancia desde el origen.

θ (theta) es el ángulo.

Para convertir a coordenadas cartesianas se usan las fórmulas:

x = r · cos(θ)

y = r · sin(θ)

Esto permite ubicar un punto en el plano usando distancia y dirección. En el código, al aumentar theta, el punto se mueve en una trayectoria circular alrededor del centro.

2. Primera modificación
let v = p5.Vector.fromAngle(theta);

¿Qué ocurre?
El círculo aparece muy cerca del centro y no mantiene la misma distancia del origen.

¿Por qué?
Porque p5.Vector.fromAngle(theta) crea un vector unitario, es decir, con magnitud 1.
Por lo tanto solo usa el ángulo y no la distancia r, por eso el punto queda muy cerca del origen.

3. Segunda modificación
let v = p5.Vector.fromAngle(theta, r);

¿Qué ocurre?
El círculo vuelve a moverse alrededor del centro formando un círculo.

¿Por qué?
Porque ahora el vector usa:

theta como dirección

r como magnitud

Esto produce el mismo resultado que calcular manualmente:

x = r · cos(θ)

y = r · sin(θ)

### Actividad 6

La función sinusoide describe un movimiento oscilatorio o repetitivo, como el de las ondas o vibraciones.

y = A\sin(\omega t + \phi)

En la simulación se observan tres parámetros importantes:

Amplitud: controla qué tan lejos se mueve el punto desde el centro.

Periodo / frecuencia: determina qué tan rápido se repite la onda.

Fase: desplaza la onda horizontalmente.

Al presionar una tecla se modifica la fase, lo que hace que una de las ondas se desplace respecto a la otra. Esto demuestra que dos ondas pueden tener la misma amplitud y velocidad, pero estar desfasadas.

Conclusión: cambiar los parámetros de una función sinusoide permite controlar el comportamiento de un movimiento periódico.

### Actividad 7
En esta actividad modifiqué la simulación de osciladores aplicando conceptos de unidades anteriores.

Primero se utiliza el concepto de aleatoriedad al asignar diferentes amplitudes y velocidades angulares a cada oscilador. Esto hace que cada uno tenga un movimiento distinto, generando un comportamiento más orgánico y variado.

Luego se puede incorporar el concepto de fuerza haciendo que una fuerza afecte la velocidad angular de los osciladores. Esto cambia gradualmente su movimiento, simulando cómo una fuerza externa puede modificar la trayectoria o velocidad de un objeto.

Durante el proceso observé que pequeños cambios en la velocidad o en la amplitud producen movimientos muy diferentes en los osciladores.

Conclusión: combinar aleatoriedad y fuerzas permite crear simulaciones más dinámicas y realistas dentro del sistema de osciladores.

### Actividad 8

En esta actividad trabajé con una simulación de una onda generada con la función seno. El código calcula la posición vertical de varios puntos usando la función sin() para formar la forma de la onda.

Para que la onda se moviera como una ola, fue necesario actualizar el ángulo en cada frame dentro de draw(). Esto hace que el valor del seno cambie continuamente y los puntos se desplacen, generando la sensación de movimiento.

La posición vertical de cada círculo se calcula con:

𝑦
=
𝐴
⋅
sin
⁡
(
𝜃
)
y=A⋅sin(θ)

donde A es la amplitud y θ el ángulo.

Al modificar el ángulo con el tiempo, la onda comienza a desplazarse horizontalmente, simulando el movimiento de una ola.

Conclusión: al cambiar el ángulo constantemente se crea una animación de onda que imita el comportamiento de una ola en movimiento. 

### Actividad 9

En esta actividad modifiqué la simulación original para crear un sistema de dos resortes conectados en serie. Para lograrlo agregué un segundo objeto bob y un segundo resorte.

El primer resorte sigue conectado al punto fijo (anchor) y al primer bob. Luego el segundo resorte usa la posición del primer bob como nuevo punto de anclaje y se conecta al segundo bob. De esta forma el movimiento del segundo objeto depende del primero.

Cada resorte aplica una fuerza según la ley de Hooke:

𝐹
=
−
𝑘
𝑥
F=−kx

Esto significa que la fuerza del resorte depende de cuánto se estira o comprime respecto a su longitud de reposo.

Durante la simulación también actúa la gravedad, que tira de los objetos hacia abajo, mientras que los resortes intentan devolverlos a su posición de equilibrio. Esto produce un movimiento de oscilación más complejo, porque ambos cuerpos influyen entre sí.

Conclusión: al conectar dos resortes en serie el sistema se vuelve más dinámico, ya que el segundo objeto responde tanto a la gravedad como al movimiento del primer resorte.

### Actividad 10

En esta actividad modifiqué la simulación para crear un sistema de dos péndulos conectados en serie. Para hacerlo fue necesario agregar un segundo péndulo cuyo punto de pivote depende de la posición del primero.

El primer péndulo funciona igual que en el código original, con un punto fijo en la parte superior. Luego el segundo péndulo usa la posición del bob del primer péndulo como su pivote, por lo que su movimiento depende directamente del movimiento del primero.

El movimiento de cada péndulo se calcula usando la relación entre gravedad, longitud del brazo y el ángulo del péndulo. La aceleración angular se basa en la siguiente expresión:

\alpha = -\frac{g}{r}\sin(\theta)

Esto hace que el péndulo oscile alrededor de su punto de equilibrio.

Al conectar dos péndulos, el movimiento se vuelve más complejo porque el segundo responde tanto a la gravedad como al movimiento generado por el primero.

Conclusión: el sistema de péndulos en serie produce un movimiento más dinámico e impredecible, mostrando cómo los sistemas conectados pueden generar comportamientos más complejos.

## Bitácora de aplicación 
### Actividad 11

Mi obra generativa parte de la idea de un ecosistema que crece y se transforma con la interacción del usuario. Uso una narrativa inspirada en el ciclo natural de crecimiento, floración y dispersión, pero no como una historia, sino como una forma de definir las reglas del sistema.

Reglas que aplica:
- Gravedad
- Resistencia al aire
- Atraccion al mouse
- Levy flight para naturalidad
- Colores aleatorios
- Distribución gaussiana, se usa bastante sin y cos

Las enredaderas representan el crecimiento del ecosistema, las flores marcan momentos de transformación y su explosión genera pétalos que dejan rastros de pintura en el espacio. El usuario interviene creando nuevas enredaderas o activando estas explosiones, lo que hace que el entorno cambie constantemente.

De esta manera, la narrativa funciona como una guía para las reglas del sistema generativo, permitiendo que la obra evolucione y produzca composiciones diferentes en cada interacción.

 Config.js 
``` js
const SEASONS = {
  1: { name:'🌸 Primavera', bg:[245,238,228], vine:[60,100,45],  ink:[[220,80,120],[180,60,200],[255,160,180],[100,180,80],[255,200,80]] },
  2: { name:'🍂 Otoño',    bg:[235,220,200], vine:[80,55,20],   ink:[[200,80,20],[180,40,10],[230,160,30],[150,50,10],[255,120,40]] },
  3: { name:'❄️ Invierno', bg:[220,230,245], vine:[40,60,90],   ink:[[80,130,220],[150,190,255],[200,220,255],[60,100,180],[180,200,240]] },
  4: { name:'🌻 Verano',   bg:[240,245,210], vine:[40,110,30],  ink:[[240,200,20],[255,140,0],[200,230,50],[255,80,60],[180,240,100]] }
};
```
Flower.js
``` js
class VineFlower {
  constructor(x, y, col) {
    this.x        = x;  this.y = y;
    this.col      = col;
    this.size     = random(11, 24);
    this.bloom    = 0;
    this.exploded = false;
    this.phase    = random(TWO_PI);
    this.age      = 0;
    this.swayX    = 0;  this.swayY = 0;
    this.petalN   = floor(random(5, 9));
  }

  update(pos) {
    if (pos && !this.exploded) { this.x = pos.x; this.y = pos.y; }
    this.age++;
    if (this.bloom < 1) this.bloom = min(1, this.bloom + 0.022);
    this.swayX = sin(this.age * 0.055 + this.phase) * 3.5;
    this.swayY = cos(this.age * 0.038 + this.phase) * 2.2;
  }

  triggerExplode() {
    if (this.exploded) return;
    this.exploded = true;
    let px = this.x + this.swayX;
    let py = this.y + this.swayY;
    paintSplash(px, py, this.col, this.size);
    
    let n = floor(random(35, 65));
    for (let i = 0; i < n; i++) petals.push(new PaintPetal(px, py, this.col));
    for (let i = 0; i < 12; i++) {
      let levyCol = random(season.ink);
      petals.push(new PaintPetal(px, py, levyCol, true));
    }
  }

  draw() {
    if (this.exploded) return;
    let px = this.x + this.swayX;
    let py = this.y + this.swayY;
    let c  = this.col;
    let b  = this.bloom;

    let glowAlpha = sin(this.age * 0.08) * 30 + 30;
    noStroke();
    fill(c[0], c[1], c[2], glowAlpha);
    circle(px, py, this.size * 3.5 * b);

    for (let i = 0; i < this.petalN; i++) {
      let a = (TWO_PI / this.petalN) * i + this.swayX * 0.05;
      let d = this.size * b;
      push();
      translate(px + cos(a)*d*0.55, py + sin(a)*d*0.55);
      rotate(a);
      fill(c[0], c[1], c[2], 210 * b);
      noStroke();
      ellipse(0, 0, d, d * 0.42);
      pop();
    }
    fill(255, 238, 80, 230 * b);
    noStroke();
    circle(px, py, this.size * 0.48 * b);
    if (b > 0.95) {
      fill(255, 255, 255, 120 + sin(this.age * 0.12) * 80);
      textSize(10);
      textAlign(CENTER, CENTER);
      text('✦', px, py - this.size * 1.4);
    }
  }
}
```
Petal.js
``` js
class PaintPetal {
  constructor(x, y, col, levy = false) {
    this.pos = createVector(x, y);
    let spd = levy ? (random() < 0.12 ? random(11, 24) : random(2, 6)) : random(3, 9);
    let ang  = random(TWO_PI);
    this.vel = createVector(cos(ang)*spd, sin(ang)*spd - random(1, 4));
    this.acc = createVector(0, 0);
    this.col     = col;
    this.size    = random(3, 13);
    this.alpha   = random(185, 255);
    this.alive   = true;
    this.angle   = random(TWO_PI);
    this.angVel  = random(-0.18, 0.18);
    this.mass    = this.size * 0.11;
    this.painted = false;
  }

  applyForce(f) {
    this.acc.add(p5.Vector.div(f, this.mass));
  }

  update() {
    let spd = this.vel.mag();
    this.applyForce(this.vel.copy().normalize().mult(-0.02 * spd * spd));
    this.applyForce(createVector(0, 0.085 * this.mass));
    let wAng = noise(this.pos.x * 0.004, this.pos.y * 0.004, noiseOff) * TWO_PI * 2;
    this.applyForce(createVector(cos(wAng)*0.045, sin(wAng)*0.022));
    
    let mouse = createVector(mouseX, mouseY);
    let dir = p5.Vector.sub(mouse, this.pos);
    let d = dir.mag();
    if (d < 190 && d > 4) {
      dir.normalize().mult(map(d, 4, 190, 0.75, 0.008));
      this.applyForce(dir);
    }
    
    this.angle += this.angVel;
    this.vel.add(this.acc);
    this.vel.limit(13);
    this.pos.add(this.vel);
    this.acc.mult(0);
    this.alpha -= 1.6;

    if ((this.alpha <= 0 || this.pos.y > height + 15) && !this.painted) {
      this.painted = true;
      if (this.pos.x > -10 && this.pos.x < width+10 && this.pos.y > -10 && this.pos.y < height+10) {
        paintLayer.noStroke();
        paintLayer.fill(this.col[0], this.col[1], this.col[2], random(70, 150));
        paintLayer.push();
        paintLayer.translate(this.pos.x, this.pos.y);
        paintLayer.rotate(this.angle);
        paintLayer.ellipse(0, 0, this.size * random(1, 2.8), this.size * 0.38);
        paintLayer.pop();
      }
      this.alive = false;
    }
  }

  draw() {
    push();
    translate(this.pos.x, this.pos.y);
    rotate(this.angle);
    noStroke();
    fill(this.col[0], this.col[1], this.col[2], this.alpha);
    ellipse(0, 0, this.size, this.size * 0.38);
    pop();
  }
}
```
vine.js
``` js
class Vine {
  constructor(x, y, angle) {
    this.pos      = createVector(x, y);
    this.vel      = createVector(cos(angle), sin(angle)).mult(random(1.2, 2.0));
    this.acc      = createVector(0, 0);
    this.age      = 0;
    this.maxAge   = random(220, 420);
    this.alive    = true;
    this.dead     = false;
    this.noiseT   = random(1000);
    this.thick    = random(1.4, 3.2);
    this.history  = [this.pos.copy()];
    this.branched = false;
    this.flower   = null;
    this.phase    = random(TWO_PI);
    this.col      = season.vine;
    this.segLen   = random(2.5, 4.2);
  }

  applyForce(f) {
    this.acc.add(p5.Vector.div(f, 0.8));
  }

  update() {
    if (this.dead) { 
      if (this.flower) this.flower.update(null); 
      return; 
    }
    if (!this.alive) { this.dead = true; return; }

    this.age++;

    if (this.flower && this.age < 100) {
        let desired = createVector(this.flower.x - this.pos.x, this.flower.y - this.pos.y);
        desired.normalize().mult(0.1);
        this.applyForce(desired);
    }

    let angle = noise(this.pos.x * 0.006, this.pos.y * 0.006, noiseOff) * TWO_PI * 2.4;
    let steer = createVector(cos(angle), sin(angle)).mult(0.035);
    this.applyForce(steer);
    this.applyForce(this.vel.copy().mult(-0.016));

    let sway = sin(this.age * 0.065 + this.phase) * 0.012;
    let lat  = createVector(-this.vel.y, this.vel.x).normalize().mult(sway);
    this.applyForce(lat);

    this.vel.add(this.acc);
    this.vel.limit(2.5);
    this.pos.add(this.vel.copy().normalize().mult(this.segLen));
    this.acc.mult(0);
    this.history.push(this.pos.copy());

    if (!this.branched && this.age > 70 && random() < 0.007) {
      this.branched = true;
      let bAng = this.vel.heading() + random(-0.85, 0.85);
      if (vines.length < 32) vines.push(new Vine(this.pos.x, this.pos.y, bAng));
    }

    if (!this.flower && this.age > this.maxAge * 0.65) {
      this.flower = new VineFlower(this.pos.x, this.pos.y, random(season.ink));
    }
    
    if (this.flower) this.flower.update(null);

    if (this.age > this.maxAge || this.pos.x < -50 || this.pos.x > width + 50 || this.pos.y < -50 || this.pos.y > height + 50) {
      this.alive = false;
    }
  }

  explodeFlower() {
    if (this.flower && !this.flower.exploded) {
      this.flower.triggerExplode();
    }
  }

  draw() {
    if (this.history.length < 2) return;
    let vc = this.col;
    let thk = this.thick * (1 + sin(this.age * 0.05 + this.phase) * 0.25);
    let alpha = (this.alive || this.dead) ? 190 : 90;
    
    strokeWeight(thk);
    stroke(vc[0], vc[1], vc[2], alpha);
    noFill();
    beginShape();
    for (let pt of this.history) curveVertex(pt.x, pt.y);
    endShape();

    if (this.history.length > 8) {
      let step = 22;
      for (let i = step; i < this.history.length; i += step) {
        let curr = this.history[i];
        let prev = this.history[i - 4];
        if (!prev) continue;
        let lAng = atan2(curr.y - prev.y, curr.x - prev.x);
        let side = (floor(i / step)) % 2 === 0 ? 1 : -1;
        push();
        translate(curr.x, curr.y);
        rotate(lAng + side * PI * 0.45);
        fill(vc[0]+15, vc[1]+35, vc[2]+10, 150);
        noStroke();
        ellipse(0, -thk*2.5, thk*2.5, thk*5);
        pop();
      }
    }
    if (this.flower) this.flower.draw();
  }
}
```
Sketch.js
``` js
let S = 1, season;
let paintLayer;
let vines = [], petals = [];
let noiseOff = 0;

function setup() {
  createCanvas(820, 580);
  colorMode(RGB, 255, 255, 255, 255);
  season = SEASONS[1];
  paintLayer = createGraphics(width, height);
  paintLayer.colorMode(RGB, 255, 255, 255, 255);
  clearPaintLayer();
  spawnInitialVines();
}

function draw() {
  noiseOff += 0.0025;
  background(season.bg[0], season.bg[1], season.bg[2]);
  
  // Textura papel
  for (let i = 0; i < 40; i++) {
    let px = random(width), py = random(height);
    let n  = noise(px*0.01, py*0.01, noiseOff*0.08);
    stroke(0, 0, 0, n * 6);
    strokeWeight(0.4);
    point(px, py);
  }

  image(paintLayer, 0, 0);

  for (let v of vines) { v.update(); v.draw(); }
  petals = petals.filter(pt => pt.alive);
  for (let pt of petals) { pt.update(); pt.draw(); }

  if (frameCount % 240 === 0) {
    vines = vines.filter(v => !(v.dead && (!v.flower || v.flower.exploded)));
  }

  if (frameCount % 300 === 0 && vines.length < 15) spawnVineFromBorder();

  noStroke();
  fill(0, 0, 0, 40);
  textSize(10);
  textAlign(RIGHT);
  text(`CLICK para flores · ESPACIO para explotar`, width - 15, height - 15);
}

// --- UTILIDADES ---
function clearPaintLayer() {
  paintLayer.clear();
  paintLayer.background(season.bg[0], season.bg[1], season.bg[2]);
}

function spawnInitialVines() {
  vines = [];
  let edges = [
    ...Array.from({length:4}, () => ({ x: random(width),  y: 0,      angle: random(PI*0.25, PI*0.75) })),
    ...Array.from({length:4}, () => ({ x: random(width),  y: height, angle: random(-PI*0.75, -PI*0.25) })),
    ...Array.from({length:3}, () => ({ x: 0, y: random(height), angle: random(-PI*0.3, PI*0.3) })),
    ...Array.from({length:3}, () => ({ x: width, y: random(height), angle: random(PI*0.7, PI*1.3) })),
  ];
  for (let e of edges) vines.push(new Vine(e.x, e.y, e.angle));
}

function spawnVineFromBorder() {
  let side = floor(random(4));
  let x, y, ang;
  if (side === 0) { x = random(width); y = 0; ang = random(PI*0.2, PI*0.8); }
  else if (side === 1) { x = random(width); y = height; ang = random(-PI*0.8, -PI*0.2); }
  else if (side === 2) { x = 0; y = random(height); ang = random(-PI*0.3, PI*0.3); }
  else { x = width; y = random(height); ang = random(PI*0.7, PI*1.3); }
  vines.push(new Vine(x, y, ang));
}

function spawnVineAtClick(tx, ty) {
  let dLeft = tx, dRight = width - tx, dTop = ty, dBottom = height - ty;
  let minDist = min(dLeft, dRight, dTop, dBottom);
  let startX, startY;
  if (minDist === dLeft) { startX = 0; startY = ty; }
  else if (minDist === dRight) { startX = width; startY = ty; }
  else if (minDist === dTop) { startX = tx; startY = 0; }
  else { startX = tx; startY = height; }

  let angle = atan2(ty - startY, tx - startX);
  let v = new Vine(startX, startY, angle);
  v.flower = new VineFlower(tx, ty, random(season.ink));
  vines.push(v);
}

function paintSplash(x, y, col, size) {
  paintLayer.push();
  paintLayer.noStroke();
  for (let i = 0; i < 8; i++) {
    let r = size * random(1.8, 4.5);
    paintLayer.fill(col[0], col[1], col[2], random(35, 120));
    paintLayer.ellipse(x+randomGaussian(0, size), y+randomGaussian(0, size), r, r*0.8);
  }
  paintLayer.pop();
}

function mousePressed() {
  let closest = null, minD = 35;
  for (let v of vines) {
    if (v.flower && !v.flower.exploded) {
      let d = dist(mouseX, mouseY, v.flower.x + v.flower.swayX, v.flower.y + v.flower.swayY);
      if (d < minD) { minD = d; closest = v; }
    }
  }
  if (closest) closest.explodeFlower();
  else spawnVineAtClick(mouseX, mouseY);
}

function keyPressed() {
  if (['1','2','3','4'].includes(key)) changeSeason(parseInt(key));
  if (key === ' ') vines.forEach(v => v.explodeFlower());
  if (key.toLowerCase() === 'c') clearPaintLayer();
}

function changeSeason(n) {
  season = SEASONS[n];
  clearPaintLayer();
  vines = []; petals = [];
  spawnInitialVines();
}
```

Link de la experiencia: https://editor.p5js.org/Jakeline-Avila/sketches/GjlVuuKUf
<img width="1108" height="896" alt="image" src="https://github.com/user-attachments/assets/33aed0fc-c6a5-4ada-81c6-208e749449ca" />
<img width="1108" height="890" alt="image" src="https://github.com/user-attachments/assets/fcd53aac-01f2-4cb5-91d4-3d47186c1c06" />
<img width="1108" height="893" alt="image" src="https://github.com/user-attachments/assets/a40fbbd7-2020-49f9-bbe2-348329054d3d" />
<img width="1110" height="885" alt="image" src="https://github.com/user-attachments/assets/c568d300-9725-4dec-a2bc-ce4bb772174c" />






## Bitácora de reflexión





