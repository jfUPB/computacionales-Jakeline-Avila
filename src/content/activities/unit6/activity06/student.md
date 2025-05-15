### Mi solución a la actividad 6

#### ¿En qué parte específica de tu código implementaste el rol de Sujeto (Subject)? Muestra el fragmento relevante.

- Implementé el rol de Sujeto en la clase ofApp. Esta clase es la que maneja las interacciones del usuario, como las teclas presionadas, y notifica a las partículas sobre lo que sucede. Por ejemplo, cuando el usuario presiona una tecla, le aviso a las partículas para que cambien su comportamiento.

Fragmento relevante:

``` c++
void ofApp::keyPressed(int key) {
    if (key == 'a') {
        notify("attract");
    }
    else if (key == 'r') {
        notify("repel");
    }
    else if (key == 's') {
        notify("stop");
    }
    else if (key == 'n') {
        notify("normal");
    }
}
```
#### ¿Qué clase(s) implementaron el rol de Observador (Observer)? Muestra el fragmento relevante de la implementación de la interfaz (ej. onNotify).

- Las partículas (Particle) actúan como los observadores. Son las que reaccionan cuando el Sujeto (en este caso ofApp) les notifica sobre un evento, como cuando deben moverse hacia el mouse o detenerse.

Fragmento relevante:


``` c++
void Particle::onNotify(std::string event) {
    if (event == "attract") {
        state = new AttractState();
    }
    else if (event == "repel") {
        state = new RepelState();
    }
    else if (event == "stop") {
        state = new StopState();
    }
    else if (event == "normal") {
        state = new NormalState();
    }
}
```
#### ¿Qué eventos concretos notificaba tu Sujeto? ¿Por qué elegiste usar Observer para esta comunicación en lugar de llamadas directas?

Los eventos que notificaba el Sujeto eran:

"attract": las partículas deben moverse hacia el mouse.

"repel": las partículas deben alejarse del mouse.

"stop": las partículas deben detenerse.

"normal": las partículas deben volver a su comportamiento original.

Elegí usar Observer porque me permitió que las partículas se mantuvieran independientes del código que gestiona las interacciones del usuario. Usar Observer hace que el código sea más flexible, ya que si quiero agregar más comportamientos, no necesito cambiar todo el sistema.

#### ¿En qué parte de tu código se utiliza el patrón (es decir, dónde se llama a notify y dónde reaccionan los observadores)?

Llamo al notify en el método keyPressed de ofApp, y las partículas reaccionan a ese evento con el método onNotify, que es donde cambian su comportamiento.

Fragmento relevante:

``` c++
void ofApp::notify(std::string event) {
    for (Particle* p : particles) {
        p->onNotify(event);
    }
}
```

#### ¿Dónde está definido tu método factory? Muestra el fragmento de código.

- El método de la fábrica está en la clase ParticleFactory. Esta clase es responsable de crear las partículas de diferentes tipos, como estrellas, cometas o planetas. Esto hace que sea fácil agregar nuevos tipos de partículas sin tener que modificar el resto del código.

Fragmento relevante:

``` c++
Particle* ParticleFactory::createParticle(const std::string& type) {
    Particle* particle = new Particle();

    if (type == "star") {
        particle->size = ofRandom(5, 10);
        particle->color = ofColor(255, 255, 0);  // Amarillo
    }
    else if (type == "comet") {
        particle->size = ofRandom(10, 15);
        particle->color = ofColor(255, 0, 0);  // Rojo
        particle->velocity *= 2;
    }
    else if (type == "planet") {
        particle->size = ofRandom(12, 18);
        particle->color = ofColor(0, 0, 255);  // Azul
    }

    return particle;
}

```
#### ¿Qué tipos específicos de objetos creaba tu factory?

La fábrica crea tres tipos de partículas:

Star: con tamaño pequeño y color amarillo.

Comet: de tamaño más grande, color rojo y velocidad más alta.

Planet: de tamaño intermedio y color azul.

#### ¿Por qué fue beneficioso usar una factory en esa parte de tu código? ¿Qué problema te ayudó a resolver o qué mejora aportó a la estructura?

