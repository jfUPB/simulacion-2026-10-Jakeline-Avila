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


## Bitácora de aplicación 



## Bitácora de reflexión
