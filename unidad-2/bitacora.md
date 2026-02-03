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

## Bitácora de aplicación 



## Bitácora de reflexión

