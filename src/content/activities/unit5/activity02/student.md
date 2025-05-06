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


- ¿Qué es el encapsulamiento? ¿Por qué es importante?
R/= Al correr el ejemplo con AccessControl, te das cuenta de que solo publicVar puede modificarse directamente. Si descomentás las líneas con protectedVar o privateVar, el compilador se queja. Y eso está bien: el encapsulamiento protege el estado interno del objeto, evitando que lo modifiques accidentalmente o de forma incorrecta desde afuera.

- ¿Cómo se implementa la herencia en C++?
R/= En C++, la herencia se implementa haciendo que una clase "hija" (o derivada) herede de una clase "padre" (o base) usando la sintaxis class Derivada : public Base {}. Internamente, el compilador organiza la memoria de un objeto derivado como si empezara por la parte base, y luego le añade los campos de la clase derivada.

- ¿Cómo se ve un objeto con herencia múltiple?
R/= La herencia múltiple en C++ permite heredar de más de una clase base, algo que C# no permite directamente.

- Analisis del metodo update:

R/= Al ejecutar el código de ofApp.cpp y observar el ciclo:

```
for (int i = 0; i < particles.size(); i++) {
    particles[i]->update(dt);
}
```
...y usando el depurador cuando el vector particles tiene diferentes tipos de partículas (por ejemplo, RisingParticle, CircularExplosion, etc.), lo que vas a notar es que aunque particles[i] es un puntero a Particle, el método update() que se ejecuta es el de la clase real del objeto.

Esto es polimorfismo en acción: el vptr de cada objeto apunta a su propia vtable, y esa vtable tiene la dirección de la versión correcta de update().

- ¿Qué relación existe entre los métodos virtuales y el polimorfismo?
R/= Total. Los métodos virtuales son la base del polimorfismo en tiempo de ejecución en C++. Si un método no es virtual, entonces el compilador resuelve qué función usar en tiempo de compilación. Pero si es virtual, la decisión se toma en tiempo de ejecución usando la vtable del objeto.