- Usar una fábrica fue útil porque centraliza la lógica de creación de partículas en un solo lugar. Esto hizo que el código fuera más limpio y modular. Si quisiera agregar nuevos tipos de partículas en el futuro, solo tendría que modificar la fábrica y no todo el código, lo que hace el proyecto más fácil de mantener.

#### Muestra un ejemplo de cómo usaste una factory en tu código cliente (ej. en setup o en respuesta a un evento).

- En el método setup, llamo a la fábrica para crear una nueva partícula del tipo "star".

Fragmento relevante:

``` c++
void ofApp::setup() {
    Particle* newParticle = ParticleFactory::createParticle("star");
    particles.push_back(newParticle);
}
```

#### ¿Qué clase actuó como Contexto (la que tiene un estado)? Muestra dónde guarda la referencia al estado actual.

La clase Particle es la que actúa como Contexto, porque mantiene una referencia al estado actual de la partícula. La referencia se guarda en un puntero a la interfaz State.

Fragmento relevante:

``` c++
class Particle {
public:
    State* state; // Aquí se guarda el estado actual
    void update();
};
```
#### ¿Cuáles fueron los ConcreteStates que implementaste? Muestra un fragmento de la implementación de update (o el método principal de comportamiento) de al menos dos estados diferentes.

- Los ConcreteStates que implementé fueron:

NormalState: la partícula se mueve aleatoriamente.

AttractState: la partícula se mueve hacia el mouse.

Fragmento relevante (de update):

``` c++
void NormalState::update(Particle* particle) {
    particle->position += particle->velocity;
}

void AttractState::update(Particle* particle) {
    ofVec2f mousePos(((ofApp*)ofGetAppPtr())->mouseX, ((ofApp*)ofGetAppPtr())->mouseY);
    ofVec2f direction = mousePos - particle->position;
    direction.normalize();
    particle->velocity += direction * 0.1;
    particle->position += particle->velocity;
}
```
#### ¿Qué desencadenaba las transiciones entre estados en tu aplicación? Muestra el código que llama a setState (o tu método equivalente).

- Las transiciones entre estados ocurrían cuando el usuario presionaba una tecla. Al presionar una tecla, se llamaba al método onNotify de las partículas, lo que cambiaba su estado.

Fragmento relevante:

``` c++
void Particle::onNotify(std::string event) {
    if (event == "attract") {
        state = new AttractState();
    }
    else if (event == "repel") {
        state = new RepelState();
    }
    else if (event == "stop") {
        state = new StopState();
    }
    else if (event == "normal") {
        state = new NormalState();
    }
}
```
#### ¿Por qué decidiste que el patrón State era apropiado para gestionar el comportamiento de esa clase en particular? ¿Qué alternativa habrías considerado y por qué la descartaste?

- Elegí el patrón State porque las partículas tienen diferentes comportamientos que dependen de su estado (por ejemplo, moverse hacia el mouse o alejarse de él). Usar este patrón me permitió organizar estos comportamientos de manera clara y modular. Podría haber usado simples condicionales (if o switch), pero eso habría complicado el código a medida que agregaba más comportamientos. El patrón State hace todo más sencillo y escalable.


#### ¿Qué es una clase?
- Una clase es como un plano o una receta que define cómo será un objeto. En otras palabras, dice qué cosas puede hacer el objeto (métodos) y qué datos tiene (atributos).

#### ¿Qué es un objeto?
- Un objeto es una instancia de una clase. Es una copia específica de esa clase, con valores concretos para sus atributos.

#### Beneficios Estructurales
- Usar estos tres patrones (Observer, Factory y State) hizo que el código fuera mucho más organizado. Cada patrón ayuda a resolver un problema específico:

- Observer me permitió manejar eventos de manera flexible sin complicar las partículas con lógica innecesaria.

- Factory hizo que la creación de nuevas partículas fuera más sencilla y centralizada.

- State me ayudó a gestionar los diferentes comportamientos de las partículas de manera clara.

- En general, estos patrones mejoraron la estructura del código, haciéndolo más fácil de entender, modificar y extender en el futuro.
