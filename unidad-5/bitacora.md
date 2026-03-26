# Unidad 5
## Bitácora de proceso de aprendizaje
### Actividad 1

Capa de comportamiento

Cada partícula tiene propiedades que se dividen en estado físico y estado vital. El estado físico está compuesto por la posición, la velocidad y la aceleración, ya que estas determinan cómo se mueve la partícula en el espacio. El estado vital está representado por el lifespan, que define cuánto tiempo permanece activa. Una partícula “muere” cuando su lifespan llega a cero o es menor, y esta muerte es gradual, ya que el valor disminuye poco a poco en cada frame, generando un efecto de desvanecimiento. En cada actualización se aplica el patrón Motion 101: la velocidad se modifica con la aceleración, la posición se actualiza con la velocidad y finalmente se reduce el lifespan, integrando así movimiento y ciclo de vida en un mismo sistema.

Capa de estructura

Las partículas son creadas por el sistema, generalmente dentro del draw, lo que permite una emisión continua en el tiempo. El mismo sistema es quien decide cuándo eliminarlas, verificando si están “muertas” mediante una condición como isDead(). El array se recorre en orden inverso al momento de eliminar partículas para evitar errores de índice; si se recorriera de forma normal (de inicio a fin), al eliminar un elemento los índices cambiarían y se podrían saltar partículas o generar comportamientos inesperados. Si no se eliminaran nunca las partículas, el sistema acumularía cada vez más objetos en memoria, lo que provocaría una caída progresiva del rendimiento y del frame rate, pudiendo incluso llegar a congelar la ejecución.

Capa de visualización

Visualmente, cada partícula se representa generalmente como una forma simple, como un círculo dibujado con ellipse(), acompañado de transparencia. El tiempo de vida (lifespan) está directamente conectado con la apariencia visual, ya que se utiliza para controlar la opacidad del color, haciendo que la partícula se desvanezca a medida que se acerca a su muerte. Si se quisiera cambiar la representación visual, por ejemplo usar líneas en lugar de círculos, solo sería necesario modificar la función de dibujo, mientras que las propiedades físicas, la lógica de actualización y el sistema de vida y muerte permanecerían intactos, evidenciando la separación entre visualización, comportamiento y estructura.

### Actividad 2

En este ejemplo, la gestión de partículas deja de hacerse directamente en el ciclo principal y se encapsula dentro de una entidad llamada emisor. Cada emisor se encarga de crear, actualizar y eliminar sus propias partículas, lo que permite una mejor organización del sistema.

El programa principal ahora maneja una colección de emisores, mientras que cada emisor contiene su propia colección de partículas, formando una estructura jerárquica de dos niveles.

Este enfoque introduce el concepto de sistema de sistemas, donde múltiples entidades autónomas administran su propio estado, ciclo de vida y comportamiento frente a fuerzas, facilitando la escalabilidad y modularidad del sistema

### Actividad 3

En este ejemplo, las distintas subclases de partículas comparten una estructura y comportamiento base definidos por la clase principal. Todas poseen atributos como posición, velocidad, aceleración y tiempo de vida, y siguen el mismo ciclo de actualización mediante métodos comunes. Sin embargo, se diferencian en su representación visual, ya que cada subclase puede redefinir la forma en que se muestra, lo que introduce variedad sin alterar la lógica fundamental del sistema.

Resulta fundamental que el emisor no necesite conocer el tipo específico de partícula que está gestionando. Esto se debe a que todas las partículas responden a la misma interfaz de comportamiento, lo que permite tratarlas de manera uniforme. Gracias a esto, el sistema se vuelve más flexible y extensible, ya que el emisor únicamente ejecuta y evalúa el estado de cada partícula sin depender de su implementación concreta.

Si se quisiera agregar un nuevo tipo de partícula, bastaría con crear una nueva subclase que herede de la clase base y, si es necesario, redefinir ciertos métodos como el de visualización. No sería necesario modificar la lógica del emisor ni el funcionamiento general del sistema, lo que evidencia una correcta separación de responsabilidades y un diseño escalable.

En comparación con el ejemplo anterior, la lógica del emisor y el mecanismo de eliminación de partículas permanecen sin cambios. La modificación se introduce exclusivamente en la capa de las partículas, donde se aplica herencia y polimorfismo para diversificar el comportamiento visual. Esto demuestra que es posible ampliar las capacidades del sistema sin alterar su estructura central.

### Actividad 4
Fuerzas globales vs. locales

En el Example 4.6, la gravedad se define en el ciclo principal como un vector constante. Esta fuerza es aplicada por el emisor a todas las partículas mediante el método applyForce(). Por lo tanto, se trata de una fuerza global, ya que afecta a todas las partículas por igual, sin depender de condiciones individuales.

En el Example 4.7, además de la gravedad, se introduce una nueva fuerza generada por un objeto llamado repeller. La diferencia principal es que la gravedad sigue siendo una fuerza global, mientras que la fuerza del repeller es local, ya que depende de la posición relativa entre cada partícula y el repeller. La gravedad “vive” en el sistema global (ciclo principal), mientras que la lógica del repeller está encapsulada dentro de su propia entidad.

La fuerza del repeller depende de la distancia entre la partícula y el repeller, siguiendo una relación inversamente proporcional al cuadrado de la distancia. Esto modela un principio físico similar a las leyes de atracción o repulsión gravitacional/electrostática, donde la intensidad de la fuerza disminuye con la distancia.

Es importante notar que la clase Particle no cambia entre los ejemplos 4.6 y 4.7. Esto implica que las partículas no necesitan conocer el origen de las fuerzas que reciben, lo que evidencia una clara separación entre el comportamiento interno de las partículas y las fuerzas externas que actúan sobre ellas.

