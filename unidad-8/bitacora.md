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

### Actividad 4

 Actividad 04: Estudio de transferencia

Este apartado detalla el proceso conceptual y técnico de trasladar los principios de simulación física desde un entorno de programación basada en texto (p5.js) a un entorno de programación visual basado en nodos (TouchDesigner).

####  Tabla Comparativa de Transferencia

| Aspecto | Sistema en p5.js (Procesamiento) | Sistema en TouchDesigner (Nodos) |
| :--- | :--- | :--- |
| **Arquitectura** | **Programación Imperativa:** Basada en escribir líneas de código secuenciales, clases y arreglos (`for loops`) para gestionar cada partícula. | **Programación Visual/Nodal:** Flujo de datos en tiempo real. Los datos (posiciones, fuerzas) viajan a través de operadores (CHOPs, SOPs). |
| **Cálculo Físico** | **Manual (Matemática de Euler):** Requiere programar manualmente las fórmulas de integración: `velocidad += aceleración` y `posición += velocidad`. | **Declarativo/Nodal:** Uso de nodos como `Particle SOP` para la gravedad o `Math CHOP` para sumar vectores de fuerzas de forma global. |
| **Generación de Forma** | **Ciclos Matemáticos:** Uso de funciones de dibujo como `ellipse()` dentro de loops de `sin()` y `cos()` para posicionar puntos. | **Scripting + Instancing:** Uso de un `Script CHOP` (Python) para la espiral y **GPU Instancing** para clonar geometría compleja sobre los puntos. |
| **Reactividad** | **Librería p5.sound:** Requiere analizar el espectro y mapear variables manualmente a las propiedades de los objetos en el código. | **CHOP Signal Analysis:** El audio es una señal viva que se conecta directamente a cualquier parámetro (Amplitud, Escala) mediante referencias. |
| **Rendimiento** | **CPU Bound:** El rendimiento cae drásticamente al superar las 1,000 partículas debido a la ejecución serial en el navegador. | **GPU Bound:** Capacidad de manejar +100,000 instancias sin latencia gracias al procesamiento paralelo en la tarjeta de video. |

####  Análisis de la Transferencia

*   **¿Qué se mantiene?**  
    Los principios fundamentales de la física: la gravedad como un vector constante hacia abajo (`-9.8`), el uso de ruido Perlin para generar turbulencia orgánica, y la trigonometría (Seno y Coseno) como base para la estructura helicoidal de la espiral.
    
*   **¿Qué cambia?**  
    La abstracción del sistema. En p5.js, el programador es "dueño" de la entidad (la partícula). En TouchDesigner, el diseñador es "dueño" del sistema (el flujo de datos). Se pasa de gestionar objetos individuales a gestionar canales de información (`tx`, `ty`, `tz`).

*   **¿Qué ventajas aparecen?**  
    *   **Post-procesamiento inmediato:** Implementar efectos como *Bloom*, *Feedback* (hilos) o *Displacement* es instantáneo mediante TOPs, algo que en p5.js requiere una lógica de renderizado compleja.
    *   **Iteración en Tiempo Real:** Es posible ajustar leyes físicas (gravedad, fricción, masa) mediante sliders mientras el sistema se ejecuta, permitiendo un diseño mucho más intuitivo.

*   **¿Qué limitaciones nuevas surgen?**  
    *   **Curva de Aprendizaje:** La interconexión entre diferentes familias de nodos (SOPs, CHOPs, TOPs) requiere una comprensión profunda de cómo se transforman los datos entre tipos de operadores.
    *   **Caja Negra:** El comportamiento interno de algunos nodos de física es más difícil de personalizar de forma granular en comparación con escribir una clase desde cero en p5.js.

####  Conclusión de Aprendizaje

Al reconstruir los sistemas de **Flow Fields** y **Gravedad** fuera de p5.js, aprendí que la simulación física es independiente de la herramienta o el lenguaje de programación. 

Trasladar la pieza a **TouchDesigner** me permitió entender que un sistema físico es, en esencia, una **red de señales interconectadas**. Mientras que en p5.js veía la física como una serie de instrucciones matemáticas, en TD la percibí como un **organismo vivo** donde el audio, el ruido y la geometría se modulan entre sí. Esta experiencia me enseñó que la clave de una buena simulación no es solo la precisión de las fórmulas, sino la forma en que los datos se comunican para crear comportamientos emergentes y estéticos.

## Bitácora de aplicación 
1. Herramienta Elegida: TouchDesigner.

He seleccionado TouchDesigner por su capacidad de procesamiento en tiempo real y su arquitectura basada en nodos, que facilita la interconexión de datos complejos. En el contexto de entretenimiento digital, es la herramienta estándar para la creación de live visuals e instalaciones interactivas, permitiendo delegar el renderizado masivo a la GPU.

2. Sistema Transferido: Flow Fields (Campos de Flujo) + Oscilación.

