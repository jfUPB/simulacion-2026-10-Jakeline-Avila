# Unidad 8

## Bitácora de proceso de aprendizaje

### Actividad 1
1. Herramienta de interés: TouchDesigner
¿Por qué?
He elegido TouchDesigner por su naturaleza de programación visual basada en nodos, lo que permite prototipar sistemas complejos de forma rápida. A diferencia de los motores de renderizado tradicionales, TD destaca en el procesamiento de datos en tiempo real. Me interesa específicamente su capacidad para integrar simulaciones físicas (mediante el motor Bullet Physics o partículas) con entradas externas como audio, cámaras o sensores, permitiendo que la simulación no sea solo una animación estática, sino un sistema vivo que reacciona al entorno.
2. Relación con mi línea de énfasis o interés profesional
Como estudiante de Entretenimiento Digital, mi interés se centra en la creación de experiencias interactivas y diseño generativo. TouchDesigner es el estándar de la industria para el diseño de escenarios, instalaciones interactivas en museos y live visuals. Dominar esta herramienta me permite cerrar la brecha entre la ingeniería de sistemas físicos (matemáticas y fuerzas) y el arte digital, permitiéndome crear entornos que respondan al movimiento humano o al sonido.
3. Referentes realizados con TouchDesigner (o su ecosistema)             
Referente 1: Refik Anadol (Proyecto: "Melting Memories" o "Unsupervised")          
Por qué: Es el máximo exponente del uso de datos para crear fluidos y partículas que parecen tener masa y gravedad real. Sus obras transforman bases de datos gigantescas en simulaciones físicas que se sienten orgánicas.                                         
Referente 2: Vincent Houzé (Proyecto: "Fluid Structure")                
Por qué: Houzé es un maestro en usar el motor de física de TouchDesigner para simular colisiones, fluidos dinámicos y estructuras cinéticas. Su trabajo demuestra cómo la física computacional puede ser extremadamente estética y no solo técnica.                    
Referente 3: TUNDRA Collective (Proyecto: "Row")                 
Por qué: Utilizan la geometría y la repetición para crear sistemas espaciales. Me interesa cómo manipulan la percepción del espacio físico a través de la luz y el movimiento sincronizado, algo que requiere una gestión precisa de señales y tiempos (CHOPs en TD).
4. ¿Qué me interesa de estos referentes?
De estos referentes me fascina la capacidad de hacer invisible la tecnología. No se siente como "software", sino como un fenómeno natural digital. Me interesa cómo logran que miles de partículas sigan leyes físicas (atracción, repulsión, fricción) para generar comportamientos emergentes que cautivan al espectador, y cómo el renderizado en tiempo real permite una calidad visual cinematográfica sin tiempos de espera.
5. Contextos profesionales para mi pieza final
He identificado dos posibles contextos para aplicar lo aprendido en el curso:
Instalación Artística Interactiva: Una pieza para una galería o espacio público donde los espectadores, a través de su movimiento (detectado por sensores como Kinect o visión computacional), afecten un sistema de partículas o un cuerpo rígido, simulando fuerzas como el viento o la gravedad magnética.
Visuales para una Obra Escénica (Danza o Teatro): Crear un sistema de simulación física que reaccione en tiempo real a la intensidad del sonido de una banda en vivo o a los movimientos de un bailarín, convirtiendo la energía física del intérprete en energía visual digital.

### Actividad 2 