| Aspecto                           | 4.2      | 4.4      | 4.5      | 4.6             | 4.7                        |
| --------------------------------- | -------- | -------- | -------- | --------------- | -------------------------- |
| ¿Quién crea partículas?           | draw()   | Emitter  | Emitter  | Emitter         | Emitter                    |
| ¿Hay clase Emitter?               | ❌ No     | ✅ Sí     | ✅ Sí     | ✅ Sí            | ✅ Sí                       |
| ¿Hay herencia?                    | ❌ No     | ❌ No     | ✅ Sí     | ❌ No            | ❌ No                       |
| ¿Hay fuerzas externas?            | ❌ No     | ❌ No     | ❌ No     | ✅ Sí (gravedad) | ✅ Sí (gravedad + repeller) |
| ¿Hay interacción entre elementos? | ❌ No     | ❌ No     | ❌ No     | ❌ No            | ✅ Sí (repeller-partículas) |
| ¿Cómo mueren las partículas?      | lifespan | lifespan | lifespan | lifespan        | lifespan                   |
Se decidió modificar el comportamiento de las fuerzas en el Example 4.7, específicamente aumentando la intensidad de la repulsión del repeller.

Para lograr esto, se modificó la línea dentro de la clase Repeller:

this.power = 150;

por un valor mayor, por ejemplo:

this.power = 300;

También podría modificarse la fórmula de fuerza en el método repel() para hacer la repulsión más intensa o más suave.
## Bitácora de aplicación 
1. Idea: Me gusta la idea de que todos al final nos convertiremos en parte de algo mayor, por ello escogí la trascendencia. Las flores las represento como si fueran almas, relacionandolas con el sentimiento de que la vida es hermosa pero no eterna, tu funcionas como si estuvieras guiando a las flores al más allá. Una vez tocas una flor esta explota en petalos los cuales se pueden arrastrar al medio convirtiendose en la silueta de un loto. En el folclor los lotos simboliza la trascendencia espiritual y la pureza, elevándose sobre aguas fangosas para florecer inmaculada. Una vez el loto este completo este explota en cenizas, como sabemos los lotos una vez se marchitan son triturados y convertidos en polvo para luego dejarlos libres en el aire, significando que las almas han completado su camino.
2. Aquí va el mapa de decisiones:

Mapa de decisiones

Emisión de partículas
Las flores nacen en los bordes del canvas sobre enredaderas que crecen orgánicamente, porque el origen en los márgenes refuerza la idea de que la vida emerge desde afuera —desde la naturaleza— y viaja hacia el centro. La explosión al hacer click representa el momento de florecimiento máximo: la flor libera todo lo que tiene.

Tipos de partículas
Hay dos tipos: PaintPetal (pétalos) y AshParticle (cenizas). Los pétalos representan la vida activa —colorida, móvil, con trayectorias impredecibles—, mientras las cenizas representan lo que queda después de la muerte: fragmentos grises, pesados, que caen y desaparecen lentamente.
Fuerzas

La gravedad y el ruido de Perlin guían a los pétalos en vuelo libre, simulando el movimiento errático del viento. La fuerza de arrastre del usuario es la única que puede redirigir ese destino, lo que le da al gesto un significado narrativo: el usuario no controla el ciclo, pero puede intervenir en él.
Condición de muerte
Los pétalos no simplemente desaparecen: al morir en vuelo libre dejan una mancha de pintura en el canvas (memoria del paso), y al marchitarse desde el loto generan cenizas. La muerte deja huella, como en cualquier ciclo real.

El loto
El loto es el corazón del ciclo: solo florece cuando recibe suficientes pétalos, permanece en bloom un tiempo limitado y luego se marchita. Representa que la plenitud es temporal y requiere un esfuerzo colectivo para ocurrir.

Interacción del usuario
Hacer click en una flor tiene el significado de provocar la floración: el usuario decide cuándo y qué flor explota. Arrastrar pétalos hacia el loto significa alimentar el ciclo: sin esa intervención, los pétalos se dispersan y el loto nunca florece. La interacción no es decorativa, es la condición necesaria para que el ciclo se complete.

Gestión de memoria
Los pétalos y cenizas muertos se filtran en cada frame (filter(p => p.alive)), y las enredaderas completamente muertas y sin flores se eliminan cada 240 frames para mantener el rendimiento sin interrumpir la experiencia visual.
Paletas por estación
Cada estación cambia los colores del fondo, las enredaderas y los pétalos porque el mismo ciclo de vida —nacer, florecer, morir— se ve y se siente distinto según el contexto. Es la misma estructura, otra emoción.

3. 
<img width="1280" height="904" alt="image" src="https://github.com/user-attachments/assets/f830105d-79cf-404c-97f7-36aa718f59ac" />

<img width="1280" height="904" alt="image" src="https://github.com/user-attachments/assets/ea16adb6-dd82-4ba2-af8a-e87419594e20" />

### Codigo:

Config.js:

