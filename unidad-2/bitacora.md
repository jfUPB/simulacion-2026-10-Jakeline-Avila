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
function setup() {
    createCanvas(800, 800);
}

function draw() {
    background(200);
    
    let lerp =   
  
    let v0 = createVector(50, 50);
    let v1 = createVector(700, 0);
    let v0c = p5.Vector.add(v0,v1);
    let v2 = createVector(0, 700);
    let v3 = p5.Vector.lerp(v1, v2, 0.5);
    let vC = p5.Vector.sub(v2, v1); // C = A - B

    drawArrow(v0, v1, 'red');
    drawArrow(v0, v2, 'blue');
    drawArrow(v0, v3, 'purple');
    drawArrow(v0c, vC, 'green');
    
  
  
    
  
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

## Bitácora de aplicación 



## Bitácora de reflexión