1. Sistema que voy a transferir:
Sistemas de Partículas (Particle Systems).      
2. ¿Cómo funcionaba este sistema en p5.js?                
En p5.js, el sistema se basaba en la Programación Orientada a Objetos (POO). Creamos una clase Particle con vectores para posición, velocidad y aceleración. Luego, en el draw(), usábamos un ciclo para actualizar cada partícula, aplicar una fuerza (como la gravedad) y dibujarla en el lienzo. Para manejar muchas partículas, necesitábamos un arreglo y eliminar las que "morían" para no saturar la memoria del navegador.           
3. Justificación: ¿Por qué transferirlo a TouchDesigner?          
Transferir este sistema a TouchDesigner tiene sentido por tres razones principales:
Rendimiento (GPU): Mientras que p5.js sufre con más de 1,000 partículas, TouchDesigner puede manejar cientos de miles en tiempo real gracias al procesamiento en tarjeta gráfica.             
Física Integrada: TD tiene nodos que permiten aplicar fuerzas como Turbulencia, Viento y Atracción magnética simplemente conectando cables, sin necesidad de programar manualmente las fórmulas de Newton.         
Modularidad: Puedo usar texturas, geometrías 3D o incluso video en vivo para influir en el comportamiento de las partículas de forma mucho más directa que en p5.js.        
4. ¿Qué tipo de pieza visual me imagino construir?          
- Me imagino una "Escultura de Humo Generativa". Sería una pieza donde un flujo constante de partículas emana de un punto central. Estas partículas estarían afectadas por un campo de fuerzas (Noise) que las hace moverse de forma fluida y orgánica, como si fuera tinta en el agua o humo. Además, me gustaría que el color y la velocidad de las partículas reaccionen a las frecuencias de una pista de audio (usando CHOPs de audio en TD).      
5. Dificultades técnicas anticipadas:                
- Gestión de Datos (SOPs vs TOPs): Entender cuándo usar geometría (SOPs) y cuándo pasar a texturas (TOPs) para que el sistema sea eficiente.    
- Renderizado: Configurar correctamente las luces y materiales (PBR) para que las partículas no se vean como simples puntos, sino que tengan profundidad y volumen.         
- Interacción con el Solver: Aprender a usar el nodo Feedback o el Particle SOP para que las partículas dejen estelas o tengan comportamientos de persistencia visual.         
### Actividad 3

1. Componentes y módulos identificados
Para reconstruir un sistema de partículas en TouchDesigner, necesito dominar cuatro familias de operadores:
- SOPs (Surface Operators):
- Sphere SOP o Grid SOP: Servirán como el "emisor" (de dónde nacen las partículas).
- Particle SOP: Es el motor principal. Aquí se definen la vida de la partícula, la velocidad inicial y la respuesta a fuerzas externas.
- Force SOP + Metaball SOP: Para crear zonas de atracción o repulsión física.
- CHOPs (Channel Operators):
- Noise CHOP: Para generar valores aleatorios suaves (como el noise() de p5.js) que muevan las partículas de forma orgánica.
- LFO CHOP: Para crear oscilaciones automáticas en los parámetros.
- TOPs (Texture Operators):
- Render TOP: Para convertir la simulación 3D en una imagen 2D.
- Feedback TOP + Blur TOP: Para crear estelas (trails) de movimiento, similar al efecto de no limpiar el fondo en cada frame de p5.js.
- COMPs (Components):
Geometry COMP, Camera COMP y Light COMP: El setup básico necesario para poder visualizar cualquier objeto 3D.

2. Pruebas técnicas realizadas
- Prueba técnica A: El Motor de Partículas Básico
- Qué resuelve: Esta prueba resuelve la generación y la física básica. Conecté un Sphere SOP a un Particle SOP.
- Resultado: Logré que las partículas nazcan de la superficie de la esfera y caigan por efecto de una gravedad interna. Configuré el parámetro "Life Expectancy" para que las partículas desaparezcan después de ciertos segundos, replicando la lógica de "muerte" de objetos en p5.js.


- Prueba técnica B: Instanciación de Geometría (Instancing)
- Qué resuelve: Esta prueba resuelve el rendimiento masivo. En lugar de usar el motor de partículas clásico, usé un Noise CHOP para mover 5,000 copias de un cubo pequeño.
- Resultado: Logré mover miles de elementos simultáneamente usando la GPU. Esto resuelve el problema de "lag" que tenía en p5.js al intentar dibujar más de 500 partículas manualmente.

  
3. Estado de la reconstrucción

- ¿Qué parte del sistema ya logré reconstruir?
Ya tengo funcional el emisor y el ciclo de vida de las partículas. También logré implementar fuerzas externas (viento y turbulencia) usando el nodo Noise dentro del Particle SOP, lo cual le da el movimiento errático que buscaba. Ya puedo visualizar el sistema en una ventana de renderizado con cámara y luces básicas.
- ¿Qué parte sigue sin resolverse?
- Colisiones complejas: Aún no logro que las partículas reboten de manera realista contra un objeto sólido específico (como un logo o un texto).
- Color dinámico: En p5.js cambiaba el color según la velocidad (mag()). En TouchDesigner aún estoy investigando cómo pasar el dato de velocidad del Particle SOP a un material para que cambie el color de cada partícula individualmente (probablemente necesite usar Texture Instancing o atributos de punto).

## Bitácora de aplicación 


## Bitácora de reflexión