``` js
// ═══════════════════════════════════════════════════════════════════
//  config.js — Constantes globales y paletas de estaciones
// ═══════════════════════════════════════════════════════════════════

const SEASONS = {
  1: { bg:[7,5,15],  vine:[70,110,55],  ink:[[220,80,120],[180,60,200],[255,160,180],[100,180,80],[255,200,80]] },
  2: { bg:[14,7,3],  vine:[100,60,18],  ink:[[200,80,20],[180,40,10],[230,160,30],[150,50,10],[255,120,40]] },
  3: { bg:[4,7,18],  vine:[40,70,120],  ink:[[80,130,220],[150,190,255],[200,220,255],[60,100,180],[180,200,240]] },
  4: { bg:[5,11,2],  vine:[35,105,25],  ink:[[240,200,20],[255,140,0],[200,230,50],[255,80,60],[180,240,100]] }
};

const SEASON_NAMES = { 1:'primavera', 2:'otoño', 3:'invierno', 4:'verano' };

// Radio del loto central — aumentado para que sea más grande en pantalla
const LOTUS_R = 290;

// Velocidad de flujo de pétalos a lo largo del camino del loto
const FLOW_SPEED = 0.45;

// Duración del ciclo de floración (en frames)
const BLOOM_DURATION  = 900;
const WITHER_DURATION = 240;

// Estado global compartido entre módulos
let season;
let paintLayer;
let petals       = [];
let ashParticles = [];
let vines        = [];
let noiseOff     = 0;
let CX, CY;

let isDragging = false;
let dragX = 0, dragY = 0;
```
Petal .js
``` js
// ═══════════════════════════════════════════════════════════════════
//  petal.js — Clases AshParticle y PaintPetal
// ═══════════════════════════════════════════════════════════════════

// ─── CENIZA ───────────────────────────────────────────────────────────────────
// Partículas de ceniza que quedan cuando un pétalo se marchita
class AshParticle {
  constructor(x, y, col) {
    this.pos   = createVector(x, y);
    let ang    = random(TWO_PI);
    this.vel   = createVector(cos(ang)*random(0.2,1.2), random(-1.5,-0.3));
    this.col   = col.slice();
    this.size  = random(1.2, 3.5);
    this.alpha = random(140, 200);
    this.alive = true;
    this.angle = random(TWO_PI);
    this.angV  = random(-0.04, 0.04);
  }

  update() {
    this.vel.y += 0.018;
    let wAng = noise(this.pos.x*0.003, this.pos.y*0.003, noiseOff)*TWO_PI*2;
    this.vel.x += cos(wAng)*0.008;
    this.vel.mult(0.985);
    this.pos.add(this.vel);
    this.angle += this.angV;
    this.alpha -= random(0.6, 1.4);
    if (this.alpha <= 0) this.alive = false;
  }

  draw() {
    push(); translate(this.pos.x, this.pos.y); rotate(this.angle);
    noStroke();
    let g = (this.col[0]+this.col[1]+this.col[2])/3;
    fill(g*0.7+40, g*0.65+35, g*0.6+30, this.alpha*0.55);
    rect(-this.size*0.5, -this.size*0.15, this.size, this.size*0.3);
    fill(this.col[0]*0.3, this.col[1]*0.3, this.col[2]*0.3, this.alpha*0.25);
    ellipse(0, 0, this.size*0.7, this.size*0.25);
    pop();
  }
}

// ─── PÉTALO ───────────────────────────────────────────────────────────────────
// Pétalo individual: puede volar libre, fluir por el loto o marchitarse
class PaintPetal {
  constructor(x, y, col, levy = false) {
    this.pos    = createVector(x, y);
    let spd     = levy ? (random()<0.12 ? random(10,22) : random(2,5)) : random(2,7);
    let ang     = random(TWO_PI);
    this.vel    = createVector(cos(ang)*spd, sin(ang)*spd - random(0.5,2.5));
    this.acc    = createVector(0,0);
    this.col    = col.slice();
    this.size   = random(4,13);
    this.alpha  = random(190,255);
    this.alive  = true;
    this.angle  = random(TWO_PI);
    this.angVel = random(-0.14,0.14);
    this.mass   = this.size*0.12;
    this.trailAlpha = random(10, 28);
    this.painted    = false;

    // Flujo en el loto
    this.lotusSlot     = null;
    this.lotusPath     = null;
    this.lotusProgress = 0;

    // Marchitamiento
    this.withering = false;
    this.witherAge = 0;
  }

  applyForce(f) {
    this.acc.add(p5.Vector.div(f, this.mass));
  }

  // Asigna el pétalo a una posición en el camino del loto
  assignToLotus(startIdx, path) {
    this.lotusSlot     = startIdx;
    this.lotusPath     = path;
    this.lotusProgress = 0;
    this.angVel       *= 0.2;
  }

  // Inicia el ciclo de marchitamiento
  startWithering() {
    this.withering = true;
    this.witherAge = 0;
    this.lotusSlot = null;
    this.lotusPath = null;
  }

  update() {
    // ── Flujo por el camino del loto ──────────────────────────────────────────
    if (this.lotusSlot !== null && this.lotusPath !== null) {
      const path = this.lotusPath;
      const N    = path.length;

      this.lotusSlot = (this.lotusSlot + FLOW_SPEED) % N;
      let i0 = floor(this.lotusSlot) % N;
      let i1 = (i0 + 1) % N;
      let t  = this.lotusSlot - floor(this.lotusSlot);

      let tx = lerp(path[i0].x, path[i1].x, t);
      let ty = lerp(path[i0].y, path[i1].y, t);
      this.pos.x = lerp(this.pos.x, tx, 0.18);
      this.pos.y = lerp(this.pos.y, ty, 0.18);

      // Orientar en la dirección del movimiento
      let nextI = (i0 + 3) % N;
      let dx = path[nextI].x - path[i0].x;
      let dy = path[nextI].y - path[i0].y;
      this.angle = lerp(this.angle, atan2(dy, dx), 0.12);

      // Pulso de brillo
      this.alpha = 190 + sin(frameCount * 0.09 + this.lotusSlot * 0.3) * 40;
      return;
    }

    // ── Marchitamiento ────────────────────────────────────────────────────────
    if (this.withering) {
      this.witherAge++;
      this.alpha -= random(2.5, 5);
      this.vel.y += 0.08;
      let wAng = noise(this.pos.x*0.004, this.pos.y*0.004, noiseOff)*TWO_PI*2;
      this.vel.x += cos(wAng)*0.015;
      this.vel.mult(0.97);
      this.pos.add(this.vel);
      this.angle += this.angVel;
      if (this.alpha <= 0) { this._spawnAsh(); this.alive = false; }
      return;
    }

    // ── Vuelo libre ───────────────────────────────────────────────────────────
    let spd = this.vel.mag();
    this.applyForce(this.vel.copy().normalize().mult(-0.016*spd*spd));
    this.applyForce(createVector(0, 0.055*this.mass));
    let wAng = noise(this.pos.x*0.004, this.pos.y*0.004, noiseOff)*TWO_PI*2;
    this.applyForce(createVector(cos(wAng)*0.04, sin(wAng)*0.02));
    this.angle += this.angVel;
    this.vel.add(this.acc); this.vel.limit(11);
    this.pos.add(this.vel); this.acc.mult(0);
    this.alpha -= 0.7;

    // Al desvanecerse, deja una huella en la capa de pintura
    if ((this.alpha <= 0 || this.pos.y > height+30) && !this.painted) {
      this.painted = true;
      if (this.pos.x > -10 && this.pos.x < width+10) {
        paintLayer.noStroke();
        paintLayer.fill(this.col[0], this.col[1], this.col[2], this.trailAlpha);
        paintLayer.push();
        paintLayer.translate(this.pos.x, this.pos.y);
        paintLayer.rotate(this.angle);
        paintLayer.ellipse(0, 0, this.size*random(1,2), this.size*0.28);
        paintLayer.pop();
      }
      this.alive = false;
    }
  }

  // Genera cenizas y mancha de pintura al morir
  _spawnAsh() {
    let n = floor(random(3,8));
    for (let i = 0; i < n; i++) {
      ashParticles.push(new AshParticle(
        this.pos.x + randomGaussian(0, this.size*0.4),
        this.pos.y + randomGaussian(0, this.size*0.4),
        this.col
      ));
    }
    paintLayer.push(); paintLayer.noStroke();
    paintLayer.fill(120, 110, 100, random(10,28));
    paintLayer.ellipse(this.pos.x, this.pos.y, this.size*0.5, this.size*0.18);
    paintLayer.pop();
  }

  draw() {
    if (!this.alive) return;
    push(); translate(this.pos.x, this.pos.y); rotate(this.angle); noStroke();

    if (this.lotusSlot !== null) {
      // Pétalo fluyendo: brilla con pulso
      let glow = sin(frameCount * 0.09 + this.lotusSlot * 0.4) * 0.45 + 0.55;
      let sz   = this.size * (0.9 + glow * 0.25);
      fill(this.col[0], this.col[1], this.col[2], this.alpha * 0.22);
      ellipse(-sz*0.6, 0, sz*1.4, sz*0.3);
      fill(this.col[0], this.col[1], this.col[2], this.alpha * glow);
      ellipse(0, 0, sz, sz*0.38);
      fill(255, 240, 210, 100 * glow);
      ellipse(0, 0, sz*0.35, sz*0.14);

    } else if (this.withering) {
      let shrink = max(0.1, 1 - this.witherAge*0.012);
      fill(this.col[0], this.col[1], this.col[2], max(0, this.alpha));
      ellipse(0, 0, this.size*shrink, this.size*0.38*shrink);

    } else {
      fill(this.col[0], this.col[1], this.col[2], this.alpha);
      ellipse(0, 0, this.size, this.size*0.38);
    }
    pop();
  }
}
```
Flower.js
``` js
// ═══════════════════════════════════════════════════════════════════
//  flower.js — Clase VineFlower (flor que crece en las vines)
// ═══════════════════════════════════════════════════════════════════

class VineFlower {
  constructor(x, y, col) {
    this.x       = x;
    this.y       = y;
    this.col     = col;
    this.size    = random(10, 22);
    this.bloom   = 0;           // 0 = capullo → 1 = flor abierta
    this.exploded = false;
    this.phase   = random(TWO_PI);
    this.age     = 0;
    this.swayX   = 0;
    this.swayY   = 0;
    this.petalN  = floor(random(5, 9));
  }

  update(pos) {
    if (pos && !this.exploded) { this.x = pos.x; this.y = pos.y; }
    this.age++;
    if (this.bloom < 1) this.bloom = min(1, this.bloom + 0.02);
    this.swayX = sin(this.age*0.055 + this.phase) * 3;
    this.swayY = cos(this.age*0.038 + this.phase) * 2;
  }

  // Explota liberando pétalos y activando el loto si estaba dormido
  triggerExplode() {
    if (this.exploded) return;
    this.exploded = true;
    let px = this.x + this.swayX;
    let py = this.y + this.swayY;

    paintSplash(px, py, this.col, this.size);

    let n = floor(random(35, 60));
    for (let i = 0; i < n; i++)
      petals.push(new PaintPetal(px, py, this.col));
    for (let i = 0; i < 14; i++)
      petals.push(new PaintPetal(px, py, random(season.ink), true));

    if (lotusPhase === 'dormant') lotusPhase = 'waiting';
  }

  draw() {
    if (this.exploded) return;
    let px = this.x + this.swayX;
    let py = this.y + this.swayY;
    let c  = this.col;
    let b  = this.bloom;

    noStroke();

    // Aura suave
    fill(c[0], c[1], c[2], sin(this.age*0.08)*25 + 22);
    circle(px, py, this.size*3.2*b);

    // Pétalos
    for (let i = 0; i < this.petalN; i++) {
      let a = (TWO_PI / this.petalN) * i + this.swayX*0.05;
      let d = this.size * b;
      push();
      translate(px + cos(a)*d*0.5, py + sin(a)*d*0.5);
      rotate(a);
      fill(c[0], c[1], c[2], 195*b);
      noStroke();
      ellipse(0, 0, d, d*0.4);
      pop();
    }

    // Centro amarillo
    fill(255, 238, 80, 215*b);
    circle(px, py, this.size*0.44*b);

    // Destello cuando está completamente abierta
    if (b > 0.95) {
      fill(255, 255, 255, 90 + sin(this.age*0.12)*65);
      textSize(9); textAlign(CENTER, CENTER);
      text('✦', px, py - this.size*1.3);
    }
  }
}
```
Lotus.js
``` js
// ═══════════════════════════════════════════════════════════════════
//  lotus.js — Construcción del path, ciclo de vida y dibujo del loto
// ═══════════════════════════════════════════════════════════════════

// Estado del loto
var lotusPath      = [];
var assignedPetals = [];
var slotsOccupied  = 0;
var lotusPhase     = 'dormant';   // dormant → gathering → blooming → withering → dead
var bloomTimer     = 0;
var witherTimer    = 0;
var lotusGlow      = 0;
var lotusCol;
var lotusDeadPause = 0;

// ─── CONSTRUCCIÓN DEL PATH ────────────────────────────────────────────────────
// Genera la trayectoria continua del loto: pétalos apuntan ARRIBA, bulbo abajo.
// En p5.js el eje Y crece hacia abajo, por eso "arriba" = ángulo -HALF_PI.
//
// petalCurve(ang, len, wid, nPts)
//   ang  — dirección de la PUNTA del pétalo (radianes, coordenadas de pantalla)
//   len  — longitud del pétalo
//   wid  — anchura máxima del pétalo
//   nPts — resolución de la curva
function buildLotusPath() {
  const S  = LOTUS_R;
  const cx = CX, cy = CY;
  let path = [];

  function petalCurve(ang, len, wid, nPts) {
    let pts = [];
    // Lado izquierdo: base → punta
    for (let i = 0; i <= nPts; i++) {
      let t   = i / nPts;
      let lat = sin(t * PI) * wid * (1 - t * 0.4) * (-1);
      let axl = t * len;
      pts.push({
        x: cx + cos(ang) * axl + cos(ang + HALF_PI) * lat,
        y: cy + sin(ang) * axl + sin(ang + HALF_PI) * lat
      });
    }
    // Lado derecho: punta → base
    for (let i = nPts; i >= 0; i--) {
      let t   = i / nPts;
      let lat = sin(t * PI) * wid * (1 - t * 0.4);
      let axl = t * len;
      pts.push({
        x: cx + cos(ang) * axl + cos(ang + HALF_PI) * lat,
        y: cy + sin(ang) * axl + sin(ang + HALF_PI) * lat
      });
    }
    return pts;
  }

  const UP = -HALF_PI; // "arriba" en coordenadas de pantalla p5.js

  // Sépalos base — muy abiertos, casi horizontales
  for (let ang of [
    UP + radians(170),
    UP + radians(140),
    UP + radians(110),
    UP - radians(110),
    UP - radians(140),
    UP - radians(170),
  ]) {
    path.push(...petalCurve(ang, S * 0.58, S * 0.14, 14));
  }

  // Pétalos laterales exteriores
  for (let ang of [UP + radians(75), UP - radians(75)]) {
    path.push(...petalCurve(ang, S * 0.78, S * 0.22, 18));
  }

  // Pétalos medios
  for (let ang of [UP + radians(48), UP - radians(48)]) {
    path.push(...petalCurve(ang, S * 0.90, S * 0.20, 18));
  }

  // Pétalos interiores
  for (let ang of [UP + radians(22), UP - radians(22)]) {
    path.push(...petalCurve(ang, S * 1.00, S * 0.17, 16));
  }

  // Pétalo central — apunta directo arriba
  path.push(...petalCurve(UP, S * 1.08, S * 0.14, 16));

  // Bulbo — círculo pequeño en la base inferior
  const BPTS = 24;
  for (let i = 0; i <= BPTS; i++) {
    let a = (i / BPTS) * TWO_PI;
    path.push({ x: cx + cos(a) * S * 0.10, y: cy + sin(a) * S * 0.09 + S * 0.32 });
  }

  return path;
}

// ─── RESET ────────────────────────────────────────────────────────────────────
function resetLotus() {
  lotusPath      = buildLotusPath();
  assignedPetals = [];
  slotsOccupied  = 0;
  lotusPhase     = 'dormant';
  bloomTimer     = 0;
  witherTimer    = 0;
  lotusDeadPause = 0;
  lotusGlow      = 0;
  lotusCol       = random(season.ink).slice();
}

// ─── ATRACCIÓN POR ARRASTRE ───────────────────────────────────────────────────
// El único mecanismo de atracción. Solo actúa mientras el usuario arrastra.
function applyDragAttraction() {
  if (!isDragging) return;
  const DRAG_RADIUS = LOTUS_R * 1.0;

  for (let p of petals) {
    if (p.lotusSlot !== null || p.withering) continue;
    let d = dist(p.pos.x, p.pos.y, dragX, dragY);
    if (d < DRAG_RADIUS) {
      let dir  = createVector(dragX - p.pos.x, dragY - p.pos.y);
      let pull = map(d, 0, DRAG_RADIUS, 0.28, 0.001);
      p.applyForce(dir.copy().normalize().mult(pull));
    }
  }
}

// ─── UPDATE ───────────────────────────────────────────────────────────────────
function updateLotus() {
  if (lotusPhase === 'dormant') return;

  const pathLen = lotusPath.length;

  if (lotusPhase === 'waiting' || lotusPhase === 'blooming') {
    if (lotusPhase === 'blooming') bloomTimer++;
    lotusGlow = lerp(lotusGlow, lotusPhase === 'blooming' ? 160 : 40, 0.025);

    // Capturar pétalos que lleguen muy cerca del centro (arrastrados por el usuario)
    for (let p of petals) {
      if (p.lotusSlot !== null || p.withering) continue;
      let d = dist(p.pos.x, p.pos.y, CX, CY);
      if (d < LOTUS_R * 0.55 && slotsOccupied < pathLen) {
        let startIdx = (slotsOccupied * floor(pathLen / 60)) % pathLen;
        p.assignToLotus(startIdx, lotusPath);
        assignedPetals.push(p);
        slotsOccupied++;
      }
    }

    // Pasar a blooming cuando haya suficientes pétalos capturados
    if (lotusPhase === 'waiting' && slotsOccupied / pathLen >= 0.30)
      lotusPhase = 'blooming';

    if (lotusPhase === 'blooming' && bloomTimer >= BLOOM_DURATION) {
      lotusPhase = 'withering';
      for (let p of assignedPetals) p.startWithering();
    }
  }

  else if (lotusPhase === 'withering') {
    witherTimer++;
    lotusGlow = lerp(lotusGlow, 0, 0.035);
    if (witherTimer >= WITHER_DURATION) lotusPhase = 'dead';
  }

  else if (lotusPhase === 'dead') {
    lotusDeadPause++;
    if (lotusDeadPause > 180) resetLotus();
  }
}

// ─── DRAW ─────────────────────────────────────────────────────────────────────
function drawLotusGuide() {
  // Silueta punteada fantasma
  let alpha = (lotusPhase === 'dormant') ? 30 : map(lotusGlow, 0, 160, 20, 4);
  noStroke();
  for (let pt of lotusPath) {
    if (random() < 0.20) {
      fill(255, 210, 180, alpha * random(0.5, 1.3));
      circle(pt.x, pt.y, random(1.0, 2.2));
    }
  }

  // Resplandor central
  if (lotusPhase !== 'dormant') {
    noStroke();
    for (let r = 4; r >= 1; r--) {
      fill(lotusCol[0], lotusCol[1], lotusCol[2], lotusGlow * 0.06 * r);
      circle(CX, CY, LOTUS_R * 0.45 * r);
    }
  }

  // HUD: segundos restantes en bloom
  if (lotusPhase === 'blooming') {
    let remaining = ceil((BLOOM_DURATION - bloomTimer) / 60);
    noStroke(); fill(255, 230, 180, 90);
    textSize(11); textAlign(CENTER); textFont('Georgia');
    text(remaining + 's', CX, CY + LOTUS_R * 1.30);
  }
  // HUD: porcentaje de llenado en waiting
  if (lotusPhase === 'waiting') {
    let pct = slotsOccupied / lotusPath.length;
    noStroke(); fill(255, 200, 160, 70);
    textSize(10); textAlign(CENTER); textFont('Georgia');
    text(nf(pct * 100, 2, 0) + '%', CX, CY + LOTUS_R * 1.30);
  }
}
```
Vine.js
``` js
// ═══════════════════════════════════════════════════════════════════
//  vine.js — Clase Vine (enredaderas con ramificación y flores)
// ═══════════════════════════════════════════════════════════════════

class Vine {
  constructor(x, y, angle) {
    this.pos     = createVector(x, y);
    this.vel     = createVector(cos(angle), sin(angle)).mult(random(1.2, 2.0));
    this.acc     = createVector(0, 0);
    this.age     = 0;
    this.maxAge  = random(300, 550);
    this.alive   = true;
    this.dead    = false;
    this.thick   = random(1.2, 2.8);
    this.history = [this.pos.copy()];
    this.phase   = random(TWO_PI);
    this.segLen  = random(2.5, 4.0);

    // Ramificación
    this.branched     = false;
    this.branchCount  = 0;

    // Flores — máximo 1 por vine, aparece en rango medio de vida
    this.flowers        = [];
    this.nextFlowerAge  = random(120, 220);
    this.flowerSpawned  = false;
  }

  applyForce(f) {
    this.acc.add(p5.Vector.div(f, 0.8));
  }

  update() {
    // Vine muerta: solo actualizar flores residuales
    if (this.dead) {
      for (let f of this.flowers) f.update(null);
      return;
    }
    if (!this.alive) { this.dead = true; return; }

    this.age++;

    // Movimiento guiado por ruido de Perlin
    let angle = noise(this.pos.x*0.006, this.pos.y*0.006, noiseOff) * TWO_PI * 2.4;
    this.applyForce(createVector(cos(angle), sin(angle)).mult(0.035));
    this.applyForce(this.vel.copy().mult(-0.016));
    let sway = sin(this.age*0.065 + this.phase) * 0.012;
    this.applyForce(createVector(-this.vel.y, this.vel.x).normalize().mult(sway));
    this.vel.add(this.acc); this.vel.limit(2.5);
    this.pos.add(this.vel.copy().normalize().mult(this.segLen));
    this.acc.mult(0);
    this.history.push(this.pos.copy());

    // Ramificación primaria
    if (!this.branched && this.age > 100 && random() < 0.005 && vines.length < 28) {
      this.branched = true;
      vines.push(new Vine(this.pos.x, this.pos.y, this.vel.heading() + random(-0.85, 0.85)));
    }
    // Ramificación secundaria
    if (this.branched && this.branchCount < 1 && this.age > 180 && random() < 0.003 && vines.length < 28) {
      this.branchCount++;
      vines.push(new Vine(this.pos.x, this.pos.y, this.vel.heading() + random(-1.1, 1.1)));
    }

    // Generar flor (una sola, probabilidad media)
    if (!this.flowerSpawned && this.age >= this.nextFlowerAge && random() < 0.025) {
      this.flowers.push(new VineFlower(this.pos.x, this.pos.y, random(season.ink)));
      this.flowerSpawned = true;
    }

    for (let f of this.flowers) f.update(null);

    // Morir si sale del canvas o supera su vida máxima
    if (this.age > this.maxAge ||
        this.pos.x < -60 || this.pos.x > width+60 ||
        this.pos.y < -60 || this.pos.y > height+60)
      this.alive = false;
  }

  // Fuerza la explosión de todas sus flores sin explotar
  explodeFlower() {
    for (let f of this.flowers) if (!f.exploded) f.triggerExplode();
  }

  draw() {
    if (this.history.length < 2) return;
    let vc  = season.vine;
    let thk = this.thick * (1 + sin(this.age*0.05 + this.phase)*0.2);

    // Tallo
    strokeWeight(thk); stroke(vc[0], vc[1], vc[2], 150); noFill();
    beginShape();
    for (let pt of this.history) curveVertex(pt.x, pt.y);
    endShape();

    // Hojitas a lo largo del tallo
    if (this.history.length > 8) {
      let step = 22;
      for (let i = step; i < this.history.length; i += step) {
        let curr = this.history[i];
        let prev = this.history[i-4];
        if (!prev) continue;
        let lAng = atan2(curr.y - prev.y, curr.x - prev.x);
        let side = (floor(i/step)) % 2 === 0 ? 1 : -1;
        push();
        translate(curr.x, curr.y); rotate(lAng + side*PI*0.45);
        fill(vc[0]+10, vc[1]+30, vc[2]+8, 120); noStroke();
        ellipse(0, -thk*2, thk*2.2, thk*4.5);
        pop();
      }
    }

    for (let f of this.flowers) f.draw();
  }
}
```