El sistema transfiere la lógica de vectores de fuerza de p5.js a un entorno 3D. Se utiliza una base matemática de oscilación (senos y cosenos) para generar una espiral, la cual es afectada por un campo de fuerzas basado en Ruido Perlin (Flow Field) y dinámicas de gravedad para cuerpos rígidos.

3. Contexto Profesional Concreto: Visuales para una Obra Escénica / Marca Cultural.

La pieza está diseñada como el componente visual para una performance basada en el universo de Honkai: Star Rail, específicamente inspirada en el personaje "Herta". El contexto es una pantalla de gran formato para un evento de cultura pop o un concierto de música de videojuegos.

4. Concepto Visual: "String Theory"

Inspirado en la canción homónima, la pieza explora la dualidad entre el orden predeterminado (la espiral armónica) y el colapso del diseño (el glitch y la gravedad).

- Hilos (Strings): Representados mediante Feedback Loops que crean estelas de luz.
- Relojería (Clockwork): Movimientos pulsantes sincronizados con el audio.
- Imperfección: Fractura de la imagen mediante mapas de desplazamiento (Displacement) cuando la música alcanza picos de energía.

5. Referencias (Moodboard)

<img width="500" height="281" alt="image" src="https://github.com/user-attachments/assets/1f057c98-5de7-4e9d-99c2-ed3183a6562c" />
<img width="480" height="270" alt="image" src="https://github.com/user-attachments/assets/0aec4ef4-d0e9-41d5-b3c5-1761e34ff1a8" />
<img width="1200" height="630" alt="image" src="https://github.com/user-attachments/assets/b743d8e4-2ba5-46fd-856e-948897296527" />
<img width="1920" height="1920" alt="image" src="https://github.com/user-attachments/assets/c2afc624-47ff-430f-8e5f-a16ffe722dad" />

6. Bocetos

<img width="899" height="1599" alt="image" src="https://github.com/user-attachments/assets/e7bdc9b4-ecef-4857-8e65-36d41e7a4670" />

7. Explicación de la Transferencia

- De p5.js: Se rescató la lógica de actualizar la posición de una partícula sumando vectores de aceleración y ruido. En p5.js, esto requería ciclos for que saturaban la CPU.
- A TouchDesigner: La transferencia se realizó mediante GPU Instancing. La espiral se genera mediante un Script CHOP (Python) y las fuerzas del campo de flujo se aplican mediante un Noise CHOP que modula la amplitud del movimiento. La interactividad de p5.sound se tradujo a un pipeline de Audio Analysis (RMS Power) con filtros de paso bajo para una reactividad rítmica precisa.

8. Mapa de Decisiones

- Decisión Técnica: Uso de un Feedback Loop con un Transform TOP (pequeñas traslaciones) para que los rastros parezcan hilos en movimiento.
- Decisión Estética: Implementación de un Bloom TOP para emular el brillo de materiales lujosos como el marfil y el oro.
- Decisión de Interacción: Mapeo de teclas (1, 2, 3) para transmutar materiales y mensajes tipográficos, permitiendo una narrativa evolutiva.
- Decisión de Física: Inserción de un Particle SOP con fuerza externa de -9.8m/s² para simular la gravedad en las llaves que caen.

9. Mapa de Presentación

La pieza se ejecutará en Perform Mode (F1) para una visualización limpia a pantalla completa. Se presentará como una sesión de VJ en vivo donde la música guía la deformación del sistema y el usuario interviene el entorno mediante el teclado.

<img width="1266" height="735" alt="image" src="https://github.com/user-attachments/assets/4015269b-58b1-4c71-b344-2a615b535c92" />

10. Uso Explícito de IA como Materializador

<img width="1249" height="568" alt="image" src="https://github.com/user-attachments/assets/c4c8cb3a-258d-4aa5-8c25-38527a27a7ba" />
<img width="868" height="574" alt="image" src="https://github.com/user-attachments/assets/9045a87d-5da9-4445-b6c7-1a0bcf7c45b5" />
<img width="1214" height="541" alt="image" src="https://github.com/user-attachments/assets/64c722b6-cfea-4b67-a077-b451d66848c1" />

11. Capturas de pantalla proyecto

<img width="2084" height="1158" alt="image" src="https://github.com/user-attachments/assets/3dfcc496-547b-4063-8058-d1c04de67dc6" />
<img width="2103" height="1132" alt="image" src="https://github.com/user-attachments/assets/6b257908-7299-4f1a-a2f5-5e92c2be8303" />
<img width="2035" height="1146" alt="image" src="https://github.com/user-attachments/assets/bf98f564-d9da-46c4-b440-0a9fea09aff7" />
<img width="1316" height="892" alt="image" src="https://github.com/user-attachments/assets/8a93d630-b451-4b10-bf5d-06bdbc3c4336" />


[TheHerta.zip](https://github.com/user-attachments/files/27771887/TheHerta.zip)











## Bitácora de reflexión
