### Mi solución a la actividad 2

- Antes de ejecutar el experimento, ¿Qué esperas ver en memoria (hipótesis)? Ejecuta el código y
muestra una captura de pantalla del objeto en la memoria. ¿Qué puedes observar? ¿Qué información te proporciona el depurador? ¿Qué puedes concluir?
![image](https://github.com/user-attachments/assets/592fa48c-6b49-4329-aa1e-cf15819cfea6)

R/= Antes de correr el programa, me puse a pensar en qué podría encontrarme cuando mire la memoria con el depurador. 
Como sé que en la programación orientada a objetos un objeto es una instancia de una clase, mi hipótesis es que voy a ver una estructura que representa a 
ofApp con todos sus atributos y métodos, incluyendo los que hereda de ofBaseApp. También me imagino que el vector particles estará ahí, listo para almacenar punteros a objetos del tipo Particle.

Además, como el vector es público, debería ser fácil de encontrar en el depurador. Si ya se creó alguna partícula 
(por ejemplo, si se llamó el método createRisingParticle()), entonces espero ver que ese vector ya tiene elementos, cada uno 
apuntando a una instancia de Particle. Probablemente también pueda ver las posiciones, velocidades u otras propiedades de esas partículas si las inspecciono desde el depurador.

Una vez que ejecuté el código y puse un breakpoint en el método setup(), abrí el depurador y busqué la instancia de ofApp. Ahí pude ver 
claramente cómo se estructura este objeto en memoria. Aparecía toda la jerarquía de clases, o sea que se mostraba que ofApp es una subclase de 
ofBaseApp, y también vi el vector particles. En ese momento estaba vacío, pero luego de ejecutar el método que crea partículas, aparecieron los 
punteros dentro del vector, apuntando a diferentes objetos Particle que se estaban creando dinámicamente.

Lo interesante es que, aunque el código se ve limpio desde fuera, en memoria el objeto tiene un montón de detalles: 
direcciones, tipos, y valores actuales. El depurador me mostró qué tan viva está esa instancia y cómo va cambiando su estado a medida que corre el programa.

- Usa de nuevo el depurador para capturar un objeto de tipo CircularExplosion. Es posible que tengas que hacer modificaciones mínimas en el código para que puedas capturar este objeto más fácilmente.
Observa con el depurador la ventana de Auto o Locals y la ventana de Memory 1. Trata de buscar en memoria todas las partes que componen al objeto tipo CircularExplosion ¿Qué puedes observar en la memoria?
¿Qué información te proporciona el depurador?
¿Qué puedes concluir? NO OLVIDES tener a la mano todas la jerarquía de clases que componen a CircularExplosion. De esta manera podrás identificar cada parte del objeto en memoria.

R/= Jerarquía de Circular explosion
```
ofBaseApp  (vptr)
 └─ Particle        (pos, vel, …)
      └─ ExplosionParticle  (color, life, size, …)
           └─ CircularExplosion  (no datos extra)
```

¿Qué nos aporta el depurador?
La alineación de cada campo (por ejemplo, float en múltiplos de 4 bytes, padding tras el ofColor).

No hay “datos secretos”: todo lo que se usa en C++ (miembros públicos/privados) está en memoria tal cual.

El vtable único al inicio y ningún puntero extra: el despachador virtual está centralizado.
Herencia múltiple de datos (aquí simple) se traduce en bloques contiguos de memoria, en orden de declaración.
![image](https://github.com/user-attachments/assets/162704b7-c3e8-4fdc-b5c2-4fa042943e39)

![image](https://github.com/user-attachments/assets/33d38c90-801a-4b29-8a22-b47f34c8b480)