Sketch.js 
``` js
// ═══════════════════════════════════════════════════════════════════
//  sketch.js — Setup, draw loop y manejo de eventos p5.js
//  Controles:
//    Click en flor  → explotar pétalos
//    Drag           → atraer pétalos cercanos
//    1 / 2 / 3 / 4  → cambiar estación
//    ESPACIO        → explotar todas las flores
//    C              → limpiar capa de pintura
//    R              → reinicio completo
// ═══════════════════════════════════════════════════════════════════

// ─── UTILIDADES ───────────────────────────────────────────────────────────────

function paintSplash(x, y, col, size) {
  paintLayer.push(); paintLayer.noStroke();
  for (let i = 0; i < 5; i++) {
    let r = size * random(1.2, 3.0);
    paintLayer.fill(col[0], col[1], col[2], random(10, 40));
    paintLayer.ellipse(x + randomGaussian(0, size), y + randomGaussian(0, size), r, r*0.72);
  }
  paintLayer.pop();
}

function clearPaintLayer() {
  paintLayer.clear();
  paintLayer.background(season.bg[0], season.bg[1], season.bg[2]);
}

function spawnInitialVines() {
  vines = [];
  let edges = [
    ...Array.from({length:4}, () => ({ x:random(width),  y:0,      angle:random(PI*0.25, PI*0.75)  })),
    ...Array.from({length:4}, () => ({ x:random(width),  y:height, angle:random(-PI*0.75, -PI*0.25) })),
    ...Array.from({length:3}, () => ({ x:0,              y:random(height), angle:random(-PI*0.3, PI*0.3) })),
    ...Array.from({length:4}, () => ({ x:width,          y:random(height), angle:random(PI*0.7, PI*1.3) })),
  ];
  for (let e of edges) vines.push(new Vine(e.x, e.y, e.angle));
}

function spawnVineFromBorder() {
  let side = floor(random(4));
  let x, y, ang;
  if      (side === 0) { x = random(width); y = 0;      ang = random(PI*0.2, PI*0.8);   }
  else if (side === 1) { x = random(width); y = height; ang = random(-PI*0.8, -PI*0.2); }
  else if (side === 2) { x = 0;    y = random(height);  ang = random(-PI*0.3, PI*0.3);  }
  else                 { x = width; y = random(height); ang = random(PI*0.7, PI*1.3);   }
  vines.push(new Vine(x, y, ang));
}

function changeSeason(n) {
  season = SEASONS[n];
  clearPaintLayer();
  vines = []; petals = []; ashParticles = [];
  resetLotus();
  spawnInitialVines();
}

// ─── SETUP ────────────────────────────────────────────────────────────────────
function setup() {
  createCanvas(windowWidth, windowHeight);
  colorMode(RGB, 255, 255, 255, 255);
  season = SEASONS[1];
  CX = width/2;
  CY = height/2 + 15;
  paintLayer = createGraphics(width, height);
  paintLayer.colorMode(RGB, 255, 255, 255, 255);
  clearPaintLayer();
  resetLotus();
  spawnInitialVines();
}

// ─── DRAW ─────────────────────────────────────────────────────────────────────
function draw() {
  noiseOff += 0.0025;
  background(season.bg[0], season.bg[1], season.bg[2]);

  // Estrellas de ruido de fondo
  for (let i = 0; i < 20; i++) {
    let px = random(width), py = random(height);
    let n  = noise(px*0.01, py*0.01, noiseOff*0.08);
    stroke(255, 255, 200, n*4); strokeWeight(0.3); point(px, py);
  }

  image(paintLayer, 0, 0);

  drawLotusGuide();
  applyDragAttraction();
  updateLotus();

  for (let v of vines) { v.update(); v.draw(); }

  petals = petals.filter(p => p.alive);
  for (let p of petals) { p.update(); p.draw(); }

  ashParticles = ashParticles.filter(a => a.alive);
  for (let a of ashParticles) { a.update(); a.draw(); }

  // Limpiar vines completamente muertas y sin flores
  if (frameCount % 240 === 0)
    vines = vines.filter(v => !(v.dead && v.flowers.every(f => f.exploded)));

  // Reponer vines si hay pocas
  if (frameCount % 180 === 0 && vines.length < 22) spawnVineFromBorder();
  if (frameCount % 180 === 0 && vines.length < 11) { spawnVineFromBorder(); spawnVineFromBorder(); }

  // Cursor de arrastre
  if (isDragging) {
    noFill(); stroke(255, 200, 160, 50); strokeWeight(1);
    circle(dragX, dragY, LOTUS_R * 0.4);
    noStroke(); fill(255, 200, 160, 25);
    circle(dragX, dragY, 16);
  }

  _drawHUD();
}

function _drawHUD() {
  // Controles
  noStroke();
  fill(255, 220, 180, 38 + sin(frameCount*0.04)*14);
  textSize(11); textAlign(LEFT); textFont('Georgia');
  text('1/2/3/4 = estación   ESPACIO = explotar todo   C = limpiar   R = reinicio', 16, height-16);

  // Instrucciones cuando el loto está dormido
  if (lotusPhase === 'dormant' || lotusPhase === 'waiting') {
    fill(255, 220, 180, 48 + sin(frameCount*0.05)*20);
    textSize(12); textAlign(CENTER); textFont('Georgia');
    text('haz click en una flor para liberar sus pétalos', CX, CY + LOTUS_R*1.42);
    text('arrastra los pétalos hasta el centro del loto',  CX, CY + LOTUS_R*1.42 + 20);
  }

  // Nombre de la estación actual
  noStroke(); fill(255, 220, 180, 45);
  textSize(10); textAlign(RIGHT); textFont('Georgia');
  for (let k in SEASONS) {
    if (SEASONS[k] === season) { text(SEASON_NAMES[k], width-16, height-16); break; }
  }
}

// ─── EVENTOS ──────────────────────────────────────────────────────────────────
function mousePressed() {
  // Buscar la flor más cercana al cursor
  let closest = null, minD = 46;
  for (let vine of vines) {
    for (let f of vine.flowers) {
      if (!f.exploded) {
        let d = dist(mouseX, mouseY, f.x + f.swayX, f.y + f.swayY);
        if (d < minD) { minD = d; closest = { vine, f }; }
      }
    }
  }
  if (closest) { closest.f.triggerExplode(); return; }

  // Si no se hizo click en una flor, activar arrastre
  isDragging = true; dragX = mouseX; dragY = mouseY;
}

function mouseDragged() {
  isDragging = true; dragX = mouseX; dragY = mouseY;
}

function mouseReleased() {
  isDragging = false;
}

function keyPressed() {
  if (['1','2','3','4'].includes(key)) changeSeason(parseInt(key));
  if (key === ' ')                vines.forEach(v => v.explodeFlower());
  if (key.toLowerCase() === 'c') clearPaintLayer();
  if (key.toLowerCase() === 'r') {
    vines = []; petals = []; ashParticles = [];
    clearPaintLayer(); resetLotus(); spawnInitialVines();
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
  CX = width/2; CY = height/2 + 15;
  paintLayer = createGraphics(width, height);
  paintLayer.colorMode(RGB, 255, 255, 255, 255);
  clearPaintLayer();
  resetLotus();
}
```
### Codigo enlace:

