### Mi solución a la actividad 3

 ¿Qué clase actúa como la Factory en este ejemplo?
La clase que actúa como la Factory es ParticleFactory.

2. ¿Cuál es el "método factory" específico? ¿Es un método de instancia o estático?
El método factory específico es ParticleFactory::createParticle(), que es un método estático. Esto significa que se puede llamar directamente desde la clase sin necesidad de crear una instancia de ParticleFactory.

3. ¿Qué tipo de objeto devuelve este método fábrica?
El método createParticle() devuelve un puntero a un objeto de tipo Particle, que es una clase concreta que representa una partícula.

4. Proceso de creación:
¿Cómo decide qué tipo de partícula específica crear y configurar?
El método createParticle() utiliza el parámetro type (un std::string) para decidir qué tipo de partícula crear. Según el tipo recibido ("star", "shooting_star", "planet"), configura las propiedades específicas de la partícula (como size, color, velocity). Si el tipo no coincide con ninguno de los casos, simplemente se crea una partícula con los valores predeterminados.

¿Qué información necesita el método fábrica para realizar su trabajo?
El método necesita el parámetro type (que es un std::string) para identificar qué tipo de partícula se debe crear. Además, dentro de cada caso del if en createParticle(), se configuran las propiedades de la partícula (como el tamaño, el color, y la velocidad).

¿Qué devuelve si se le pasa un tipo desconocido? ¿Cómo podrías mejorar esto?
Si el tipo proporcionado no es reconocido (es decir, no es "star", "shooting_star", o "planet"), el método sigue devolviendo una partícula con las configuraciones predeterminadas, ya que no hay un control específico para tipos desconocidos.
Mejora: Podrías agregar una validación para gestionar tipos desconocidos, como lanzar una excepción o devolver un valor nulo, por ejemplo:

``` c++
if (type == "star") {
    // configuración para "star"
} else if (type == "shooting_star") {
    // configuración para "shooting_star"
} else if (type == "planet") {
    // configuración para "planet"
} else {
    throw std::invalid_argument("Tipo desconocido de partícula");
}
```
5. Uso de Factory:
¿Cómo se utiliza la ParticleFactory para poblar el vector particles?
En el método setup() de ofApp, se utiliza ParticleFactory::createParticle() para crear partículas de diferentes tipos y agregarlas al vector particles:

``` c++
Particle* p = ParticleFactory::createParticle("star");
particles.push_back(p);
```
Comparación con la alternativa sin Factory:
Si no se usara la fábrica, ofApp::setup() tendría que crear y configurar las partículas directamente, algo como esto:

``` c++
Particle* p = new Particle();
p->size = ofRandom(2, 4);
p->color = ofColor(255, 0, 0);
p->velocity = ofVec2f(0, 0);
particles.push_back(p);
```
Habría que repetir este proceso de configuración en múltiples lugares para cada tipo de partícula ("shooting_star", "planet", etc.), lo que haría que el código fuera más repetitivo y difícil de mantener.

6. Propósito del patrón Factory Method:
El propósito del patrón Factory Method es desacoplar la creación de objetos del resto de la aplicación. En lugar de tener código que sabe cómo crear instancias de clases específicas (como new Camion()), la fábrica delega esa responsabilidad a un único método central que sabe cómo crear los objetos, y el resto del código solo interactúa con interfaces o clases base.

Problema principal que aborda: El patrón resuelve el problema de tener un código cliente que está acoplado directamente a las clases concretas y la lógica de creación. Esto facilita la modificación o extensión de la creación de objetos sin cambiar el código cliente.

7. Ventajas de usar ParticleFactory en ofApp::setup:
Organización del código (SRP - Single Responsibility Principle): Al centralizar la creación de partículas en la fábrica, se cumple el principio de responsabilidad única, ya que ofApp se enfoca en manejar la lógica de la aplicación, no en la creación de objetos.

Legibilidad: La creación de las partículas está claramente separada en la fábrica, lo que mejora la legibilidad y evita la repetición del código.

Facilidad para añadir nuevos tipos de partículas: Si en el futuro se desea agregar un nuevo tipo de partícula (por ejemplo, "black_hole"), solo sería necesario modificar ParticleFactory, sin necesidad de cambiar ofApp::setup. Esto facilita la extensión y mantenimiento del código.

8. Agregar un nuevo tipo de partícula ("black_hole"):
Pasos para implementar el nuevo tipo de partícula utilizando ParticleFactory:
Modificar ParticleFactory::createParticle():

Añadir un nuevo caso en el bloque if que maneje el tipo "black_hole", configurando las propiedades adecuadas:

```c++
else if (type == "black_hole") {
    particle->size = ofRandom(10, 15);  // tamaño grande
    particle->color = ofColor(0, 0, 0);  // color negro
    particle->velocity = ofVec2f(0, 0);  // velocidad muy lenta
}
```
No se necesitaría modificar ofApp::setup():

ofApp::setup() seguiría funcionando de la misma manera. Si deseas crear partículas del tipo "black_hole", simplemente llamarías a ParticleFactory::createParticle("black_hole").

9. Método createParticle como estático:
Implicaciones de tener createParticle como estático:
Ventajas:

No se necesita crear una instancia de ParticleFactory para llamar al método. Esto es útil cuando no necesitas mantener estado entre diferentes llamadas al método.

Simplifica la llamada al método, ya que puedes invocar directamente ParticleFactory::createParticle().

Desventajas:

No puede ser sobrecargado: No puedes tener múltiples versiones de este método que dependan de la instancia de la clase, lo que limita la flexibilidad en algunos escenarios.

Prueba y extensibilidad: Al ser estático, no es tan fácil extender o probar la clase ParticleFactory mediante herencia, ya que los métodos estáticos no se pueden sobrescribir en clases derivadas.