- https://editor.p5js.org/Jakeline-Avila/sketches/gD0FGrylR
<img width="1093" height="1005" alt="image" src="https://github.com/user-attachments/assets/28110e23-4263-41c6-a103-97dd706f91c8" />
<img width="1092" height="949" alt="image" src="https://github.com/user-attachments/assets/8c95c563-df23-408e-ab05-39882ae68cbf" />
<img width="1015" height="933" alt="image" src="https://github.com/user-attachments/assets/e7d8c410-ae00-4d2a-915a-491b118faa45" />




## Bitácora de reflexión

Parte 1 — Principios fundamentales
1. Una partícula es una entidad con estado.
Cada pétalo en mi pieza tiene su propia posición, velocidad, color, tamaño, ángulo y nivel de transparencia. No son copias idénticas: cada una recuerda dónde está y cómo se siente en ese momento. Eso es tener estado.
2. Una partícula tiene ciclo de vida.
Un pétalo nace cuando una flor explota, vuela libremente afectado por el viento, puede ser capturado por el loto y fluir en él, y eventualmente muere: dejando una mancha de pintura si muere en vuelo, o generando cenizas si se marchita desde el loto. La muerte no es solo desaparecer, comunica el final de algo.
3. Un sistema de partículas gestiona colecciones dinámicas de elementos.
En sketch.js hay un arreglo petals[] que en cada frame se actualiza, se dibuja y se filtra. El sistema no sabe nada de cada pétalo individual: solo itera sobre todos y les dice "actualízate" y "dibújate". La colección crece y encoge constantemente.
4. La creación y eliminación de partículas no es un detalle técnico menor, sino parte central del modelo.
En mi pieza, cuándo nace un pétalo (cuando el usuario hace click en una flor) y cómo muere (con cenizas, con mancha de pintura) son decisiones narrativas. Si simplemente aparecieran y desaparecieran sin contexto, la pieza no comunicaría nada sobre el ciclo de vida.
5. Debe haber separación entre la lógica de una partícula individual y la lógica del sistema.
PaintPetal sabe cómo moverse, cómo dibujarse y cómo morir. No sabe cuántas otras partículas existen ni qué hace el loto. Esa responsabilidad es del sistema en sketch.js y lotus.js. Cada capa hace solo su trabajo.
6. Un emisor o particle system es una abstracción importante.
Las flores VineFlower actúan como emisores: cuando explotan, generan un lote de pétalos con parámetros específicos. No son partículas ellas mismas, son la fuente que decide cuántos pétalos nacen, con qué colores y con qué velocidades iniciales.
7. Pueden existir sistemas de sistemas.
Las enredaderas Vine son un sistema que contiene flores VineFlower, que a su vez son emisores de pétalos PaintPetal, que al morir generan cenizas AshParticle. Hay al menos tres niveles anidados: el sistema de vines contiene el sistema de flores contiene el sistema de pétalos contiene el sistema de cenizas.
8. Puede haber heterogeneidad usando herencia y polimorfismo.
PaintPetal y AshParticle son dos tipos de partículas distintos con comportamientos diferentes, pero el sistema los trata de forma similar: ambos tienen update(), draw() y un flag alive. Esa interfaz común es lo que permite mezclarlos en el mismo loop sin que el sistema necesite saber exactamente qué tipo es cada uno.
9. Las partículas pueden responder a fuerzas globales y locales.
Los pétalos responden a la gravedad y al ruido de Perlin como fuerzas globales (afectan a todos por igual). Pero también responden a fuerzas locales: la atracción del cursor cuando el usuario arrastra, o la fuerza de captura del loto cuando un pétalo entra en su radio. La misma partícula puede estar bajo influencias distintas según su posición y contexto.
10. La representación visual puede variar sin cambiar el principio algorítmico de fondo.
Un pétalo en vuelo libre, un pétalo fluyendo en el loto y un pétalo marchitándose se dibujan de formas distintas (con brillo pulsante, encogido, con aura) pero el algoritmo de fondo es el mismo: tiene posición, se mueve, tiene alpha. El draw() cambia según el estado, pero la estructura de la partícula no.

Parte 2 — Transferencia a Unity
Qué se mantendría igual
Lo que es independiente de la herramienta son los principios lógicos:

El ciclo de vida de tres fases (vuelo libre → capturado → marchitamiento) seguiría siendo el mismo, implementado con una máquina de estados.
La separación entre partícula individual y sistema gestor se mantiene: en Unity sería un ParticleData script por objeto y un PetalSystem manager separado.
Las fuerzas (gravedad, ruido de Perlin, atracción al cursor) son matemáticamente idénticas — Unity tiene Rigidbody y se puede implementar Perlin noise igual.
La lógica del loto como sistema con fases (dormant → waiting → blooming → withering → dead) es pura lógica de estados, no depende de p5.js.


Qué cambiaría
Lo que cambiaría al pasar a Unity es principalmente la capa técnica de implementación. El renderizado ya no sería con funciones simples como ellipse() sino con sprites o meshes con shaders. La gestión de memoria requeriría object pooling en lugar de simplemente filtrar un array, porque instanciar y destruir objetos constantemente en Unity es costoso. El ruido de Perlin seguiría existiendo pero a través de Mathf.PerlinNoise(). La capa de pintura que en p5.js se logra con un createGraphics() necesitaría una Render Texture con un paint shader. Y los eventos del usuario pasarían del simple mousePressed() a un Input System con raycast sobre un plano 2D.


Qué partes son verdaderamente independientes de la herramienta
El concepto narrativo completo: que el usuario no controla el ciclo sino que interviene en él, que la muerte deja huella, que el loto solo florece con esfuerzo colectivo. Esas decisiones de diseño no viven en ningún archivo de código ,viven en la idea, y se pueden trasladar a cualquier herramienta.
